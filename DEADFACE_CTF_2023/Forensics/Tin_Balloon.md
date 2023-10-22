### Tin Balloon

We are given a zip file containing 2 files, a mp3 and encrypted docx file.

```
$ unzip -l tin_baloon.zip 
Archive:  tin_baloon.zip
  Length      Date    Time    Name
---------  ---------- -----   ----
  9903700  2023-10-10 21:22   Sequence 01.mp3
    18944  2023-10-14 20:10   Untitlednosubject.docx
---------                     -------
  9922644                     2 files

$ file Untitlednosubject.docx 
Untitlednosubject.docx: CDFV2 Encrypted
```

Upon listening to the mp3 file, we hear some noise in between, thus checking out the spectrogram gives us the following.

![Spectrogram](https://github.com/suds4131/CTF-Writeups/blob/main/DEADFACE_CTF_2023/Forensics/sequence_01_spectrogram.png?raw=true)

It is the password for the encrypted docx, thus we decrypt it by the following.

```
$ msoffcrypto-tool ctf/deadface_ctf_23/tin_baloon/Untitlednosubject.docx ctf/deadface_ctf_23/tin_baloon/decrypted.docx -p Gr33dK1Lzz@11Wh0Per5u3
$ unzip -l decrypted.docx 
Archive:  decrypted.docx
  Length      Date    Time    Name
---------  ---------- -----   ----
     1312  1980-01-01 00:00   [Content_Types].xml
      590  1980-01-01 00:00   _rels/.rels
     3627  1980-01-01 00:00   word/document.xml
      817  1980-01-01 00:00   word/_rels/document.xml.rels
     8393  1980-01-01 00:00   word/theme/theme1.xml
     3103  1980-01-01 00:00   word/settings.xml
    29455  1980-01-01 00:00   word/styles.xml
      894  1980-01-01 00:00   word/webSettings.xml
     1658  1980-01-01 00:00   word/fontTable.xml
      751  1980-01-01 00:00   docProps/core.xml
      989  1980-01-01 00:00   docProps/app.xml
---------                     -------
    51589                     11 files
```

Upon opening the file, we get to see the below: -
```
We have the ID card of one the brand new employees Alejandro, We now know the location of Techno Global, we have a man on sight that has been tailing him. We believe we can get into the facility at 3 am. We don’t know how long we can have a foothold on the system but we are going to use Wh1t3_N01Z3.exe to sent out a reverse shell. Be prepared to listen for the signal.
```

### Flag
`flag{Wh1t3_N01Z3.exe}`
