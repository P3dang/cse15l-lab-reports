**Finding files by name**
```
find -name [name of file]
```
**Finding specific types of files in a directory:**
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
What this command is doing is searching with a specific directory for a specific data type. Though this command doesn't find the exact file, it helps narrow down the search if you at least know the data type of that specific item you're looking for. I found this command from ChatGPT.

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
...
```

What this command does is searches through a directory looking for files larger or smaller than the specified ammount. This could be useful when you roughly know the size of the file. I found this command from ChatGPT, and used `man find` for the `b` suffix. 

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
```
[cs15lsp23ca@ieng6-203]:skill-demo1:504$ find  ./technical/plos -readable 
```
```
./technical/plos
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
...
```
Similar to the finding by type, but this command specifically only finds files that can we read, which most likely are ".txt" files. This can be useful, to narrow down the search. I found this from `man find`. 

**finding files and deleting them:**
```
find [any of the find command above] -delete
```
```
[cs15lsp23ca@ieng6-203]:~:511$ ls
bash-for-quiz  path-examples  skill-demo1   stringsearch-data  tutor
lab7           perl5          stringsearch  t.txt              wavelet
[cs15lsp23ca@ieng6-203]:~:512$ find -name t.txt -delete
[cs15lsp23ca@ieng6-203]:~:513$ ls
bash-for-quiz  path-examples  skill-demo1   stringsearch-data  wavelet
lab7           perl5          stringsearch  tutor
```
```
[cs15lsp23ca@ieng6-203]:~:513$ ls
bash-for-quiz  path-examples  skill-demo1   stringsearch-data  wavelet
lab7           perl5          stringsearch  tutor
[cs15lsp23ca@ieng6-203]:~:514$ find -name tutor  -delete
[cs15lsp23ca@ieng6-203]:~:515$ ls
bash-for-quiz  path-examples  skill-demo1   stringsearch-data
lab7           perl5          stringsearch  wavelet
```
This command delete the item that is found, this can be useful if you know which items to delete or if you want to delete all the items with "banana" in the title. I didn't run this in the /technical directory since I didn't want to delete any important data, and it would be harder to see since /techincal is a really large file. I found this from `man find`
