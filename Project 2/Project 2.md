### Project 2

1. palindrome  
palindrome翻译为“回文”，即正读反读都一样的词语 or 对象。
   1. 找出词典中所有的 palindromes，把每个 palindrome 及它在词典中的行号按行输出到文本文件 palindromes.txt，行号占6位、右对齐，空格后接该 palindrome，最后换行；
   2. 给出 palindromes 的统计信息，单起一行报告词典中共有多少个 palindromes；
   3. 记所有 palindromes 中最长的单词的长度为 max_length，输出长度分别为 2 至 max_length 的 palindromes 的个数。

```python
1.def palindromes(s):  
2.    s2=s[:]  
3.    l2=list(s2)  
4.    l1=list(s)  
5.    l1.reverse()  
6.    if l1==l2:  
7.        return True  
8.    else:  
9.        return False  
10.list_p=[]  
11.list_l=[]  
12.with open('words.txt','r') as f:  
13.    n=f.readlines()  
14.for i in range(len(n)):  
15.    if palindromes(n[i][:-1]):  
16.        list_l.append(len(n[i])-1)  
17.        list_p.append(str(i+1).rjust(6)+' '+n[i])  
18.with open('palindromes.txt','w',encoding='utf-8') as f:  
19.    f.writelines(list_p)  
20.    f.write('\n')  
21.    f.write('=== palindromes 的统计信息 ==='+'\n')  
22.    f.write('There are %d palindromes in the dictionary.'%len(list_p)+'\n')  
23.    f.write('length | count'+'\n')  
24.    for i in range(2,max(list_l)+1):  
25.        f.write(str(i).rjust(6)+' | '+str(list_l.count(i)).ljust(5)+'\n')  
```

2. anagram  
anagram 翻译为“变位词”，即把单词 A 的字母顺序打乱，重新排列后变成一个新单词 B，这样A与B互为anagram。
   1. 找出词典中的所有 anagram 组，每个组包含至少2个单词，组内的单词互为anagram；按在词典中出现的先后顺序把每个anagram组写入到文本文件anagrams.txt中，每行一个组；
   2. 给出 anagram 组的统计信息，报告词典中共有多少个 anagram 组；
   3. 记所有 anagram 组中单词个数最多的组的长度 (即该组中不同单词的个数) 为 max_group，记所有 anagram 组中单个单词长度的最大值为 max_word，打印这两个数；
   4. 输出所有组长度为 max_group 的 anagram 组的成员；
   5. 输出所有单词长度为 max_word 的 anagram 组的成员。

```python
1.with open('words.txt','r') as f:  
2.    n=f.readlines()  
3.n2=n[:]  
4.for i in range(len(n2)):  
5.    n2[i]=n2[i][:-1]  
6.d,ans= {},[]  
7.list_str=[]  
8.list_lc=[]  
9.list_lw=[]  
10.for i in n2:  
11.    sortstr=''.join(sorted(i))  
12.    if sortstr in d:  
13.        d[sortstr]+=[i]  
14.    else:  
15.        d[sortstr]=[i]  
16.for i in d:  
17.    tmp=d[i]  
18.    tmp.sort()  
19.    ans+=[tmp]  
20.for i in range(len(ans)):  
21.    if len(ans[i])>1:  
22.        list_str+=[ans[i]]  
23.for i in list_str:  
24.    list_lc+=[len(i)]  
25.    list_lw+=[len(i[0])]  
26.lc=max(list_lc)  
27.lw=max(list_lw)  
28.lcc=[idx for idx,i in enumerate(list_lc) if i==lc]  
29.lww=[idx for idx,i in enumerate(list_lw) if i==lw]  
30.with open('anagrams.txt','w',encoding='utf-8') as f:  
31.    for i in range(len(list_str)):  
32.        f.write(' '.join(list_str[i])+'\n')  
33.    f.write('\n')  
34.    f.write('=== anagrams 组的统计信息 ==='+'\n')  
35.    f.write('There are %d anagram groups in the dictionary.'%len(list_str)+'\n')  
36.    f.write('max_group = %d, max_word = %d.'%(lc,lw)+'\n')  
37.    f.write('组长度为 max_group 的组如下:'+'\n')  
38.    for i in lcc:  
39.        f.write(str(list_str[i])+'\n')  
40.    f.write('单词长度为 max_word 的组如下:'+'\n')  
41.    for i in lww:  
42.        f.write(str(list_str[i])+'\n')  
```

3. letter frequency
   1. 统计词典中26个小写英文字母出现的频率，按字母顺序输出该字母及对应频率；
   2. 自学 matplotlib，画出频率的直方图。

```python
import matplotlib.pyplot as plt  
with open('words.txt','r') as f:  
    n=f.readlines()  
n2=n[:]  
for i in range(len(n)):  
    n2[i]=n[i][:-1]  
s=''.join(n2)    
print('ch| frequency')  
x=[]  
y=[]  
for i in range(97,123):  
    x.append(chr(i))  
    y.append(s.count(chr(i)))  
    print(chr(i),'|',s.count(chr(i)))  
plt.bar(x,y)  
plt.ylabel('Frequency')  
plt.show()  
```

4. strings in python
   1. 简述str data type中下述函数的作用；
|函数	|作用|
|--|--|
|center	|居中显示。|
|count	|计算某字符出现次数。|
|encode	|对字符串进行编码。|
|endswith	|判断字符串是否以特定字符结尾。|
|find	|找到指定字符在字符串中的位置。|
|format	|格式化，将字符串中占位符替换为指定的值。|
|isidentifier	|判断字符串是否为有效的Python标识符。|
|isprintable	|判断字符串打印出来是否可见。|
|isspace	|判断字符串中是否全为空白符。|
|ljust	|左对齐显示。|
|maketrans	|创建两个字符串之间的映射关系。|
|replace	|用指定字符替换字符串中指定字符。|
|rsplit	|从右开始用指定字符将字符串分割。|
|split	|用指定字符将字符串分割。|
|splitlines	|以换行为分隔符将字符串分割。|
|strip	|去除字符串两端的指定字符。|
|translate	|将字符串用某种映射关系翻译为另一个字符串。|
|zfill	|返回指定长度的字符串。右对齐，空白部分用0填充。|
   2. 用python代码展示上表中部分函数的用法：
1. 对于字符串'to be, or not to be'，分别给出'a'，'b'，'be'出现的次数；
2. 对于字符串'to be, or not to be'，分别检查它是否以'to'开头，是否以'be'结尾；
3. 对于字符串'to be, or not to be'，检查'be'是否是它的子串，若是，给出该子串在原串出现的位置 (即下标)；
4. 对于字符串'to be, or not to be'，把'to'替换为'TO'，但只替换一次；
5. 对于字符串列表idens=['','5','5a','a','a5','_','_3','__a']，打印出属于python语言的合法的identifier的那些字符串；
6. 对于ascii表中0-127号字符，调用isspace()判断哪些是whitespaces，输出whitespaces的两位大写hex码；
7. 本题考察对齐字符串时经常用到的三个函数：ljust()，rjust()，and center()。在下面的code snippet中直接填入三行代码即可：

1.s='to be, or not to be'  
2.print('-----1.测试count()-----')  
3.print('a在to be, or not to be中出现了%d次'%s.count('a'))  
4.print('b在to be, or not to be中出现了%d次'%s.count('b'))  
5.print('be在to be, or not to be中出现了%d次'%s.count('be'))  
6.print()  
7.print('-----2.测试startswith()和endswith()-----')  
8.print('to be, or not to be是否以to开头? Answer:%s'%s.startswith('to'))  
9.print('to be, or not to be是否以be结尾? Answer:%s'%s.endswith('be'))  
10.print()  
11.print('-----3.测试find()-----')  
12.print('be是否to be, or not to be的子串? Answer:%s'%bool(s.find('be')+1))  
13.print('be在to be, or not to be出现的位置:%d'%s.find('be'))  
14.print()  
15.print('-----4.测试replace()-----')  
16.print(s.replace('to','TO',1))  
17.print()  
18.print('-----5.测试isidentifier()-----')  
19.idens=['', '5', '5a', 'a', 'a5', '_', '_3', '__a']  
20.print([s for s in idens if s.isidentifier()])  
21.print()  
22.print('-----6.测试isspace()-----')  
23.print(['{:02x}'.format(i).upper() for i in range(0,128) if chr(i).isspace()])  
24.print()  
25.print('-----7.测试ljust()、rjust()、center()-----')  
26.ruler='12345678901234567890'  
27.s='python'  
28.print(ruler)  
29.print('|',s.ljust(18),'|',sep='')  
30.print('|',s.rjust(18),'|',sep='')  
31.print('|',s.center(18),'|',sep='')  
32.print(ruler)  



5.(printable or not?) 
Python 的 str data type 中对 0-127 的 ascii 字符用 isprintable() 函数来判断该字符是否 printable， string module 中 string.printable 变量按特定顺序给出所有 printable 的字符。分别把它们漂亮打印出来，继而简述这两种方式的异同。

1.L1=[(chr(i),'{:02x}'.format(i)) for i in range(0,128) if chr(i).isprintable()]  
2.print('There are %d printable ASCII characters in the str data type.'%len(L1))  
3.print('C  H|'*15,'C  H',sep='')  
4.print('----+'*15,'----',sep='')  
5.for i in range(int(len(L1)/16)+1):  
6.    for j in range(15):  
7.        if 16*i+j>len(L1)-1:  
8.            break  
9.        print(L1[16*i+j][0].ljust(2),L1[16*i+j][1],'|',sep='',end='')  
10.    if 16*i+15>len(L1)-1:  
11.        print('\n',end='')  
12.        break  
13.    else:  
14.        print(L1[16*i+15][0].ljust(2),L1[16*i+15][1],sep='',end='')  
15.    print('\n',end='')  
16.print('-'*79)  



1.import string  
2.L2=[[repr(i)[1:-1],'{:02x}'.format(ord(i)).upper()] for i in list(string.printable)]  
3.L2[85][0]='\\'  
4.L2[98][0]=r'\v'  
5.L2[99][0]=r'\f'  
6.print('There are %d printable ASCII characters in the string module.'%len(L2))  
7.print('ch hex|'*9,'ch hex',sep='')  
8.print('------+'*9,'------',sep='')  
9.for i in range(int(len(L2)/10)):  
10.    for j in range(9):  
11.        if 10*i+j>len(L2)-1:  
12.            break  
13.        print(L2[10*i+j][0].rjust(2),' ',L2[10*i+j][1],' |',sep='',end='')  
14.    if 10*i+9>len(L2)-1:  
15.        print('\n',end='')  
16.        break  
17.    else:  
18.        print(L2[10*i+9][0].rjust(2),' ',L2[10*i+9][1],sep='',end='')  
19.    print('\n',end='')  
20.print('-'*68)  


在0-127 的 ascii 字符中，
相似：isprintable()和string.printable都包含95个可打印字符。
区别：string.printable中额外包含5个转义符。

6. ROT13
中文翻译为“回转13位”，其中的ROT是rotation的简写。ROT13 是一种简易的替换式密码算法， 并且是它自身的逆反，即要还原成原文只要再次使用同一算法即可。它的原理是把字母a前移13个位置变为n，把字母b前移13个位置变为o,...，把字母m前移13个位置变为z；把字母n后移13个位置变为a,...，把字母z后移13个位置变为m。大写字母也类似。请编写一个函数 rot13()，把如下的两个句子解码出来。

1.def rot13(s):  
2.    l1='abcdefghijklmnopqrstuvwxyz'  
3.    l2='nopqrstuvwxyzabcdefghijklm'  
4.    code=str.maketrans(l1+l1.upper(),l2+l2.upper())  
5.    return s.translate(code)  
6.s1='Yvsr vf cngurgvp, yrg\'f clgubavp!'  
7.r1=rot13(s1)  
8.print(r1)  
9.print(s1 == rot13(r1))  
10.s2="Jvgu terng cbjre, pbzrf terng erfcbafvovyvgl!"  
11.r2=rot13(s2)  
12.print(r2)  
13.print(s2 == rot13(r2))  



7. 整数和汉字的关系
19.1 定义两个整数a=47802，b=65226，打印出它们的hex码；
19.2 把a,b两个整数以native方式pack 成一个 bytes 对象bs (这里视a,b为无符号的16位整数)，打印bs；
19.3 把bs解码成gbk字符串s，打印s；
19.4 用open()函数打开一个文本文件struct1.txt，写入s，并额外多写一个换行符后关闭该文件；
19.5 用open()函数以二进制追加的方式打开struct1.txt，写入bs后关闭该文件；
19.6 用记事本 (winos) 或者 TextEdit (macos) 打开struct1.txt，正常情况你将看到两行一样的文字。简单解释一下前面的两种写入方式为什么得到了同样的结果。

1.from struct import pack  
2.a=47802  
3.b=65226  
4.print('hex(a) = %s'%hex(a))  
5.print('hex(b) = %s'%hex(b))  
6.bs=pack('HH',a,b)  
7.s=bs.decode('gbk')  
8.print('bs = %s'%bs)  
9.print('s = %s'%s)  
10.with open('struct1.txt','w') as f:  
11.    f.write(s+'\n')  
12.with open('struct1.txt','ab') as f:  
13.    f.write(bs)  



解释：第一种直接将文字写入文档；第二种将同样的文字转为二进制形式，然后写入以二进制形式打开的文档，结果一样。

8. (GB 2312) 
用 python 程序把 GB2312 字符集中的 6763 个汉字输出到文本文件 gb2312.txt，每行16个汉字 (最后一行可少于16个)。在报告中简述你是如何找到这些汉字的。

1.l=['fa','fb','fc','fd','fe']  
2.ls=[]  
3.for head in range(0xb0,0xf8):  
4.    for body in range(0xa1,0xff):  
5.        val=f'{head:x}{body:x}'  
6.        if val[:2]=='d7' and val[2:] in l:  
7.            pass  
8.        else:  
9.            str=bytes.fromhex(val).decode('gb2312')       
10.            ls.append(str)  
11.with open('gb2312.txt','w') as f:  
12.    for i in range(int(len(ls)/16)+2):  
13.        for j in range(16):  
14.            if 16*i+j+1<=len(ls):  
15.                f.write(ls[16*i+j])  
16.        f.write('\n')  

通过汉字的编码找到的这些汉字，GB2312汉字的编码范围为B0A1-F7FE。

9. (png file) 图像信息的提取
21.1 自制一个合法的.png文件，图中显示个人姓名的全部拼音；
21.2 简述png文件头的结构；
21.3 写一段python程序打印该png文件的width和height。

png文件头结构：
89 50 4E 47 0D 0A 1A 0A：PNG头部署名域，表示这是一个PNG图片
00 00 00 0D：描述IHDR头部的大小
49 48 44 52：表示Chunk Type Code，此处为IHDR
00 00 00 CE 00 00 00 CE 08 02 00 00 00：描述Chunk Data
F9 7D AA 93：对IHDR的CRC校验

1.from struct import unpack   
2.with open('zyp.png','rb') as f:  
3.    n=f.read(16)  
4.    s=f.read(8)  
5.w,l=unpack('>II',s)    
6.print('width = %d, height = %d'%(w,l))  



10. nested sum
Write a function called nested_sum that takes a nested list of integers and adds up the elements.

1.def nested_sum(l):  
2.    s=0  
3.    for i in l:  
4.        if isinstance(i,list):  
5.            s=s+nested_sum(i)  
6.        else:  
7.            s=s+i  
8.    return s  
9.L1=list(range(100))  
10.print(nested_sum(L1))  
11.L2 = [[1, 2], 3, [4, 5, 6]]  
12.print(nested_sum(L2))  
13.L3 = [[1, 2], [3], [4, 5, 6]]  
14.print(nested_sum(L3))  
15.L4 = [1, 2, [3], [4, 5, 6]]  
16.print(nested_sum(L4))  
17.L5 = [[1, 2], [3], [4, 5, 6]]  
18.print(nested_sum(L5))  
19.L6 = [[1, 2], [3], [4, 5, 6], [[7, 8], 9]]  
20.print(nested_sum(L6))  
21.L7 = [[1, 2], [3], [4, 5, 6], [[7, 8], [9]]]  
22.print(nested_sum(L7))  



11. (two dimensional array) 矩阵的转置和乘法
23.1 随机产生三个正整数m,n,q，三者都在2和9之间，包含2和9，打印m,n,q；
23.2 随机产生一个m行n列的矩阵A，该矩阵的每个元素在-99到99之间，包含-99和99。打印A和A的转置矩阵；
23.3 随机产生一个n行q列的矩阵B，该矩阵的每个元素在-99到99之间，包含-99和99。A和B的乘积记为C，打印B和C。

1.import random  
2.import numpy as np  
3.def printmatrix(matrix):  
4.    m=matrix.shape[0]  
5.    n=matrix.shape[1]  
6.    print('  |',end='',sep='')  
7.    for i in range(n):  
8.        print('  ',i+1,end='')  
9.    print('\n',end='')  
10.    print('---'+'-'*4*n)  
11.    for i in range(m):  
12.        print(i+1,'| ',end='')  
13.        for j in range(n):  
14.            print(str(matrix[i][j]).rjust(3),'',end='')  
15.        print('\n')   
16.def printbigmatrix(matrix):  
17.    m=matrix.shape[0]  
18.    n=matrix.shape[1]  
19.    print('  |',end='',sep='')  
20.    for i in range(n):  
21.        print('     ',i+1,end='')  
22.    print('\n',end='')  
23.    print('---'+'-'*7*n)  
24.    for i in range(m):  
25.        print(i+1,'| ',end='')  
26.        for j in range(n):  
27.            print(str(matrix[i][j]).rjust(6),'',end='')  
28.        print('\n')   
29.m=random.randint(2,9)  
30.n=random.randint(2,9)  
31.q=random.randint(2,9)  
32.A=np.random.randint(-99,99,(m,n))  
33.B=np.random.randint(-99,99,(n,q))  
34.print('m = %d, n = %d, q = %d'%(m,n,q)+'\n')  
35.print('The matrix A is')  
36.printmatrix(A)  
37.print()  
38.print('The transpose of matrix A is')  
39.printmatrix(A.T)  
40.print()  
41.print('The matrix B is')  
42.printmatrix(B)  
43.print()  
44.print('The matrix C=A*B is')  
45.printbigmatrix(np.dot(A,B))  




12. (Kobe Shot Selection) Kobe投篮数据集的初步分析
数据 data.csv 可以通过课程网站的主页 or 课程ftp的下载账号获取相应的.zip文件后解压得到。
24.1 用汉语简单解释一下25个字段的意义:
字段	意义
action_type	具体进攻方式
combined_shot_type	进攻方式
game_event_id	比赛时间id
game_id	比赛id
lat	纬度
loc_x	X轴位置
loc_y	Y轴位置
lon	经度
minutes_remaining	剩余时间
period	节数
playoffs	是否为季后赛
season	赛季
seconds_remaining	剩余秒数
shot_distance	投篮距离
shot_made_flag	是否进球
shot_type	两分球或三分球
shot_zone_area	投篮区域
shot_zone_basic	具体投篮区域
shot_zone_range	投篮范围
team_id	队伍id
team_name	队伍名字
game_date	比赛日期
matchup	比赛双方
opponent	对手
shot_id	投篮id
24.2 打印出所有的不同的 action_type；
24.3 打印出所有的不同的 combined_shot_type；
24.4 多种 action_type 可以被“归类” (combined) 到同一种 combined_shot_type，请打印出所有的combined_shot_type及其对应的多种 action_type；
24.5 统计每一种combined_shot_type的频率 (即Kobe用该种方式投篮的次数)，用matplotlib的bar()函数画出该频率的直方图；
24.6 打印Kobe曾效力的球队；
24.7 打印出所有的不同的 shot_zone_range；
24.8 打印出所有的不同的 shot_type；
24.9 打印出所有的不同的 shot_made_flag，并解释不同的shot_made_flag的意义；
24.10 shot_made_flag==''代表该数据缺失了，请把这些信息写入到 kobe_missing.csv文件，shot_id为该行的最后一列，shot_made_flag因为缺失了，我们统一赋值为0.5。
24.11 统计Kobe总共参与了多少场比赛；
24.12 统计Kobe总共打了多少场季后赛(playoffs)；
24.13 统计Kobe季后赛总投篮次数；
24.14 打印Kobe参加的最早一场比赛的日期，及该场比赛的投篮次数；
24.15 打印Kobe参加的最后一场比赛的日期，及该场比赛投中、投失、or数据缺失的次数(由shot_made_flag字段确定)；
24.6 打印Kobe得分最多的一场比赛的日期，及该场比赛的投篮次数、二分球个数、三分球个数(如果有数据缺失，缺失的部分不用统计)。

1.import matplotlib.pyplot as plt  
2.import csv  
3.data=[]  
4.dic={}  
5.dic2={}  
6.with open('data.csv','r') as f:  
7.    reader=csv.reader(f)  
8.    for row in reader:  
9.        data.append(row)  
10.column1=[row[0] for row in data[1:]]  
11.column2=[row[1] for row in data[1:]]  
12.team=data[1][20]  
13.gameidall=[row[3] for row in data[1:]]  
14.gameid=list(set(gameidall))
15.Gameid.sort()  
16.shotzone=set([row[18] for row in data[1:]])  
17.times=set([row[3] for row in data[1:]])  
18.shotmiss=[row[14] for row in data[1:]]  
19.playoffs=[row[10] for row in data[1:]]  
20.date=[row[21] for row in data[1:]]  
21.date2=date[:]  
22.date2.sort()  
23.start=[i for i,j in enumerate(date) if j==date2[0]]  
24.end=[i for i,j in enumerate(date) if j==date2[-1]]  
25.shotstart=shotmiss[start[0]:start[-1]+1]  
26.shotend=shotmiss[end[0]:end[-1]+1]  
27.t=playoffs.index('1')  
28.playoffshottimes=[row[3] for row in data[t+1:]]  
29.playofftimes=set(playoffshottimes)  
30.shotflag=set(shotmiss)  
31.flag=[]  
32.for i in range(len(shotmiss)):  
33.    if shotmiss[i]=='1':  
34.        flag.append(1)  
35.    else:  
36.        flag.append(0)  
37.pt=[row[15] for row in data[1:]]  
38.pt2=[int(j[0])*flag[i] for i,j in enumerate(pt)]  
39.score=[]  
40.for i in gameid:  
41.    index=[z for z,j in enumerate(gameidall) if j==i]  
42.    score.append(sum(pt2[index[0]:index[-1]+1]))  
43.maxscore=max(score)  
44.ind2=score.index(maxscore)  
45.maxgame=gameid[ind2]  
46.index==[i for i,j in enumerate(gameidall) if j==maxgame]  
47.shottype=set(pt)  
48.l1=set(column1)  
49.l2=set(column2)  
50.for i in l2:  
51.    dic[i]=[]  
52.    dic2[i]=column2.count(i)  
53.X=list(dic2.keys())  
54.Y=list(dic2.values())  
55.for i in l1:  
56.    ind=column1.index(i)  
57.    dic[column2[ind]].append(i)  
58.header=['shot_id','shot_made_flag']  
59.miss=[[i+1,0.5] for i,j in enumerate(shotmiss) if j=='']  
60.with open('kobe_missing.csv','w',newline='') as f:  
61.    writer=csv.writer(f)  
62.    writer.writerow(header)  
63.    for row in miss:  
64.        writer.writerow(row)  
65.print('----- 2. action_type -----')  
66.print('There are %d action types:'%len(l1))  
67.print(l1)  
68.print()  
69.print('----- 3. combined_shot_type -----')  
70.print('There are %d combined shot types:'%len(l2))  
71.print(l2)  
72.print()  
73.print('----- 4. details of combined_shot_type -----')  
74.for i in dic.keys():  
75.    print(i.ljust(10),str(len(dic[i])).ljust(3),','.join(dic[i]))  
76.print()  
77.print('----- 5. combined_shot_type 的直方图 -----')  
78.print(dic2)  
79.plt.bar(X,Y)  
80.plt.show()  
81.print()  
82.print('----- 6. Kobe 曾效力的球队 -----')  
83.print(team)  
84.print()  
85.print('----- 7. shot_zone_range -----')  
86.print(shotzone)  
87.print()  
88.print('----- 8. shot_type -----')  
89.print(shottype)  
90.print()  
91.print('----- 9. shot_made_flag -----')  
92.print(shotflag)  
93.print()  
94.print('----- 10. shot_made_flag (missing data) -----')  
95.print(len(miss))  
96.print()  
97.print('----- 11. Kobe总共参与了多少场比赛 -----')  
98.print(len(times))  
99.print()  
100.print('----- 12. Kobe总共打了多少场季后赛 (playoffs) -----')  
101.print(len(playofftimes))  
102.print()  
103.print('----- 13. Kobe季后赛总投篮次数 -----')  
104.print(len(playoffshottimes))  
105.print()  
106.print('----- 14. Kobe参加的最早一场比赛 -----')  
107.print('最早一场比赛的日期: %s'%date2[1])  
108.print('最早一场比赛的投篮次数: %d'%len(shotstart))  
109.print()  
110.print('----- 15. Kobe参加的最后一场比赛 -----')  
111.print('最后一场比赛的日期: %s'%date2[-1])  
112.print('最后一场比赛投中的次数: %d'%shotend.count('1'))  
113.print('最后一场比赛投失的次数: %d'%shotend.count('0'))  
114.print('最后一场比赛数据缺失的次数: %d'%shotend.count(''))  
115.print()  
116.print('----- 16. Kobe得分最多的一场比赛 -----')  
117.print('得分最多的一场比赛的日期: %s'%date[index[0]])  
118.print('得分最多的一场比赛的投篮次数: %d'%len(date[index[0]:index[-1]]))  
119.print('得分最多的一场比赛的二分球个数: %d'%pt2[index[0]:index[-1]].count(2))  
120.print('得分最多的一场比赛的三分球个数: %d'%pt2[index[0]:index[-1]].count(3))  







