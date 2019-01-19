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
- $[1, 0, 100], [0, 1, 100]])$ # Row: 2, column: 3
- => $A: 2 * 2 and B: 2 * 1$
- A: $[ [1, 0], [0, 1] ]$
- B: $[[100], [200]]$
- input: $matrix C  (xy)$
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

## Rotation

```python
import cv2
import numpy as np

img = cv2.imread('../../Assets/Images/lena.jpg', 1)

cv2.imshow("src", img)
imgInfo = img.shape

height = imgInfo[0]
width = imgInfo[1]

matRotate = cv2.getRotationMatrix2D((height*0.5, width*0.5), 45, 0.5)

dst = cv2.warpAffine(img, matRotate, (height, width))

cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

![Image Rotation](https://i.imgur.com/nVOq3bL.png){#fig:}


# Color Effect

## RGB2Gray

### Use imread

```python
import cv2
img0 = cv2.imread('../../Assets/Images/flower-white.jpeg', 1)
img1 = cv2.imread('../../Assets/Images/flower-white.jpeg', 0)
print(img0.shape)
print(img1.shape)
cv2.imshow('src', img1)
cv2.waitKey(0)
```

Result:

```sh
(238, 212, 3)
(238, 212)
```
![ImreadRGB2Gray](https://i.imgur.com/g9rsRN0.png){#fig:}

### Use cvtColor

```python
import cv2
img = cv2.imread('../../Assets/Images/flower-white.jpeg', 1)
print(img.shape)
dst = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
cv2.imshow('dst', dst)
cv2.waitKey(0)
```
### Pixel Convertion

```python
import cv2
import numpy as np
img = cv2.imread('../../Assets/Images/flower-white.jpeg', 1)
imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]
dst = np.zeros((height, width, 3), np.uint8)
for i in range(0, height):
    for j in range(0, width):
        (b, g, r) = img[i,j]
        gray = int(b)*0.114 +int(g)*0.587 + int(r)*0.299
        dst[i, j] = np.uint8(gray)
cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Optimization:

```python
# 浮点转定点进行优化.  '>>' is  better than '+- */'
b = int(b)
g = int(g)
r = int(r)
#gray = (r*1 + g*2 + b*1)/4
gray = (r+(g<<1)+b)>>2
```

## Color Invert
### Gray Image

```python
import cv2
import numpy as np
img = cv2.imread('../../Assets/Images/flower-white.jpeg', 1)

imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]

gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
dst = np.zeros((height, width, 1), np.uint8)

for i in range(0, height):
    for j in range(0, width):
        grayPixel = gray[i, j]
        dst[i, j] = 255 - grayPixel

cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

![colorInvert](https://i.imgur.com/F3B4GzV.png){#fig:}

### Color Image

```python
import cv2
import numpy as np

img = cv2.imread('../../Assets/Images/flower-white.jpeg', 1)

imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]

dst = np.zeros((height, width, 3), np.uint8)

for i in range(0, height):
    for j in range(0, width):
        (b, g, r) = img[i, j]
        dst[i, j] = (255 - b, 255-g, 255-r)

cv2.imshow('src', img)
cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

![Color Image Invert](https://i.imgur.com/um9IYBT.png){#fig:}

## Mosaic

```python
import cv2
import numpy as np

img = cv2.imread('../../Assets/Images/flower-white.jpeg', 1)

imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]


for m in range(50, 200):
    for n in range(50,100):
        # pixel -> 10 * 10
        if m%10 == 0 and n%10 ==0:
            for i in range(0, 10):
                for j in range(0,10):
                    (b, g, r) = img[m, n]
                    img[i+m, j+n] = (b, g, r)

cv2.imshow('img', img)
cv2.waitKey(0)
```

Result:

![Mosaic](https://i.imgur.com/5tmoLx2.png){#fig:}

## Frosted glass

```python
import cv2
import numpy as np
import random

img = cv2.imread('../../Assets/Images/flower0.jpeg', 1)

imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]

dst = np.zeros((height, width, 3), np.uint8)

mm = 8

for m in range(0, height - mm):
    for n in range(0, width - mm):
        index = int(random.random() * mm) # 0 - range
        (b,g,r) = img[m+index, n+index]
        dst[m, n] = (b, g, r)


cv2.imshow('img', img)
cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

![FrostedGlass](https://i.imgur.com/zPm2o5L.png){#fig:}


## Image Fusion

```python
import cv2
import numpy as np
import random

img0 = cv2.imread('../../Assets/Images/flower0.jpeg', 1)
img1 = cv2.imread('../../Assets/Images/dog.jpeg', 1)

imgInfo = img0.shape
height = imgInfo[0]
width = imgInfo[1]

# ROI
roiH = int(height-50)
roiW = int(width-50)

img0ROI = img0[0:roiH, 0:roiW]
img1ROI = img1[0:roiH, 0:roiW]


dst = np.zeros((roiH, roiW, 3), np.uint8)
dst = cv2.addWeighted(img0ROI, 0.5, img1ROI, 0.5, 0)

cv2.imshow('img0', img0)
cv2.imshow('img1', img1)
cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

![Image Fusion](https://i.imgur.com/CN4WpE6.png){#fig:}

## Canny Edge Detection

```python

import cv2
import numpy as np
import random

img = cv2.imread('../../Assets/Images/flower-white.jpeg', 1)

imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]

cv2.imshow('img', img)

gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

imgG = cv2.GaussianBlur(gray, (3, 3), 0)
dst = cv2.Canny(img, 50, 50)

cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

![Canny](https://i.imgur.com/6O98jEL.png){#fig:}

## Sobel Edge Detection

1. 算子模板

Verticle:

$$
\begin{bmatrix}
1 & 2 & 1 \\
0 & 0 &  0 \\
-1  & -2 & -1
\end{bmatrix}
$$

Horizental:

$$
\begin{bmatrix}
1 & 0 & -1  \\
2 & 0 & -2  \\
1 & 0 & -1
\end{bmatrix}
$$

2. 图片卷积
3. 计算梯度
3. 域值判别

```python

import cv2
import numpy as np
import math
import random

img = cv2.imread('../../Assets/Images/flower-white.jpeg', 1)

imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]

cv2.imshow('img', img)

gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

dst = np.zeros((height, width, 1), np.uint8)

for i in range(0, height-2):
    for j in range(0, width-2):
        gy = gray[i, j]*1 + gray[i, j+1]*2 + gray[i,j+2]*1 - gray[i+2, j]*1 - gray[i+2, j+1]*2 - gray[i+2, j+2]*1
        gx = gray[i, j]*1 - gray[i, j+2]*1 + gray[i+1, j]*2 - gray[i+1, j+2]*2 + gray[i+2, j]*1 - gray[i+2, j+2]*1
        grad = math.sqrt(gx*gx + gy*gy)
        if grad > 50:
            dst[i, j] = 255
        else:
            dst[i, j] = 0

cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

![Sobel Edge Detection](https://i.imgur.com/V9qmvtQ.png){#fig:}

## Embossing

```python

import cv2
import numpy as np

img = cv2.imread('../../Assets/Images/flower-white.jpeg', 1)

imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]

cv2.imshow('img', img)

gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# newPixel = gray0(First pixel) - gray1 (next pixel) + 150

dst = np.zeros((height, width, 1), np.uint8)

for i in range(0, height):
    for j in range(0, width-1):
        grayP0 = int(gray[i, j])
        grayP1 = int(gray[i, j+1])
        newP = grayP0 - grayP1 + 150
        if newP > 255:
            newP = 255
        if newP < 0:
            newP = 0
        dst[i, j] = newP


cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

![Embossing](https://i.imgur.com/QEEuWC6.png){#fig:}

## Color Style

```python

import cv2
import numpy as np

img = cv2.imread('../../Assets/Images/flower-white.jpeg', 1)

imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]

cv2.imshow('img', img)

dst = np.zeros((height, width, 3), np.uint8)

for i in range(0, height):
    for j in range(0, width):
        (b, g, r) = img[i, j]
        b = b * 1.5
        g = g * 1.3
        if b > 255:
            b = 255
        if g > 255:
            g = 255
        dst[i, j] = (b, g, r)

cv2.imshow('dst', dst)
cv2.waitKey(0)
```

Result:

More blue than before:

![ChangeColorStyle](https://i.imgur.com/z0rkcP0.png){#fig:}

## Oil painting effect

1. BGR to gray
1. Segment 7*7 10*10
2. Map: 0-255  <br>
  0-63, 64-127, ... <br>
Eg. 10 maps to 0-63
1. count the number of pixels in each bucket
2. dst = result (the average Value)


```python
import cv2
import numpy as np

img = cv2.imread('../../Assets/Images/dog.jpeg', 1)

imgInfo = img.shape
height = imgInfo[0]
width = imgInfo[1]

cv2.imshow('img', img)

gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

dst = np.zeros((height, width, 3), np.uint8)
for i in range(4, height-4):
    for j in range(4, width-4):
        array1 = np.zeros(8, np.uint8) # 8个灰度等级的像素个数
        for m in range(-4, 4):
            for n in range( -4, 4):
                p1 = int(gray[i+m, j+n]/32)
                array1[p1] = array1[p1]+1

        #计算哪个段所含像素最多
        currentMax = array1[0]
        l = 0 #当前处于哪个块中
        for k in range(0, 8):
            if currentMax < array1[k]:
                currentMax = array1[k]
                l = k

       #Here I added by my idea
        count = 0
        newB = 0
        newG = 0
        newR = 0
        for m in range(-4, 4):
            for n in range(-4, 4):
                if gray[i+m, j+n] >= (l*32) and gray[i+m, j+n] <= ( (l+1)*32):
                    (b, g, r) = img[i+m, j+n]
                    newB = newB + b
                    newG = newG + g
                    newR = newR + r
                    count = count + 1

        dst[i, j] = ( int(newB/count), int(newG/count), int(newR/count))

cv2.imshow('dst',dst)
cv2.waitKey(0)

```

Result:

![Oil Painting](https://i.imgur.com/dCtMzy7.png){#fig:}







# Reference
- [人工智能——机器视觉及图像识别](https://www.bilibili.com/video/av33208345/?p=1)
- [SoureCode-Github-me](https://github.com/yubaoliu/AI.git)
