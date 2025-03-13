# **Static Routing**

---

## **Configuration**

### Show Commands
- `#` `show ip interface brief`
- `#` `show ip route`

### Static Route Configuration
- https://serverfault.com/a/171552
- `(config)#` `ip route NETWORK_IP SUBNET_MASK NEXT_HOP_IP`  
	- Route via next hop IP

	```
	# ip route 192.168.3.0 255.255.255.0 192.168.2.2
	#             ^             ^             ^
	#           network        mask         gateway
	```
- `(config)#` `ip route IP_ADDRESS SUBNET_MASK EXIT_INTERFACE`  
	- Route via exit interface
- `(config)#` `ip route 0.0.0.0 0.0.0.0 DEFAULT_HOP_IP`  
	- Default route

---

