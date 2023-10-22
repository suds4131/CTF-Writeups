### Host Busters 2

Was doing my usual recon I do on linux machines during privesc and found a weird open udp port.

```
vim@77be64eddf2b:~$ ss -tulpn
Netid    State     Recv-Q    Send-Q       Local Address:Port        Peer Address:Port    Process
udp      UNCONN    0         0                  0.0.0.0:9023             0.0.0.0:*        users:(("srv",pid=7,fd=3))
tcp      LISTEN    0         128                0.0.0.0:22               0.0.0.0:*
tcp      LISTEN    0         128                   [::]:22                  [::]:*
vim@77be64eddf2b:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
vim            1  0.0  0.0   2576   948 pts/0    Ss   15:59   0:00 /bin/sh /usr/bin/start
vim            7  0.0  0.0   1036   740 pts/0    S    15:59   0:00 /usr/bin/srv
vim            8  0.3  0.0  11692  9200 pts/0    Sl   15:59   0:00 /bin/vim /home/gh0st404/config
vim           10  0.0  0.0   2576   920 pts/0    S    15:59   0:00 sh -c /bin/bash
vim           11  0.0  0.0   4188  3440 pts/0    S    15:59   0:00 /bin/bash
root          20  0.0  0.0  15404  1316 ?        Ss   15:59   0:00 sshd: /usr/sbin/sshd [listener] 0 of 10-100 startups
vim           23  0.0  0.0   8088  3964 pts/0    R+   15:59   0:00 ps aux
```

So just connected to it using netcat to check what's up.

```
vim@77be64eddf2b:~$ nc -nv 127.0.0.1 -u 9023
(UNKNOWN) [127.0.0.1] 9023 (?) open

flag{Hunt_4_UDP_s3rv3r}
flag{Hunt_4_UDP_s3rv3r}^C
```
Flags start popping everytime i hit enter.

### Flag
`flag{Hunt_4_UDP_s3rv3r}`
