# Requests库实例



## 实例1：京东商品页面的爬取

```python
import requests
url = "https://item.jd.com/2967929.html"
try:
    r = requests.get(url)
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.test[:1000])
except:
    print("爬取失败")
```



## 实例2：亚马逊商品页面的爬取

```python
import requests
url = "https://www.amazon.cn/gp/product/B01M8L5Z3Y"
try:
    kv = {'user-agent':'Mozilla/5.0'}
    r = requets.get(url, headers=kv)
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.test[1000:2000])
except:
    print("爬取失败")
```



## 实例3：百度/360搜索关键字提交

```python

```



## 实例4：网络图片的爬取和存储





## 实例5：IP地址归属地的自动查询

