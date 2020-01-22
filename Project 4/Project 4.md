1. 写一个模块 mymod1, 在其内定义全局整形变量int1, 函数func1, 类class1, 并写一个相应的模块测试程序. 

```python
int1=10  
def func1(c):  
    return 2*c  
class class1():  
    def __init__(self):  
        self.attr1='zyp'  
        self.attr2=24  
    def print_attrs(self):  
        print('attr1 = %s, attr2 = %d'%(self.attr1,self.attr2))  
if __name__=='__main__':  
    print('mymod1 is self-run.')  
else:  
    print('mymod1 is imported.')  
    print('mymod1.int1 = %d'%int1)  
    print(func1)  
    print('mymod1.func1(123) = %d'%func1(123))  
    cla=class1()  
    print(cla)  
    cla.print_attrs()  
```

2. The Collatz conjecture concerns a sequence defined as follows: start with any positive integer n>1. Then each term is obtained from the previous term as follows: if the previous term is even, the next term is one half the previous term. If the previous term is odd, the next term is 3 times the previous term plus 1. The conjecture is that no matter what value of n, the sequence will always reach 1. 编写一个 python 程序验证 Collatz 猜想在1-1000000之间成立. 

```python
import sys  
def collatz(n,max=None):  
    m=n  
    list1=[m]  
    if max==None:  
        while m!=1:  
            if m%2==0:  
                m=int(m/2)  
                list1+=[m]  
            else:  
                m=3*m+1  
                list1+=[m]  
        return list1  
    else:  
        com=[]  
        num=n  
        for i in range(n,max+1):  
            tem=collatz(i)  
            if len(tem)>=len(com):  
                num=i  
                com=tem  
        print('When n = %d, collatz(n) for n between %d and %d produces the longest sequence with length %d:'%(num,n,max,len(com)))  
        print(com)  
if len(sys.argv)==2:  
    print(collatz(int(sys.argv[1])))  
elif len(sys.argv)==3:  
    collatz(int(sys.argv[1]),int(sys.argv[2]))  
```

3. 用正则表达式删除多余的空行, 替换单词, 或者验证日期的有效性. 

```python
import re  
s1 = '''''1st line\n2nd line\n\n3rd line\n\n\n4th line\n'''  
s1=re.sub('\n{2,}','\n',s1)  
s1=re.sub('$\n','',s1)  
print('----------- re test #1: 删除空行 -----------')  
print(s1)  
print('----------- re test #2: 替换单词 -----------')  
with open('ZenOfPython.txt','r') as f:  
    txt=f.read()  
front=re.findall(r'\b[a-zA-Z]+\b is better than',txt)  
front=[i[:-15] for i in front]  
behind=re.findall(r'is better than \b[a-zA-Z]+\b',txt)  
behind1=[i[15:] for i in behind]  
behind2=[i[15].upper()+i[16:] for i in behind]  
for i in range(len(front)):  
    txt=re.sub(front[i]+' is better than',behind2[i]+' is better than',txt,1)  
    txt=re.sub('is better than '+behind1[i],'is worse than '+front[i].upper(),txt,1)  
print(txt)  
print('----------- re test #3: 验证日期 -----------')  
dates=['1900-01-01', '1942 06 30', '1949/12/06', '1999.10.01',  
       '2000-02-28', '2004.03.31', '2008/08/08', '2099 12 31',  
       '2000-02/28', '2004 03.31', '2008/8/08', '2100-04-30']  
for i in dates:  
    flag=re.match(r'(?:19|20)[0-9]{2}([- /.])(?:0[1-9]|1[012])\1(?:0[1-9]|[12][0-9]|3[01])',i)  
    if flag==None:  
        print('%s is an invalid date.'%i)  
```

4. 用os.walk遍历dir1路径 (dir1路径及内含的文件在p401src.zip里): 若遇到的是子路径, 就打印出该路径名后接空格后接D; 若遇到的是文件, 就打印出该文件名后接空格后接文件的大小 (以字节计算).

```python
import os  
from os.path import basename, getsize  
  
mydir='dir1'  
for root, dirs, files in os.walk(mydir):  
    level = root.replace(mydir, '').count(os.sep)  
    dir_form = "    " * level  
    file_form = "    "* (level+1)  
    print('%s%s D' % (dir_form, basename(root)))  
    for f in files:  
        filepath = root + os.sep + f  
        print('%s%s %d' % (file_form, f, getsize(filepath)))  
```

5. 给定一个文本文件, 比如ZenOfPython.txt, 逐行读取此文件, 然后倒序写入另外一个文件, 比如ZenOfPython_2.txt. 输入和输出的文件名都从命令行上获取. 

```python
import sys  
filepath=sys.argv[1]  
filepath2=sys.argv[2]  
with open(filepath,'r') as f:  
    text=f.readlines()  
for i in range(len(text)):  
    for j in range(len(text[i])):  
        if text[i][j]==' ':  
            text[i]=text[i][:j].upper()+text[i][j:]  
            break  
with open(filepath2,'w') as f:  
    for i in range(len(text),0,-1):  
        f.write(('%d'%(i)).zfill(2)+' ')  
        f.write(text[i-1])  
```

6. 用Python实现bubble sort, 并探讨swap count的规律. Python代码a, b = b, a称为一次swap. 

```python
import operator  
import numpy as np  
def bubble_sort(L,func=operator.lt):  
    n=len(L)  
    t=0  
    for i in range(n):  
        for j in range(0, n-i-1):  
            if not func(L[j],L[j+1]):  
                L[j], L[j+1] = L[j+1], L[j]  
                t+=1  
    return t  
def myabs(x, y):  
    return True if abs(x)<abs(y) else False  
if __name__ == '__main__':  
    L1=[-3, 9, -8, 7, 0, 2, -1, 5, -4, 6]  
    L2=L1[:]  
    L3=L1[:]  
    print('--------------- 测试#1: 从小到大 ---------------')  
    print('排序前: L1 = %s'%str(L1))  
    c=bubble_sort(L1)  
    print('排序后: L1 = %s'%str(L1))  
    print('swap count: %d'%c)  
    print()  
    print('--------------- 测试#2: 从大到小 ---------------')  
    print('排序前: L2 = %s'%str(L2))  
    c=bubble_sort(L2,operator.ge)  
    print('排序后: L2 = %s'%str(L2))  
    print('swap count: %d'%c)  
    print()  
    print('--------------- 测试#3: 按绝对值从小到大 ---------------')  
    print('排序前: L3 = %s'%str(L3))  
    c=bubble_sort(L3,myabs)  
    print('排序后: L3 = %s'%str(L3))  
    print('swap count: %d'%c)  
    print()  
    print('--------------- 测试#4: 随机全排列排序 ---------------')  
    print('结果存在文件bubble_sort.txt里')  
    with open('bubble_sort.txt','w') as f:  
        for i in range(10,5010,10):  
            f.write(str(i).rjust(4)+' ')  
            L=list(np.random.permutation(i))  
            c=bubble_sort(L)  
            f.write('%.4f'%(c/(i*i))+'\n')  
```

*解释为什么为何 swapcount / (n*n) 趋近于 1/4 as n goes to infinity：  
因为冒泡排序的过程是遍历前n个元素、遍历前n-1个元素、...、遍历前2个元素，假设整个列表完全反序，那么最多交换n(n-1)/2次。当n趋于无穷时，根据大数定律，列表中正序和反序组合的比例趋于1：1，那么冒泡排序只需要交换n(n-1)/4次。所以swapcount / (n*n)趋于1/4。*

7. 本题考查 zipfile module 的使用.  
写出在终端调用 zipfile module 把文件: p401.doc, logistic.model.png, logistic.soln.png打包成zf1.zip的命令：
```python
import zipfile
zf=zipfile.ZipFile('zf1.zip','w')
zf.write('p468.doc')
zf.write('logistic.model.png')
zf.write('logistic.soln.png')
zf.close
```

写出在终端调用 zipfile module 把 zf2.zip 里的文件解压到当前路径的子路径 zf2dir 下的命令：
```python
import zipfile
zf=zipfile.ZipFile('zf2.zip')
zf.extractall(path='zf2dir')
zf.close()
```

```python
from zfinfo import zfinfo  
import zipfile  
str1 = '这个字符串不属于任何硬盘上的文件, 但我们可以把它作为文件, 比如zf_str1.txt, 写入zip文件里. 解压的时候它将被释放成文件zf_str1.txt.'  
with open('zf_str1.txt','w') as f:  
    f.write(str1)  
zf=zipfile.ZipFile('zf2.zip','w',zipfile.ZIP_DEFLATED)  
zf.write('p468.doc')  
zf.write('logistic.model.png')  
zf.write('logistic.soln.png')  
zf.write('zf_str1.txt')  
zf.comment='此文件内含有重要信息。'.encode('utf-8')  
zf.infolist()[0].comment='my .doc file'.encode('utf-8')  
zf.infolist()[1].comment='我的第1个.png文件'.encode('utf-8')  
zf.infolist()[2].comment='我的第2个.png文件'.encode('utf-8')  
zf.infolist()[3].comment='信息来源于字符串, 而不是文件.'.encode('utf-8')  
zf.close()  
zfinfo('zf2.zip')  
```

8. 用hashlib计算文件的sha1 sum. 

```python
from hashlib import sha1  
from sys import argv  
from os.path import isfile  
from glob import glob  
def sha(file):  
    if isfile(file):  
        with open(file,'rb') as f:  
            mySha1 =sha1()  
            mySha1.update(f.read())  
            print(mySha1.hexdigest(),end='')  
            print('  '+file)  
    else:  
        for i in glob(file+'/**'):  
            sha(i)  
for inp in argv[1:]:  
    L=glob(inp)  
    for i in L:  
        sha(i)  
```

9. 可以用 Python Image Library (PIL) 包处理图片. 请把p401src.zip里的imgs/orig.jpg文件 crop 成11个文件: p00.jpg, p01.jpg, ..., p10.jpg, 其中p00.jpg保存头部的红底白字(含)及其上面的信息, p01.jpg, ..., p10.jpg依次保存图片中的第一步至第十步的信息. 你可以参看资料包里提供的样图: q00.jpg, q01.jpg, ..., q10.jpg. 

```python
from PIL import Image  
height=[1500,1300,1850,1110,1110,1110,1110,1100,1100,1100,990,0]  
img = Image.open('imgs/orig.jpg')  
y1=0  
y2=height[0]  
for i in range(11):  
    newimg=img.crop((0,y1,img.size[0],y2))  
    newimg.save('imgs/p'+str(i).zfill(2)+'.jpg')  
    y1=y2  
    y2+=height[i+1]  
```

10. Desgin and implement classes and inheritance: 定义类Animal和它的两个子类Horse和Fish. 

```python
class Animal():  
    def __init__(self,name,weight):  
        self._name=name  
        self._weight=weight  
    def __str__(self):  
        return '%s with weight %d'%(self._name, self._weight)  
    def __repr__(self):  
        return 'name: %s, weight: %d'%(self._name, self._weight)  
    def move(self):  
        print('%s is moving'%self._name)  
class Horse(Animal):  
    habitat='land'  
    def move(self):  
        print('%s is galloping'%self._name)  
class Fish(Animal):  
    def __init__(self,name,weight):  
        Animal.__init__(self,name,weight)  
        self.__color='white'      
    @property  
    def color(self):  
        return self.__color  
    @color.setter  
    def color(self,value):  
        if value in {'white','red','gold'}:  
            self.__color=value  
        else:  
            raise ValueError("Color is one of {'white','red','gold'}.")  
    def move(self):  
        print('%s is swimming'%self._name)  
    @classmethod  
    def livein(self):  
        print('Fish lives in water')  
anm=Animal('动物1',100)  
print(anm)  
print(repr(anm))  
anm.move()  
f=Fish('鱼2',3)  
print(f)  
print(repr(f))  
f.move()  
f.livein()  
Fish.livein()  
print(f.color)  
f.color='gold'  
print(f.color)  
try:  
    f.color='cyan'  
except ValueError as e:  
    print(e)  
h=Horse('马3',200)  
print(h)  
print(repr(h))  
h.move()  
print(h.habitat)  
print(Horse.habitat)  
```

11. 求解常微分方程的近似解的最简单方法是欧拉单步法 (Euler's Method). 本题考查用numpy中的数据结构来计算近似解, 并用matpotlib画图.

```python
import numpy as np  
import matplotlib.pyplot as plt  
h=0.1  
x=np.arange(0,20+h,h)  
y=5000/(1+4999*np.exp(-x))  
plt.plot(x,y,label='true soln')  
yp=[1]  
yk1=1  
for i in range(int(20/h)):  
    yk=yk1  
    yk1=0.0002*(5000-yk)*yk*h+yk  
    yp.append(yk1)  
plt.scatter(x,yp,c='y',label='approx.soln')  
plt.title('Logistic model')  
plt.ylabel('Population')  
plt.legend()  
plt.show()  
```

12. 写一个 generator function 来产生 Lucas 数.

```python
import sys  
def Lucas(max=-1):  
    a=1  
    b=3  
    if max==-1:  
        yield a  
        yield b  
        while True:  
            s=a+b  
            yield s  
            a=b  
            b=s  
    elif max==1:  
        yield 1  
    elif max==2:  
        yield 1  
        yield 3  
    else:  
        yield a  
        yield b  
        for i in range(max-2):  
            s=a+b  
            yield s  
            a=b  
            b=s  
c1=sys.argv[1]  
c2=sys.argv[2]            
if int(c1)==-1:  
    f=int(c2)  
else:  
    f=min(int(c1),int(c2))  
for i in Lucas(f):  
    print(i,end='')  
    print(' ',end='')  
```

13. 写一个 function decorator 来装饰 bubble_sort() 函数, 该函数请从第33题中的 bubble_sort.py 中直接 import, 装饰器的功能是报告每一次bubble sort完成排序工作所花去的时间(以秒计), 并最终统计调用次数和总时间花销(即累加各次的时间花销).

```python
import numpy as np  
import operator, functools, time  
from bubble_sort import bubble_sort  
def timer(func):  
    bubble_sort.ncalls=0  
    bubble_sort.time=0  
    @functools.wraps(func)  
    def wrapper(L,func2=operator.lt):  
        L1=[str(i) for i in L[:5]]  
        start=time.time()  
        t=func(L,func2)  
        end=time.time()  
        delta=end-start  
        bubble_sort.ncalls+=1  
        bubble_sort.time+=delta  
        L2=[str(i) for i in L[:5]]  
        print('排序前序列的前5个数为: %s'%' '.join(L1))  
        print('排序后序列的前5个数为: %s'%' '.join(L2))  
        print('bubble_sort花了%f秒, swapcount = %d.'%(delta,t))  
    return wrapper  
if __name__ == '__main__':  
    bubble_sort = timer(bubble_sort)  
    for i in range(np.random.randint(3, 8)):  
        n = np.random.randint(1000, 3001)  
        L = list(np.random.permutation(n))  
        func = operator.gt  
        swapcnt = bubble_sort(L, func)  
    print(f'\n共调用{bubble_sort.__name__}函数\  
{bubble_sort.ncalls}次, 总时间为{bubble_sort.time:.2f}秒.')  
```

14. 写一个 class decorator 来装饰 bubble_sort() 函数. 功能和第40题完全一样, 只不过这里我们用类. 

```python
import numpy as np  
import operator, functools, time  
from bubble_sort import bubble_sort  
class timer(object):  
    def __init__(self,func):  
        self.func=func  
        self.ncalls=0  
        self.time=0  
        self.name=func.__name__  
    def __call__(self,L,func2=operator.lt):  
        L1=[str(i) for i in L[:5]]  
        start=time.time()  
        t=self.func(L,func2)  
        end=time.time()  
        delta=end-start  
        self.time+=delta  
        self.ncalls+=1  
        L2=[str(i) for i in L[:5]]  
        print('排序前序列的前5个数为: %s'%' '.join(L1))  
        print('排序后序列的前5个数为: %s'%' '.join(L2))  
        print('bubble_sort花了%f秒, swapcount = %d.'%(delta,t))  
bubble_sort = timer(bubble_sort)  
for i in range(np.random.randint(3, 8)):  
    n = np.random.randint(1000, 3001)  
    L = list(np.random.permutation(n))  
    func = operator.gt  
    swapcnt = bubble_sort(L, func)  
print(f'\n共调用{bubble_sort.name}函数\  
{bubble_sort.ncalls}次, 总时间为{bubble_sort.time:.2f}秒.')   
```

15. 写两个 decorators 来嵌套装饰 bubble_sort() 函数, 第一个装饰器函数 timer() 从第40题的dec_func.py中直接import. 

```python
import numpy as np  
import time  
import operator, functools, time, sys  
from bubble_sort import bubble_sort  
from dec_func import timer   
def star(c1='-', c2='*', repeat=42):  
    t=0  
    bubble_sort.ncalls=0  
    bubble_sort.time=0  
    def box(func):  
        @functools.wraps(func)  
        def wrapper(*args, **kwargs):  
            nonlocal t  
            t+=1  
            print('第%d次调用%s:'%(t,str(func.__name__)))  
            print(c1*int(repeat))  
            start=time.time()  
            func(*args, **kwargs)  
            end=time.time()  
            delta=end-start  
            bubble_sort.ncalls+=1  
            bubble_sort.time+=delta  
            print(c2*int(repeat))  
            print()  
        return wrapper  
    return box  
@star()  
def say_hello(name):  
    print(f'hello {name}')  
    return f'HELLO {name}'  
say_hello('无名')  
say_hello('Ming Wu')  
say_hello('John Doe')  
if len(sys.argv) == 1:  
    bubble_sort = star()(timer(bubble_sort))  
else:  
    bubble_sort = star(*sys.argv[1:])(timer(bubble_sort))  
for i in range(np.random.randint(3, 8)):  
    n = np.random.randint(1000, 3001)  
    L = list(np.random.permutation(n))  
    func = operator.gt  
    swapcnt = bubble_sort(L, func)  
print(f'\n共调用{bubble_sort.__name__}函数\  
{bubble_sort.ncalls}次, 总时间为{bubble_sort.time:.2f}秒.') 
```

16. 对grades.xls文件里记录的学生成绩进行分析, 特别是预测序号为161-169的学生的“总评”成绩, 预测成绩写入grades_predict.xls. 

```python
import xlrd  
import xlwt  
import numpy as np  
from sklearn import linear_model  
myWorkbook=xlrd.open_workbook('grades.xls')  
mySheets=myWorkbook.sheets()  
mySheet=mySheets[0]  
print('------------------ 测试 #1: head -------------------')  
print('  序号  作业  考勤  测验  加分  卷面  总评')  
for i in range(1,6):  
    for j in mySheet.row_values(i):  
        print(str(j).rjust(5)+' ',end='')  
    print()  
print('------------------ 测试 #2: tail -------------------')  
print('  序号  作业  考勤  测验  加分  卷面  总评')  
for i in range(161,170):  
    for j in range(6):  
        print(str(mySheet.row_values(i)[j]).rjust(5)+' ',end='')  
    print(str(mySheet.row_values(i)[6])+' NaN')  
print('----------------- 测试 #3: 卷面>=98 ------------------')  
print('  序号  作业  考勤  测验  加分  卷面  总评')  
score=mySheet.col_values(5)  
good=[i for i in range(1,len(score)) if score[i]>=98]  
for i in good:  
    for j in mySheet.row_values(i):  
        print(str(j).rjust(5)+' ',end='')  
    print()  
print('----------------- 测试 #4: predict ------------------')  
print('  序号  作业  考勤  测验  加分  卷面  总评')  
x_train=[]  
for i in range(1,6):  
    x_train+=[mySheet.col_values(i)[1:161]]  
x_train=np.array(x_train).transpose()  
y_train=np.array(mySheet.col_values(6)[1:161]).reshape(-1,1)  
x_test=[]  
for i in range(1,6):  
    x_test+=[mySheet.col_values(i)[161:170]]  
x_test=np.array(x_test).transpose()  
regr=linear_model.LinearRegression()  
regr.fit(x_train,y_train)  
y_predict=regr.predict(x_test)  
workbook=xlwt.Workbook(encoding='utf-8')  
worksheet=workbook.add_sheet('sheet1')  
for i in range(len(mySheet.row_values(0))):  
    worksheet.write(0,i,mySheet.row_values(0)[i])  
for i in range(161,170):  
    for j in range(len(mySheet.row_values(0))-1):  
        worksheet.write(i-160,j,mySheet.row_values(i)[j])  
        print(str(mySheet.row_values(i)[j]).rjust(5)+' ',end='')  
    worksheet.write(i-160,6,y_predict[i-161,0])  
    print('%.2f'%y_predict[i-161,0])  
workbook.save('grades_predict.xls')  
print('----------------- 测试 #5: 总评<60 ------------------')  
print('  序号  作业  考勤  测验  加分  卷面  总评')  
score=mySheet.col_values(6)  
good=[i for i in range(1,len(score)-9) if score[i]<60]  
for i in good:  
    for j in mySheet.row_values(i):  
        print(str(j).rjust(5)+' ',end='')  
    print()  
```
