### Description
Brian tries to send some crucial information from the spacestation about an impending disaster through a super secure line to his friend through a picture. Help his friend uncover the truth.

### Solution
Running exiftool on super_secret.jpg
```
$ exiftool super_secret.jpg
...
Comment                         : the aliens are here try slowscan
Image Width                     : 2394
Image Height                    : 1690
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:4:4 (1 1)
Image Size                      : 2394x1690
Megapixels                      : 4.0
```
`slowscan`: I google this and came across SSTV. I also came across [this](https://ourcodeworld.com/articles/read/956/how-to-convert-decode-a-slow-scan-television-transmissions-sstv-audio-file-to-images-using-qsstv-in-ubuntu-18-04) awsome blog which was helpful later.
Running binwalk.
```
$ binwalk super_secret.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
166246        0x28966         Zip archive data, at least v1.0 to extract, compressed size: 9725992, uncompressed size: 9725992, name: hidden.jpg
9892256       0x96F1A0        End of Zip archive, footer length: 22
9892370       0x96F212        End of Zip archive, footer length: 22
```
Running binwalk on hidden.jpg.
```
binwalk hidden.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
30            0x1E            TIFF image data, little-endian offset of first image directory: 8
39697         0x9B11          Zip archive data, at least v2.0 to extract, compressed size: 9686117, uncompressed size: 10611338, name: SupEr_s3CrET_AuD10.wav
9725970       0x946812        End of Zip archive, footer length: 22
```
We can use our previously fonud blog along with this audio file to decode image from audio.
![image](https://github.com/suds4131/CTF-Writeups/assets/128071555/3927763c-a3e9-4817-ab7f-68c6a80f52cc)

Scanning the QR code gives `dsc{un5af3_sp4C3_coD3}`.

### Flag
`dsc{un5af3_sp4C3_coD3}`
