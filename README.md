#### 写在前面
由于宜出行的登录策略更新，导致无法使用qq登录直接爬取人流量的问题，近期进行了代码升级，已经解决了该问题，并且能顺利爬取数据，示例如下。目前暂不提供源代码，如有需要宜出行数据，可联系：917961898，进行爬取(非免费)，示例数据：
![
](https://img-blog.csdnimg.cn/2019091609403833.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0NDY0OTI2,size_16,color_FFFFFF,t_70)

可视化效果图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190916094104405.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0NDY0OTI2,size_16,color_FFFFFF,t_70)
目前也有腾讯位置大数据爬取的在线工具免费使用，不过该数据精度不够高，如果对精度要求高，推荐使用宜出行爬取。

工具链接：[腾讯出行人流量爬取工具](http://www.mapboxx.cn/tool/tencet/)

这是腾讯位置大数据可视化效果图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828153306464.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0NDY0OTI2,size_16,color_FFFFFF,t_70)

欢迎加入地图数据爬取交流群：626697156，有问题可以反馈给群主

#### 工具介绍：
该工具基于微信中的宜出行提供的数据接口进行爬取，能够爬取一定范围内的当前时间点的人流量数据。地址：https://liujiao111.github.io/

#### 环境：
- windows
- python3+
- 安装第三方包：缺啥安装啥

#### 使用指南：
- 申请多个qq号，并将qq号放入当前目录下的qqlist.py文件中，格式如下：
```
qq_list = 
[["11111111", "11111111"],
["11111111", "11111111"],
["11111111", "11111111"],
["11111111", "11111111"],
["11111111", "11111111"],
["11111111", "11111111"],
["11111111", "11111111"],
["11111111", "11111111"]]
```
根据你需要爬取的城市范围大小，适当申请多个qq号进行爬取(我试了下用6个号爬取来宾市的是没什么的)，因为每个QQ号能爬取的数据量有限。将每个QQ号放入该文件中，并遵循已有的格式。
- 确定需要爬取的城市矩形范围。使用百度地图提供的坐标拾取工具，确定城市的左上角、右上角、右下角、左下角四个点的坐标(大概组成一个矩形，不用太准确)，并将拾取的四个坐标点依次填入setting.py文件中,并对应下面四个变量,示例：
```
city_bound_point_A = [114.286652,30.642638] #左上角点，x619
city_bound_point_D = [114.239273,30.580588] #左下角点，农场十一队
city_bound_point_B = [114.462433,30.574677] #右上角点，木妙
city_bound_point_C = [114.418488,30.479746] #右下角点，牛场右下角
```
- 双击 `run.bat`文件，执行爬取程序，需要注意的是程序会自动打开谷歌浏览器并进行登陆操作，属于正常现象需要提前装好谷歌浏览器。
- 等待一段时间后(具体不一定，大概10分钟)，爬取后的结果存放到example文件夹中，里面txt文件就是爬取到的人流量数据，文件使用爬取的时间点进行命名，数据有四个字段 `count`,`wgs_lng`,`wgs_lat,time`,分别代表人流量，经度，纬度，时间点，后面可以使用该文件进行解析得到需要的数据，并进行可视化。

-  这里提供了一个可以解析人流量txt数据文件，并生成用于百度地图热力图展示需要的数据的代码，见目录下的read_data_to_txt.py代码，需要修改代码中file_path的路径，修改为上面生成的example文件夹中txt格式的人流量数据所在文件路径，保存然后执行data2txt.bat，执行后会在当前目录下生成data_flow.xls和data.txt两个人流量数据文件。
- 上面生成的txt文件可以拷贝内容到baidu_relitu.html文件中(文件内容有点多，请耐心等待)，将html文件中第31行`var points = `后面的内容替换为上面data.txt中的文本内容，并且将第27行的中心点坐标替换为31行中随意一个坐标点的坐标，保存后在浏览器打开该HTML文件，即可看到在地图上展示的热力图数据。
