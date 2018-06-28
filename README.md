# Shadowsocks Client Config in Centos

``shell
yum install python-pip

pip install shadowsocks
```

1. shadowsocks.json config file in /etc/shadowsocks.json

```
{
  "server":"your server ip",
  "server_port":your port,
  "local_port":1080,
  "password":"MyPassWord",
  "timeout":600,
  "method":"aes-256-cfb"
}
```


2.star client

```shell
 sslocal -c /etc/shadowsocks.json -d start
```

>list the client process use

```shell
ss -lntup | grep sslocal
```

### use polipo 

>install 

```shell
git clone https://github.com/jech/polipo.git
cd polipo
make all
make install
```

>write config for polipo in /etc/polipo/config
```shell
  socksParentProxy = "127.0.0.1:1080"
  socksProxyType = socks5
  logFile = /var/log/polipo
  logLevel = 99
  logSyslog = true
```

> start polipo

```shell
polipo -c /etc/polipo/config
```
>polipo listen 8123 port,list process like that

```shell
 ss -lntup | grep polipo
```

#### set env

```shell
export http_proxy=http://localhost:8123

#delete env

unset http_proxy
```
