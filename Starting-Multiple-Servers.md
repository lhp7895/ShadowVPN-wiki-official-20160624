For each server, change the following configuration to be different from each other:

server1
-------

/etc/shadowvpn/server1.conf:

    # ...
    port=1001
    intf=tun1
    up=/etc/shadowvpn/server1_up.sh
    down=/etc/shadowvpn/server1_down.sh
    pidfile=/var/run/shadowvpn_server1.pid
    # ...

/etc/shadowvpn/server1_up.sh:

   # ...
   ifconfig $intf 10.1.0.1 netmask 255.255.255.0
   # ...

server2
-------

/etc/shadowvpn/server2.conf:

    # ...
    port=1002
    intf=tun2
    up=/etc/shadowvpn/server2_up.sh
    down=/etc/shadowvpn/server2_down.sh
    pidfile=/var/run/shadowvpn_server2.pid
    # ...

/etc/shadowvpn/server2_up.sh:

   # ...
   ifconfig $intf 10.2.0.1 netmask 255.255.255.0
   # ...
