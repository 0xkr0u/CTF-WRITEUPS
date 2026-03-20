# Disk Analysis & Autopsy

Welcome to the disk analysis and autopsy. <br>
To begin with,we need to know a few things here <br>
You will need these tools and knowledge about them : <br>

```bash
1. Autopsy
2. Windows FileSystem
```
## We may begin : 
Make sure you have signed in with the credentials below: <br>

```bash
IP: X.X.X.X
Username: administrator
Password: letmein123!
```

You can connect using Remmina <br>

Lets Start the investigation now.<br>

The first question is<br>
```
What is the MD5 hash of the E01 image?
```

there is a document that comes with the same name but with a different file extension: <br>
```
HASAN2.E01.txt
```
which has the file hashes <br>
```
 MD5 checksum:    3f08c518adb3b5c1359849657a9b2079
 SHA1 checksum:   d5ae22ab381cb5884140ef6bfab3946a8f3cf9f2
```

So we have the answer for the first question <br>
Another way you can get the file hash is : <br>
```
Get-FileHash -Path C:\Users\Administrator\Desktop\'Case Files'\HASAN2.E01 -Algorithm MD5
```


