### Solution
Exiftool provided lots of info.

```
$ binwalk ctf/Deconstructf/snowy_rock_fi.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
13250         0x33C2          TIFF image data, big-endian, offset of first image directory: 8
28624         0x6FD0          Copyright string: "Copyright (c) 1998 Hewlett-Packard Company"
248341        0x3CA15         Zip archive data, encrypted at least v2.0 to extract, compressed size: 1037, uncompressed size: 2289, name: snowyrock.txt
249548        0x3CECC         End of Zip archive, footer length: 22
```

The extracted zip file was encrypted thus, we use zip2john to extract hash and crack it using rockyou.txt which. After cracking we get the password i.e, `11snowbird`.
Using the password gives us snowyrock.txt.
I was stuck here for a long time, I knew it had to do with `stegsnow` but I was trying various passwords with it.
There was the below segment in snowy_rock.txt
```
//////////////snow/flag/
*Something about friday the ......... :P*
///////////////////
```
So I tried various Friday the 13th charecters names as passwords. But turns out it is a different hint.
You don't need a password for the `stegsnow` part. (Bruh)
```
$ stegsnow -C snowyrock.txt                               
OFTHA62GMFBGUX3FIJYFQZS7ONBGKX3FGM2HS7I=
$ echo OFTHA62GMFBGUX3FIJYFQZS7ONBGKX3FGM2HS7I= | base32 -d
qfp{FaBj_eBpXf_sBe_e34y}
$ echo 'qfp{FaBj_eBpXf_sBe_e34y}' | rot13                          
dsc{SnOw_rOcKs_fOr_r34l}
```
The Friday the 13th hint was for the last part.

### Flag
`dsc{SnOw_rOcKs_fOr_r34l}`
