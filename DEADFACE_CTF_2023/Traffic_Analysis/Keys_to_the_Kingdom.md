### Keys to the Kingdom

Upon checking out the provided PCAP, we see TCP data being transmitted in 34 packets. And the "JFIF" string in the first data packet is enough for us to realize that a jpg image is being transferred.

```
$ tshark -r Thekeytothekingdom.pcap -T fields -e tcp.payload > 1.raw.txt
$ # The hex data from different packets will be on different lines. Thus we delete the lines and decode the hex, which gives us a jpg file.
$ cat 1.raw.txt | tr -d '\n' | xxd -r -p > 1.raw.jpg
$ file 1.raw.jpg
1.raw.jpg: JPEG image data, JFIF standard 1.01, aspect ratio, density 1x1, segment length 16, baseline, precision 8, 700x939, components 3
```

Given Ciphertext in chall description: `ÓÄÖëÄøõàñããàøâñãõùãªÞåýåøåûåýñûùñûùñùñüåþñýÿâí`

Upon using the magic module of Cyber Chef with intensive mode on the provided ciphertext, we get the below: -

![CC](https://github.com/suds4131/CTF-Writeups/blob/main/DEADFACE_CTF_2023/Traffic_Analysis/cyberchef_ct.png?raw=true)

It is a XOR with 0x90.

We get `CTF{Thepassphraseis:Numuhukumakiakiaialunamor}`, this passphrase can be used with steghide to extract the encrypted file.

```
$ steghide extract -sf 1.raw.jpg
Enter passphrase:
wrote extracted data to "flag.txt".
$ cat flag.txt
flag{Error404FlagNotFound}
```

### Flag
`flag{Error404FlagNotFound}`
