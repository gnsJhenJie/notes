今天發生了好多地震，想用Python來查地震報告嗎? 中央氣象局提供了Open API的平台，讓大家可以輕鬆地透過API抓取各類氣象資料，當然地震報告也包括在內， 那我們現在就來看看如何透過Python抓取地震資料吧！
## 註冊氣象資料開放平臺會員
先到[https://opendata.cwb.gov.tw/userLogin](https://opendata.cwb.gov.tw/userLogin) 註冊會員(Facebook登入目前無法使用)，接著到[API授權碼](https://opendata.cwb.gov.tw/user/authkey)頁面產生並記下屬於自己的授權碼(**API授權碼不要讓別人知道喔**)
<img width="1486" alt="Screen Shot 2022-03-23 at 14 45 39" src="https://user-images.githubusercontent.com/32983347/159639374-5f2e2835-fbb1-4e50-8be8-358259b2317f.png">
有了授權碼後就可以使用氣象局提供的各個API了。
## 找尋適合的API
接著需要到[說明文件](https://opendata.cwb.gov.tw/dist/opendata-swagger.html#/)尋找適合使用的API，經過一番尋找後...看起來這支API就是我們要的了。  
<img width="1486" alt="Screen Shot 2022-03-23 at 14 50 24" src="https://user-images.githubusercontent.com/32983347/159640087-71774e9d-13fa-41ce-b866-0d5efb2cdd19.png">

可以先在[說明文件](https://opendata.cwb.gov.tw/dist/opendata-swagger.html#/%E5%9C%B0%E9%9C%87%E6%B5%B7%E5%98%AF/get_v1_rest_datastore_E_A0015_001)的網頁試試看這支API會回傳的資料內容
<img width="1486" alt="Screen Shot 2022-03-23 at 14 51 47" src="https://user-images.githubusercontent.com/32983347/159640282-7b269681-9353-473b-a017-7fcdc43638b5.png">

## 透過Python抓取API資料
接著就是透過Python 來取得API的資料啦~ 程式如下，大家可以自己更改內容取得不同的資料！
```python
import requests
import json
token = "CWB-E96B2DF1-95E9-42E7-978D-99154DD54E22" # 換成自己的API授權碼
limit = 20 # 取得最近20筆地震報告
req = requests.get(
    f"https://opendata.cwb.gov.tw/api/v1/rest/datastore/E-A0015-001?Authorization={token}&limit={limit}") # API的接入點
data = json.loads(req.text)
earthquakes = data["records"]["earthquake"]
for earthquake in earthquakes:
    print("地震編號:", earthquake["earthquakeNo"])
    for area in earthquake["intensity"]["shakingArea"]:
        print(area["areaName"], area["areaIntensity"]
              ["value"], area["areaIntensity"]["unit"])
```
Output:
<img width="513" alt="Screen Shot 2022-03-23 at 14 57 03" src="https://user-images.githubusercontent.com/32983347/159641046-a2ce4653-0690-4ecd-9ff3-8c6f9d670dc8.png">

