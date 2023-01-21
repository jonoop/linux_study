### ssh无法连接docker container
```
kex_exchange_identification: Connection closed by remote host
```

解决方法：
```
sudo apt-get update
sudo apt-get install openssl-server
sudo service ssh start
```

### ssh报错
```
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ED25519 key sent by the remote host is
SHA256:1Wl0GBrg8t0VXFZ1LeLMmvWlWgKlIgQhyvu09oT3rk4.
Please contact your system administrator.
Add correct host key in /Users/cyk3/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /Users/cyk3/.ssh/known_hosts:6
Host key for [192.81.131.209]:20000 has changed and you have requested strict checking.
Host key verification failed.
```
解决方法：
```
ssh-keygen -f ".ssh/known_hosts" -R "[192.81.131.209]:20000"
```
