### Fetching Secrets

Using stegseek on the image with rockyou.txt as worlist. As steghide without a password doesn't give us anything.

```
stegseek image.png rockyou.txt
```

Running it will give us a password of `kira` and also automatically extract the contents into a new file.
The created flag.txt will contain the flag.

### Flag
`flag{g00d_dawg_woofw00f}`
