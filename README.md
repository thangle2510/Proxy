# Proxy Auto Config
# Squid - Autoconfig
!!! note Preparation
- Squid proxy
- web server with virtual host configured
- PAC file
- Guide link of FindProxyForURL function: 
  - [Proxy Auto-Configuration (PAC) file - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file)
!!!
### Web server configuration
```shell
touch /etc/httpd/conf.d/proxy.conf
```
```shell
echo "
<VirtualHost *:80>
	ServerName proxy
	DocumentRoot "/var/www"
	#Redirect /wpad.dat http://proxy/wpad.pac
</VirtualHost>
" > /etc/httpd/conf.d/proxy.conf
```
### PAC file
-- By convention, the PAC file is normally named **proxy.pac**. The WPAD standard uses **wpad.dat**
```js
function FindProxyForURL(url, host) {
	// Forward request to Fw if destination url request match:
	if (shExpMatch(host, "tuoitre.vn"))
	{
		return "DIRECT";
	}

	// URLs within this network are accessed through
	// port 8080 on fastproxy.example.com:
	if (isInNet(host, "10.0.0.0", "255.255.248.0"))
	{
		return "PROXY fastproxy.example.com:8080";
	}

	// All other requests go through port 8080 of proxy.example.com.
	// should that fail to respond, go directly to the WWW:
	return "PROXY proxy.example.com:8080; DIRECT";
}
```

```js
function FindProxyForURL(url, host) {
        var x = "\*tuoitre\*"
        var y = "\*vnexpress\*"
        if ((shExpMatch(url, x)) || (shExpMatch(url, y))) {
                return "PROXY proxy:3128";
        }

        else {
                return "DIRECT";
        }
}

```
