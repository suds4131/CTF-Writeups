### Sonic Hide and Seek

We are given a wav file, 1st part of which sounds like a SSTV transmission, 2nd part has part 1 of the flag in its spectrogram.

![image](https://github.com/suds4131/CTF-Writeups/assets/128071555/1570c9cd-c59c-4844-b22c-5d6e601a1fb8)

Opening this file in deep sound gives us a hidden file named 3.txt which has part 3 of the flag.

![image](https://github.com/suds4131/CTF-Writeups/assets/128071555/0f089374-d233-4da1-9c4c-f4183e4b8376)

We get part 2 of the flag from the sstv transmission, I researched this suject online and found [this](https://ourcodeworld.com/articles/read/956/how-to-convert-decode-a-slow-scan-television-transmissions-sstv-audio-file-to-images-using-qsstv-in-ubuntu-18-04) cool blog, I also used it in the past to solve a similar chal.

Following the mentioned steps, we can get the 2nd part of the flag.

![image](https://github.com/suds4131/CTF-Writeups/assets/128071555/ba2e26c0-3ffa-4cdc-a413-60df36122d5e)

```
PART1: flag{aud105
PART2: _4r3_c00l_
PART3: 4r5n't_th3y?}
```

### Flag

`flag{aud105_4r3_c00l_4r5n't_th3y?}`
