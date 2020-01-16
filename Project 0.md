#### Part I: 两个简单的python程序

1. 在windows系统的桌面建立目录hello_python;
2. 在hello_python里用“记事本”或者其它文本编辑器产生两个python程序hello_world.py和var1.py, 保存为UTF-8 NO BOM 编码格式;
3. hello_world.py可以和教案 (即py-ch06.pdf) page 32 “第一个完整的python脚本”一样;
4. var1.py中先定义常量PI (page 37), 并print出来; 再定义变量shot_id, 并把该变量及其类型print出来 (page 43);
5. 在命令行 or terminal 通过python解释器运行上面两个程序, 截图后换掉下面展示的示意图:
6. 把hello_python目录(里面只含两个.py源程序)打包成压缩包p001.zip, 以备后面上传; 01 换成自己的课堂编号.


#### Part II: sftp 客户端的使用

*以下叙述以 psftp.exe Release 0.70 (可以在命令行下键入psftp.exe -V查看其版本号) 为准; 如果你用的是其它客户端, 请自己适当调整. 从这里开始, 全部在sftp client软件或程序里完成.*

7. 打开psftp.exe后, 键入help命令, 把该命令及输出展示在下面 (可以贴截图; 也可以直接把文本形式的命令 and/or 输出拷贝在下面. 下同.):
8. 用中文解释如下命令的作用:

|命令 | 作用|
|:--: |:--: |
|get | 下载文件到本地|
put|上传文件到服务器
mget|批量下载
mput|批量上传
ls|查看当前目录下的文件
rm|删除服务器上的文件
mv|移动或重命名文件
cd|更改服务器当前目录
pwd|查看服务器当前路径
lcd|更改本地当前目录
lpwd|查看本地当前路径
close|关闭当前连接而不退出客户端
open|建立连接

*注意: 第7步仅给出了命令的简短说明, 如果想得到get命令的详细说明, 可以键入命令 help get; 读懂help get 的输出并辅以适当练习, 就可以完全掌握该命令了. 其它命令的详细说明类似.*

9. 用close命令关掉当前连接而不退出sftp 客户端:

```psftp> close```

10. 用open命令连接sftp server, 要求把username, ip address, port number 直接打在open 的后面:

```psftp> open u19f68@10.168.0.217```

11. 查看本机的当前路径:

```psftp> lpwd```

12. 查看sftp server 的当前路径:

```psftp> pwd```

13. 列出sftp server 上的文件:

```psftp> ls```

14. 把3个文件a.txt, b.txt, c.txt (这三个文件可以用py19fd账号从p0目录预先下载到本地) 用一条命令上传到sftp server, 并用ls命令确认上传成功:

```
psftp> mput a.txt b.txt c.txt
psftp> *.txt
```

15. 删除c.txt, 并用ls命令确认删除成功:

```
psftp> rm c.txt
psftp> *.txt
```

16. 把b.txt重命名为b2.txt, 并用ls命令确认重命名成功:

```
psftp> mv b.txt b2.txt
psftp> *.txt
```

17. 把第1步中创建的 hello_python 目录整体上传到sftp server的根目录下:

```psftp> put -r C:/Users/Administrator/Desktop/hello_python```

18. 把sftp server上的hello_python目录整体下载到桌面上的hello_python_new目录, hello_python_new下有且仅有两个文件hello_world.py和var1.py, 不要有多余的子目录:

```psftp> get -r hello_python C:/Users/Administrator/Desktop/hello_python_new```

19. 打一条本地命令, 使得sftp client的窗口被清空 (即屏幕左上角只有提示符psftp>, 就像下图显示的一样). 报告中请删除下图, 直接写下你用的命令:

```！cls```

20. 用一条命令, 列出服务器上所有不以. (i.e., dot) 开头的文件和目录 (在linux系统中, 以.开头的文件是隐藏文件). 下图示例中, 我的sftp server的根目录有2个文件和一个目录hello_python, 命令本身我抹掉了. 显然你需要想出此命令, 运行, 截图后换掉下图:

```psftp> ls [a-z]*```
