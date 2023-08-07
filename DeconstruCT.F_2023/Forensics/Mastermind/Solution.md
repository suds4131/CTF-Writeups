### Description
You are a hugeee swiftie! You really want to go to The Era's Tour but cannot because you are located in India. You call up Taylor Swift to request her to come to India. She will only come if you can get her a flag. Here's a recording of the call. Can you get her the flag?

### Solution

After hearing the provided audio file, we can conclude that some telephone numbers are being pressed and these tones are called the DTMF tones.

I initially tried decoding them with the response voice but wasn't getting accurate results. So i split the initial wav file into 4 parts with only the DTMF tones.

I tried many tools but [this website](http://dialabc.com/sound/detect/index.html) gave me the best results.

And finally I got the following outputs from the 4 files.
```
41323036267601217574 36710992825315281347 60924906937541136999 02333
```
We can remove the spaces to get `41323036267601217574367109928253152813476092490693754113699902333`.

Then we can convert decimal to hex using [this](https://www.rapidtables.com/convert/number/decimal-to-hex.html) website.

Getting the bytes from hex gives us the flag: -
```
$ echo 6473637B6D30746833725F31735F6D3074683372316E675F74737D | xxd -r -p
dsc{m0th3r_1s_m0th3r1ng_ts}
```

### Flag
`dsc{m0th3r_1s_m0th3r1ng_ts}`
