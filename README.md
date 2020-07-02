# Фильтрация трафика 

Схема стенда:

![alt-текст](https://github.com/awesomenmi/iptables/blob/master/Untitled%20Diagram%20(1).png)

Предварительные настройки и запуск стенда:
```
chmod +x setup.sh guest/knock.sh disable-if-eth0.sh
vagrant up
./setup.sh
```

## knocking port

Подключимся к _centralRouter_:
```
ssh -i ~/.vagrant.d/insecure_private_key -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null vagrant@127.0.0.1 -p 8001
```
Убедимся, что ssh-порт закрыт:
```
ssh 192.168.255.1
```
Откроем порт через knock-скрипт:
```
[vagrant@centralRouter ~]$ /vagrant/guest/knock.sh open
ssh port was opened
```
Убедимся, что ssh-порт открыт:
```
[vagrant@centralRouter ~]$ ssh 192.168.255.1
The authenticity of host '192.168.255.1 (192.168.255.1)' can't be established.
ECDSA key fingerprint is SHA256:yGpMMxXCxn3C/6VL0lQXAXg0+2IHAwA85JxW4vcDeDY.
ECDSA key fingerprint is MD5:f8:7b:d3:45:88:14:93:0d:83:1e:6e:2b:aa:9a:9a:b4.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.255.1' (ECDSA) to the list of known hosts.
[vagrant@inetRouter ~]$ exit
logout
Connection to 192.168.255.1 closed.
```
Закроем ssh-порт:
```
[vagrant@centralRouter ~]$ /vagrant/guest/knock.sh close
ssh port was closed
```

## port-forwarding

Подключимся к _inetRouter2_:
```
[vagrant@centralRouter ~]$ ssh 192.168.254.1

```

```
[root@inetRouter2 vagrant]# curl -I localhost:8080
HTTP/1.1 200 OK
Server: nginx/1.16.1
Date: Thu, 02 Jul 2020 12:14:29 GMT
Content-Type: text/html
Content-Length: 4833
Last-Modified: Fri, 16 May 2014 15:12:48 GMT
Connection: keep-alive
ETag: "53762af0-12e1"
Accept-Ranges: bytes
```

_curl_ с хостовой машины:
```
[root@localhost homeww17]# curl -I localhost:8080
HTTP/1.1 200 OK
Server: nginx/1.16.1
Date: Thu, 02 Jul 2020 12:21:32 GMT
Content-Type: text/html
Content-Length: 4833
Last-Modified: Fri, 16 May 2014 15:12:48 GMT
Connection: keep-alive
ETag: "53762af0-12e1"
Accept-Ranges: bytes

```

P.S. Подключение к _centralServer_:
```
ssh -i ~/.vagrant.d/insecure_private_key -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null vagrant@127.0.0.1 -p 8002
```

