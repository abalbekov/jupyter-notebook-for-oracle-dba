This technique can be used to transfer and then remotely execute a Unix shell script while running Jupyter Notebook on Windows.
It uses "pscp" and "plink" commands from putty family. These commands need to be in system PATH.

Steps:

1. On Windows create a shell script aaa.sh and save using path relative to notebook location

``` shell
aaa.sh :

echo "parameter : $1"
```

2. Then transfer and remotely execute the script :

``` python

HOST="remote_host"
USER="remote_user"
print("Enter password :")
import getpass
psw=getpass.getpass()

print("Transfering script ...")
!pscp -pw {psw} aaa.sh {USER}@{HOST}:/tmp 2>NUL

print("setting SSH alias ...") 
%alias SSH plink -batch -pw {ora_psw} {USER}@{HOST}

print("Setting executable bit ...")
%SSH chmod u+x /tmp/aaa.sh  2>NUL

print("Executing ...")
param="Hey!"
%SSH /tmp/aaa.sh {param} 2>NUL
```

```
Output :

Enter password :
········
Transfering script ...

aaa.sh                    | 0 kB |   0.0 kB/s | ETA: 00:00:00 | 100%
setting SSH alias ...
Setting executable bit ...
Executing ...
parameter : Hey!
```
