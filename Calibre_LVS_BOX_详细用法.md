[回到目录](../README.md)  
LVS BOX的使用对于后端的团队协作起到非常便利的作用。  
通过在lvs rules file添加BOX的相关语句可以达到这个目的，但也可以通过配置LVS Options等来更加灵活的使用。  
依照不同的实际情况，主要有下面三种对应的数据匹配方法。  

# 1、匹配版图和电路同名。  

例如下面的buf包含两个inv单元：  
 ![](https://upload-images.jianshu.io/upload_images/1319303-59aa644db13a5696.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

对应的buf版图，inv单元版图只预留PIN：  
 ![](https://upload-images.jianshu.io/upload_images/1319303-3c5c5ced84b6be9c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

勾选Calibre LVS中的LVS Options选项。  
 ![](https://upload-images.jianshu.io/upload_images/1319303-0121322857b19a11.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后在LVS Options→include中勾选Include Rule Statements，并输入：  

```
LVS BOX inv
```

 ![](https://upload-images.jianshu.io/upload_images/1319303-49955d7f9b33e9f0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Run LVS结果会有BOX单元提示。  
 ![](https://upload-images.jianshu.io/upload_images/1319303-26d898a26e35aba2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


# 2、匹配版图和电路不同名。  

例如如版图的名称是```inv_box```，但电路依然为```inv```，这种情况需要使用到H-cells。  
首先需要创建一个hcell文件，按照格式：```[版图名]``` ```[空格]``` ```[电路名]```的格式输入信息。  
![](https://upload-images.jianshu.io/upload_images/1319303-84033e69285dea03.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后在Inputs→H-Cells中勾选Use H-Cells file，并选择上述的hcell文件。  
![](https://upload-images.jianshu.io/upload_images/1319303-49f907b35872f220.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

同时也需要修改LVS Options→include→Include Rule Statements信息。  
![](https://upload-images.jianshu.io/upload_images/1319303-c544f48ffbf2b12c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

最后Run LVS。  


# 3、匹配多个不同名的版图和同一个电路。  

同一个inv可能由于版图的形状不同等原因存在不同名的单元，假设电路```inv```，版图有```inv_box```和```inv_ip```。  

在上一种情况的基础上修改hcell文件。  

```
inv_box inv
inv_ip inv
```

![](https://upload-images.jianshu.io/upload_images/1319303-45f66fee4bb13a74.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

修改LVS Options→include→Include Rule Statements信息。  
![](https://upload-images.jianshu.io/upload_images/1319303-86002f9d0566f078.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 

最后Run LVS。  

[回到目录](../README.md)  
