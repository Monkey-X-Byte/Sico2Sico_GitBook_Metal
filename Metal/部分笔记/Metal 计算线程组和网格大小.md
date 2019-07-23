# 计算线程组和网格大小

您可以根据两个属性计算每个线程组的线程数。一个属性是（可以在单个线程组中的最大线程数）。另一个是（计划在GPU上并行执行的线程数）。[`MTLComputePipelineState`](https://developer.apple.com/documentation/metal/mtlcomputepipelinestate)[`maxTotalThreadsPerThreadgroup`](https://developer.apple.com/documentation/metal/mtlcomputepipelinestate/1414927-maxtotalthreadsperthreadgroup)[`threadExecutionWidth`](https://developer.apple.com/documentation/metal/mtlcomputepipelinestate/1414911-threadexecutionwidth)

该属性取决于设备，计算内核的寄存器使用情况以及线程组内存使用情况。在创建计算管道状态后，其值不会更改，但同一设备上的两个管道状态可能会返回不同的值。`maxTotalThreadsPerThreadgroup``maxTotalThreadsPerThreadgroup`

每个线程组的线程数不能超过。在值为512和a 为32的设备上，每个线程组的合适线程数为32（线程执行宽度）x 16（每个线程组的总线程数除以线程执行宽度）。[清单1](https://developer.apple.com/documentation/metal/calculating_threadgroup_and_grid_sizes#2922042)显示了根据线程执行宽度和每个线程组的最大线程定义线程组维度的示例。`maxTotalThreadsPerThreadgroup``maxTotalThreadsPerThreadgroup``threadExecutionWidth`

清单1

 

计算每个线程组的线程数。

```
let w = pipelineState.threadExecutionWidth
let h = pipelineState.maxTotalThreadsPerThreadgroup / w
let threadsPerThreadgroup = MTLSizeMake(w, h, 1) 
```

在支持非均匀线程组大小的设备上，Metal能够计算网格（在本例中为图像或纹理）如何最佳地划分为非均匀，任意大小的线程组。compute命令编码器的方法需要线程的总数 - 每个线程负责一个像素 - 以及[清单1中](https://developer.apple.com/documentation/metal/calculating_threadgroup_and_grid_sizes#2922042)计算的值，如以下示例所示：[`dispatchThreads(_:threadsPerThreadgroup:)`](https://developer.apple.com/documentation/metal/mtlcomputecommandencoder/2866532-dispatchthreads)`threadsPerThreadgroup`

```
let threadsPerGrid = MTLSize(width: texture.width,
                             height: texture.height,
                             depth: 1)
        
computeCommandEncoder.dispatchThreads(threadsPerGrid,
                                      threadsPerThreadgroup: threadsPerThreadgroup)
```

当Metal执行此计算时，它可以沿网格边缘生成较小的线程组，如下所示。与统一线程组相比，此技术简化了内核代码并提高了GPU性能。

要确定设备是否支持非均匀线程组，请参阅“ [金属特征集表”。](https://developer.apple.com/metal/Metal-Feature-Set-Tables.pdf)

![非均匀线程组。](https://docs-assets.developer.apple.com/published/60fff83501/c8d2ae2f-3bb7-4621-8c1e-6d5e2143d424.png)



### 计算每个网格的线程组

如果需要精确控制线程组的大小和数量，可以手动计算网格的划分方式。在您的代码中，确保有足够的线程组来覆盖整个图像。这是一个例子：

```
let threadgroupsPerGrid = MTLSize(width: (texture.width + w - 1) / w,
                                  height: (texture.height + h - 1) / h,
                                  depth: 1)
```

给定1024 x 768的纹理，上面的代码返回一个[`MTLSize`](https://developer.apple.com/documentation/metal/mtlsize)32 x 48 x 1 的对象，这意味着纹理被分成1536个线程组，每个线程组包含512个线程，总共786,432个线程。在这种情况下，该数字与图像中的像素数匹配，并且处理整个图像时没有未充分利用的线程。但是，情况可能并非总是如此（例如，对于1920 x 1080的图像尺寸）。此代码通过四舍五入，确保有足够的线程来处理整个图像。

使用这种方法，线程组生成的网格可能比您的数据大。因此，如果网格中的线程位置超出数据范围，则代码应该提前退出。下图显示了一组4 x 4线程组如何在网格的边界上扩展，从而导致线程利用不足：

![统一线程组导致未充分利用的线程。](https://docs-assets.developer.apple.com/published/60fff83501/d0a263a8-19f7-4708-9ad4-48efb90ae541.png)

[清单4](https://developer.apple.com/documentation/metal/calculating_threadgroup_and_grid_sizes#2922050)显示了一个简单的内核，它将不透明的白色写入每个像素。它首先将线程位置与纹理边界进行比较，如果位置超出纹理范围，则返回。`outputTexture`

清单4

越界越界越界越界。

```swift
kernel void
simpleKernelFunction(texture2d<float, access::write> outputTexture [[texture(0)]],
                     uint2 position [[thread_position_in_grid]]) {
    
    if (position.x >= outputTexture.get_width() || position.y >= outputTexture.get_height()) {
        return;
    }
    
    outputTexture.write(float4(1.0), position);
}
```

