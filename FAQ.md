1. I started but the shadowvpn process is missing

   Check /var/log/shadowvpn.log for what happened

2. can not open /dev/net/tun: open: No such file or directory

   Try

        opkg install kmod-tun
        modprobe tun
        mkdir /dev/net
        mknod /dev/net/tun c 10 200

3. ip: command not found

   Try

        opkg install ip