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

