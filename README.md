#Queries

###Efficiency

HDBs are date partitioned.
**Always** put a date clause first in queries to reduce the directories kdb+needs to look in.

```q
select from Quote where date = .z.d-1
```
##Joins

##lj
```q
x:([]a:1 2 3;b:`I`J`K;c:10 20 30)
y:([a:1 3;b`I`K]c:1 2;d:10 20)

q)x lj y
a b c  d
---------
1 I 1  10
2 J 20
3 K 2  20
```
##aj 
```q
x:([]time:11 13 14;sym:`msft`ibm`ge;qty:100 200 150)
y:([]time:10 10 10 12;sym:`ibm`msft`msft`ibm;px:100 99 101 98)

q)aj [sym`time;x;y]
time  sym   qty   px 
----------------------
11     msft   100  101
13     ibm    200  98
14     ge     150
```
##ij
```q
x:([]a:1 2;b:`x`y;c:10 20)
y:([a:1 2]b:``z;c:1 0N)

q)x ij y 
a b c
-----
1   1
2 z
```
##File System

###File and Filepaths

Find files in a directory:
```q
q)key `:/home/yyacalo/dir
,file
```
```q
q)` sv `:/home/yycalo/dir,file
`:/home/yyacalo/dir/file
```
Create file paths for all files in a directory:
```q
q)` sv 'directory,'key directory
```
###FILE SIZES

Find the uncompressed size of a file (2 ways):(-21!x)`uncompressedLenght;hcount `:file

Compress a file: -19!(arc;tgt;lbs;alg;lvl)

Find the compression stats for a file: -21!file

Find the compressed size of a file: (-21!files)`compressed size

Open a handle to a file:hopen `:datafile

Delete a file:hdelete `:datafile

