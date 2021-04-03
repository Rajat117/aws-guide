Private subnet also needs public internet access. For cases such as software update.

NAT stands B/w Private Subnet and WWW(public internet).
Actually it stands b/w private subnet & IGW(internet gateway) and IGW stands b/w public subnet and WWW(public internet)

So A rough Diagram:
```
PrivateSubnet
-------------
NAT - (In PublicSubnet)
------------
IGW
------------
(WWW) Public Internet
```

# Characteristic
- Managed by AWS on its own