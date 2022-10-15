# 影像處理HW1 
# 透視變形校正 Perspective Distortion Correction

## STEP 1、讀取圖片
![](https://i.imgur.com/dTlG9BH.png)<br>
## STEP 2、用小畫家找4點像素座標
![](https://i.imgur.com/dhbxMoq.png)<br>
## STEP 3、計算out_img： width and height
直接用歐式距離取大值或平均，比例仍易變形，故套網路上程式<br>
![](https://i.imgur.com/NMmKWwu.png)<br>
![](https://i.imgur.com/kv1sMVF.jpg)<br>
![](https://i.imgur.com/fZOqzTS.png)<br>

依算出的width and height，得到原圖in_img 4點對應到out_img的4點對應座標。<br>

![](https://i.imgur.com/QqDJ9fC.jpg)<br>

## STEP4、解AX=b
A為out_img的4點座標代入得8個方程式，<br>
b為in_img的4點座標，<br>
利用 python 程式庫 解出a ~h 8個參數 X = solve(A,b)。<br>
因圖片是(row,col) 即 (y,x) 故先 y 後 x 去做計算<br>
![](https://i.imgur.com/FlZROWy.png)<br>
![](https://i.imgur.com/IH7u364.png)<br>
![](https://i.imgur.com/MT6jEvb.png)<br>
![](https://i.imgur.com/6Casp7e.jpg)<br>

得X (參數a~h)
![](https://i.imgur.com/ZYNPkFa.png)

## STEP5、Inverse mapping算出轉置後的圖於原圖的位置並進行雙線性插值
![](https://i.imgur.com/JFsjTDf.png)
### STEP5-1、轉置後的圖於原圖的位置
將A的四個點帶入Pseudo Affine公式 <br>
![](https://i.imgur.com/qEjnwdf.png)

X=row*x[0]+col*x[1]+row*col*x[2]+x[3] <br>
即 新X=原圖y*a+原圖x*b+原圖x*y*c+d <br>
Y=row*x[4]+col*x[5]+row*col*x[6]+x[7] <br>
即 新Y=原圖y*e+原圖x*f+原圖x*y*g+h <br>

### STEP5-2、進行雙線性插值
![](https://i.imgur.com/ffQxdr1.png)<br>
![](https://i.imgur.com/z5Rtorc.jpg)<br>
![](https://i.imgur.com/7NueNdE.jpg)<br>

### STEP6、結果：
![](https://i.imgur.com/Hg2yogd.png)<br>
