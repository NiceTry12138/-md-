---
title: 骚鸡儿的 Python
date: 2019-1-30 18:39:24
tags: 

---



# Github上关注的库，定时检查是否更新



```python
import requests
import time
import webbrowser

api_url = 'https://api.github.com/repos/usuiforhe/2048'
visit_url = 'https://github.com/usuiforhe/2048'

last_time = '2019-01-10T15:44:05Z' # 初始化时间

headher = {
    'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36'
}

while(True):
    data = requests.get(api_url, headers=headher).json() # 请求数据

    new_time = data['updated_at'] # 获取当前时间

    if new_time > last_time:
        last_time = new_time # 更新时间
        webbrowser.open(visit_url) # 之后打开浏览器

    time.sleep(3600) # 休息事件 3600s， 也就是说每一小时请求一次

```



# 关注领域的库有更新？发送提醒到手机？

