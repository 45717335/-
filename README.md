README
===========================
本文是初学Python者 使用 第三方库 将 交易数据(csv) 绘制成蜡烛图的一个示例.

****
xfgao@163.com	
****
## 目录
* [# 前提准备](#前提准备)
     1. 第三方库 pyecharts
* [# 效果展示](#效果展示)
* [# 代码](#代码)
* [# 下载](#下载)
* [# 打包可执行程序](#打包可执行程序)


## 前提准备

* 第三方库 pyecharts 
     这里使用的版本是: 0.1.9.4
     
    pip install pyecharts==0.1.9.4 -i http://pypi.douban.com/simple --trusted-host pypi.douban.com
    
    原始是这个三方库一直在升级,很多东西的调用方式,会随版本不同而发生变化.

## 效果展示


![蜡烛图](https://github.com/45717335/Python_Candle/blob/main/Python_candle1.gif "蜡烛图")


## 代码

```python
import csv
import os
import sys
import webbrowser
from pyecharts import Kline
if __name__ == '__main__':
    print(os.path.dirname(__file__))
    print(os.path.dirname(os.path.realpath(sys.executable)))
    s_input1=input("请输入包含 需要分析CSV的文件夹:")
    for root, dirs, files in os.walk(s_input1):
        for name in files:
            print(os.path.join(root, name))
            f=csv.reader(open(os.path.join(root, name),'r'))
            kline = Kline(name)
            ff = list(f)
            v1 = ff[60:1:-1]
            titblk = []
            vlu1 = []
            for x in v1:
                titblk.append(x[0])
                vlu1.append(x[1:5:1])
            kline.add(name, titblk, vlu1)
            kline.render("D:\\" + name + ".html")

            webbrowser.open_new_tab("D:\\" + name + ".html")
        break
    input("TOBEcontinue")
```



## 下载

[蜡烛图.zip](https://github.com/45717335/Python_Candle/blob/main/%E8%9C%A1%E7%83%9B%E5%9B%BE.zip "悬停显示")

## 打包可执行程序

     打包可执行程序后,会出现找不到 模板文件的问题,所以code里面的 两个 python程序做了一下两处修改: 
     在template.py    中的   def get_resource_dir(folder): 函数增加了: 
```python
     #20201208 xfgao@163.com 编译后的.exe 容易找不到文件的情况
    if os.path.exists(resource_path)==False:
        resource_path= os.path.join(os.path.dirname(os.path.realpath(sys.executable)),folder)
    #20201208 xfgao@163.com 编译后的.exe 容易找不到文件的情况
```

     在 loaders.py 中的 ,def __init__(self, searchpath, encoding="utf-8", followlinks=False): 函数 增加了:
```python
        #20201208 xfgao@163.com some reason can not find template in .exe
        self.searchpath.append(os.path.dirname(os.path.realpath(sys.executable)))
        #20201208 xfgao@163.com some reason can not find template in .exe
```
     


