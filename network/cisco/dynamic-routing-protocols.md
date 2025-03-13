```
#  IGP (Interior Gateway Protocol)
#   ├──────────── Distance Vector 
#   │                 ├──────────── RIP (Routing Information Protocol)
#   │                 └──────────── EIGRP (Enhanced Interior Gateway Protocol)
#   │
#   └──────────── Link State
#                     ├──────────── OSPF (Open Shortest Path First)
#                     └──────────── IS-IS (Intermediate System to Intermediate System)
#
#  EGP (Exterior Gateway Protocol)
#   └──────────── Path Vector
#                     └──────────── BGP (Border Gateway Protocol)
```

## OSPF
- **LSA (Link State Advertisement)**
- **LSDB (Link State Data Base)**
- Routers will *flood* **LSAs** until all routers in the OSPF *area* develop the same map of the network **(LSDB)**

### OSPF configuration
- `(config)#` `router ospf PROCESS_ID`
- `(config-router)#` `network NETWORK_IP WILDCARD_MASK area AREA_NUMBER`
- `(config-router)#` `network 10.0.12.0 0.0.0.255 area 0`
	- network command tells OSPF to:
		- Look for any interfaces with an IP address contained in the specified range
		- Activate OSPF on those interfaces
		- Router will try to become OSPF neighbors with other OSPF-activated neighbor roughers
- `(config-router)#` `passive-interface g0/0`
	- Tells router not to send OSPF messages out of specified interface
	- But still send LSAs about specified interface network to router's OSPF neighbors
- `(config-router)#` `default-information originate`
	- Optionally!
	- To advertise router's default gateway to it's OSPF neighbors
- `#` `show ip protocols`
	 - To check configuration