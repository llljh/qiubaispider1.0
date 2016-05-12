# qiubaispider1.0
#qiubaispider

# encoding: utf-8
import urllib
import urllib2
import re


page = 1
url = 'http://www.qiushibaike.com/hot/page/' + str(page)
user_agent = 'Mozilla/4.0 (compatible; MSIE 5.5; Windows NT)'
headers = { 'User-Agent' : user_agent }
try:
    request = urllib2.Request(url,headers = headers)
    response = urllib2.urlopen(request)
    content = response.read().decode('utf-8')
    myItems = re.findall('h2>(.*?)</h2.*?content">(.*?)</.*?number">(.*?)</.*?<img src="(.*?)".*?',content,re.S)
    items = []
    for item in myItems:
        items.append([item[0],item[1]])
        print item[1]
except urllib2.URLError, e:
    if hasattr(e,"code"):
        print e.code
    if hasattr(e,"reason"):
        print e.reason
