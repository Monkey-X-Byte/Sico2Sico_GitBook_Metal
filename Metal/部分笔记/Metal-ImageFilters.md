## ImageFilters

### 形态学图像滤波器

```
class MPSImageAreaMax
```

一种过滤器，用于查找以源图像中每个像素为中心的矩形区域中的最大像素值。

```
class MPSImageDilate
```

一种过滤器，用于查找以源图像中每个像素为中心的矩形区域中的最大像素值。

```
class MPSImageAreaMin
```

一种过滤器，用于查找以源图像中每个像素为中心的矩形区域中的最小像素值。

```
class MPSImageErode
```

一种过滤器，用于查找以源图像中每个像素为中心的矩形区域中的最小像素值。

### 卷积图像滤波器

```
class MPSImageConvolution
```

一个过滤器，用于将图像与具有奇数宽度和高度的给定内核进行卷积。

```
class MPSImageMedian
```

在中心区域中应用中值滤波器的滤波器，该中心区域以源图像中的每个像素为中心。

```
class MPSImageBox
```

一个过滤器，用于将图像与具有奇数宽度和高度的给定内核进行卷积。

```
class MPSImageTent
```

使用帐篷过滤器对图像进行卷积的过滤器。

```
class MPSImageGaussianBlur
```

一种滤镜，用于在x和y方向上对具有给定西格玛的高斯模糊的图像进行卷积。

```
class MPSImageGaussianPyramid
```

用高斯金字塔卷积图像的滤镜。

```
class MPSImageSobel
```

用Sobel运算符压缩图像的滤镜。

```
class MPSImageLaplacian
```

优化的拉普拉斯滤波器，易于使用。

```
class MPSImageLaplacianPyramid
```

使用拉普拉斯滤波器对图像进行卷积的滤镜。

```
class MPSImageLaplacianPyramidAdd
```

将图像与附加拉普拉斯金字塔卷积的滤镜。

```
class MPSImageLaplacianPyramidSubtract
```

将图像与减法拉普拉斯金字塔进行卷积的滤镜。

```
class MPSImagePyramid
```

用于创建不同类型金字塔图像的基类。

### 直方图图像滤镜

```
class MPSImageHistogram
```

用于计算图像直方图的过滤器。

```
class MPSImageHistogramEqualization
```

用于均衡图像直方图的滤镜。

```
class MPSImageHistogramSpecification
```

对图像执行直方图指定操作的过滤器。

### 图像阈值过滤器

```
class MPSImageThresholdBinary
```

一个过滤器，它为每个像素返回一个值大于指定阈值的指定值，否则返回0。

```
class MPSImageThresholdBinaryInverse
```

对于每个像素返回0的过滤器，其值大于指定阈值或否则为指定值。

```
class MPSImageThresholdToZero
```

一个过滤器，返回值大于指定阈值的每个像素的原始值，否则返回0。

```
class MPSImageThresholdToZeroInverse
```

对于每个像素返回0且值大于指定阈值的过滤器，否则返回原始值。

```
class MPSImageThresholdTruncate
```

将返回值钳制到较高指定值的过滤器。

### 图像积分滤波器

```
class MPSImageIntegral
```

一种过滤器，用于计算图像中指定区域的像素总和。

```
class MPSImageIntegralOfSquares
```

一种滤镜，用于计算图像中指定区域的像素平方和。

### 图像处理过滤器

```
class MPSImageConversion
```

用于执行颜色空间，Alpha或像素格式转换的过滤器。

```
class MPSImageScale
```

用于调整图像宽高比并调整其宽高比的滤镜。

```
class MPSImageLanczosScale
```

使用Lanczos重采样调整图像宽高比的滤镜。

```
class MPSImageBilinearScale
```

使用双线性重采样调整图像宽高比的滤镜。

```
class MPSImageTranspose
```

转置图像的过滤器。

### 图像统计过滤器

```
class MPSImageStatisticsMean
```

一个内核，用于计算图像给定区域的均值。

```
class MPSImageStatisticsMeanAndVariance
```

一个内核，用于计算图像给定区域的均值和方差。

```
class MPSImageStatisticsMinAndMax
```

一个内核，用于计算图像给定区域的最小和最大像素值。

### 图像缩小滤镜

```
class MPSImageReduceRowMax
```

一个过滤器，它返回图像中每行的最大值。

```
class MPSImageReduceRowMin
```

一个过滤器，它返回图像中每行的最小值。

```
class MPSImageReduceRowSum
```

一个过滤器，它返回图像中行的所有值的总和。

```
class MPSImageReduceRowMean
```

一个过滤器，返回图像中每行的平均值。

```
class MPSImageReduceColumnMax
```

一个过滤器，它返回图像中每列的最大值。

```
class MPSImageReduceColumnMin
```

一个过滤器，它返回图像中每列的最小值。

```
class MPSImageReduceColumnSum
```

一个过滤器，返回图像中列的所有值的总和。

```
class MPSImageReduceColumnMean
```

一个过滤器，返回图像中每列的平均值。

```
class MPSImageReduceUnary
```

缩减过滤器的基类，它将单个源作为输入。

### 图像算术滤波器

```
class MPSImageAdd
```

一个过滤器，返回其两个输入图像的元素和。

```
class MPSImageSubtract
```

一个过滤器，返回其两个输入图像的元素差异。

```
class MPSImageMultiply
```

一个过滤器，返回其两个输入图像的元素乘积。

```
class MPSImageDivide
```

一个过滤器，返回其两个输入图像的元素商。

```
class MPSImageArithmetic
```

基本算术节点的基类

### 欧氏距离变换滤波器

```
class MPSImageEuclideanDistanceTransform
```

对图像执行欧几里德距离变换的滤镜。

### 快速导向滤波器

```
class MPSImageGuidedFilter
```

用于对图像执行边缘感知过滤的过滤器。

### 关键点

```
class MPSImageFindKeypoints
```

用于查找关键点列表的内核。

```
struct MPSImageKeypointData
```

指定关键点信息的结构。

```
struct MPSImageKeypointRangeInfo
```

一种结构，指定用于查找图像中关键点的信息。

### 图像过滤器基类

```
class MPSUnaryImageKernel
```

一个消耗一个纹理并生成一个纹理的内核。

```
class MPSBinaryImageKernel
```

一个消耗两个纹理并生成一个纹理的内核。

### 常量

MPSRect No Clip

内核对象的默认剪切矩形。