因為最近在標記(label)訓練機器學習模型用的資料集，當中需要把影片的每個frame存成圖片，所以找到了透過Python來達成這件事的方法:

1. 安裝OpenCV (以前有安裝過的話這步就不用了)
`python3 -m pip install opencv-python`
2. 執行以下程式
(影片檔需命名為`video.mp4`並與程式碼放在同一個資料夾下)
```python
import cv2
vidcap = cv2.VideoCapture('video.mp4') # source video
success, image = vidcap.read()
while success:
    cv2.imwrite("frame_"+"{:06n}".format(count)+".PNG",
                image)     # save frame as PNG file
    success, image = vidcap.read()
```
3. 圖片檔就產生囉~
<img width="1431" alt="Screen Shot 2022-03-09 at 14 00 00" src="https://user-images.githubusercontent.com/32983347/157381636-55041796-e3a3-4ee3-80b9-dc5b8128c414.png">
 
原本約11MB的影片檔，竟然產生了約600MB的圖片檔，可見mp4的壓縮率真的很強！大家也可以試試看把code改成每幾個frame才存成圖片~
