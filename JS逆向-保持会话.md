```python
'''
第六题
'''

import execjs
import requests

# 建立一个会话
session = requests.session()
# 忽略警告
requests.packages.urllib3.disable_warnings()

def conversion(head):
    items = [item.split(': ') for item in head.split('\n')]
    header = {}
    for item in items:
        header.update({item[0]: item[1]})
    return header


page_header = '''Host: www.python-spider.com
Connection: keep-alive
Cache-Control: max-age=0
sec-ch-ua: " Not A;Brand";v="99", "Chromium";v="98", "Google Chrome";v="98"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9'''

# 总和
sum_numbers = 0

# 100页数据
for page in range(1, 101):
    session.headers = conversion(page_header)
    data = {'page': page}
    page_url = f'https://www.python-spider.com/api/challenge6'
    if page == 1:
        session.get(url=page_url, verify=False)
    response = session.post(url=page_url, verify=False, data=data)
    session.headers.update({'Cookie': 'Hm_lvt_337e99a01a907a08d00bed4a1a52e35d=1646145435; Hm_lpvt_337e99a01a907a08d00bed4a1a52e35d=1646145453;sign='+response.cookies.items()[0][0]+';sessionid='+response.cookies.items()[0][1]})
    print(f'第{page}页的数据：{response.json().get("data")}')
    for value in response.json().get('data'):
        sum_numbers += int(value.get('value'))
print(sum_numbers)


'''

'''
```





```html
<script src="https://lib.sinaapp.com/js/jquery/2.0.2/jquery-2.0.2.min.js"></script>【爱锭云盾V1.0】您的IP处于异常状态，导致您的IP已被暂时封禁，<span id="a">3566</span>秒后解封
<script>
    b=function(){
        a=$('#a').text();
        $('#a').text(a-1);
        if(a-1<=0){
            location.reload()
        }
    };
    setInterval('b()',1000);</script>
```

