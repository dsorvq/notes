## **Show commands**

- `#` `show ip dhcp binding` *(shows all of the DHCP clients with assigned IPs)*

## **Configuration**

### Configure DHCP server
- `(config)#` `ip hdcp excluded-addresses LOW_END_IP_RANGE TOP_END_IP_RANGE` *(optionally)*
- `(config)#` `ip hdcp pool POOL_NAME` *(pool should be difference for each separate network)*
- `(hdcp-config)#` `network NET_IP NET_MASK`
- `(hdcp-config)#` `dns-server DNS_IP`
- `(hdcp-config)#` `doman-name some.com` *(don't know why do we need that)*
- `(hdcp-config)#` `default-router DEFAULT_RAUTER_IP` 
- `(hdcp-config)#` `lease days hours minutes`

- `#` `show ip dhcp binding`

### Configure DHCP Client
- `(config)#` `interface g0/0`
- `(config-if)#` `ip address dhcp`

### Configure DHCP Relay Agent
- `(config)#` `interface g0/0`
- `(config-if)#` `ip helper-address IP_OF_DHCP_SERVER`
