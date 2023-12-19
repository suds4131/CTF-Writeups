### Forenscript

Analyzing the given file in a hexeditor, we see that the original file has been grouped into bytes of 4 and reversed every block, so reversing once more will give us the original. I wrote a small script for that.

```py
f = open('a.bin','rb')
a = f.read()
#print(a,len(a),type(a))
b = b""
for i in range(0,len(a),4):
	b += (a[i:i+4])[::-1]
#print(b)
f.close()
w = open("b.png","wb")
w.write(b)
w.close()
```

![b.png](https://raw.githubusercontent.com/suds4131/CTF-Writeups/main/BackdoorCTF_2023/Forensics/b.png)

The newly created png file has another png file embedded within it, I used HxD to extract it, we can use binwalk or any other tool like dd.

The extracted png from b.png has the final flag.

![c.png](https://raw.githubusercontent.com/suds4131/CTF-Writeups/main/BackdoorCTF_2023/Forensics/c.png)

### Flag

`flag{scr1pt1ng_r34lly_t0ugh_a4n't_1t??}`
