# What is it?

P2P communication is hindered by the fact that almost everybody is behind a NAT router on a public network. 

There are two problems with this:

1. The sender of a communication does not know the SENDER ip and port that the NAT router will place on packets. In particular, the port given is random.
2. The NAT router will reject any incoming packets that aren't in a reply to a previous outgoing packet (as identified by having the same DESTINATION ip and port as a recently sent packet)

To get around this, a method called "Holepunching" is used, as detailed wonderfully [here.](http://www.brynosaurus.com/pub/net/p2pnat/)

This project extends stylesuxx's implementation of this solution found [here](https://github.com/stylesuxx/udp-hole-punching)  
to gracefully fall back to LAN addressing when two hosts are behind the same NAT router.

This project demonstrates the connection, but does not implement any keep-alive functionality. After some idle time, the NAT will no longer accept incoming packets as replies to previous outgoing packet.

# How to use?

Run the demo-server.py on a machine (in the cloud preferably- but it will work in a LAN if both clients
are in the same LAN). Run two instances of demo-peer.py:

```
 python demo-peer.py  server <server-name> 
```

to register a server host, and 

```
 python demo-peer.py  host <user-name> <server-name> 
```

to connect with a given server.

Note that you must change **HANDSHAKE_SERVER_IP** and **HANDSHAKE_SERVER_PORT** in demo-peer.py. They default
to '127.0.0.1' and 5160 respectively. **HANDSHAKE_SERVER_PORT** must match **SERVER_PORT** in demo-server.py.

# License

This code is meant for education purposes. Use it with the same freedom as you would the sun's rays, but
I wouldn't recommend using it for anything other than a starting point.