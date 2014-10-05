If you use pppoe, the default init scripts may be not good.
When pppoe reconnects, the VPN breaks down. If you want to let
your router automatically configure IP, routes automatically,
you should use LuCI to configure all this stuff instead.

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

(Optional) Add [chnroutes script](https://github.com/clowwindy/ShadowVPN/blob/master/samples/chnroutes.sh).
Save it to `/etc/hotplug.d/iface/30-chnroutes`

Save and apply. Then:

    /etc/init.d/network restart