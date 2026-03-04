Before we begin, i would really love to  start by saying that this was a hard but terrible ctf <br>
but we can still proceed anyways. <br>

so we have a our file red.png<br>
As always, we can use binwalk, file and exiftool to check for any interesting info<br>

### Binwalk: <br>
```bash
 binwalk red.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 128 x 128, 8-bit/color RGBA, non-interlaced
284           0x11C           Zlib compressed data, default compression
```
### File:
```bash
file red.png
red.png: PNG image data, 128 x 128, 8-bit/color RGBA, non-interlaced
```

### exiftool: <br>
```bash
exiftool red.png
ExifTool Version Number         : 12.57
File Name                       : red.png
Directory                       : .
File Size                       : 796 bytes
File Modification Date/Time     : 2026:03:03 15:43:32+03:00
File Access Date/Time           : 2026:03:03 00:00:00+03:00
File Inode Change Date/Time     : 2026:03:03 15:43:34+03:00
File Permissions                : -rwxr-xr-x
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 128
Image Height                    : 128
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Poem                            : Crimson heart, vibrant and bold,.Hearts flutter at your sight..Evenings glow softly red,.Cherries burst with sweet life..Kisses linger with your warmth..Love deep as merlot..Scarlet leaves falling softly,.Bold in every stroke.
Image Size                      : 128x128
Megapixels                      : 0.016
```

So i tried taking my first outcome as my decision maker.<br>
and i tried to unzip the document using the following command from dd since steghide doesnt accept png i think. <br>
```bash
dd if=red.png of=red.zlib skip=284 bs=1 
512+0 records in
512+0 records out
512 bytes copied, 0.496899 s, 1.0 kB/s
```
so i thought that the document was holding important information and decided to print some of it: <br>

```bash
strings red.zlib
IEND
```

Holding the string can be so important after <br>
we can look furthur and use these tools,```https://aperisolve.fr/  (online)``` ```stegseek (password cracker) ``` ```zsteg (png) ``` ``` steghide (jpeg/jpg)```<br>
### Aperisolve
has the flag but lets do it manually <br>

### Stegseek
there was no cracking needed

### zsteg 
We should use zsteg because our image is a png so that cancels out steghide<br>

```bash
08:38:12 kr0u@penguin Red → zsteg red.png
meta Poem           .. text: "Crimson heart, vibrant and bold,\nHearts flutter at your sight.\nEvenings glow softly red,\nCherries burst with sweet life.\nKisses linger with your warmth.\nLove deep as merlot.\nScarlet leaves falling softly,\nBold in every stroke."
chunk:0:IHDR        .. file: Adobe Photoshop Color swatch, version 0, 128 colors; 1st RGB space (0), w 0x80, x 0x806, y 0, z 0; 2nd HSB space (1), w 0x100, x 0, y 0xff01, z 0xff
b1,rgba,lsb,xy      .. text: "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ=="
b1,rgba,msb,xy      .. file: OpenPGP Public Key
b2,g,lsb,xy         .. text: "ET@UETPETUUT@TUUTD@PDUDDDPE"
b2,rgb,lsb,xy       .. file: OpenPGP Secret Key
b2,bgr,msb,xy       .. file: OpenPGP Public Key
b2,rgba,lsb,xy      .. file: OpenPGP Secret Key
b2,rgba,msb,xy      .. text: "CIkiiiII"
b2,abgr,lsb,xy      .. file: OpenPGP Secret Key
b2,abgr,msb,xy      .. text: "iiiaakikk"
b3,rgba,msb,xy      .. text: "#wb#wp#7p"
b3,abgr,msb,xy      .. text: "7r'wb#7p"
b4,b,lsb,xy         .. file: 0421 Alliant compact executable not stripped
08:38:20 kr0u@penguin Red → echo "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==" | base64 -d
picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}
```


# 0xKr0u PWNED THIS LAB!!!
and we got our flag!!

