# Squid Proxy
!!! note Guide Links
- [Chapter 1. Introduction :: Squid. The definitive guide :: Server Administration :: eTutorials.org](http://etutorials.org/Server+Administration/Squid.+The+definitive+guide/Chapter+1.+Introduction/)

- [31.4.�The Configuration File /etc/squid/squid.conf](https://www.pks.mpg.de/~mueller/docs/suse10.2/html/opensuse-manual_en/manual/sec.squid.configfile.html)
- [Proxy Auto-Configuration (PAC) file - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file)


!!!
## Preparing
  - CentOS 7: 10.1.1.21
  - Squid Version 3.5.20 as Proxy server
  - Windows clients
  - Web browser
  - Internal subnet: 10.1.1.0/24

## Installation
```shell
yum -y update
yum -y install squid
squid -v 
```
## Minimal configuration
```shell
cache_dir ufs /var/spool/squid/ 500 16 256
acl internal_subnet_10x src 10.1.1.0/24 
http_access allow internal_subnet_10x
```
## Start and enable Squid
```shell
systemctl start squid
systemctl enable squid
```
### All left to do is configure our Firefox browser to use our proxy
1. Open menu
2. Select Preferences
3. Under General go to Network Proxy settings
4. Specify Manual proxy configuration
5. Set HTTP Proxy to 10.1.1.21 and Port 3128

### Monitor log file when browsing Internet you will see connection through your newly build proxy
```shell
tail -f /var/log/squid/access.log
```
## SquidGuard
```shell
squidGuard -b -d -C all
```













