1.  

   ```swift
   //创建一个新的纹理缓存，用于从影片帧的像素缓冲区创建纹理
   CVMetalTextureCacheCreate(kCFAllocatorDefault, nil, device, nil, &textureCache) 
   
   纹理缓存区的创建
   ```


2. 

   ```swift
   // CVMetalTextureCacheCreateTextureFromImage用于从a创建Metal纹理（CVMetalTexture）
   //         CVPixelBuffer（或更确切地说，来自支持CVPixelBuffer的IOSurface的纹理）。
   // 注意：调用CVMetalTextureCacheCreateTextureFromImage不会增加使用次数
   // IOSurface;只有CVPixelBuffer和CVMTLTexture拥有这个IOSurface。至少有两个
   // 必须保留，直到完成金属渲染。 MTLCommandBuffer完成处理程序很适合
   // 这个目的。
   
   CVMetalTextureCacheCreateTextureFromImage(kCFAllocatorDefault, metalTextureCache, pixelBuffer, nil, MTLPixelFormat.bgra8Unorm, width, height, 0, &texture)
   ```

3. 

   ```swift
   //IOSurface
   
   //跨多个进程共享硬件加速缓冲区数据（帧缓冲区和纹理）。更有效地管理图像内存。 高速内存访问区间
   Share hardware-accelerated buffer data (framebuffers and textures) across multiple processes. Manage image memory more efficiently.
   
   
   ```

4. 

   ```swift
   暂时的理解是 纹理和 缓存数据 进行了绑定 中间有一个高速拷贝内存区 IOSurface 供 GPU和CPU 访问
   ```


