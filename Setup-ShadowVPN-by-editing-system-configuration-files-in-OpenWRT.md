According to [Configure via LuCI on OpenWRT](https://github.com/clowwindy/ShadowVPN/wiki/Configure-via-LuCI-on-OpenWRT)
,You can also modify system config file to get ShadowVPN run in your OpenWRT(OpenWrt Barrier Breaker 14.07) box.

### 1 
Install ShadowVPN

### 2
Clear the content of /etc/shadowvpn/client_up.sh and /etc/shadowvpn/client_down.sh so that they won't change route table any more. Remove /etc/hotplug.d/iface/30-shadowvpn if it exists.

### 3 
Edit file "/etc/config/network",

Append this line to interface 'wan':

`option defaultroute '0'`

And append the following lines to the end of this file:

```

config interface 'tun'
	option proto 'static'
	option ifname 'tun0'
	option ipaddr '10.7.0.2'
	option netmask '255.255.255.0'
	option gateway '10.7.0.1'

config route
	option interface 'wan'
	option target 'YOUR SERVER IP'
	option metric '10'

config route
	option interface 'tun'
	option target '0.0.0.0'
	option netmask '0.0.0.0'
	option gateway '10.7.0.1'
	option metric '5'

```

Replace the 'YOUR SERVER IP' to your server ip. 

### 4
Edit file '/etc/config/firewall',
Append the following lines to the end of this file:

```
config zone
	option input 'ACCEPT'
	option forward 'REJECT'
	option output 'ACCEPT'
	option name 'tun'
	option network 'tun'
	option masq '1'

config forwarding
	option dest 'wan'
	option src 'tun'

config forwarding
	option dest 'tun'
	option src 'lan'
```

### 5 
(Optional) Add [chnroutes script](https://github.com/clowwindy/ShadowVPN/blob/master/samples/chnroutes.sh).
   Save it to `/etc/shadowvpn/chnroutes.sh`. Then

        chmod +x /etc/shadowvpn/chnroutes.sh

   Create `/etc/hotplug.d/iface/35-chnroutes`

        #!/bin/sh
        [ ifup = "$ACTION" ] && {
          [ wan = "$INTERFACE" ] && {
             /etc/shadowvpn/chnroutes.sh
          }
        }

### 6

Save and apply. Then:

        /etc/init.d/network restart