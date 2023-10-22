### Host Busters 4

Get upto having a shell as root, follow Host Busters 5 writeup.

You can do it in 2 ways, either check .bash_history and download the proposal.pdf for yourself or just cat it on the remote machine.
```
root@a5f852d7b453:/home/spookyboi# cat.bash_history
ls
ip a
ls -l
cd .keys
cd..
wget https://tinyurl.com/mr47bxn7
file mr47bxn7
mv mr47bxn7 proposal.pdf
```

Download the proposal.pdf from the url and open it, we get the flag.

```
root@a5f852d7b453:/home/spookyboi# cat proposal.pdf
...
SG9zdCBCdXN0ZXJzIDQ6IGZsYWd7QWJ1czNfb0ZfcDB3M1J9Cg==

kali@kali:~$ echo SG9zdCBCdXN0ZXJzIDQ6IGZsYWd7QWJ1czNfb0ZfcDB3M1J9Cg== | base64 -d
Host Busters 4: flag{Abus3_oF_p0w3R}
```

### Flag
`flag{Abus3_oF_p0w3R}`
