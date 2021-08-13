### redis GEO Spatial & Hyperloglogs

**geo spatial**

指令：

geoadd citys 121.48 21.22 sh 113.01 28.19 cs

geopos  citys cs

geopos citys sh cs km

georadius citys 113.01 28.19 5 km

georadiusbymember citys cs 20 km

添加两个城市的经纬度

显示某个城市的经纬度

计算两个城市的距离

显示某个位置5km的城市



**hyperloglogs**

指令：

pfadd log 1 2 3 4 5 6 7 8

pfcount log

pfadd qs a b c d e f g

pfcount qs 

pfmerge result log qs

应用：

统计网站用户的访问量