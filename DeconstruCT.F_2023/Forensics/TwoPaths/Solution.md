### Description
Logan gave me this image file before disappearing..
I've been breaking my head over it for long
Can you decode it?

### Solution
Running binwalk gives us 2 files i.e., greenpill.jpg and redpill.jpg.
```
$ binwalk hello.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
30            0x1E            TIFF image data, little-endian offset of first image directory: 8
1801          0x709           Copyright string: "Copyright (c) 1998 Hewlett-Packard Company"
86856         0x15348         Zip archive data, at least v2.0 to extract, compressed size: 151849, uncompressed size: 152413, name: greenpill.jpg
238726        0x3A486         End of Zip archive, footer length: 22
238748        0x3A49C         Zip archive data, at least v1.0 to extract, compressed size: 41267125, uncompressed size: 41267125, name: redpill.jpg
41505892      0x2795464       End of Zip archive, footer length: 22
41506102      0x2795536       End of Zip archive, footer length: 22
```
Run binwalk on the extracted files now.
```
binwalk greenpill.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
89956         0x15F64         Zip archive data, at least v2.0 to extract, compressed size: 62307, uncompressed size: 71081, name: flag.jpg
152391        0x25347         End of Zip archive, footer length: 22

$ binwalk redpill.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
68806         0x10CC6         Zip archive data, at least v2.0 to extract, compressed size: 1228, uncompressed size: 175644, name: morse.wav
70073         0x111B9         Zip archive data, at least v1.0 to extract, compressed size: 41196805, uncompressed size: 41196805, name: secrett.zip
41266897      0x275AED1       End of Zip archive, footer length: 22
41267103      0x275AF9F       End of Zip archive, footer length: 22
```
The flag.jpg from greenpill.jpg is a troll.
We get 2 files from the zip in redpill.jpg i.e., morse.wav and secrett.zip.
secrett.zip is encrypted and contains a file named deep_secret.wav, thus going forward with morse.wav.
We decode the morse.wav using audio morse code decoder [this](https://morsecode.world/international/decoder/audio-decoder-adaptive.html) works for me fine.
Decoded morse: `T H E P A S S W O R D I S T H E H O V E R C R A F T O F M O R P H E U S`
Thus from the above the password is `nebuchadnezzar`.
`7z x secrett.zip` gives us the deep_sound.wav

From previous experience, whenever I see "deep" mentioned in a audio based challenge I am immediately reminded of `DeepSound`.
I learnt about it from [here](https://wiki.bi0s.in/steganography/deep-sound/).
Opening the deep_sound.wav in DeepSound gives us a file named `twopathsflag.txt` which can be extracted to our specified destination.

![image](https://github.com/suds4131/CTF-Writeups/assets/128071555/8ce1aeb2-50c7-4924-ada2-426e126e5dac)

The text file gives us the flag `dsc{u_ch053_THE_cOrr3Ct_pill!}`.

### Flag
`dsc{u_ch053_THE_cOrr3Ct_pill!}`
