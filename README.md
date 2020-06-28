# Фильтрация трафика 

```
chmod +x setup.sh guest/knock.sh disable-if-eth0.sh
```

## knocking port

```
ssh -i ~/.vagrant.d/insecure_private_key -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null vagrant@127.0.0.1 -p 8001
```
Убедимся, что ssh-порт закрыт:
```
ssh 192.168.255.1
```
Откроем порт через knock-скрипт:
```
/vagrant/guest/knock.sh open
```
Убедимся, что ssh-порт открыт:
```
ssh 192.168.255.1
exit
```
Закроем ssh-порт:
```
/vagrant/guest/knock.sh close
```
