## **Show commands**
- `#` `show hosts`
	- *to list learned and configured hosts*
- `#` `show ip name-server`
	- *to list primary DNS server*

## **Configuration**

### Configure DNS server
- `(config)#` `ip dns server` *(act as a DNS server)*

- `(config)#` `ip host HOST_NAME_1 HOST_IP_1`
- `(config)#` `ip host HOST_NAME_2 HOST_IP_2`

- `(config)#` `ip name-server 8.8.8.8` *(fallback DNS server)*

### Configure DNS client
- `(config)#` `ip name-server 8.8.8.8` 
	- *(use Google's DNS server for example)*
- `(config)#` `ip domain lookup` 
	- *(enable to perform DSN queries)*
