# APP瘦身

## 资源瘦身

一般来说，APP资源过大主要是由于图片资源造成的。
而图片的优化也分为2个方面：

1. 由于快速迭代，项目中图片的引用可能已经不存在了，但是未被清理
2. 部分图片可能很大，没有很好的压缩就被使用。

### 废弃图片查找

首先要做的是把无用的Controller，View等删除，然后使用工具找出不用的资源文件。

使用一下工具来查找废弃图片：
* [LSUnusedResources](https://github.com/tinymind/LSUnusedResources)
* [FengNiao](https://github.com/onevcat/FengNiao)

根据结果，删除无用的图片。

### 资源压缩

#### 把容量大的png转webP

转换工具：[isparta](http://isparta.github.io/)
iOS webP解析库：[webP解析](https://github.com/carsonmcdonald/WebP-iOS-example)


#### 音频文件可以适度压缩

#### 简单的图片可以使用代码来编写实现


## 编译后的瘦身

### 无用类、代码清理

使用**APPCode**查找无用的源文件以及无用方法。

### 根据源代码字符查找相似的代码

> SameCodeFinder is a static code text scanner which can find the similar or the same code file in a big directory.

[SameCodeFinder](https://github.com/startry/SameCodeFinder)


