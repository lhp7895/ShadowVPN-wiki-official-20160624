Clear the content of client_up.sh and client_down.sh so that
they won't change route table any more.

Add a new interface, select tun0.

![image](https://cloud.githubusercontent.com/assets/1073082/4519784/4b303254-4ccb-11e4-8c93-65b193612104.png)

Disable `Use default gateway` of wan.

![image](https://cloud.githubusercontent.com/assets/1073082/4519789/7a262276-4ccb-11e4-846e-85f31584b1d0.png)

Add a new zone called tun. Add `interface tun` to `tun zone`. And update forward rules: lan => tun, tun => wan.

![image](https://cloud.githubusercontent.com/assets/1073082/4519773/fccd4138-4cca-11e4-945b-b1da19e63c92.png)

Add two routes

![image](https://cloud.githubusercontent.com/assets/1073082/4519796/b98a5edc-4ccb-11e4-8fbc-ceccd14c35fc.png)

(Optional) Add chnroutes script.

![image](https://cloud.githubusercontent.com/assets/1073082/4519799/d7e51ce6-4ccb-11e4-8876-34f81e0dd47c.png)

chnroutes looks like:

    #!/bin/sh
    route add -net 1.0.1.0 netmask 255.255.255.0 pppoe-wan
    route add -net 1.0.2.0 netmask 255.255.254.0 pppoe-wan
    ...

Save and apply.

    /etc/init.d/network restart
    /etc/init.d/firewall restart