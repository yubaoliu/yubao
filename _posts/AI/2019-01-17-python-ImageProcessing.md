---
layout: "post"
title: "Python OpenCV"
date: "2019-01-17 21:33"
---

# Image Processing

## Test Opencv
```python
import cv2
print('Hello Opencv')
```


## Image Resize
```python
import cv2
img = cv2.imread('../../Assets/Images/lena.jpg', 1)

imgInfo = img.shape
print(imgInfo)

height = imgInfo[0]
width = imgInfo[1]
mode = imgInfo[2]

#same Scale放大 縮小 等比例
dstHeight = int(height*0.5)
dstWidth = int(width*0.5)

# 插值：最近臨域插值， 雙線性插值 像素關系重採樣 立方插值
dst = cv2.resize(img, (dstWidth, dstHeight))

cv2.imshow('image', dst)

cv2.waitKey(0)
```



## Nearest Interpolation  最近臨域插值

Algorithm:

- src -> 10*20; dst -> 5*10
- dst <- src; (1,2 ) <- (2,4)
- newX = x*(src row/destination row) newX=1*(10/5)=2
- newY = y*(src column/destination column); newY = 2*(20/10)=4
- 10.3 -> 10

```python
import cv2
import numpy as np

img = cv2.imread('../../Assets/Images/lena.jpg', 1)

imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]

dstHeight = int(height/2)
dstWidth = int(width/2)

dstImage = np.zeros((dstHeight,dstWidth,3),np.uint8) # 0-255

for i in range(0, dstHeight): # row
    for j in range(0,dstWidth): # column
        iNew = int(i*(height*1.0/dstHeight))
        jNew = int(j*(width*1.0/dstWidth))
        dstImage[i,j] = img[iNew, jNew]

cv2.imshow('dst', dstImage)
cv2.waitKey(0)
```
Result:

![Nearest Interpolation Result](https://i.imgur.com/VxryVeX.png){#fig:}

## Bilinear Interpolation 雙線性插值

![雙線性插值](https://i.imgur.com/bUnimUD.png){#fig:}

- A1 = 20% * leftup + 80% * leftdown; (A2)
- B1 = 30% * leftup + 70% * rightup; (B2)
- newPoint = A1 * 30% + A2 * 70% OR newPoint = B1 * 20% + B2 *70%

## Image Crop

![crop task](https://i.imgur.com/x4m6cpQ.png){#fig:}

```python
# 100 -> 200 x
# 100 -> 300 y

import cv2

img = cv2.imread('../../Assets/Images/lena.jpg', 1)
dst = img[100:200, 100:300]
cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

![Image Crop Result](https://i.imgur.com/3Ip3fC3.png){#fig:}

## Image Shift

### API
- [1, 0, 100], [0, 1, 100]]) # Row: 2, column: 3
- => A: 2 * 2 and B: 2 * 1
- A: [ [1, 0], [0, 1] ]
- B: [[100], [200]]
- input: matrix C  (xy)
- ->
$$ A * C + B =   [[1 * x + 0*y ], [0 * x + 1 * y ]] + [[100], [200]]
\\
= [ [x + 100 ], [ y + 200]]
$$

```python
import cv2
import numpy as np
img = cv2.imread('../../Assets/Images/lena.jpg', 1)
cv2.imshow("src",img)
imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]
matShift = np.float32([[1, 0, 100], [0, 1, 100]]) # 2 3
dst = cv2.warpAffine(img, matShift, (height, width)) # p1: original data; p2: shift mat; p3: image info
cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

![Image Shift Result](https://i.imgur.com/tyeZzWM.png){#fig:}

### Pixel Level
Pixel (10, 20) -> (110, 120)

```python
import cv2
import numpy as np

img = cv2.imread('../../Assets/Images/lena.jpg', 1)

cv2.imshow("src",img)
imgInfo = img.shape

dst = np.zeros(img.shape, np.uint8)

height = imgInfo[0]
width = imgInfo[1]
for i in range (0, height):
    for j in range (0, width-100):
        dst[i, j+100] =img[i, j]

cv2.imshow('image', dst)
cv2.waitKey(0)
```

## Image Flip
```python
import cv2
import numpy as np

img = cv2.imread('../../Assets/Images/tree.jpg', 1)

cv2.imshow("src",img)
imgInfo = img.shape

height = imgInfo[0]
width = imgInfo[1]
deep = imgInfo[2]

newImgInfo = (height*2, width, deep)

dst = np.zeros(newImgInfo, np.uint8 )

for i in range(0, height):
    for j in range(0, width):
        dst[i,j] = img[i, j]
        # x y = 2*h - y -1
        dst[height*2-i-1, j] = img[i,j ]

for i in range(0, width):
    dst[height, i] = (0, 0, 255) #BGR

cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

![Flip tree](https://i.imgur.com/NvUBANH.png){#fig:}

## Image Scale
```python
import cv2
import numpy as np
img = cv2.imread('../../Assets/Images/lena.jpg', 1)
cv2.imshow("src",img)
imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]
matShift = np.float32([[0.5, 0, 0], [0, 0.5, 0]]) # 2 3
dst = cv2.warpAffine(img, matShift, (int(height/2), int(width/2) )) # p1: original data; p2: shift mat; p3: image info
cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

![Image Scaled](https://i.imgur.com/UUSuiF9.png){#fig:}


## Affine TransForm

```python
import cv2
import numpy as np
img = cv2.imread('../../Assets/Images/tree.jpg', 1)
cv2.imshow("src",img)
imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]
matSrc = np.float32([ [0, 0], [0, height-1], [width-1, 0] ])
matDst = np.float32( [[50, 50], [300, height-200], [width-300, 100] ])
matAffine = cv2.getAffineTransform(matSrc, matDst)
dst = cv2.warpAffine(img, matAffine, (width, height))
cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

![Affine TransForm Result](https://i.imgur.com/6dEXSyZ.png){#fig:}



# Reference
- [人工智能——机器视觉及图像识别](https://www.bilibili.com/video/av33208345/?p=1)
- [SoureCode-Github-me](https://github.com/yubaoliu/AI.git)
