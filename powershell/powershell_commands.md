# Powershell Commands

## GET HEX 
```
$ Format-Hex .\pfx\publickey.cer
```
## Encode bytes
```
$FilePath = "c:\setup\foo.exe"
$File = [System.IO.File]::ReadAllBytes($FilePath);
$Base64String = [System.Convert]::ToBase64String($File);
 ```