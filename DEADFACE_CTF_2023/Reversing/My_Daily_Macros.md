### My Daily Macros

We are given a HR_List.zip file.
```
$ unzip -l MDM_HR_List.zip 
Archive:  MDM_HR_List.zip
  Length      Date    Time    Name
---------  ---------- -----   ----
    17770  2023-10-12 19:31   HR_List.xlsm
---------                     -------
    17770                     1 file
$ unzip MDM_HR_List.zip
$ file HR_List.xlsm          
HR_List.xlsm: Microsoft Excel 2007+
$ unzip -l HR_List.xlsm
  Length      Date    Time    Name
---------  ---------- -----   ----
     1223  1980-01-01 00:00   [Content_Types].xml
      588  1980-01-01 00:00   _rels/.rels
     1625  1980-01-01 00:00   xl/workbook.xml
      820  1980-01-01 00:00   xl/_rels/workbook.xml.rels
    18760  1980-01-01 00:00   xl/worksheets/sheet1.xml
     7079  1980-01-01 00:00   xl/theme/theme1.xml
     1547  1980-01-01 00:00   xl/styles.xml
    10073  1980-01-01 00:00   xl/sharedStrings.xml
    14848  1980-01-01 00:00   xl/vbaProject.bin
      682  1980-01-01 00:00   docProps/core.xml
      814  1980-01-01 00:00   docProps/app.xml
---------                     -------
    58059                     11 files
```

This excel sheet contains macro, we can see that by the .xlsm extension and also the presence of a vbaProject.bin file.
We can use olevba to extract the vba from this file.

```
$ olevba ~/ctf/deadface_ctf_23/MDM/xl/vbaProject.bin
VBA MACRO Module1 
in file: /home/kali/ctf/deadface_ctf_23/MDM/xl/vbaProject.bin - OLE stream: 'Module1'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Sub Deadface()
function Invoke-RandomCode {
    $randomCodeList = @(
        {
            # Random code block 1
            Write-Host "Hello, World!"
            $randomNumber = Get-Random -Minimum 1 -Maximum 100
            Write-Host "Random number: $randomNumber"
        },
        {
            # Random code block 2
            # flag{youll_never_find_this_}
            $randomString = [char[]](65..90) | Get-Random -Count 5 | foreach { [char]$_ }
            Write-Host "Random string: $randomString"
        },
        {
            # Random code block 3
            $currentTime = Get-Date
            Write-Host "Current time: $currentTime"
        }
    )

    $randomIndex = Get-Random -Minimum 0 -Maximum $randomCodeList.Count
    $randomCodeBlock = $randomCodeList[$randomIndex]

    & $randomCodeBlock
}

Invoke -RandomCode

End Sub
-------------------------------------------------------------------------------
VBA MACRO ThisWorkbook 
in file: /home/kali/ctf/deadface_ctf_23/MDM/xl/vbaProject.bin - OLE stream: 'ThisWorkbook'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
(empty macro)
-------------------------------------------------------------------------------
VBA MACRO Sheet1 
in file: /home/kali/ctf/deadface_ctf_23/MDM/xl/vbaProject.bin - OLE stream: 'Sheet1'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
(empty macro)
+----------+--------------------+---------------------------------------------+
|Type      |Keyword             |Description                                  |
+----------+--------------------+---------------------------------------------+
|Suspicious|Write               |May write to a file (if combined with Open)  |
|Suspicious|Hex Strings         |Hex-encoded strings were detected, may be    |
|          |                    |used to obfuscate strings (option --decode to|
|          |                    |see all)                                     |
+----------+--------------------+---------------------------------------------+
```

The flag is in the form of a comment.

This can also be extracted by oledump.py
```
$ python3 oledump.py ~/ctf/deadface_ctf_23/MDM/xl/vbaProject.bin     
  1:       531 'PROJECT'
  2:        86 'PROJECTwm'
  3: M    2667 'VBA/Module1'
  4: m     977 'VBA/Sheet1'
  5: m     985 'VBA/ThisWorkbook'
  6:      2644 'VBA/_VBA_PROJECT'
  7:      1130 'VBA/__SRP_0'
  8:        74 'VBA/__SRP_1'
  9:       136 'VBA/__SRP_2'
 10:       103 'VBA/__SRP_3'
 11:       573 'VBA/dir'
$ python3 oledump.py ~/ctf/deadface_ctf_23/MDM/xl/vbaProject.bin -s 3 -v
Attribute VB_Name = "Module1"
Sub Deadface()
function Invoke-RandomCode {
...
...
End Sub
```

### Flag
`flag{youll_never_find_this_}`
