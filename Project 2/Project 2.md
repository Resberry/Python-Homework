### Project 2

1. palindrome  
palindrome翻译为“回文”，即正读反读都一样的词语 or 对象。
   1. 找出词典中所有的 palindromes，把每个 palindrome 及它在词典中的行号按行输出到文本文件 palindromes.txt，行号占6位、右对齐，空格后接该 palindrome，最后换行；
   2. 给出 palindromes 的统计信息，单起一行报告词典中共有多少个 palindromes；
   3. 记所有 palindromes 中最长的单词的长度为 max_length，输出长度分别为 2 至 max_length 的 palindromes 的个数。

```python
def palindromes(s):  
    s2=s[:]  
    l2=list(s2)  
    l1=list(s)  
    l1.reverse()  
    if l1==l2:  
        return True  
    else:  
        return False  
list_p=[]  
list_l=[]  
with open('words.txt','r') as f:  
    n=f.readlines()  
for i in range(len(n)):  
    if palindromes(n[i][:-1]):  
        list_l.append(len(n[i])-1)  
        list_p.append(str(i+1).rjust(6)+' '+n[i])  
with open('palindromes.txt','w',encoding='utf-8') as f:  
    f.writelines(list_p)  
    f.write('\n')  
    f.write('=== palindromes 的统计信息 ==='+'\n')  
    f.write('There are %d palindromes in the dictionary.'%len(list_p)+'\n')  
    f.write('length | count'+'\n')  
    for i in range(2,max(list_l)+1):  
        f.write(str(i).rjust(6)+' | '+str(list_l.count(i)).ljust(5)+'\n')  
```

2. anagram  
anagram 翻译为“变位词”，即把单词 A 的字母顺序打乱，重新排列后变成一个新单词 B，这样A与B互为anagram。
   1. 找出词典中的所有 anagram 组，每个组包含至少2个单词，组内的单词互为anagram；按在词典中出现的先后顺序把每个anagram组写入到文本文件anagrams.txt中，每行一个组；
   2. 给出 anagram 组的统计信息，报告词典中共有多少个 anagram 组；
   3. 记所有 anagram 组中单词个数最多的组的长度 (即该组中不同单词的个数) 为 max_group，记所有 anagram 组中单个单词长度的最大值为 max_word，打印这两个数；
   4. 输出所有组长度为 max_group 的 anagram 组的成员；
   5. 输出所有单词长度为 max_word 的 anagram 组的成员。

```python
with open('words.txt','r') as f:  
    n=f.readlines()  
n2=n[:]  
for i in range(len(n2)):  
    n2[i]=n2[i][:-1]  
d,ans= {},[]  
list_str=[]  
list_lc=[]  
list_lw=[]  
for i in n2:  
    sortstr=''.join(sorted(i))  
    if sortstr in d:  
        d[sortstr]+=[i]  
    else:  
        d[sortstr]=[i]  
for i in d:  
    tmp=d[i]  
    tmp.sort()  
    ans+=[tmp]  
for i in range(len(ans)):  
    if len(ans[i])>1:  
        list_str+=[ans[i]]  
for i in list_str:  
    list_lc+=[len(i)]  
    list_lw+=[len(i[0])]  
lc=max(list_lc)  
lw=max(list_lw)  
lcc=[idx for idx,i in enumerate(list_lc) if i==lc]  
lww=[idx for idx,i in enumerate(list_lw) if i==lw]  
with open('anagrams.txt','w',encoding='utf-8') as f:  
    for i in range(len(list_str)):  
        f.write(' '.join(list_str[i])+'\n')  
    f.write('\n')  
    f.write('=== anagrams 组的统计信息 ==='+'\n')  
    f.write('There are %d anagram groups in the dictionary.'%len(list_str)+'\n')  
    f.write('max_group = %d, max_word = %d.'%(lc,lw)+'\n')  
    f.write('组长度为 max_group 的组如下:'+'\n')  
    for i in lcc:  
        f.write(str(list_str[i])+'\n')  
    f.write('单词长度为 max_word 的组如下:'+'\n')  
    for i in lww:  
        f.write(str(list_str[i])+'\n')  
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
   2. 用python代码展示上表中部分函数的用法：
      1. 对于字符串'to be, or not to be'，分别给出'a'，'b'，'be'出现的次数；
      2. 对于字符串'to be, or not to be'，分别检查它是否以'to'开头，是否以'be'结尾；
      3. 对于字符串'to be, or not to be'，检查'be'是否是它的子串，若是，给出该子串在原串出现的位置 (即下标)；
      4. 对于字符串'to be, or not to be'，把'to'替换为'TO'，但只替换一次；
      5. 对于字符串列表`idens=['','5','5a','a','a5','_','_3','__a']`，打印出属于python语言的合法的identifier的那些字符串；
      6. 对于ascii表中0-127号字符，调用isspace()判断哪些是whitespaces，输出whitespaces的两位大写hex码；
      7. 本题考察对齐字符串时经常用到的三个函数：ljust()，rjust()，and center()。在下面的code snippet中直接填入三行代码即可：

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

```python
s='to be, or not to be'  
print('-----1.测试count()-----')  
print('a在to be, or not to be中出现了%d次'%s.count('a'))  
print('b在to be, or not to be中出现了%d次'%s.count('b'))  
print('be在to be, or not to be中出现了%d次'%s.count('be'))  
print()  
print('-----2.测试startswith()和endswith()-----')  
print('to be, or not to be是否以to开头? Answer:%s'%s.startswith('to'))  
print('to be, or not to be是否以be结尾? Answer:%s'%s.endswith('be'))  
print()  
print('-----3.测试find()-----')  
print('be是否to be, or not to be的子串? Answer:%s'%bool(s.find('be')+1))  
print('be在to be, or not to be出现的位置:%d'%s.find('be'))  
print()  
print('-----4.测试replace()-----')  
print(s.replace('to','TO',1))  
print()  
print('-----5.测试isidentifier()-----')  
idens=['', '5', '5a', 'a', 'a5', '_', '_3', '__a']  
print([s for s in idens if s.isidentifier()])  
print()  
print('-----6.测试isspace()-----')  
print(['{:02x}'.format(i).upper() for i in range(0,128) if chr(i).isspace()])  
print()  
print('-----7.测试ljust()、rjust()、center()-----')  
ruler='12345678901234567890'  
s='python'  
print(ruler)  
print('|',s.ljust(18),'|',sep='')  
print('|',s.rjust(18),'|',sep='')  
print('|',s.center(18),'|',sep='')  
print(ruler)  
```

5. (printable or not?)  
Python 的 str data type 中对 0-127 的 ascii 字符用 isprintable() 函数来判断该字符是否 printable， string module 中 string.printable 变量按特定顺序给出所有 printable 的字符。分别把它们漂亮打印出来，继而简述这两种方式的异同。

```python
L1=[(chr(i),'{:02x}'.format(i)) for i in range(0,128) if chr(i).isprintable()]  
print('There are %d printable ASCII characters in the str data type.'%len(L1))  
print('C  H|'*15,'C  H',sep='')  
print('----+'*15,'----',sep='')  
for i in range(int(len(L1)/16)+1):  
    for j in range(15):  
        if 16*i+j>len(L1)-1:  
            break  
        print(L1[16*i+j][0].ljust(2),L1[16*i+j][1],'|',sep='',end='')  
    if 16*i+15>len(L1)-1:  
        print('\n',end='')  
        break  
    else:  
        print(L1[16*i+15][0].ljust(2),L1[16*i+15][1],sep='',end='')  
    print('\n',end='')  
print('-'*79)  
```

```python
import string  
L2=[[repr(i)[1:-1],'{:02x}'.format(ord(i)).upper()] for i in list(string.printable)]  
L2[85][0]='\\'  
L2[98][0]=r'\v'  
L2[99][0]=r'\f'  
print('There are %d printable ASCII characters in the string module.'%len(L2))  
print('ch hex|'*9,'ch hex',sep='')  
print('------+'*9,'------',sep='')  
for i in range(int(len(L2)/10)):  
    for j in range(9):  
        if 10*i+j>len(L2)-1:  
            break  
        print(L2[10*i+j][0].rjust(2),' ',L2[10*i+j][1],' |',sep='',end='')  
    if 10*i+9>len(L2)-1:  
        print('\n',end='')  
        break  
    else:  
        print(L2[10*i+9][0].rjust(2),' ',L2[10*i+9][1],sep='',end='')  
    print('\n',end='')  
print('-'*68)  
```

*在0-127 的 ascii 字符中，  
相似：isprintable()和string.printable都包含95个可打印字符。  
区别：string.printable中额外包含5个转义符。*

6. ROT13  
中文翻译为“回转13位”，其中的ROT是rotation的简写。ROT13 是一种简易的替换式密码算法， 并且是它自身的逆反，即要还原成原文只要再次使用同一算法即可。它的原理是把字母a前移13个位置变为n，把字母b前移13个位置变为o,...，把字母m前移13个位置变为z；把字母n后移13个位置变为a,...，把字母z后移13个位置变为m。大写字母也类似。请编写一个函数 rot13()，把如下的两个句子解码出来。

```python
def rot13(s):  
    l1='abcdefghijklmnopqrstuvwxyz'  
    l2='nopqrstuvwxyzabcdefghijklm'  
    code=str.maketrans(l1+l1.upper(),l2+l2.upper())  
    return s.translate(code)  
s1='Yvsr vf cngurgvp, yrg\'f clgubavp!'  
r1=rot13(s1)  
print(r1)  
print(s1 == rot13(r1))  
s2="Jvgu terng cbjre, pbzrf terng erfcbafvovyvgl!"  
r2=rot13(s2)  
print(r2)  
print(s2 == rot13(r2))  
```

7. 整数和汉字的关系
   1. 定义两个整数a=47802，b=65226，打印出它们的hex码；
   2. 把a,b两个整数以native方式pack 成一个 bytes 对象bs (这里视a,b为无符号的16位整数)，打印bs；
   3. 把bs解码成gbk字符串s，打印s；
   4. 用open()函数打开一个文本文件struct1.txt，写入s，并额外多写一个换行符后关闭该文件；
   5. 用open()函数以二进制追加的方式打开struct1.txt，写入bs后关闭该文件；
   6. 用记事本 (winos) 或者 TextEdit (macos) 打开struct1.txt，正常情况你将看到两行一样的文字。简单解释一下前面的两种写入方式为什么得到了同样的结果。

```python
from struct import pack  
a=47802  
b=65226  
print('hex(a) = %s'%hex(a))  
print('hex(b) = %s'%hex(b))  
bs=pack('HH',a,b)  
s=bs.decode('gbk')  
print('bs = %s'%bs)  
print('s = %s'%s)  
with open('struct1.txt','w') as f:  
    f.write(s+'\n')  
with open('struct1.txt','ab') as f:  
    f.write(bs)  
```

*解释：第一种直接将文字写入文档；第二种将同样的文字转为二进制形式，然后写入以二进制形式打开的文档，结果一样。*

8. (GB 2312)  
用 python 程序把 GB2312 字符集中的 6763 个汉字输出到文本文件 gb2312.txt，每行16个汉字 (最后一行可少于16个)。在报告中简述你是如何找到这些汉字的。

```python
l=['fa','fb','fc','fd','fe']  
ls=[]  
for head in range(0xb0,0xf8):  
    for body in range(0xa1,0xff):  
        val=f'{head:x}{body:x}'  
        if val[:2]=='d7' and val[2:] in l:  
            pass  
        else:  
            str=bytes.fromhex(val).decode('gb2312')       
            ls.append(str)  
with open('gb2312.txt','w') as f:  
    for i in range(int(len(ls)/16)+2):  
        for j in range(16):  
            if 16*i+j+1<=len(ls):  
                f.write(ls[16*i+j])  
        f.write('\n')  
```

*通过汉字的编码找到的这些汉字，GB2312汉字的编码范围为B0A1-F7FE。*

9. (png file) 图像信息的提取
   1. 自制一个合法的.png文件，图中显示个人姓名的全部拼音；
   2. 简述png文件头的结构；
   3. 写一段python程序打印该png文件的width和height。

*png文件头结构：  
89 50 4E 47 0D 0A 1A 0A：PNG头部署名域，表示这是一个PNG图片  
00 00 00 0D：描述IHDR头部的大小  
49 48 44 52：表示Chunk Type Code，此处为IHDR  
00 00 00 CE 00 00 00 CE 08 02 00 00 00：描述Chunk Data  
F9 7D AA 93：对IHDR的CRC校验*

```python
from struct import unpack   
with open('zyp.png','rb') as f:  
    n=f.read(16)  
    s=f.read(8)  
w,l=unpack('>II',s)    
print('width = %d, height = %d'%(w,l))  
```

10. nested sum  
Write a function called nested_sum that takes a nested list of integers and adds up the elements.

```python
def nested_sum(l):  
    s=0  
    for i in l:  
        if isinstance(i,list):  
            s=s+nested_sum(i)  
        else:  
            s=s+i  
    return s  
L1=list(range(100))  
print(nested_sum(L1))  
L2 = [[1, 2], 3, [4, 5, 6]]  
print(nested_sum(L2))  
L3 = [[1, 2], [3], [4, 5, 6]]  
print(nested_sum(L3))  
L4 = [1, 2, [3], [4, 5, 6]]  
print(nested_sum(L4))  
L5 = [[1, 2], [3], [4, 5, 6]]  
print(nested_sum(L5))  
L6 = [[1, 2], [3], [4, 5, 6], [[7, 8], 9]]  
print(nested_sum(L6))  
L7 = [[1, 2], [3], [4, 5, 6], [[7, 8], [9]]]  
print(nested_sum(L7))  
```

11. (two dimensional array) 矩阵的转置和乘法
   1. 随机产生三个正整数m,n,q，三者都在2和9之间，包含2和9，打印m,n,q；
   2. 随机产生一个m行n列的矩阵A，该矩阵的每个元素在-99到99之间，包含-99和99。打印A和A的转置矩阵；
   3. 随机产生一个n行q列的矩阵B，该矩阵的每个元素在-99到99之间，包含-99和99。A和B的乘积记为C，打印B和C。

```python
import random  
import numpy as np  
def printmatrix(matrix):  
    m=matrix.shape[0]  
    n=matrix.shape[1]  
    print('  |',end='',sep='')  
    for i in range(n):  
        print('  ',i+1,end='')  
    print('\n',end='')  
    print('---'+'-'*4*n)  
    for i in range(m):  
        print(i+1,'| ',end='')  
        for j in range(n):  
            print(str(matrix[i][j]).rjust(3),'',end='')  
        print('\n')   
def printbigmatrix(matrix):  
    m=matrix.shape[0]  
    n=matrix.shape[1]  
    print('  |',end='',sep='')  
    for i in range(n):  
        print('     ',i+1,end='')  
    print('\n',end='')  
    print('---'+'-'*7*n)  
    for i in range(m):  
        print(i+1,'| ',end='')  
        for j in range(n):  
            print(str(matrix[i][j]).rjust(6),'',end='')  
        print('\n')   
m=random.randint(2,9)  
n=random.randint(2,9)  
q=random.randint(2,9)  
A=np.random.randint(-99,99,(m,n))  
B=np.random.randint(-99,99,(n,q))  
print('m = %d, n = %d, q = %d'%(m,n,q)+'\n')  
print('The matrix A is')  
printmatrix(A)  
print()  
print('The transpose of matrix A is')  
printmatrix(A.T)  
print()  
print('The matrix B is')  
printmatrix(B)  
print()  
print('The matrix C=A*B is')  
printbigmatrix(np.dot(A,B))  
```

12. (Kobe Shot Selection) Kobe投篮数据集的初步分析  
数据 data.csv 可以通过课程网站的主页 or 课程ftp的下载账号获取相应的.zip文件后解压得到。
   1. 打印出所有的不同的 action_type；
   2. 打印出所有的不同的 combined_shot_type；
   3. 多种 action_type 可以被“归类” (combined) 到同一种 combined_shot_type，请打印出所有的combined_shot_type及其对应的多种 action_type；
   4. 统计每一种combined_shot_type的频率 (即Kobe用该种方式投篮的次数)，用matplotlib的bar()函数画出该频率的直方图；
   5. 打印Kobe曾效力的球队；
   6. 打印出所有的不同的 shot_zone_range；
   7. 打印出所有的不同的 shot_type；
   8. 打印出所有的不同的 shot_made_flag，并解释不同的shot_made_flag的意义；
   9. shot_made_flag==''代表该数据缺失了，请把这些信息写入到 kobe_missing.csv文件，shot_id为该行的最后一列，shot_made_flag因为缺失了，我们统一赋值为0.5。
   10. 统计Kobe总共参与了多少场比赛；
   11. 统计Kobe总共打了多少场季后赛(playoffs)；
   12. 统计Kobe季后赛总投篮次数；
   13. 打印Kobe参加的最早一场比赛的日期，及该场比赛的投篮次数；
   14. 打印Kobe参加的最后一场比赛的日期，及该场比赛投中、投失、or数据缺失的次数(由shot_made_flag字段确定)；
   15. 打印Kobe得分最多的一场比赛的日期，及该场比赛的投篮次数、二分球个数、三分球个数(如果有数据缺失，缺失的部分不用统计)。

```python
import matplotlib.pyplot as plt  
import csv  
data=[]  
dic={}  
dic2={}  
with open('data.csv','r') as f:  
    reader=csv.reader(f)  
    for row in reader:  
        data.append(row)  
column1=[row[0] for row in data[1:]]  
column2=[row[1] for row in data[1:]]  
team=data[1][20]  
gameidall=[row[3] for row in data[1:]]  
gameid=list(set(gameidall))
Gameid.sort()  
shotzone=set([row[18] for row in data[1:]])  
times=set([row[3] for row in data[1:]])  
shotmiss=[row[14] for row in data[1:]]  
playoffs=[row[10] for row in data[1:]]  
date=[row[21] for row in data[1:]]  
date2=date[:]  
date2.sort()  
start=[i for i,j in enumerate(date) if j==date2[0]]  
end=[i for i,j in enumerate(date) if j==date2[-1]]  
shotstart=shotmiss[start[0]:start[-1]+1]  
shotend=shotmiss[end[0]:end[-1]+1]  
t=playoffs.index('1')  
playoffshottimes=[row[3] for row in data[t+1:]]  
playofftimes=set(playoffshottimes)  
shotflag=set(shotmiss)  
flag=[]  
for i in range(len(shotmiss)):  
    if shotmiss[i]=='1':  
        flag.append(1)  
    else:  
        flag.append(0)  
pt=[row[15] for row in data[1:]]  
pt2=[int(j[0])*flag[i] for i,j in enumerate(pt)]  
score=[]  
for i in gameid:  
    index=[z for z,j in enumerate(gameidall) if j==i]  
    score.append(sum(pt2[index[0]:index[-1]+1]))  
maxscore=max(score)  
ind2=score.index(maxscore)  
maxgame=gameid[ind2]  
index==[i for i,j in enumerate(gameidall) if j==maxgame]  
shottype=set(pt)  
l1=set(column1)  
l2=set(column2)  
for i in l2:  
    dic[i]=[]  
    dic2[i]=column2.count(i)  
X=list(dic2.keys())  
Y=list(dic2.values())  
for i in l1:  
    ind=column1.index(i)  
    dic[column2[ind]].append(i)  
header=['shot_id','shot_made_flag']  
miss=[[i+1,0.5] for i,j in enumerate(shotmiss) if j=='']  
with open('kobe_missing.csv','w',newline='') as f:  
    writer=csv.writer(f)  
    writer.writerow(header)  
    for row in miss:  
        writer.writerow(row)  
print('----- 2. action_type -----')  
print('There are %d action types:'%len(l1))  
print(l1)  
print()  
print('----- 3. combined_shot_type -----')  
print('There are %d combined shot types:'%len(l2))  
print(l2)  
print()  
print('----- 4. details of combined_shot_type -----')  
for i in dic.keys():  
    print(i.ljust(10),str(len(dic[i])).ljust(3),','.join(dic[i]))  
print()  
print('----- 5. combined_shot_type 的直方图 -----')  
print(dic2)  
plt.bar(X,Y)  
plt.show()  
print()  
print('----- 6. Kobe 曾效力的球队 -----')  
print(team)  
print()  
print('----- 7. shot_zone_range -----')  
print(shotzone)  
print()  
print('----- 8. shot_type -----')  
print(shottype)  
print()  
print('----- 9. shot_made_flag -----')  
print(shotflag)  
print()  
print('----- 10. shot_made_flag (missing data) -----')  
print(len(miss))  
print()  
print('----- 11. Kobe总共参与了多少场比赛 -----')  
print(len(times))  
print()  
print('----- 12. Kobe总共打了多少场季后赛 (playoffs) -----')  
print(len(playofftimes))  
print()  
print('----- 13. Kobe季后赛总投篮次数 -----')  
print(len(playoffshottimes))  
print()  
print('----- 14. Kobe参加的最早一场比赛 -----')  
print('最早一场比赛的日期: %s'%date2[1])  
print('最早一场比赛的投篮次数: %d'%len(shotstart))  
print()  
print('----- 15. Kobe参加的最后一场比赛 -----')  
print('最后一场比赛的日期: %s'%date2[-1])  
print('最后一场比赛投中的次数: %d'%shotend.count('1'))  
print('最后一场比赛投失的次数: %d'%shotend.count('0'))  
print('最后一场比赛数据缺失的次数: %d'%shotend.count(''))  
print()  
print('----- 16. Kobe得分最多的一场比赛 -----')  
print('得分最多的一场比赛的日期: %s'%date[index[0]])  
print('得分最多的一场比赛的投篮次数: %d'%len(date[index[0]:index[-1]]))  
print('得分最多的一场比赛的二分球个数: %d'%pt2[index[0]:index[-1]].count(2))  
print('得分最多的一场比赛的三分球个数: %d'%pt2[index[0]:index[-1]].count(3))  
```
