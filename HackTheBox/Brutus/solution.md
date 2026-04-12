# Investigating an auth.log

Download the file and unzip using the password ```hacktheblue```

unzip doesn't work on my side so using ```7z x <filename>``` worked best.

and now we have the auth.log


We can start with comparing failed attempts and succesful attempts and verdict something useful


```
cat auth.log | grep -iE "accepted|failed"
Mar  6 06:19:52 ip-172-31-35-28 sshd[1465]: AuthorizedKeysCommand /usr/share/ec2-instance-connect/eic_run_authorized_keys root SHA256:4vycLsDMzI+hyb9OP3wd18zIpyTqJmRq/QIZaLNrg8A failed, status 22
Mar  6 06:19:54 ip-172-31-35-28 sshd[1465]: Accepted password for root from 203.101.190.9 port 42825 ssh2
Mar  6 06:31:33 ip-172-31-35-28 sshd[2327]: Failed password for invalid user admin from 65.2.161.68 port 46392 ssh2
Mar  6 06:31:33 ip-172-31-35-28 sshd[2331]: Failed password for invalid user admin from 65.2.161.68 port 46436 ssh2
```
Verdict:
login attempts after a succesful one indicates that the ip: ```203.101.190.9``` is legitimate and ip: ```65.2.161.68``` is quite the suspicous one


now we have sth we can cling on.
We can filter all content that is using the ip addres ```65.2.161.68``` and it in a text file.
```bash
cat auth.log | grep -i "65.2.161.68" > 65_2_161_68.txt
```
or you can just ise ```ctrl``` + ```shift``` + ```f``` in sublime text and you will get it separately 

from a clear point of view i can see that there is a brute force of both password and usernames.
```
backup 
admin 
server_adm
svc_account
root
```
And realized that user root was succesfully logged in within the bruteforce and even <b>after the bruteforce</b>.
now more activity shows that another user pops up who is cyberjunkie.

which we can assume is the method used for persistence


## I will not display the flags but this should serve as a guide line
