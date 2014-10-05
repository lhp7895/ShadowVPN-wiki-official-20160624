ShadowVPN
=========

[![Build Status]][Travis CI]

ShadowVPN 是一个基于 libsodium 的高速、安全的 VPN。特别为低端硬件，如 OpenWRT 路由器设计。

更多详情见[这里][Compare]。

目前处在完善阶段，仍有[许多需要做的][Issue Tracker]。如果你希望使用稳定的版本，可以过段时间再过来看看。

安装
----

Linux:

请确保 configure 时使用了 `--sysconfdir=/etc` 参数。

    sudo apt-get install build-essential automake libtool
    git submodule update --init
    ./autogen.sh
    ./configure --enable-static --sysconfdir=/etc
    make && sudo make install

OpenWRT:

[下载预编译版]： ar71xx, brcm63xx, brcm47xx, ramips_24kec.

或者自行编译： 进入 [SDK] 根目录，然后：

    pushd package
    git clone https://github.com/clowwindy/ShadowVPN.git
    popd
    make menuconfig # select Network/ShadowVPN
    make V=s
    scp bin/xxx/ShadowVPN-xxx-xxx.ipk root@192.168.1.1
    # then log in your box and use opkg to install that ipk file

配置
----

- 可以在 `/etc/shadowvpn` 目录下找到所有配置文件。
- 对于客户端，编辑 `client.conf`。
- 对于服务器端，编辑 `server.conf`。
- 修改配置文件中的 `server` 和 `password` 字段。
- `up` 字段指定的脚本会在 VPN 启动后执行。
- `down` 字段指定的脚本会在 VPN 退出后执行。
- 如果需要自定义路由，可以修改上面两个脚本。在脚本最后有一段注释，
可以把修改路由的命令放在相应的位置。

需要注意的是 ShadowVPN 是一个点对点 VPN。意味着对于每个客户端，需要一个对应的服务端。
可以开启多个服务端进程，用 `-c` 参数指定不同的配置文件。请确保对于不同的服务端和客户端，
在 `up` 和 `down` 脚本中指定了不同的 IP。

使用
-----

服务器：

    sudo shadowvpn -c /etc/shadowvpn/server.conf -s start
    sudo shadowvpn -c /etc/shadowvpn/server.conf -s stop

客户端：

    sudo shadowvpn -c /etc/shadowvpn/client.conf -s start
    sudo shadowvpn -c /etc/shadowvpn/client.conf -s stop

客户端（OpenWRT）：

    /etc/init.d/shadowvpn start
    /etc/init.d/shadowvpn stop

对于 DNS 污染，可以直接使用 Google DNS 8.8.8.8，或者使用
[ChinaDNS] 综合使用国内外 DNS 得到更好的解析结果。

可选： OpenWRT 用户可以看看 [LuCI Configuration]。

Wiki
----

所有的文档可以在 wiki 中找到:
https://github.com/clowwindy/ShadowVPN/wiki

License
-------
MIT

Bugs and Issues
----------------

* [Issue Tracker]
* [Mailing list]

[Build Status]:         https://img.shields.io/travis/clowwindy/ShadowVPN/master.svg?style=flat
[Compare]:              https://github.com/clowwindy/ShadowVPN/wiki/Compared-to-Shadowsocks-and-OpenVPN
[ChinaDNS]:             https://github.com/clowwindy/ChinaDNS-C
[下载预编译版]:    https://github.com/clowwindy/ShadowVPN/releases
[Issue Tracker]:        https://github.com/clowwindy/ShadowVPN/issues?state=open
[LuCI Configuration]:   https://github.com/clowwindy/ShadowVPN/wiki/Configure-Via-LuCI-on-OpenWRT
[Mailing list]:         http://groups.google.com/group/shadowsocks
[SDK]:                  http://wiki.openwrt.org/doc/howto/obtain.firmware.sdk
[Travis CI]:            https://travis-ci.org/clowwindy/ShadowVPN