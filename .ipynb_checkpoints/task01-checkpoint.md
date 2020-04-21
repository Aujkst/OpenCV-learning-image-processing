# Algorithm: Interpolation

## Nearest Neighbor Interpolation

- Use the value of nearest point
- Piecewise-constant function

## Bilinear Interpolation

**Linear Interpolation ==> Bilinear Interpolation**

&emsp;The block uses the weighted average of two translated pixel values for each output pixel value.

&emsp;Although each step is **linear** in the sampled values and in the position, the interpolation as a whole is not linear but rather **quadratic** in the sample location.

$$
\left\{
\begin{array}{ccccc}
f(x, 0) & = & f(0,0) & + & \big[f(1,0)-f(0,0)\big] x\\
f(x, 1) & = & f(0,1) & + & \big[f(1,1)-f(0,1)\big] x\\
f(x, y) & = & f(x,0) & + & \big[f(x,1)-f(x,0)\big] y
\end{array}
\right.
$$

$$
\Longrightarrow f(x, y)=a x+b y+c x y+d
$$


## Bicubic Interpolation

**cubic Interpolation ==> bicubic Interpolation**

# Example: Interpolation


```python
import cv2
```

- `cv.INTER_NEAREST`: Nearest Neighbor
- `cv.INTER_LINEAR`: Bilinear
- `cv.INTER_CUBIC`:	Bicubic
- `cv.INTER_AREA`: Resampling Using Pixel Area Relation
- `cv.INTER_LANCZOS4`: Lanczos


```python
# cv2.IMREAD_UNCHANGED 用图片原来格式打开
img = cv2.imread('pla.jpg', cv2.IMREAD_UNCHANGED)
```


```python
# 图片原始尺寸
img.shape
```




    (1350, 1080, 3)




```python
# 设定缩放尺寸30%
scale_percent = 30
width = int(img.shape[1] * scale_percent / 100)
height = int(img.shape[0] * scale_percent / 100)
dim = (width, height)
dim
```




    (324, 405)




```python
# 变换
resized = cv2.resize(img, dim, interpolation = cv2.INTER_LINEAR)
```


```python
# 再按1.5倍放大
fx = 1.5
fy = 1.5

resized1 = cv2.resize(resized, dsize = None, 
                      fx = fx, fy = fy, 
                      interpolation = cv2.INTER_NEAREST)

resized2 = cv2.resize(resized, dsize = None, 
                      fx = fx, fy = fy, 
                      interpolation = cv2.INTER_LINEAR)
```


```python
cv2.imshow("resized", resized)
cv2.imshow("nearest method", resized1)
cv2.imshow("bilinear method", resized2)
cv2.waitKey(0)
cv2.destroyAllWindows()
```


```python

```
