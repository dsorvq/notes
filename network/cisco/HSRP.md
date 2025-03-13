## **HSRP**

### **Info**
- **Cisco proprietary**

- **Active and Standby rounters are elected**

- **Version 1 and Version 2**
	- Version 1 multicast ip: 224.0.0.2
	- Version 2 multicast ip: 224.0.0.102

---

### **Configuration**
- `(config)#` `interface g0/0`
- `(config-if)#` `standby version 2`
- `(config-if)#` `standby GROUP_NUMBER ip VIRTUAL_IP`
- `(config-if)#` `standby GROUP_NUMBER priority <0-255>`
	- Active router will be with the highest priority
	- Or highest IP in case of match
- `(config-if)#` `standby GROUP_NUMBER preempt`
	- In case of higher priority
	- Take the role of active even if another router is avtive

- `#` `show standby`
---

