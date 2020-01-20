### Project 1

1. (python version) 在 console 或者 terminal 里显示自己的 python 解释器版本号。

```python -V```

2. (run python interpreter quietly) 在 console 或者 terminal 里运行 python, 但只给出提示符>>>, 在提示符后输入代码, 打印zen of python。

```python
>>> import this
```

3. (display python's keyword (关键字)) 在 console 或者 terminal 里运行 python, 但只给出提示符>>>, 多次在提示符后输入代码, 打印python的关键字的个数及全部关键字。

```python
>>> import keyword
>>> keyword.kwlist
>>> len(keyword.kwlist)
```

4. (BE vs LE) 请查阅文献和Internet资源, 简述自己对“大小端”的理解, 并用python 代码查出自己的计算机到底是"big"还是"little"。

*大端模式，指数据的高字节存在内存的低地址中，数据的低字节存在内存的高地址中。地址由小向大增加，而数据从高位往低位放。*

*小端模式，指数据的高字节存在内存的高地址中，数据的低字节存在内存的低地址中，高地址部分权值高，低地址部分权值低。*

```python
import sys  
print(sys.byteorder)  
```

5. (leap year) 要求用户输入一个年份，通过程序判断并输出是否为闰年。注意，程序应当检测输入是否合法，就算输入非法，程序还可以继续，直到用户输入q才能退出。

```python
tip='please input a positive integer(or press q to quit):\n'  
while True:  
    year=input(tip)  
    if year=='q':  
        print('All down, quitting...')  
        exit()  
    try:   
        year=int(year)  
    except ValueError as e:  
        print(str(e))  
    else:  
        if year<=0:  
            print('11')  
        elif year%400==0 or (year%4==0 and year%100!=0):  
            print('%d is a leap year!'%year)  
        else:  
            print('%d is not a leap year!'%year)  
```

6. binomial coefficient

   1. Write a function that computes the binomial coefficient C(n,k) efficiently. 程序请命名为cnk.py;
   2. 了解一下中国福利彩票“双色球”的玩法. 假设你购买了一注该彩票, 中一等奖的概率为1/n, 改写上面的cnk.py为lottery.py, lottery.py的作用是算出正整数n;
   3. 打印出杨辉三角, 程序请命名为yanghui.py。
   
```python
import sys  
def cnk(n,k):  
    s1=1  
    s2=1  
    for i in range(k):  
        s1=s1*(n-i)  
        s2=s2*(i+1)  
    return int(s1/s2)  
n=int(sys.argv[1])  
k=int(sys.argv[2])  
print(cnk(n,k))  
```

```python
def cnk(n,k):  
    s1=1  
    s2=1  
    for i in range(k):  
        s1=s1*(n-i)  
        s2=s2*(i+1)  
    return int(s1/s2)  
n=cnk(33,6)*cnk(16,1)  
print(n)  
```

```python
import sys  
def cnk(n,k):  
    s1=1  
    s2=1  
    for i in range(k):  
        s1=s1*(n-i)  
        s2=s2*(i+1)  
    return int(s1/s2)  
n=int(sys.argv[1])  
for i in range(0,n+1):  
    for j in range(1,n-i+3):  
        print('  ',end='')  
    for k in range(0,i+1):  
        print(cnk(i,k),'  ',end='')  
    print('\n')  
```

7. ltds exercise 1(ltds代表list, tuple, dict, set及其它的python基本数据类型.)

   1. 随机产生一个7到14之间的正整数 (包含7或者14) n, 打印n;
   2. 产生一个长度为n的随机整数的list, list名字为L1, 每个整数在-10到10之间(包含-10或者10), 打印L1;
   3. 新建dict D1, D1中的key为L1中的不同元素, value为该元素在L1中出现的次数, 打印D1;
   4. 分3次拷贝L1为L2, 第1次对L2从小到大排序后输出L2; 第2次对L2从大到小排序后输出L2; 第3次对L2按绝对值从小到大排序后输出L2; 整个过程L1保持不变;
   5. 反向输出L1, 且L1变为了原来的反向.

```python
import random  
n=random.randint(7,14)  
print(n)  
L1=[random.randint(-10,10) for i in range(n)]  
print(L1)  
D1_list=[(i,L1.count(i)) for i in L1]  
D1=dict(D1_list)  
print(D1)  
L2=L1[:]  
L2.sort()  
print(L2)  
L2.sort(reverse=True)  
print(L2)  
L2.sort(key=abs)  
print(L2)  
L1.reverse()  
print(L1)  
```

8. ltds exercise 2.

   1. 用如下语句创建tuple T1:`T1=([1,2,3],{'A':90, 'B': 80}, {-100,0,100})`
   2. 打印T1;
   3. 更改T1里内嵌的list的第1个位置的元素为20 (位置从0开始计), 打印T1;
   4. 在T1里内嵌的list的尾部增加一个元素4, 打印T1;
   5. 更改T1里内嵌的dict的'A'对应的值为99, 打印T1;
   6. 删除T1里内嵌的set中的元素-100, 打印T1.

```python
T1=([1,2,3],{'A':90, 'B': 80}, {-100,0,100})  
print(T1)  
T1[0][1]=20  
print(T1)  
T1[0].append(4)  
print(T1)  
T1[1]['A']=99  
print(T1)  
T1[2].remove(-100)  
print(T1)  
```

9. ltds exercise 3. 
   1. 用list comprehension产生学生姓名list L1, 内含学生姓名"u19f34"至"u19f72" (不包括引号), 共39个;
   2. 用tuple comprehension产生学生的语文成绩的tuple T1, T1的每个元素为0-100之间的随机整数, 共39个元素;  
用tuple comprehension产生学生的数学成绩的tuple T2, T2的每个元素为0-100之间的随机整数, 共39个元素;  
用tuple comprehension产生学生的英语成绩的tuple T3, T3的每个元素为0-100之间的随机整数, 共39个元素;
   3. 用dict comprehension产生成绩单dict D1 (显然要从上面的list和tuples创建此dict);
   4. 漂亮打印出原始成绩单D1;
   5. 拷贝D1为D2, 按语文成绩从低到高漂亮打印出D2;
   6. 拷贝D1为D3, 按三门课的总成绩从高到低漂亮打印出D3;
   7. 拷贝D1为D4, 按语文成绩从低到高 (若语文成绩相同, 则按数学成绩从高到低) 漂亮打印出D4。

```python
import random  
L1=['u19f%s'%i for i in range(34,73)]  
T1=[random.randint(0,100) for i in range(1,40)]  
T1=tuple(T1)  
T2=[random.randint(0,100) for i in range(1,40)]  
T2=tuple(T2)  
T3=[random.randint(0,100) for i in range(1,40)]  
T3=tuple(T3)  
D1_list=[(l,(t1,t2,t3)) for l,t1,t2,t3 in zip(L1,T1,T2,T3)]  
D1=dict(D1_list)  
print(' 姓名    语文 数学 英语')  
for i in range(39):  
    print(D1_list[i][0].ljust(6),'|',str(D1_list[i][1][0]).ljust(4),  
        str(D1_list[i][1][1]).ljust(4),str(D1_list[i][1][2]).ljust(4))  
print('\n')  
D2_list=D1_list[:]  
D2_list.sort(key=lambda x:x[1][0])  
print(' 姓名    语文 数学 英语')  
for i in range(39):  
    print(D2_list[i][0].ljust(6),'|',str(D2_list[i][1][0]).ljust(4),  
        str(D2_list[i][1][1]).ljust(4),str(D2_list[i][1][2]).ljust(4))  
print('\n')  
D3_list=[(l,t1+t2+t3) for l,t1,t2,t3 in zip(L1,T1,T2,T3)]  
D3_list.sort(reverse=True,key=lambda x:x[1])  
print(' 姓名   总成绩')  
for i in range(39):  
    print(D3_list[i][0].ljust(6),'|',str(D3_list[i][1]).ljust(4))  
print('\n')  
D4_list=D1_list[:]  
D4_list.sort(key=lambda x:(x[1][0],x[1][1]))  
print(' 姓名    语文 数学 英语')  
for i in range(39):  
    print(D4_list[i][0].ljust(6),'|',str(D4_list[i][1][0]).ljust(4),  
        str(D4_list[i][1][1]).ljust(4),str(D4_list[i][1][2]).ljust(4))  
```

10. (finding primes) 改写或者全新地写lecture中讲过的计算素数的程序, 找出1-10,000,000之间的素数, 报告该算法所花的时间。

```python
import time  
t0=time.time()  
n=10000000  
L=[True]*n  
for i in range(2,int(n**0.5)+1):  
    if L[i]:  
        for j in range(i*i,n,i):  
            L[j]=False  
for x in range(2,n):  
    if L[x]:  
        print(x)  
print('所用时间：%fs'%(time.time()-t0))  
```

11. (fibonacci numbers) 写一个程序, 打印出小于10,000,000的所有fibonacci数. 第0个和第1个fibonacci数均为1, 从第0个开始打印, 逗号加空格隔开, 但最后一个数后面无逗号 or 空格, 格式在下面。

```python
n=10000000  
print('1, 1',end='')  
t1=1  
t2=2  
while t2<n:  
    print(', ',end='')  
    print(t2,end='')  
    t=t2  
    t2=t2+t1  
    t1=t  
```

12. (ansi vs utf8 encoding) 找出自己的汉语名字的ansi (gb2312) 和 utf8编码, 每个字分别找。

```python
name=['张','翼','鹏']  
L1=[str(i.encode('gbk')).replace(r'\x','').replace('\'','').upper() for i in name]  
L2=[str(i.encode('utf-8')).replace(r'\x','').replace('\'','').upper() for i in name]  
for i in range(len(name)):  
    print('%s的ansi编码为%s %s,utf8编码为%s %s %s'%(name[i],  
        L1[i][1:3],L1[i][3:],L2[i][1:3],L2[i][3:5],L2[i][5:]))  
```
