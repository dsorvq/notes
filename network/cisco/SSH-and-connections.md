## **Console Line**

### С паролем
- `(config)#` `line console 0`
	- Как я понял, через эту комманда мы заходим в настройку подключения к CLI
	- Цифра 0, скорее всего означает, нулевой интерфейс для консоли (с высокой вероятность, он единственный?)
- `(config-line)#` `password PASSWORD`
- `(config-line)#` `login` 
	- Без этого пароль зарпашиваться не будет
	
### С логином
- `(config)#` `username USERNAME secret PASSWORD`
- `(config)#` `line console 0`
- `(config-line)#` `password PASSWORD`
- `(config-line)#` `login local` 
	- Без этого пароль зарпашиваться не будет
	- Очевидно и без соменний, если написать локал то будут запрашивать логины

## **Configuration**

### SSH
#### server
- `(config)#` `ip domain name some.com`
- `(config)#` `crypto key generate rsa 2048`
- `(config)#` `ip ssh version 2`
- `#` `show ip ssh`
- `(config)#` `enable secret PASSWORD`
- `(config)#` `username USERNAME secret PASSWORD`
- `(config)#` `line vty 0 15`
	- Настройка сразу всех 16 линий
- `(config-line)#` `login local`
- `(config-line)#` `transport input ssh`

#### client
- `shh -l USERNAME IP_ADDRESS`
- `shh USERNAME@IP_ADDRESS`

### Connection to a switch using SVI (Switch Virtual Interface)
- `(config)#` `interface vlan1`
- `(config-if)#` `ip address IP IP_MASK`
- `(config-if)#` `no shutdown`
- `(config)#` `ip default-gateway IP_OF_DEFAULT_GATEWAY`

### Telnet
- `(config)#` `enable secret PASSWORD`
- `(config)#` `username USERNAME secret PASSWORD`
	- Я не понял, нужно ли вводить первое или можно только второе
- `(config)#` `access-list 1 permit host IP_OF_THE_HOST`
	- Не знаю, что за цифра 1
- `(config)#` `line vty 0 15`
	- Настройка сразу всех 16 линий
- `(config-line)#` `login local`
- `(config-line)#` `transport input [telnet, ssh, none, all]`
- `(config-line)#` `access-class 1 in`
	- Это вот с той цифрой 1 связано, не знаю точно, что за аксесс листы
	
