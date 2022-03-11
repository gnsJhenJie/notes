DNS over Https是一種查詢DNS的方式，相較於傳統以明文(UDP)查詢的方式更能保護使用者上網時的隱私。
## 什麼是DNS查詢 (DNS Query)
**DNS** (Domain Name System) 可以將使人們易讀易記的網域名稱(例如: www.ncu.edu.tw) 轉換為機器需要的IP位址(例如: 140.115.17.82)，因此你可以透過facebook.com, google.com這樣的網址上網其實都是DNS的功勞，而在做這樣的轉換則需透過DNS Server (DNS Resolver)來完成。
## 傳統DNS查詢技術 - DNS over UDP
目前DNS的查詢大部分都是透過 UDP來查詢的，像是你在Windows控制台設定的 DNS server就是透過 UDP查詢的
<img width="300" src="https://user-images.githubusercontent.com/32983347/157655454-7543a86c-dac1-4711-ad5d-8a26941a06f8.png"/>  
你也可能聽過以下提供 DNS over UDP的 DNS Server：

- [Google Public DNS](https://developers.google.com/speed/public-dns/): 8.8.8.8
- [Cloudflare](https://1.1.1.1/): 1.1.1.1
- [Quad9](https://www.quad9.net/): 9.9.9.9
- [Hinet DNS](https://domain.hinet.net/): 168.95.1.1
- [中央大學電算中心DNS](https://www.cc.ncu.edu.tw/page/dns): 140.115.1.31 (**有使用宿網的一定設定過這個IP吧**)

透過UDP來做DNS查詢方式事實上是存在隱私問題的，除了查詢的 DNS Server可以知道你上過哪些網站外，因為 UDP使用明文傳輸的特性，網路傳輸過程中的路由器、ISP甚至是有心人士也都可以監視你的 DNS查詢。  
<img width="600" src="https://cf-assets.www.cloudflare.com/slt3lc6tev37/5Cgzkxb8COyIZ9evqqGFyF/384df7ee28643474080bbcd564fc3cfa/dns-traffic-unsecured.svg"/>

> (圖片來源：[Cloudflare](https://www.cloudflare.com/zh-cn/learning/dns/dns-over-tls/))

## DNS over Https (DoH)
DNS over Https 是一個安全性較高的DNS查詢方法，透過以https的方式查詢DNS紀錄，其傳輸過程經過加密，使網路傳輸過程的中間者無法窺探DNS查詢的內容，而且其會隱藏在一般https流量中，減弱了ISP等網路業者的可見性，更能增加使用者隱私。  
<img width="600" src="https://cf-assets.www.cloudflare.com/slt3lc6tev37/7qcyOJwWyOt4EVJykiIRTn/30e34453409eb42fa1ec36680609ad8d/dns-traffic-over-tls-https.svg"/>
> (圖片來源：[Cloudflare](https://www.cloudflare.com/zh-cn/learning/dns/dns-over-tls/))

  
目前macOS可透過描述檔的方式設定DNS over Https，可參考[Apple Developer Documentation](https://developer.apple.com/documentation/devicemanagement/dnssettings)，而Windows作業系統本身僅支援特定幾家DNS over Https廠商，無法任意選擇，設定方法可參考[How to enable DNS over Https](https://www.howtogeek.com/765940/how-to-enable-dns-over-https-on-windows-11/)
以下是幾個較知名的DNS over Https Server：
- [Cloudflare](https://1.1.1.1/dns/): https://chrome.cloudflare-dns.com/dns-query
- [Google](https://dns.google/): https://dns.google/dns-query{?dns}
- [OpenDNS (Cisco)](https://www.opendns.com/): https://doh.opendns.com/dns-query{?dns}

## 以Python實作DNS over Https查詢
因為是透過Https查詢，因此DNS over Https在Python上相當容易實作，
```python
from pprint import pprint
import requests
server_url = "https://dns.google/resolve"
client = requests.session()
query = {
    'name': 'ncu.edu.tw',
    'type': 'A',
}

res = client.get(server_url, params=query)
print(res.status_code)
pprint(res.json())
```
<img width="529" alt="Screen Shot 2022-03-11 at 22 54 15" src="https://user-images.githubusercontent.com/32983347/157891357-1b967ede-9a11-4fa6-9bc4-0412ba13bab0.png">  

而透過較底層方法的DNS over UDP 因為在Python實作上較複雜，所以這邊就不寫了，可以參考 [dnspython](https://dnspython.readthedocs.io/en/stable/query.html#udp)  
