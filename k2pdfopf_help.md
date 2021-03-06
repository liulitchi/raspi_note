k2pdfopt 是一个很方便的pdf重排工具，当然，它的功能不止于此，这里，我们简单学习一下它的功能。

终端里输入 `k2pdfopt -h` ， 我们可以看到类似的文本显示:

```
k2pdfopt v2.42 (w/MuPDF,DjVuLibre,OCR) (c) 2017, GPLv3, http://willus.com
    Compiled May 20 2017 with Gnu C v4.8.5 for Linux on x64.

 a. Autostraighten (-as)                 n. Native PDF output (-n)
 b. Bitmap type (-jpg,-png,-bpc)         o. Output name (-o)
bp. Break pages (-bp,-f2p)              oc. OCR (-ocr,-ocrvis,...)
 c. Color/Negative output (-c, -neg)    om. Output margins (-om)
co. Column detection (-col,-ch,...)      p. Page range (-p)
cs. Contrast/Sharpen (-cmax,-g,-s,-wt)  pd. Padding/Marking (-p[lrbt],-mc)
 d. Device selection (-dev,-h,-w,-dpi)   r. Right-to-left page scans (-r)
ds. Document scale factor (-ds)         rt. Rotate source page (-sr)
 f. Fit to single column (-fc)           s. Special (-de,-evl,-gs)
gt. Gap thresholds (-gt...)             sm. Show marked source (-sm)
 j. Justification (-j)                   u. Usage (command line opts)
 l. Landscape mode (-ls)                 v. Vertical spacing (-vb,-vs)
 m. Margin to ignore (-m)                w. Wrap/Reflow text (-wrap,-ws)
mo. Mode (-mode)                         x. Exit on completion (-x)

Selected options:  -help

Enter option above (h=help, q=quit):
```

具体解释一下：

第一行和第二行解释的软件的版本和编译信息等细节，如它也具备OCR功能。

下面具体我们一一解释:

```
 a.自动增强（-as）               
 n.本地PDF输出（-n）
 b.bitmap类型（-jpg，-png，-bpc） 
 O.输出名称（-o）
 BP.中断页面（-bp，-f2p）
 OC.OCR（-ocr，-ocrvis，...）
 C.彩色/负输出（-c，-neg）
 OM.输出边距（-om）
 co.列检测（-col，-ch，...）
 p.页面范围（-p）
 CS.对比度/锐化（-cmax，-g，-s，-wt）
 PD.填充/标记（-p [lrbt]， - mc）
 d.设备选择（-dev，-h，-w，-dpi）
 r.从右到左扫描页面（-r）
 DS.文档比例因子（-ds）
 RT.旋转源页面（-sr）
 F.适合单列（-fc）
 s.特殊（-de，-evl，-gs）
 GT.差距阈值（-gt ...）
 SM.显示标记的源（-sm）
 j.理由（-j）
 u.用法（命令行opts）
 l.横向模式（-ls）
 v.垂直间距（-vb，-vs）
 m.要忽略的余量（-m）
 W.包装文本/重排文本（-wrap，-ws）
 mo.模式（ -mode）
 X.完成后退出（-x）
 ```
 
 ## VIII.
 ## IX.ubuntu 下安装 tesseract-ocr:
   > 更新系统：sudo apt update
   
   > 安装软件：sudo apt install tesseract-ocr
   
   > 安装简体中文包：sudo apt install tesseract-ocr-chi-sim
   
   备注：一个可选的图形客户端：ocrfeeder
 ## X.linux设置TESSERACT_PREFIX环境变量：
  > cat >> .pam_environment
  
  > TESSDATA_PREFIX=/usr/share/tesseract-ocr/
  
  回车，键入 Ctrl-D 确认。注销电脑以使设置生效。
  
  注：如果未设置环境变量，将会使用 GOCR 作 OCR，显示可能如下：
  ```
  Initializing OCR for 2 threads xx
  Could not find Tesseract data (env var TESSDATA_PREFIX = (not assigned)).
  Using GOCR v0.50.
 ```
 ## XI.TESSERACT 与 GOCR 的区别:
 
 OCR默认情况下未打开，可使用 -ocr命令启动。
 有两种不同的OCR引擎来转换为文本。默认是Google的开源项目 Tesseract（需要另安装），支持中文等多种语言。
 另一个是 GOCR ， GOCR不需要额外的文件，比 Tesseract 快十倍以上，不过仅支持 ACSII编码（也就是说，不支持中文）。
 
 ## XII.如何图片转文字：
   可以采用多（如 英文+简体中文）语言输入： ` k2pdfopt -ocr t -ocrlang eng+chi_sim -col 1 测试文件.pdf`
   
   回车后等待（输出文件仍为pdf）  
 
 ### 调整输出：
   1.屏幕尺寸：
   
     设置阅读器的屏幕尺寸，可选择-w（代表宽度）和-h（代表高度）命令行选项。
     屏幕尺寸以像素分辨率为单位，kindle基础版分辨率为600*800，建议选择输出560*735;
     kindle DX 分辨率是 824*1200 ，建议设置 -w 784 -h 1135。
   
   3.横向模式：
     
     命令行里 -ls ，或者菜单设置 (l)。横向显示，显示放大效果。
   
   4.输出文件大小：
     
     为减小PDF体积，可使用 -bpc  选项改变， 默认值是4 ，
     设置 -bpc 2 （或 -bpc 1）会使文件体积大约减小一半（或1/4）。
     也可使用 -jpeg 命令选项降低图片质量。
     如 -jpeg 50 ，质量值越低，输出文件越小。
   
   5.设置边距:
     
 ### 处理选项：
   1.显示标记：
   
   2.增加放大倍率:
   
     -idpi和 -odpi设置控制着k2pdfopt输出PDF文件的质量和放大倍数。
     DPI代表每英寸点数, -idpi表示k2pdfopt每英寸或分辨率用于渲染源（输入）PDF文件的点数，
     
     -odpi表示k2pdfopt输出设备（读取器屏幕）的每英寸点数。
   
   3.原生PDF输出：
   
   4.自动矫正：
   
   9.从右到左扫描页面(-r)：
   
     有些语言书写方式是从右向左的，比如希伯来文。选择 -r ，让软件从右开始扫描。
  
