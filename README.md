Python爬取`多点商城`整站商品数据，在爬取之前我们需要进行需求分析，我们要清楚我们需要爬取什么，我们需要什么样的数据，我们需要怎样来设计表结构，我们是否需要保存数据到本地等等一系列问题，我们带着这些问题来分析`多点商城`设计特点，我们用我们掌握的爬取知识点来爬取需要的商品信息，并对得到的商品信息进行数据解析，源码请点击[Python爬取多点商城整站](https://github.com/lb2281075105/LBDuoDian)。
```
Python爬取多点商城整站步骤介绍：
1、Python开发工具pycharm安装，Python-3.6.4(Mac、Windows)即可，PHPStudy/XMAPP集成环境搭建(其他集成环境也可)；
2、展示多点商城设计特点图；
3、列出分析爬取多点整站思维导图；
4、需求分析；
5、爬取操作过程；
6、编写代码；
7、表结构设计，代码经过多次修改健壮无比，导出sql文件使用即可；
8、注意事项(申明)
```
一、工具和环境搭建
① Python开发工具pycharm安装，百度一下找到比较新的版本安装即可，链接地址[安装Pycharm](https://www.jetbrains.com/pycharm/download/#section=mac)，这个没有过多的要求，展示图如下：![pycharm.png](http://upload-images.jianshu.io/upload_images/3276082-ab4674fb755433ba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
② Python-3.6.4(Mac、Windows)安装，Python2.x版本即将停止更新了，学习Python，最好使用较新的版本，Python3.6.4是比较稳定的，我们下载这个就可以，链接地址[安装Python3.6.4](https://www.python.org/downloads/windows/)
Window:
![python3.6.4-window.png](http://upload-images.jianshu.io/upload_images/3276082-034ddf2f304efac5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
Mac:
![pycharm-mac.png](http://upload-images.jianshu.io/upload_images/3276082-ad8b5c63f08a0c7a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
③ PHPStudy/XMAPP集成环境搭建，下载安装即可使用
PHPStudy-window:
![phpstudy-window.png](http://upload-images.jianshu.io/upload_images/3276082-ad2d09c0d6839e29.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

XMAPP-mac:
![xmapp-mac.png](http://upload-images.jianshu.io/upload_images/3276082-3aaa13c28799bb0e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

二、多点商城设计特点图
① 首先我们先浏览下多点商城页面，展示图如下：![多点1.png](http://upload-images.jianshu.io/upload_images/3276082-f06eba3c3068218a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![多点2.png](http://upload-images.jianshu.io/upload_images/3276082-8f2396d8212d7715.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


② 我们主要关注爬取页设计结构，对应上图中的`分类`模块，`分类`模块包含了`多点`商城全部数据，我们只爬取`分类`模块就可以了，展示图如下：
![多点3.png](http://upload-images.jianshu.io/upload_images/3276082-de06e8b89d1cb5a7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
三、列出分析爬取多点整站思维导图

在文章开头列出了很多疑问，我们应该怎么样获取我们需要的数据那，这部分我们用思维导图来列出我们需要做的事情，思维导图会更加清晰的理清我们的思路，思维导图如下：
![多点爬取分析思维导图.png](http://upload-images.jianshu.io/upload_images/3276082-f275cf9aff27caf3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

四、需求分析
`多点商城`中的商品信息比较全面，符合我们工作需求，`多点商城`中商品图片很是清晰，商品包括的信息全面：商品名字、商品展示图、商品详情轮播图、商品规格参数、商品介绍图、商品分类、品牌brand、商品唯一对应的skuid、商品分类id、猜你喜欢商品图、商品价格等等。
① 获取到数据录入sql数据表设计展示如下：
![duodianSql.png](http://upload-images.jianshu.io/upload_images/3276082-29dea54e93d9c9a3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
② 本地数据展示图
![本地数据截图.png](http://upload-images.jianshu.io/upload_images/3276082-f848675a2cd2fa26.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
设置好自己的域名以后，可以远程或者本地连接自己的数据库(商品库)，终于拥有了属于自己的商品库喽。
五、爬取操作过程
① 获取爬取网站链接[多点商城](https://i.dmall.com/?source_id=wxmp#wxdmall/view/home/home)
② 进入分类，分析大分类和小分类之间的联系，并分析我们爬取数据的对象，爬取对象是`小分类`，截图如下：
![多点4.png](http://upload-images.jianshu.io/upload_images/3276082-8ee23fc31a5f1a1f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
③ 我们应该怎么样获取`小分类`的链接哪，接下来我们展示操作过程，鼠标点击右键查看`检查`审查元素，获取到的[链接地址](https://gatewx.dmall.com/customersite/searchWareByCategory?param=%7B%22pageNum%22%3A1%2C%22pageSize%22%3A30%2C%22venderId%22%3A%221%22%2C%22storeId%22%3A%22108%22%2C%22sort%22%3A%221%22%2C%22categoryId%22%3A11347%2C%22categoryLevel%22%3A3%2C%22cateSource%22%3A1%2C%22bizType%22%3A%221%22%7D&token=&source=2&tempid=C7DB797E4D30000213C96611102027D0&pubParam=%7B%22utmSource%22%3A%22wxmp%22%7D&_=1517559789814)，操作过程截图如下：
![多点5.png](http://upload-images.jianshu.io/upload_images/3276082-289f98f9861d5195.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![多点6.png](http://upload-images.jianshu.io/upload_images/3276082-8c7d37e4ac631702.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
④ 对于审查得到的数据我们应该怎么获取数据哪，接下来我对链接到的数据进行分析，在浏览器中打开我们获取的数据列表如下：
![多点7.png](http://upload-images.jianshu.io/upload_images/3276082-68cb26e9cb861e10.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
⑤ 接下来就是编写代码的时候，编写代码我放到下部分进行分享
六、撸代码(撸代码是一件很快乐的事)
① 在Ptython3.6.4环境中进行开发的，在开发过程中用到了很多Python包如下：
```
# urllib请求用到的开发包
from  urllib import request
# os是创建文件或者文件夹的开发包
import os
# json处理python对象和字符串之间的转换
import json
# jsonpath获取数据中需求字段的开发包
import jsonpath
# time主要用来设置休眠时间
import time
# ssl验证
import ssl
# selenium自动化，处理动态js
from selenium import webdriver
# pymysql连接数据库包
import pymysql
# lxml解析包
from lxml import etree
```
② 打开PHPStudy或者XMAPP集成服务器，用`pymysql`包连接mysql，自动创建数据库、表名、生成我们设定的字段；
③ 我们用`urllib`包来请求我们审查到的链接，请求到数据并转化成我们需要的json格式；
④ 用`jsonpath`模块来解析json数据，获取我们需要的字段；
⑤ 用`selenium `动态获取js数据，并分析获取到数据页数；
⑥ 所有工作准备完毕后，执行成功后，就插入数据表中，并同时把图片保存到本地

附源码
```
# 盐糖味精
# 1、共页爬取所有商品
# 2、通过商品skuId获取商品详情页面
# 3、用到动态获取商品信息selenium，自动化

# 商品列表原链接：https://gatewx.dmall.com/customersite/searchWareByCategory?param=%7B%22pageNum%22%3A1%2C%22pageSize%22%3A30%2C%22venderId%22%3A%221%22%2C%22storeId%22%3A%22108%22%2C%22sort%22%3A%221%22%2C%22categoryId%22%3A10905%2C%22categoryLevel%22%3A3%2C%22cateSource%22%3A1%2C%22bizType%22%3A%221%22%7D&token=&source=2&tempid=C7B357489E400002B1514BD01B00E270&pubParam=%7B%22utmSource%22%3A%22wxmp%22%7D&_=1512268447989
# 商品列表url解码后连接：https://gatewx.dmall.com/customersite/searchWareByCategory?param={"pageNum":1,"pageSize":30,"venderId":"1","storeId":"108","sort":"1","categoryId":10905,"categoryLevel":3,"cateSource":1,"bizType":"1"}&token=&source=2&tempid=C7B357489E400002B1514BD01B00E270&pubParam={"utmSource":"wxmp"}&_=1512268447989

# https://i.dmall.com/?source_id=wxmp#item/view/item/item:id=1-108-11348
# 商品详情有 --- 轮播图、猜你喜欢图片、商品宣传图
from  urllib import request
import os
import json
import jsonpath
import time
import ssl
from selenium import webdriver
import pymysql
from lxml import etree
ssl._create_default_https_context = ssl._create_unverified_context

class PythonSugar():
def __init__(self):
# 爬取分类修改修改：商品列表地址、商品详情地址、存储的商品分类id=11347
self.url =  'https://gatewx.dmall.com/customersite/searchWareByCategory?param={"pageNum":1,"pageSize":41,"venderId":"1","storeId":"108","sort":"1","categoryId":10905,"categoryLevel":3,"cateSource":1,"bizType":"1"}&token=&source=2&tempid=C7B357489E400002B1514BD01B00E270&pubParam={"utmSource":"wxmp"}&_=1512268447989'
self.headers = {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:56.0)'}
self.detailurl = 'https://i.dmall.com/?source_id=wxmp#item/view/item/item:id=1-108-'
# if page == 1:
self.get_connect()

def get_connect(self):

self.tablename = 'duodian'
self.db = pymysql.connect(host='127.0.0.1', user='root', passwd='', db='test', charset='utf8')
self.cur = self.db.cursor()
self.cur.execute('USE test')
try:
# 创建表
self.cur.execute(
'CREATE TABLE ' + self.tablename + ' (id BIGINT(7) NOT NULL AUTO_INCREMENT, title VARCHAR(1000), img VARCHAR(1000), lunfanimg VARCHAR(1000), spec VARCHAR(1000), xcimg VARCHAR(1000), skuid VARCHAR(1000),pimg VARCHAR(1000), plunfanimg VARCHAR(1000),pxcimg VARCHAR(1000) ,categoryid VARCHAR(1000),price VARCHAR(1000),brandname VARCHAR(1000),categoryname VARCHAR(1000),created TIMESTAMP DEFAULT CURRENT_TIMESTAMP, PRIMARY KEY(id))')
except pymysql.err.InternalError as e:
print(e)
# 修改表字段
self.cur.execute('ALTER DATABASE test CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE title title VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE img img VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE lunfanimg lunfanimg VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE spec spec VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE xcimg xcimg VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE skuid skuid VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
# 存储本地
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE pimg pimg VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE plunfanimg plunfanimg VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE pxcimg pxcimg VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE categoryid categoryid VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE price price VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE brandname brandname VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE categoryname categoryname VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')

def get_html(self):
req = request.Request(self.url,headers=self.headers)
response = request.urlopen(req)
html = response.read()
return html

def get_mkdir(self):
jsonobj = json.loads(self.get_html().decode('utf-8'))
# 列表页 - 图片
imgList = jsonpath.jsonpath(jsonobj, '$..img')
# 列表页 - 价格
pricelist = jsonpath.jsonpath(jsonobj, '$..price')
# 列表页 - 商品名
titleList = jsonpath.jsonpath(jsonobj, '$..title')
# 列表页 - 商品id -- skuId
skuIdList = jsonpath.jsonpath(jsonobj, '$..promotionInfo.skuId')
# 商品价格
priceList = jsonpath.jsonpath(jsonobj, '$..price')
# 商品品牌
brandList = jsonpath.jsonpath(jsonobj, '$..brandName')
# 商品分类
categoryList = jsonpath.jsonpath(jsonobj, '$..thirdCatName')
listdata = zip(titleList, imgList, pricelist,skuIdList,priceList,brandList,categoryList)

for item in listdata:

print(item)

# 替换'/'
import re
strinfo = re.compile('/')
itemdir = strinfo.sub('-', item[0])
print(itemdir)
time.sleep(1)
# 商品名称目录
if not os.path.exists(itemdir):
os.makedirs(itemdir)
else:
print(itemdir + ' -- 目录已存在！')
self.dataurl = ''
# 存储本地主页图片链接地址
self.pimg = ''
# 列表页 - 图片

# 文件夹和文件命名不能出现这9个字符：/ \ : * " < > | ？

if os.path.exists( itemdir + '/' + item[1][-20:].replace('/','-').replace('\\','-').replace(':','-').replace('*','-').replace('"','-').replace('<','-').replace('>','-').replace('|','-').replace('?','-') + '.webp'):
print('文件已存在！')
# return 0
else:

if item[1].startswith('//'):
self.dataurl = "http:" + item[1]
else:
self.dataurl = item[1]
try:
req = request.Request(self.dataurl, headers=self.headers)
reponse = request.urlopen(req)
get_img = reponse.read()
self.pimg = '/pimgs/' + itemdir + '/' + self.dataurl[-20:].replace('/','-').replace('\\','-').replace(':','-').replace('*','-').replace('"','-').replace('<','-').replace('>','-').replace('|','-').replace('?','-') + '.webp'
with open( itemdir + '/' + self.dataurl[-20:].replace('/','-').replace('\\','-').replace(':','-').replace('*','-').replace('"','-').replace('<','-').replace('>','-').replace('|','-').replace('?','-') + '.webp', 'wb') as fp:
fp.write(get_img)
except Exception as e:
print(e)
# 详情目录
if not os.path.exists(itemdir  + '/详情'):
os.makedirs(itemdir  + '/详情')
else:
print('详情' + ' -- 目录已存在！')
driver = webdriver.PhantomJS(executable_path='./phantomjs-2.1.1-macosx/bin/phantomjs')
time.sleep(5)
driver.get(self.detailurl + str(item[3]))
time.sleep(5)
driver.find_element_by_class_name('tipinfo').click()
time.sleep(5)
html = etree.HTML(driver.page_source)
imglist = html.xpath('//img/@src')
print(self.detailurl + str(item[3]))
# 轮番图
lunfantu = html.xpath('//img[@class="detail-img"]/@src')
# 猜你喜欢
# like = html.xpath('//img[@class="J_ItemImage recommend-img"]/@src')
# 商品宣传图
xuanchuan = html.xpath('//div[@class="J_descriptionDetail parameter"]//img/@src')
# 规格
# 左边的参数名
leftspec = html.xpath('//div[@class="left attr_key border-1px border-r border-b"]/text()')
# 右边的参数值
rightspec = html.xpath('//div[@class="left attr_value border-1px border-b"]/span/text()')
spec = zip(leftspec,rightspec)
# time.sleep(5)
# print(driver.page_source)
print(str(item[3]))
print("-------------------------- 轮播图 --------------------------------")
print(lunfantu)
print("--------------------------- 规格 ---------------------------------")
print(spec)
print("-------------------------- 介绍图 ---------------------------------")
print(xuanchuan)
print("-------------------------- 主页图 ---------------------------------")
print(self.dataurl)

for simple in imglist:
if not os.path.exists( itemdir + '/详情/' + simple[-20:].replace('/','-').replace('\\','-').replace(':','-').replace('*','-').replace('"','-').replace('<','-').replace('>','-').replace('|','-').replace('?','-') + '.webp'):
request.urlretrieve(simple, itemdir +  '/详情' + '/' + simple[-20:].replace('/','-').replace('\\','-').replace(':','-').replace('*','-').replace('"','-').replace('<','-').replace('>','-').replace('|','-').replace('?','-') + ".webp")
print("正在下载......")
else:
print('文件已存在！')

#     NOT
#     NULL
#     AUTO_INCREMENT, title
#     VARCHAR(1000), img
#     VARCHAR(1000), lunfanimg
#     VARCHAR(1000), spec
#     VARCHAR(1000), xcimg
#     VARCHAR(1000),
# 插入数据库l
# 判断数据库是否有skuId，有就不插入，无则插入

result = self.cur.execute("select skuid from duodian WHERE skuid=" + str(item[3]))
print(str(result) + '-----------------------')


if result:
print("数据库里面存在此数据")
else:
# 不存在，存数据
lunfantu1 = {}
specpagram ={}
xuanchuan1 = {}
# 轮番图
for index1, item1 in enumerate(lunfantu):
lunfantu1[index1] = item1
# 规格
speckey = 0
for itemspec in spec:
specvalue = str(itemspec[0]) + '-' + str(itemspec[1])
specpagram[str(speckey)] = specvalue
speckey += 1
# 介绍图
for index3, item3 in enumerate(xuanchuan):
xuanchuan1[index3] = item3
# 存储本地图片链接地址
plunfantu = {}
pxuanchuan = {}
for pindex1, pitem1 in enumerate(lunfantu):
plunfantu[pindex1] = '/pimgs/' + itemdir + '/详情/' + pitem1[-20:].replace('/','-').replace('\\','-').replace(':','-').replace('*','-').replace('"','-').replace('<','-').replace('>','-').replace('|','-').replace('?','-') + '.webp'
for pindex2, pitem2 in enumerate(xuanchuan):
pxuanchuan[pindex2] = '/pimgs/' + itemdir + '/详情/' + pitem2[-20:].replace('/','-').replace('\\','-').replace(':','-').replace('*','-').replace('"','-').replace('<','-').replace('>','-').replace('|','-').replace('?','-') + '.webp'
self.cur.execute(
'INSERT INTO ' + self.tablename + ' (title, img, lunfanimg, spec, xcimg,skuid,pimg, plunfanimg, pxcimg,categoryid,price,brandname,categoryname) VALUES (%s, %s, %s, %s, %s, %s, %s, %s, %s,%s, %s, %s,%s)',
(itemdir, self.dataurl, json.dumps(lunfantu1,ensure_ascii=False), json.dumps(specpagram,ensure_ascii=False), json.dumps(xuanchuan1,ensure_ascii=False),str(item[3]),self.pimg,json.dumps(plunfantu,ensure_ascii=False),json.dumps(pxuanchuan,ensure_ascii=False),'10905','%.2f'%(item[4]/100),str(item[5]),str(item[6])))
self.cur.connection.commit()
print("------------------------  插入成功  ----------------------------------")

if __name__ == "__main__":

# for page in range(1,3):
pythonSugar = PythonSugar()
pythonSugar.get_mkdir()
print(" -- 爬取完毕 -- ")
```
七、表结构设计
表结构中字段的设计是我在代码中自动生成的，如果某个字段不符合我们的需求，可以任意修改代码中药修改的字段即可，运行程序就能修改成功，无须在mysql数据库中手动操作，主要用到了游标对象，这样设计表结构，简单快捷，设计如下：

```
# 修改表字段
self.cur.execute('ALTER DATABASE test CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE title title VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE img img VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE lunfanimg lunfanimg VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE spec spec VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE xcimg xcimg VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE skuid skuid VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
# 存储本地
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE pimg pimg VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE plunfanimg plunfanimg VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE pxcimg pxcimg VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE categoryid categoryid VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE price price VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE brandname brandname VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
self.cur.execute(
'ALTER TABLE ' + self.tablename + ' CHANGE categoryname categoryname VARCHAR(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci')
```
数据表结构展示图：
![表结构.png](http://upload-images.jianshu.io/upload_images/3276082-77dc2c1e256ead79.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
八、申明
到此为止，`多点商城`就爬取完毕了，爬取商品信息我看了看10多G，真是一次不小的收获呀，小伙伴们如果有不懂的地方可以私信我哦。有好多小伙伴私信我，为什么不建一个学习群那，我说那好吧，今天就创建了一个微信学习群，希望小伙伴们多多宣传哦，后期会有更多更深入的Python文章分享。
![微信群.jpeg](http://upload-images.jianshu.io/upload_images/3276082-647cb23f3c6c090d.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

爬取整站商品申明：如果侵犯了某公司权益，请及时告诉我，我会马上删除爬取的整站的商品信息。本次分享的文章主要是学习所用，不作为商业使用，共同学习。
源码请链接到[爬取多点商城整站商品](https://github.com/lb2281075105/LBDuoDian)
