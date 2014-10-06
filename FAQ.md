1. I started but the shadowvpn process is missing

   Check `/var/log/shadowvpn.log` for what happened

2. `can not open /dev/net/tun: open: No such file or directory`

   Try

        opkg install kmod-tun
        modprobe tun
        mkdir /dev/net
        mknod /dev/net/tun c 10 200

3. ip: command not found

   Try

        opkg install ip

4. if scripts don't work, you can try to [configure via LuCI](https://github.com/clowwindy/ShadowVPN/wiki/Configure-Via-LuCI-on-OpenWRT)

5. general diagnose steps:

    1. on client ping server real IP
    2. on client ping server VPN IP 10.7.0.1
    3. on client `traceroute 8.8.8.8` make sure it goes through 10.7.0.1
    4. on client `ping 8.8.8.8`; on server `sudo tcpdump -i tun0` see if any packet arrives
    5. you can also run `sudo tcpdump host 8.8.8.8` or `sudo tcpdump port 53` etc on the client or server
    6. on server `netstat -nr` and `ifconfig` check if your wan is `eth0` if not, update server_*.sh
    7. on client `netstat -nr` and `ifconfig` check if your lan is `eth0`. if not, update client_*.sh

Submit an issue if you still can't solve your problem.
Post what you have tried and provide as much information as possible.
