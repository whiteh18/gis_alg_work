2024.12.25 begin<br>
# gis基础算法作业<br>
超级超级菜^_^<br>
大概率有很多不对的地方<br>
仅做记录，不做参考<br>
怎么理论都懂，就是写不出代码呢<br>
此处省略100个哭泣的表情包<br>
不是其实我还不怎么会用这个东西，谁懂英语困难户的难T_T<br>
-----------------------------------------分界线-----------------------------------------<br>
# 一. 在家乡的地图上投影自己的名字（老师课件-空间数据编码）<br>
（小小吐槽一下，老师竟然边“吹牛”（褒义褒义绝对褒义）边讲完了这节课！然后就要我这个菜鸟写代码了！！哈哈第二节课老师就从最简单的开始教我们怎么写，此时我洋洋得意，觉得不过如此！没想到，后面就直接“放养”了，哈哈哈哈（扶额苦笑无奈）。。。。。。咳咳，回到内容上来。）<br>

（这一章的作业用到了anaconda+jupyter+python）<br>

1 绘制坐标格网，在网格中书写汉字<br>
即为姓名建立坐标参考系<br>
2 分析汉字特征点，进行姓名编码<br>
即提取姓名的特征点，记录这些点的坐标<br>
生成点、线的表格文件（不懂有啥用，后来还是要改成生成geojson文件，可能这也算是一种编码）<br>
3 生成geojson格式的编码文件<br>
大致格式可参考**name.geojson** （数据已被修改，仅供参考格式）<br>
建议访问 https://geojson.cn/docs/ref/geojson 等相关说明格式的网站<br>
4 但是通过观察发现老师的geojson文件中的坐标是经纬度坐标，而我自己编码的只是简单的平面直角坐标系下的坐标数据，于是我就想将这些坐标变换为类似经纬度坐标，参考了下一章的内容，用了变换矩阵处理了一下原始geojson文件中的坐标，生成了新的geojson文件。<br>
新的geojson文件**my_name_tra.geojson** （数据已被修改，仅供参考格式）中，中文就乱码了，我暂时还不知道怎么改，不过对实验影响不大<br>
对应文件**lat_lon.py**<br>
5 使用ipyleaflet库在家乡地图上显示姓名<br>
借助天地图，添加卫星影像地图，需要密钥<br>
当时正值天地图维修时期，我们使用的是老师的^_^，嘴硬心软的老师^_^。不过现在可以申请成为开发者获得密钥。<br>
不过如果不需要显示在影像地图上，ipyleaflet.GeoJSON便足够了<br>
对应文件**name_prj.py**<br>

(不过也可以直接在https://geojson.io/#map=2/0/20 网站中输入JSON文件，可以在线在地图上显示姓名）<br>

completed!

# 二. 在上一章的基础上实现姓名的下列变换（老师课件-平面坐标变换）
左斜变换<br>
耸肩变换<br>
比例变换<br>
旋转变换<br>
平移变换<br>
（这一章的作业用到了anaconda+jupyter+python）<br>
1 老师使用的是turf库来做的，但是对于python我只能下载到turfpy/pyturf，而且还总是报错，于是果断改变决策<br>

2 参考原理书上平面坐标变换的原理，决定使用平面坐标变换矩阵（对就是上一章我用的那个方法）<br>
于是问题演变为上述的这些变换对应的**平面坐标变换矩阵**是什么<br>
除去理论中已经讲解的比例、旋转和平移，剩下需要探究的便是**左斜和耸肩**，我现在写得变换矩阵可能需要修改<br>
另外提一句，我计算了好几遍，总感觉书上写的顺时针旋转变换矩阵应该是**逆时针旋转变换矩阵**<br>
还有，我可能得考虑书上所写的**相对于(Xf,Yf)点的变换**<br>
对应代码文件**name_bh.py**<br>

确实是要相对于某点进行坐标变换<br>

complteted!<br>

大体完成，仍然存在的问题是**左斜变换**<br>

# 三. 中国版图和世界版图投影转换+北京-巴黎大圆轨迹（老师课件-地图投影）
（实验提供的是.gen格式数据，但是我是真不会处理这种文件T_T，于是借助工具将其转换为了.shp格式文件）<br>
（这一章的作业用到了anaconda+jupyter+python）<br>

1 根据所给的中国版图数据（'china.shp',且原始数据就是北京54坐标系下的数据）<br>
– 绘制显示基于北京54坐标系的经纬度数据<br>
– 编写兰勃特投影转换程序，转换上述数据，并显示<br>
– 编写墨卡托投影转换程序，转换上述数据，并显示<br>
– 同时，要绘制相对应的经纬网格，网格间距5度<br>
2 根据所给的世界版图数据<br>
– 绘制显示基于WGS84坐标系的经纬度数据<br>
– 编写墨卡托投影转换程序，转换上述数据，并显示<br>
– 计算北京到巴黎的大圆轨迹，并显示<br>
– 同时，要绘制相对应的经纬网格，网格间距5度<br>

注：实验提供，兰伯特投影参数——中央经线：105；标准纬线：20，40；原始纬线 0<br>
墨卡托投影参数——原始纬线：0；中央经线：0<br>

可恶，我按照原理书上的投影转换公式进行投影转换结果错的离谱，于是借助ai检查并转换了一下投影转换公式^_^<br>
这一章代码我还会再检查重新写的 ^_^ #_#<br>
最大的问题出在每隔5度的经纬网格的绘制 T_T <br>
对应代码文件**china_world_prj.py**<br>

completed!

# 四. 计算面积+投影反算+梯形面积法（老师课件-空间度量算法）
根据所给的江苏省境界数据<br>
– 显示并计算江苏省十三个地市的面积<br>
– 编写墨卡托投影反算程序，转换上述数据为经纬度坐标，并显示<br>
– 根据地球椭球体表面上的梯形面积计算方法，基于经纬度坐标计算江苏省十三个地市的面积<br>
^_^

# 五. 道格拉斯-普克压缩算法（老师课件-矢量数据压缩）
1、根据道格拉斯一普克法，编写程序对经过兰勃特投影的中国版图数据进行压缩和过滤<br>
2、屏幕绘图显示压缩前后的地图数据<br>
3、数据压缩率为50%<br>

# 六. 四叉树+morton码（老师课件-四叉树）
矩阵四叉树转换为对应的四进制编码和十进制编码<br>
矩阵四叉树文件见**squad_tree.txt**<br>
转换代码文件见**morton_410.cpp**<br>

# 七. 左转算法生成多边形拓扑（老师课件-多边形拓扑生成）
已有弧段数据<br>
左转算法<br>
岛的判断<br>
多边形拓扑<br>
参考大佬优秀html文件，见**left_turn.html**

# 八. 地图符号的绘制（老师课件-地图符号）（加分项）
地图符号的几何特征<br>
• 点状地图符号绘制<br>
• 线状地图符号绘制<br>
• 面状地图符号绘制<br>

# 九. 点、线、面栅格化（老师课件-矢量数据转栅格数据）
①点坐标→**行列号**<br>
②**全路径栅格化**；**八方向栅格化**<br>
③内部点扩散；射线法；扫描法；**边界代数法**<br>
