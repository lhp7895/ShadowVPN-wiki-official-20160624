                  |  OpenVPN  |   ShadowSocks  | ShadowVPN
----------------- | --------- | -------------- | ----------
Layer             |     IP    |     TCP/UDP    |     IP
Frontend          |    VPN    | socks/iptables |    VPN
Security          |    CCA    |       CPA      |    CCA
Protocol Sniffing |  possible |    difficult   | difficult
Tamper Proof      |     Y     |        N       |     Y
RST Proof         |     N     |        N       |     Y
Speed             | fast(UDP) |       fast     |    fast
CPU utilization   |    high   |      medium    |    low
RAM               |    low    |      medium    |    low