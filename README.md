# opencv-haar-classify
训练opencv的级联分类器

### 环境
mac ox操作系统
安装opencv：`conda install opencv`
安装好opencv后就可以使用里面的脚本训练了。

### 数据准备
1. 正向数据：pos/XX.jpg
2. 负向数据：neg/XX.jpg
3. 正向文本`pos.txt`:

        pos/XX.jpg 1 0 0 60 60

        # pos/XX.jpg 图片路径，1 样本数，60 宽，60 高
4. 负向文本`neg.txt`：

        neg/XX.jpg

        # neg/XX.jpg 仅放图片路径

### 训练步骤
1. 训练正向数据的vec文件
`opencv_createsamples -vec pos.vec  -info pos.txt -num 15 -w 60 -h 60 pause`

参数  |  数值  |  说明
-----------  |  ----------  |  ---------
-vec|pos.vec|生成的vec文件名
-info|pos.txt|使用的正向脚本
-num|15|样本数 
-w|60|图像宽
-h|60|图像高

目录出现`pos.vec`说明训练成功

2. 训练xml文档
   新建`cascades`目录

`opencv_traincascade -data cascades -vec pos.vec -bg neg.txt -numPos 15 -numNeg 15 -numStages 5 -w 60 -h 60 -minHitRate 0.9999 -maxFalseAlarmRate 0.5 -mem 2048 -mode ALL`

参数  |  数值  |  说明
-----------  |  ----------  |  ---------
-data|cascades|训练后生成xml的文件夹
-vec|pos.vec|正向数据
-bg|neg.txt|负向数据
-numPos|15|正向样本数
-numNeg|15|负向样本数
-numStages|5|训练迭代数
-w|60|图像宽
-h|60|图像高
-minHitRate|0.9999|期望最小检测率
-maxFalseAlarmRate|0.5|期望最大误检率
-mem|2048|使用的计算内存数（M）
-mode|ALL|选择用来训练的haar特征集的种类




参考文章：
[https://blog.csdn.net/txiaomiao/article/details/64132273](https://blog.csdn.net/txiaomiao/article/details/64132273)(windows版本)

----

Author: suimingyang 

Email : suimingyang123@gmail.com

Blog  : [https://suimingyang.github.io/](https://suimingyang.github.io/)

----