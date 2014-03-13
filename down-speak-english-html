#encoding:utf-8
'''
Created on 2014-3-12
get the english-learning matiarial from talkenglish.com
@author: zhaoliang
'''
import urllib2
from bs4 import BeautifulSoup
import re

def down_task(url):
    req = urllib2.Request(url, headers={'User-Agent' : "Magic Browser"}) 
    print url
    try:
        webpage = urllib2.urlopen(req)
        content=webpage.read().decode('utf8','ignore')
        soup = BeautifulSoup(content)
        table=soup.find(id="GridView1")
        title=soup.title.string
        print title
        title='<h1>'+title+'</h1>'
        lesson=table.find('td')
        a_ptn = re.compile('"<a.+?">',re.DOTALL)
        a2_ptn = re.compile('</a>"',re.DOTALL)
        h_ptn = re.compile('<h1>.+?</h1>',re.DOTALL)
        other_ptn = re.compile('<(br/|td|/td|strong|/strong)+?>',re.DOTALL)
        tip_ptn = re.compile('(Short Answers|Long Answers|Long Answer)+?',re.DOTALL)
        
        s=h_ptn.sub('',str(lesson))
        s=a_ptn.sub('<p class="answer">"',str(lesson))
        s=a2_ptn.sub('"</p>',s)
        s=other_ptn.sub('',s)
        s=tip_ptn.sub('',s)
        return s
    except Exception as e:
        print "Error happened"
        return ""

 

title='Talk English'
page = '<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"><html lang="en" xmlns="http://www.w3.org/1999/xhtml"><head>'
page += '<title>'+title+'</title>'
page += '<style>body{background-color: #FFFFFF;color: #000000;font-family: verdana;font-size: 10.5pt;font-style:italic;}.answer{font-weight:bold;font-style:normal;}</style></head><body>'

url_header = 'http://www.talkenglish.com/'
main_url='http://www.talkenglish.com/LessonIndex.aspx'
req = urllib2.Request(main_url, headers={'User-Agent' : "Magic Browser"})
webpage = urllib2.urlopen(req)
content=webpage.read().decode('utf8','ignore')
soup = BeautifulSoup(content)
atags=soup.findAll('a')
pattern = re.compile(r'/*LessonDetails\.aspx\?ALID=\d+')
for a in atags:
    href=a.get('href')
    match = pattern.match(href)
    if  match:
        url=url_header+match.group()
        url=url.replace('//L','/L')
        page += (down_task(url))
    
page += '</body></html>'
filename='c:/'+title+'.html';
file_object = open(filename,'wb')
file_object.write(page)
file_object.close()
