
## **Configuration**

### Show commands
- `#` `show clock`
- `#` `show clock detail`

### Manual software clock Configuration
- `(config)#` `clock timezone ?`
- `(config)#` `clock set 14:30:00 27 Dec 2024`
- `(config)#` `clock summer-time ?`

### Manual hardware clock Configuration
- `#` `calendar set 14:30:00 27 Dec 2024` *to manually set time*
- `#` `clock update calendar` *to set time from software time*


## **NTP**

- **NTP uses only UTC**
- **NTP doesn't update calendar by default**
- NTP modes
	- Server
	- Client
	- Symmetric active mode

### Show commands
- `#` `show ntp associations`
- `#` `show ntp status`

### Client Configuration
- `(config)#` `ntp server NTP_SERVER_IP_ADDRESS`
- `(config)#` `ntp server NTP_SERVER_IP_ADDRESS` *can be multiple*
- `(config)#` `not update calendar` *to also update hardware clock*
- `(config)#` `clock timezone ?` *NPT doesn't update calendar by default*

### Server configuration
- `(config)#` `interface loopback0`
- `(config-if)#` `ip address IP_ADDRESS IP_ADDRESS_NETMASK` 
- `(config)#` `ntp source loopback0`
	- Я не понял зачем точно нужны комманды выше, их можно просто не писать

- `(config)#` `ntp master`
	- Чтобы начать отвечать на NTP запросы
