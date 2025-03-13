# **Network Configuration Notes**

---

## **Basic Configuration**

### Device Configuration
- `configure terminal`
- `(config)#` `hostname HOSTNAME`
- `(config)#` `interface fastEthernet 0/0`
- `(config-if)#` `ip address 192.168.1.1 255.255.255.0`

### Useful Show Commands
- `#` `show ip interface brief`
- `#` `show interfaces [fastEthernet 0/0]`
- `#` `show ip route`
- `#` `show vlan brief`
- `#` `show interfaces trunk`
- `#` `show interfaces status`
- `#` `show ip protocols`

---

## **Configuration Files**

### Running Configuration
- `#` `show running-config`  
  *(Displays the current active configuration)*

### Startup Configuration
- `#` `show startup-config`  
  *(Displays the configuration that loads on device restart)*
- **Save Running Configuration to Startup Configuration**  
  *(All commands below do the same thing)*
  - `#` `write`
  - `#` `write memory`
  - `#` `copy running-config startup-config`

---

## **Password Configuration**

### Set Password (Unencrypted - Not Recommended)
- `(config)#` `service password-encryption`
- `(config)#` `enable password PASSWORD`

### Set Secret (Encrypted - Recommended)
- `(config)#` `enable secret PASSWORD`  
  *(Always encrypted)*

---

## **VLAN Configuration**

### Show Commands
- `#` `show vlan brief`
- `#` `show interfaces trunk`
### Create VLAN
- `#` `show vlan brief`  
  *(Check existing VLANs)*
- `(config)#` `vlan 2`  
  *(Create VLAN 2)*
- `(config-vlan)#` `name SOME_NAME`  
  *(Assign a name to VLAN 2)*

### Assign Interface to VLAN
- `(config)#` `interface fastEthernet 0/0`
- `(config-if)#` `description "SUBJECT"`
- `(config-if)#` `switchport mode access`
- `(config-if)#` `switchport access vlan 2`

### Configure Trunk Port
- `(config-if)#` `switchport mode trunk`
- `(config-if)#` `switchport trunk allowed vlan 2,101-104`  
  *(Allow VLANs 2, 101-104 on trunk)*
- `(config-if)#` `switchport trunk allowed vlan add 105`  
  *(Add VLAN 105 to the trunk)*

### ROAS (Router On A Stick)
#### 1. Configure Switch Connection as a Trunk
- `(config)#` `interface fastEthernet 0/1`  
- `(config-if)#` `switchport mode trunk`  
- `(config-if)#` `switchport trunk allowed vlan 10,20,30`  
- `#` `show interfaces trunk`
#### 2. Configure Router's Sub-Interfaces
- `(config)#` `interface gigabitEthernet 0/0`  
- `(config-if)#` `no shutdown`  

- `(config)#` `interface gigabitEthernet 0/0.10`  
- `(config-subif)#` `encapsulation dot1Q 10`  
  *(Assign VLAN 10 traffic to this (g0/0.10) sub-interface)*
- `(config-subif)#` `ip address 192.168.10.1 255.255.255.0`  

- `(config)#` `interface gigabitEthernet 0/0.20`  
- `(config-subif)#` `encapsulation dot1Q 20`  
  *(Assign VLAN 20 traffic to this (g0/0.20) sub-interface)*
- `(config-subif)#` `ip address 192.168.20.1 255.255.255.0`  

- `(config)#` `interface gigabitEthernet 0/0.30`  
- `(config-subif)#` `encapsulation dot1Q 30`  
  *(Assign VLAN 30 traffic to this (g0/0.30) sub-interface)*
- `(config-subif)#` `ip address 192.168.30.1 255.255.255.0`  

- `#` `show ip interface brief`

### SVI (Switch Virtual Interface)
#### 1. Enable Layer 3 routing on the L3 switch
- `(config)#` `ip routing`
#### 2. Manually create needed VLANs
- `(config)#` `vlan 10`
- `(config-vlan)#` `name VLAN_NAME`
#### 3. Configure SVIs (Switch Virtual interfaces)
- `(config)#` `interface vlan10`
- `(config-if)#` `no shutdown`
- `(config-if)#` `ip address IP_ADDRESS SUBNET_MASK`
#### 4. Configure physical interfaces as a routed ports if needed
- `(config)#` `interface gigabitEthernet 0/1`
- `(config-if)#` `no switchport`
- `(config-if)#` `no shutdown`
  *(Disable Layer 2 functionality (switchport mode)*
- `(config-if)#` `ip address AP_ADDRESS SUBNET_MASK`
- `(config-if)#` `exit`
- `(config)#` `ip route 0.0.0.0 0.0.0.0 NEXT_HOP_IP`
  *(as a default gateway for example)*

---

## **Routing Configuration**

### Show Commands
- `#` `show ip interface brief`
- `#` `show ip route`

### Static Route Configuration
- https://serverfault.com/a/171552
- `(config)#` `ip route NETWORK_IP SUBNET_MASK NEXT_HOP_IP`  
```
# ip route 192.168.3.0 255.255.255.0 192.168.2.2
#             ^             ^             ^
#           network        mask         gateway
```
  *(Route via next hop IP)*
- `(config)#` `ip route IP_ADDRESS SUBNET_MASK EXIT_INTERFACE`  
  *(Route via exit interface)*
- `(config)#` `ip route 0.0.0.0 0.0.0.0 DEFAULT_HOP_IP`  
  *(Default route configuration)*

---
