Upgrade to ShadowVPN 0.2.0 on both client and server side.

Server side
-----------

Edit server.conf and add multiple user tokens.

```
# Users allowed. Each must be HEX of 8 bytes. You can generate on by running:
#     xxd -l 8 -p /dev/random
# See `net` for more information.
user_token=7e335d67f1dc2c01,ff593b9e6abeb2a5,e3c7b8db40a96105

# Local IP and subnet of the VPN tunnel.
# 
# If user_token is specified, NAT mode will be enabled on server side, and
# the client does not need to have the same network with the server.
# In NAT mode, each user will be assigned an IP automatically.
# for example:
#     tun0 is 10.7.0.1
#     client IPs will be 10.7.0.2, 10.7.0.3, 10.7.0.4, etc
# You'll see them in the log when ShadowVPN starts with -v:
#     assigning 10.7.0.2 to user 7e335d67f1dc2c01
#     assigning 10.7.0.3 to user ff593b9e6abeb2a5
#     assigning 10.7.0.4 to user e3c7b8db40a96105
#     VPN started
net=10.7.0.1/16
```

Client side
-----------

Edit `client.conf` and give each user a different user token. For example:

```
# Identify a user. Must be HEX of 8 bytes. You can generate on by running:
#     xxd -l 8 -p /dev/random
# See `net` for more information.
user_token=7e335d67f1dc2c01

# Local IP and subnet of the VPN tunnel.
# If user_token is specified, NAT mode will be enabled on server side, and
# the client does not need to have the same network with the server.
net=10.7.0.2/24
```

You don't have to set `net` to the same as the server will assign to you.
ShadowVPN server will do NAT on server side.

**Notice: Keep your user token secret to other users.**

Compatibility
-------------

If `user_token` is not set, ShadowVPN will run in traditional protocol and will be backward compatible.

If you set `user_token` on only one side of the client and server, ShadowVPN will not work.

Security Model
--------------

The data is protected by `password`. It should be kept secret from public. All users share the same password.

Each user is authenticated by `user_token`. Each user's user token should be kept secret from other users.

If you really want to use different passwords for different users, you should start multiple ShadowVPN server instances.