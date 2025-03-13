## **EtherChannel Configuration**

### **Show Commands**
- **View EtherChannel Load-Balancing Method:**  
  `#` `show etherchannel load-balance`  
  *Displays the load-balancing algorithm used for EtherChannel.*

- **Check EtherChannel Summary:**  
  `#` `show etherchannel summary`  
  *Provides a summary of all EtherChannel groups, including their status and member interfaces.*

- **Verify IP Interface Status:**  
  `#` `show ip interface brief`  
  *Shows a brief overview of all IP interfaces, including EtherChannel groups.*

---

### **Configuration**

#### **Configuring LACP (Link Aggregation Control Protocol)**
1. **Select Interfaces for EtherChannel:**  
   `(config)#` `interface range f1/0 - 5`  
   *Selects a range of interfaces to be part of the EtherChannel group.*

2. **Assign Interfaces to a Channel Group:**  
   `(config-if-range)#` `channel-group 1 mode [active | passive]`  
   - **Active Mode:** Actively sends LACP packets to negotiate the EtherChannel.  
   - **Passive Mode:** Responds to LACP packets but does not initiate negotiation.  
   - **Important Notes:**  
     - The channel group number does not need to match on different switches.  
     - `passive + passive` will **not** form an EtherChannel.  
     - `active + [passive | active]` will successfully form an EtherChannel.

3. **Configure the Port-Channel Interface:**  
   `(config)#` `interface port-channel 1`  
   *Enters configuration mode for the logical port-channel interface.*

4. **Additional Configuration (if needed):**  
   `(config-if)# `...`  
   *Add any additional configuration (e.g., VLANs, trunking, etc.) to the port-channel interface.*


### **Configuration Brief**
#### ! Step 1: Configure the Port-Channel interface as a trunk
- Switch(config)# interface port-channel 1
- Switch(config-if)# switchport mode trunk
- Switch(config-if)# switchport trunk allowed vlan 10,20
- Switch(config-if)# exit

#### ! Step 2: Assign physical interfaces to the EtherChannel
- Switch(config)# interface range GigabitEthernet0/1 - 2
- Switch(config-if-range)# channel-group 1 mode active
- Switch(config-if-range)# exit

#### ! Step 3: Verify the configuration
- Switch# show etherchannel summary
- Switch# show interfaces trunk
- Switch# show interfaces port-channel 1
