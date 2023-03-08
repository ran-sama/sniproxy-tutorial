# sniproxy-tutorial
Handle incoming port 80 HTTP and 443 HTTPS requests based on domain names.

![alt text](https://raw.githubusercontent.com/ran-sama/sniproxy-tutorial/master/overview.png)

## Why bother?
* you only have one port 80 and one port 443 per IP
* run as many servers as your hardware can handle on just these ports
* requests that did not include a domain-/hostname can be trashed
* is a transparent proxy and doesn't need your secret certs

## Install and configure

```
sudo apt install sniproxy
```
Edit the config in a way that reflects your server infrastructure:

```
sudo nano /etc/sniproxy.conf
```

```
user daemon

pidfile /tmp/sniproxy.pid

error_log {
    syslog daemon
    priority notice
}

listener 0.0.0.0:80 {
    protocol http
    table TableHTTP
    fallback 127.0.0.1:7890
}

listener 0.0.0.0:443 {
    protocol tls
    table TableHTTPS
    fallback 127.0.0.1:7891
}

table TableHTTP {
    example.myftp.org 10.0.0.16:9080
    example.noip.me 127.0.0.1:9080
    example.ddns.net 127.0.0.1:9080
}

table TableHTTPS {
    example.myftp.org 10.0.0.16:2443
    example.noip.me 127.0.0.1:3443
    example.ddns.net 127.0.0.1:4443
}
```

To reload sniproxy configuration without terminating existing connections simply send a SIGHUP via ```htop``` or ```kill```.
```
sudo kill -s SIGHUP $(</tmp/sniproxy.pid)
```


## Honeypots for disconnecting bots

https://github.com/ran-sama/http-and-https-honeypot  

## License
Licensed under the WTFPL license.
