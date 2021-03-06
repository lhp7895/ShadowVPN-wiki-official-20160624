首先确保你的ShadowVPN 的NAT转发能够正常工作，也就是能够在配置路由的表的情况下正常翻墙。 

ipset只是用来代替部分路由表。

> 这里假设你已经有了一个ipset 集合命名为`wallips`， 一般是通过带ipset功能的dns软件，来追加需要翻墙的IP列表。这一部分可以参考许多shadowsocks ss-redir + dnsmasq + ipset 的教程。

ipset相关
---------

+ `[ $(ipset list wallips 2>/dev/null| wc -l) -eq 0 ] && { ipset -N wallips iphash; }` 
+ `ipset add wallips 8.8.8.8`

添加操作
-------

+ `iptables -t mangle -N fwmark`
+ `iptables -t mangle -A PREROUTING -j fwmark`

> 我这里OpenWRT 已经带了上面两条操作。

+ `iptables -t mangle -A OUTPUT -j fwmark` (可选)

+ `iptables -t mangle -A fwmark -m set --match-set wallips dst -j MARK --set-mark 0xffff`
+ `echo "99 gfw" >> /etc/iproute2/rt_tables`  (一次性？)
+ `ip rule add fwmark 0xffff table gfw`
+ `ip route add default dev tunX table gfw` 

移除操作
-------
+ `ip rule del table gfw`
+ `iptables -t mangle -D fwmark -m set --match-set wallips dst -j MARK --set-mark 0xffff`
