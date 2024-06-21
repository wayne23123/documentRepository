https://www.python.org/

2 個都勾

pip install requests

pip install BeautifulSoup4
-> html 解析器


pip install notebook


jupyter notebook

右邊 New

Python 3 (ipykernel)

https://jwlin.github.io/py-scraping-analysis-book/ch1/connect.html


import requests
from bs4 import BeautifulSoup

response=requests.get("https://jwlin.github.io/py-scraping-analysis-book/ch1/connect.html")

print(response)

soup=BeautifulSoup(response.text,"html.parser")

print(soup)


print(soup.find("h1"))
-><h1>歡迎</h1>


print(soup.find("h1").text)
->歡迎


print(soup.select("title"))
->[<title>test </title>]


print(soup.select("title")[0].text)
->test 


正則表達式

* __ 前一字元或括號內字元出現0次或多次 __ a*b* __ aaaab、aabb、bbb

+ __ 前一字元或括號內字元出現1次或多次 __ a+b+ __ aaabb、abbbb、abbbbb

{m,n} __ 前一字元或括號內字元出現m次到n次(包含m,n) __ a{1,2}b{3,4} __ abbb、aabbbb、aabbb

[] __ 符合括號內的任一字元 __ [A-Z]+ __ APPLE、QWER

\ __ 跳脫字元 __ \. \+ \* __ .|\


import re
pattern = "a*b+c"
string = " find aabc ac skip abb,dd "
re.findall(pattern,string)

->['aabc']


import re
pattern = "[0-9]+"
string = "12個22個35 個"
re.findall(pattern,string)

->['12', '22', '35']


list_temp=re.findall(pattern,string)
list_temp[1]

-> '12'



import re
pattern = "123"
string = "abc123, ser123"
re.findall(pattern,string)

->['123', '123']



import re
pattern = "[cmf]an"

cmf三種都可以，後面加an

string = "find canmanfanasd"
re.findall(pattern,string)

->['can','man','fan']



import re
pattern = "jim{2,5}y"
string = "findjimmyjimmmmmy"
re.findall(pattern,string)

->['jimmy','jimmmmmy']





