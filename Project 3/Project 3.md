1. 对于男同学：将 http://www.bit.edu.cn/ 上的“焦点关注”的数据用 python 爬下来，清理后保存为 bitjdgz1.html。源文件请命名为 bitjdgz1.py。

```python
import re  
from urllib.request import urlopen  
from bs4 import BeautifulSoup  
url='http://www.bit.edu.cn/'  
html=urlopen(url)  
item_list=re.findall(r'<div.*?class="item-txt01">(.*?)</div>',html.read().decode(),re.S)  
href=re.findall(r'(?<=href=\").+?(?=\")|(?<=href=\').+?(?=\')',item_list[0],re.S)  
text=re.findall(r'<a .*?>(.*?)</a>',item_list[0],re.S)  
html=urlopen(url)  
item_list=re.findall(r'<div.*?class="item-txt02">(.*?)</div>',html.read().decode(),re.S)  
for i in item_list:  
    href=href+re.findall(r'(?<=href=\").+?(?=\")|(?<=href=\').+?(?=\')',i,re.S)  
    text=text+re.findall(r'<a .*?>(.*?)</a>',i,re.S)  
text=[i.replace('\n','').replace('\r','').strip() for i in text]  
list_n=['<a href="'+url+i+'">'+j+'</a><br>' for i,j in zip(href,text)]  
with open('bitjdgz1.html','w') as f:  
    for i in list_n:  
        f.write(i)  
        f.write('\n')  
```

2. 对于男同学：将 http://www.bit.edu.cn/ 上的“焦点关注”的数据用 python 爬下来，用BeautifulSoup4分析后保存为 bitjdgz2.html。源文件请命名为 bitjdgz2.py。

```python
from urllib.request import urlopen  
from bs4 import BeautifulSoup  
url='http://www.bit.edu.cn/'  
html=urlopen(url)  
soup=BeautifulSoup(html,'lxml')  
n1=soup.find('div','item-txt01')  
n1='<a href="'+url+n1.a['href']+'">'+n1.text+'</a><br>'  
list_n=soup.find_all('div','item-txt02')  
list_n=['<a href="'+url+i.a['href']+'">'+i.text.replace('\n','').replace(' ','')[:-11]+'</a><br>' for i in list_n]  
list_n=[n1]+list_n  
with open('bitjdgz2.html','w') as f:  
    for i in list_n:  
        f.write(i)  
        f.write('\n')  
```

3. Web crawler project using python

```python
import sys  
import xlwt  
import time  
from urllib.request import urlopen,quote  
from bs4 import BeautifulSoup  
flag=0  
search_keyword=sys.argv[1]  
origin='http://ico.bit.edu.cn/opac/openlink.php?strSearchType=title&strText='+search_keyword  
logfilename='log.'+search_keyword+'.txt'  
excelfilename='books.'+search_keyword+'.xls'  
head=['序号','分类','书名','作者','索书号','馆藏复本','可借复本','出版社','出版年份']  
def write_xls(url_list):  
    workbook=xlwt.Workbook(encoding='utf-8')  
    worksheet=workbook.add_sheet('sheet1')  
    for i in range(len(head)):  
        worksheet.write(0,i,head[i])  
    for n,i in enumerate(url_list):  
        url=quote(i,safe=";/?:@&=+$,")  
        html=urlopen(url)  
        soup=BeautifulSoup(html,'lxml')  
        list_book=soup.find_all('li','book_list_info')  
        for j in range(len(list_book)):  
            worksheet.write(j+20*n+1,0,j+1+20*n)  
            worksheet.write(j+20*n+1,1,list_book[j].span.text)  
            worksheet.write(j+20*n+1,2,list_book[j].h3.a.text[2:])  
            info=list_book[j].p.get_text('\n','<br/>').split('\n')  
            contents=list_book[j].p.contents  
            ay=contents[4].strip().split()  
           if len(ay)==2:  
                worksheet.write(j+20*n+1,7,ay[0])  
                worksheet.write(j+20*n+1,8,ay[1])  
            elif len(ay)==1:  
                worksheet.write(j+20*n+1,8,ay[0])  
            worksheet.write(j+20*n+1,3,contents[2].strip())  
            worksheet.write(j+20*n+1,4,list_book[j].h3.contents[2].strip())  
            worksheet.write(j+20*n+1,5,info[0][5])  
            worksheet.write(j+20*n+1,6,info[1][5])    
    workbook.save(excelfilename)  
url=quote(origin,safe=";/?:@&=+$,")  
html=urlopen(url)  
soup=BeautifulSoup(html,'lxml')  
t=soup.find('span',style="color:#f00;")  
if t!=None:  
    flag=3  
else:  
    num=int(soup.find('strong','red').text)  
    if num<=20:  
        flag=2  
    else:  
        flag=1  
        pages=num//20+1 if num%20!=0 else num//20  
if flag==1:  
    start=time.time()  
    url_list=[origin]  
    total_books=num  
    total_pages=pages  
    url_list=url_list+[origin+'&page=%d'%i for i in range(2,total_pages+1)]  
    write_xls(url_list)  
    end=time.time()  
    with open(logfilename,'w') as f:  
        f.write('total_books = %s'%str(total_books)+'\n')  
        f.write('total_pages = %s'%str(total_pages)+'\n')  
        f.write('elapsed time = %f'%(end-start))  
if flag==2:  
    start=time.time()  
    url_list=[origin]  
    total_books=num  
    total_pages=1  
    write_xls(url_list)  
    end=time.time()  
    with open(logfilename,'w') as f:  
        f.write('total_books = %s'%str(total_books)+'\n')  
        f.write('total_pages = %s'%str(total_pages)+'\n')  
        f.write('elapsed time = %f'%(end-start))  
if flag==3:  
    with open(logfilename,'w') as f:  
        f.write(t.text)  
```
