- [一、爬虫的法律问题](#一爬虫的法律问题)
- [二、什么是robots协议](#二什么是robots协议)
- [三、爬虫的主要作用及其实现思路](#三爬虫的主要作用及其实现思路)
- [四、一个简单的爬虫案例](#四一个简单的爬虫案例)

# Python实现网络爬虫



## 一、爬虫的法律问题

- 严格遵守网站设置的robots协议
- 在规避反爬虫措施的同时，需要优化自己的代码，避免干扰被访问网站的正常运行；
- 在设置抓取策略时，应注意编码抓取视频、音乐等可能**构成作品的数据**，或者针对某些特定网站批量抓取其中的用户生成内容；
- 在使用、传播抓取到的信息时，应审查所抓取的内容，如发现属于用户的**个人信息**、隐私或者他人的**商业秘密**的，应及时停止并删除。
- 严禁抓取涉及个人**隐私的数据**公民的姓名、身份证件号码、通信通讯联系方式、住址、账号密 码、财产状况、行踪轨迹等个人信息

## 二、什么是robots协议

​		**robots协议也叫robots.txt（统一小写）**是一种存放于网站根目录下的ASCII编码的文本文件，它通常告诉网络搜索引擎的漫游器（又称网络蜘蛛），**此网站中的哪些内容是不应被搜索引擎的漫游器获取的**，哪些是可以被漫游器获取的。因为一些系统中的URL是大小写敏感的，所以robots.txt的文件名**应统一为小写**。

​		robots协议并不是一个规范，而只是约定俗成的，所以并不能保证网站的隐私。

**robots协议的主要写法：**

- User-agent：指定对哪些爬虫生效
- Disallow：指定要屏蔽的网址

以小米的官网为例 https://www.mi.com/robots.txt

```
# robots.txt for http://www.mi.com
# 2016/2/15

# *通配符指对所有的爬虫生效
User-agent: *

# 禁止带问号的页面以及问号前后的任何值
Disallow: /*?* 
# 禁止/后带问号的
Disallow: /?*
# 禁止带search_的Disallow: 
/search_* 
# 禁止带/item/
Disallow: /item/ 
# 禁止带/comment/
Disallow: /comment/ 
# 禁止带/accessories/
Disallow: /accessories/ 
# 禁止带/cart/
Disallow: /cart/ 
# 禁 止 带 /misc/ 
Disallow: /misc/
```

## 三、爬虫的主要作用及其实现思路

**爬虫实现的主要方式：**

- 实现方式一

![实现方式一](https://github.com/xujiangchen/Python/blob/main/notes/applicance/imgs/%E7%88%AC%E8%99%AB%E5%AE%9E%E7%8E%B0%E6%96%B9%E5%BC%8F%E4%B8%80.png)

- 实现方式二

![实现方式二](https://github.com/xujiangchen/Python/blob/main/notes/applicance/imgs/%E7%88%AC%E8%99%AB%E5%AE%9E%E7%8E%B0%E6%96%B9%E5%BC%8F%E4%BA%8C.png)

**实现爬虫所需要的五大组件：**

- 1、**爬虫调度器：**主要是配合调用其他四个模块，所谓调度就是取调用其他的模板

- 2、**URL管理器：**就是负责管理URL链接的，URL链接分为已经爬取的和未爬取的，这就需要URL 管理器来管理它们，同时它也为获取新URL链接提供接口

- 3、**HTML下载器：**就是将要爬取的页面的HTML下载下来

- 4、**HTML解析器：**就是将要爬取的数据从HTML源码中获取出来，同时也将新的URL链接发送给

  URL管理器以及将处理后的数据发送给数据存储器

- 5、**数据存储器：**就是将HTML下载器发送过来的数据存储到本地

![爬虫五大件](https://github.com/xujiangchen/Python/blob/main/notes/applicance/imgs/%E7%88%AC%E8%99%AB%E5%BF%85%E5%A4%87%E7%BB%84%E4%BB%B6.png)

## 四、一个简单的爬虫案例

为了防止触犯相关法律法规，我们自己搭建一个被爬网站

被爬网站使用一个github上面的开源电商网站代码： https://codeload.github.com/Keraun/xiaomi/zip/master ，代码的运行环境我们使用 HBuilder。

### 4.1 爬取策略

- 明确抓取的需求（爬取页面中所有商品的名称，介绍，价格）
- 仔细观察待抓取网页特点
- 拉取网站
- 提取数据

### 4.2 抓取数据

- 定义结果类

  ```python
  class product:
      """
      定义结果类，并且重写eq和hash两个方法，防止存储时存储相同的数据，增加代码负担
      """
  
      def __init__(self, name, desc, price):
          self.name = name
          self.desc = desc
          self.price = price
  
      def __eq__(self, o: object) -> bool:
          return self.name == o.name
  
      def __hash__(self) -> int:
          return hash(self.name)
  
      def __str__(self) -> str:
          return '产品名：%s 描述：%s 价格：%s' % (self.name, self.desc, self.price)
  ```

- 数据存储器

  ```python
  class DataStorage:
      """
      数据的存储器
      """
  
      def storage(self, products):
          """
          数据存储	为了方便直接打印提取的结果
          :param products:	set结构
          :return:
          """
          for i in products:
              print(i)
  
  ```

- html下载器

  ```python
  import requests
  
  
  class HtmlDownloader:
  
      def downloader(self, url):
          """
          根据给定的url下载网页
          :param url:
          :return: 下载好的文本
          """
          result = requests.get(url)
          return result.content.decode("utf-8")
  ```

- html的解析器

  ```python
  import re
  from spider import product
  
  
  class HtmlParser:
      item_pattern = r'<li class="brick-item">[\s\S]*?</li>'
      title_pattern = r'<h3 class="title"><a href="javascript:;">([\s\S]*?)</a></h3 > '
      desc_pattern = r'<p class="desc">([\s\S]*?)</p>'
      price_pattern = r'<span class="num">([\s\S]*?)</span>'
  
      def parser(self, html):
          """
          解析给定的html
          :param html:	html
          :return:	product set 
          """
          items = re.findall(self.item_pattern, html)
  
          result = set()
          for i in items:
              title = re.findall(self.title_pattern, i)
              desc = re.findall(self.desc_pattern, i)
              price = re.findall(self.price_pattern, i)
              result.add(product(title[0], desc[0], price[0]))
  
          return result
  
  ```

- URL管理器

  ```python
  class UrlManager:
      """
      URL的管理器
      """
  
      def __init__(self):
          # 使用set的原因是防止url重复，减少爬取次数
          self.new_urls = set()   # 用了存储未被爬取的地址
          self.old_urls = set()   # 用于存储已被爬取的地址
  
      def __get_new_url(self):
          """
          创建一个私有方法
          :return: 弹出一个未被爬取的地址
          """
          return self.new_urls.pop()
  
      def __add_new_url(self, url):
          """
          创建一个私有方法，添加未被爬取的地址
          """
          self.new_urls.add(url)
  
      def add_old_url(self, url):
          """
          添加已经爬取过的url
          :param url:	爬取过的url
          :return:
          """
          self.old_urls.add(url)
  ```

- 调度器

  ```python
  from spider.data_storage import DataStorage
  from spider.html_downloader import HtmlDownloader
  from spider.html_parser import HtmlParser
  from spider.url_manager import UrlManager
  
  
  class SpiderMain:
  
      def __init__(self):
          """
          初始化方法，主要是将其他组件实例化
          """
          self.url_manager = UrlManager()
          self.html_downloader = HtmlDownloader()
          self.html_parser = HtmlParser()
          self.data_storage = DataStorage()
  
      def start(self):
          """
          爬虫的主启动方法
          :return:
          """
          self.url_manager.add_new_url("http://127.0.0.1:8848/xiaomi-master/index.html")
          # 从url管理器里面获取url
          url = self.url_manager.get_new_url()  # 将获取到的url使用下载器进行下载
          html = self.html_downloader.download(url)  # 将html进行解析
          result = self.html_parser.parser(html)  # 数据存储
          self.data_storage.storage(result)
  
  
  if __name__ == "__main__":
      main = SpiderMain()
      main.start()
  
  ```

  