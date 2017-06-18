Tar.gz:

打包:`tar czf file.tar.gz file.txt`

解压:`tar xzf file.tar.gz`

Bz2:

打包:`bzip2 [-k]  文件`

解压:`bunzip2 [-k] 文件`

Gzip（只对文件，不保留原文件）

打包:`gzip file1.txt`

解压:`gunzip file1.txt.gz`

`Zip: -r 对目录`

打包:`zip file1.zip file1.txt`

解压:`unzip file1.zip`


tar命令

[root@linux ~]# tar [-cxtzjvfpPN] 文件与目录 ....

参数：
-c ：建立一个压缩文件的参数指令(create 的意思)；

-x ：解开一个压缩文件的参数指令！

-t ：查看 tarfile 里面的文件！

**特别注意，在参数的下达中， c/x/t 仅能存在一个！不可同时存在！
因为不可能同时压缩与解压缩。**

-z ：是否同时具有 gzip 的属性？亦即是否需要用 gzip 压缩？

-j ：是否同时具有 bzip2 的属性？亦即是否需要用 bzip2 压缩？

-v ：压缩的过程中显示文件！这个常用，但不建议用在背景执行过程！

-f ：使用档名，请留意，在 f 之后要立即接档名喔！不要再加参数！

　　　例如使用『 tar -zcvfP tfile sfile』就是错误的写法，要写成
　　　『 tar -zcvPf tfile sfile』才对喔！

-p ：使用原文件的原来属性（属性不会依据使用者而变）

-P ：可以使用绝对路径来压缩！

-N ：比后面接的日期(yyyy/mm/dd)还要新的才会被打包进新建的文件中！

--exclude FILE：在压缩的过程中，不要将 FILE 打包！

## 常用命令
	tar -zxvf php-src.tar.gz # 解php-src.tar.gz包并且解包的是gzip压缩格式，并且解包过程中显示解包文件进度
	tar -zcvf php-src.tar.gz # 将当前目录打包到php-src.tar.gz包并且打包的是gzip压缩格式，并且打包过程中显示打包文件进度

