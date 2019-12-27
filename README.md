

## Installation

CoreOS

Download CoreOS image
``` 
https://coreos.com/os/docs/latest/booting-with-iso.html

add new user
https://coreos.com/os/docs/latest/adding-users.html

Generating RSA Key
https://help.github.com/en/enterprise/2.17/user/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
```

Set Password for CoreOS

```
sudo passwd core

enter your password
```

SSH To CoreOS

```
ssh core@ip

enter password
```

Create  ``` ignition.json on your computer ``` for confing CoreOS 

Hash Password with openssl
```
openssl passwd -1

enter your passord
```

```
{
 "ignition": {
   "config": {},
   "security": {
     "tls": {}
   },
   "timeouts": {},
   "version": "2.2.0"
 },
 "networkd": {
   "units": [
     {
       "contents": "[Match]\nName=eth0\n\n[Network]\nAddress=192.168.0.101/24\nGateway=192.168.0.2\nDNS=8.8.8.8 8.8.4.4\n",
       "name": "static.network"
     }
   ]
 },
 "passwd": {
   "users": [
     {
       "groups": [
         "sudo",
         "docker"
       ],
       "name": "server", //server name
       "passwordHash": "$1$xe8P8N70$P3VQrp.F61VF06c.xxumk1",
       "sshAuthorizedKeys": [
         "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDz9+d/rDGqAUkVRTwH/p0wlgpVQZT302GG8XvU40oc8JrLjIN52Q0U6qHADSR/JdM3wNxctxyQkYDTScn9h8Cds+FYMXZ27CV79ZK1uNPA4UgmvLOl9nTj6ZLHj7pzHrBsgjyhC/9AA7D/r/7e1gF75V3N7VgdZoWIX7YXErmgzdyB1njP8SJvN92Ow5w9LWt36h8wSYN+/RmKqeqn0fn+21G4gZq3i/JYTaPlbTkwSKpRbVShASFWdSVZhJNllOypJiyopP2KhHossURpHw7FpDaCBpQrKaTMQOYJPB08XnK3gGq7AF+rVNMf70V8O3NEWKoMPdva5qakYLvqEyScE2O4Ihuj6gtkg6ma06CD0z23m75no6jPOp3LxFcWNI0mnYs77fjwvfdd1wLy5oSOssrXjVV7avq7rzRuQvtKT8LPXTGADF1GFI5zvmk+bGO9yxX/hGh2cGabaSWlhAtovh4b1Ed6GE9CBplPuPPy5rKK6oPPsYtQYIcCjC2+ycMPchXi9aUGICKlArnOIXm1Xdg4L2qApnVrQnqIr1Uvpg7bmHq5lgazSmWk8cqUDuZcsoFDMPrVH2/Ud59UGW5Ajbvqy/x4WJHsEvq8AsAqdv1nkGbEuGtpmoqS3si3CE6UlhZmRq1eGsetuAsriy3L6aquq3GM0mfhs02cc5D76w== server"
       ]
     }
   ]
 },
 "storage": {
   "files": [
     {
       "filesystem": "root",
       "path": "/etc/hostname",
       "contents": {
         "source": "data:,coreos1",
         "verification": {}
       },
       "mode": 420
     }
   ]
 },
 "systemd": {}
}


```


# How to copy file remotely via SSH
from ``` https://www.simplified.guide/ssh/copy-file ```


1. Copy single file from local to remote.
```
$ scp myfile.txt remoteuser@remoteserver:/remote/folder/
```

2. Copy single file from remote to local.
```
$ scp remoteuser@remoteserver:/remote/folder/myfile.txt  myfile.txt
```

3. Copy multiple files from local to remote.
```
$ scp myfile.txt myfile2.txt remoteuser@remoteserver:/remote/folder/
```
4. Copy all files from local to remote.
``` 
$ scp * remoteuser@remoteserver:/remote/folder/
```

5. Copy all files and folders recursively from local to remote.
```
$ scp -r * remoteuser@remoteserver:/remote/folder/
```