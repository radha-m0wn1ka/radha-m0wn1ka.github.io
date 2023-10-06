## video to audio converter
```
https://challenge-0723.intigriti.io/
https://www.youtube.com/watch?v=032mvb1038E
for white space in linux terminal u can use  ${IFS}
dd command
┌──(radha㉿kali)-[~/Downloads/xss/july23]
└─$ dd if=/dev/zero of=dd.mp4 bs=1024 count=1
file ls 
tldr to get example commands
ls -lh file_name longlist with human readale formate
command substitution
date_var=`date`
date_var=$(date)
assign and access vars by
'''
var1=9
echo $var1
'''
set}
env}to see assigned vars
source ~/.bashrc ::to restrate the sesion
~ means home
echo 'export MY_VARIABLE="new_value"' >> ~/.bashrc
                                                                                                                                                                       
┌──(radha㉿kali)-[~/Downloads/xss/july23]
└─$ echo "hi`ls`"  
┌──(radha㉿kali)-[~/Downloads/xss/july23]
└─$ echo "hii$(sleep 5)HIIIIII"


```
## NGROK WEBSERVER LOCAL
```
In a empty dirctory $webup
in anothr terminal say ngrok 80
u will get a url
request to that url can be seen in terminal webup
