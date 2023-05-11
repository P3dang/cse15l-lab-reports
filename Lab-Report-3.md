**Finding files by name**
```find -name [name of file]
```
çFinding specific types of files in a directory:**
```
find  -type [file_type] 
```
Here are different types of files you can search for and their coresponding character:
```
f: regular file
d: directory
l: symbolic link
c: character device file
b: block device file
p: named pipe (FIFO)
s: socket
```
Using find command for direcotry:
```
[cs15lsp23ca@ieng6-202]:stringsearch-data:468$ find  ./technical -type d 
./technical
./technical/911report
./technical/biomed
./technical/government
./technical/government/About_LSC
./technical/government/Alcohol_Problems
./technical/government/Env_Prot_Agen
./technical/government/Gen_Account_Office
./technical/government/Media
./technical/government/Post_Rate_Comm
./technical/plos
[cs15lsp23ca@ieng6-202]:stringsearch-data:469$ 
```
```
[cs15lsp23ca@ieng6-202]:stringsearch-data:472$ find  ./technical/plos -type f 
./technical/plos/journal.pbio.0020001.txt
./technical/plos/journal.pbio.0020010.txt
./technical/plos/journal.pbio.0020012.txt
./technical/plos/journal.pbio.0020013.txt
./technical/plos/journal.pbio.0020019.txt
./technical/plos/journal.pbio.0020028.txt
./technical/plos/journal.pbio.0020035.txt
./technical/plos/journal.pbio.0020040.txt
./technical/plos/journal.pbio.0020042.txt
./technical/plos/journal.pbio.0020043.txt
./technical/plos/journal.pbio.0020046.txt
./technical/plos/journal.pbio.0020047.txt
./technical/plos/journal.pbio.0020052.txt
./technical/plos/journal.pbio.0020053.txt
./technical/plos/journal.pbio.0020054.txt
./technical/plos/journal.pbio.0020063.txt
./technical/plos/journal.pbio.0020064.txt
./technical/plos/journal.pbio.0020067.txt
./technical/plos/journal.pbio.0020068.txt
./technical/plos/journal.pbio.0020071.txt
./technical/plos/journal.pbio.0020073.txt
./technical/plos/journal.pbio.0020100.txt
./technical/plos/journal.pbio.0020101.txt
./technical/plos/journal.pbio.0020105.txt
./technical/plos/journal.pbio.0020112.txt
./technical/plos/journal.pbio.0020113.txt
./technical/plos/journal.pbio.0020116.txt
./technical/plos/journal.pbio.0020121.txt
./technical/plos/journal.pbio.0020125.txt
./technical/plos/journal.pbio.0020127.txt
./technical/plos/journal.pbio.0020133.txt
./technical/plos/journal.pbio.0020140.txt
./technical/plos/journal.pbio.0020145.txt
./technical/plos/journal.pbio.0020146.txt
./technical/plos/journal.pbio.0020147.txt
./technical/plos/journal.pbio.0020148.txt
./technical/plos/journal.pbio.0020150.txt
./technical/plos/journal.pbio.0020156.txt
./technical/plos/journal.pbio.0020161.txt
./technical/plos/journal.pbio.0020164.txt
./technical/plos/journal.pbio.0020169.txt
./technical/plos/journal.pbio.0020172.txt
./technical/plos/journal.pbio.0020183.txt
./technical/plos/journal.pbio.0020187.txt
```

I found this command from ChatGPT.
**Find files by size:**

```
find  -size [+/-][size][unit]
```

Here are all the different unit types with their coresponding suffix:

``` 
c: bytes
k: kilobytes (1024 bytes)
M: megabytes (1024 kilobytes)
G: gigabytes (1024 megabytes)
T: terabytes (1024 gigabytes)
```
But `b` will be used if no suffix is used which is a 512-byte blocks.

Examples: 

```
[cs15lsp23ca@ieng6-202]:stringsearch-data:478$ find  ./technical/plos -size -2k 
./technical/plos/pmed.0020191.txt
./technical/plos/pmed.0020226.txt
```

```
[cs15lsp23ca@ieng6-202]:stringsearch-data:479$ find  ./technical/plos -size +20k 
./technical/plos/journal.pbio.0020053.txt
./technical/plos/journal.pbio.0020113.txt
./technical/plos/journal.pbio.0020161.txt
./technical/plos/journal.pbio.0020347.txt
./technical/plos/journal.pbio.0020406.txt
./technical/plos/journal.pbio.0020439.txt
./technical/plos/pmed.0010008.txt
./technical/plos/pmed.0010028.txt
./technical/plos/pmed.0010036.txt
./technical/plos/pmed.0010045.txt
./technical/plos/pmed.0010062.txt
./technical/plos/pmed.0010064.txt
./technical/plos/pmed.0010066.txt
./technical/plos/pmed.0020015.txt
./technical/plos/pmed.0020016.txt
./technical/plos/pmed.0020018.txt
./technical/plos/pmed.0020045.txt
./technical/plos/pmed.0020050.txt
./technical/plos/pmed.0020059.txt
./technical/plos/pmed.0020061.txt
./technical/plos/pmed.0020073.txt
./technical/plos/pmed.0020103.txt
./technical/plos/pmed.0020123.txt
./technical/plos/pmed.0020140.txt
./technical/plos/pmed.0020160.txt
./technical/plos/pmed.0020162.txt
./technical/plos/pmed.0020182.txt
./technical/plos/pmed.0020246.txt
./technical/plos/pmed.0020249.txt
```



I found this command from ChatGPT, and used `man find` for the `b` suffix. 

**finding files that are readable:**
```
find -readable 
```
Example: 
```
[cs15lsp23ca@ieng6-202]:stringsearch-data:485$ find  ./technical/plos -readable -size -2k  
./technical/plos/pmed.0020191.txt
./technical/plos/pmed.0020226.txt

```

I found this from `man find`. 

**finding files and deleting them:**
```
find [any of the find command above] -delete
```

I found this from `man find`
