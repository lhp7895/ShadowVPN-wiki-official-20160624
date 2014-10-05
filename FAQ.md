1. I started but the shadowvpn process is missing

   Check `/var/log/shadowvpn.log` for what happened

2. can not open /dev/net/tun: open: No such file or directory

   Try

        opkg install kmod-tun
        modprobe tun
        mkdir /dev/net
        mknod /dev/net/tun c 10 200

3. ip: command not found

   Try

        opkg install ip

4. general diagnose steps:

    1. on client ping server real IP
    2. on client ping server VPN IP 10.7.0.1
    3. on client `traceroute 8.8.8.8` make sure it goes through 10.7.0.1
    4. on client `ping 8.8.8.8`; on server `sudo tcpdump -i tun0` see if any packet arrives
    5. you can also run `tcpdump host 8.8.8.8` or `tcpdump port 53` etc on the client or server
