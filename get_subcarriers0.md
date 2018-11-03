# Get zero_sub carrier 's data
## date:10-28 	author: charliegean
一、Reason：
===========
 在chronos测量TOF过程中，需要测量zero-subcarriers的值，但是在80211n标准中，zero-subcarrier不携带任何信号，所以，但是幸运的是，我们可以利用信号的物理性质计算出它的值。
 
 二、Way：
 ==============
[cubic spline interpolation.(三次样条插值)](https://baike.baidu.com/item/%E4%B8%89%E6%AC%A1%E6%A0%B7%E6%9D%A1%E6%8F%92%E5%80%BC/3476729?fr=aladdin)

[CODE](https://www.cnblogs.com/xpvincent/archive/2013/01/26/2878092.html)

三、Detail：
===========
1. 利用read_bf_file.m文件读取.dat数据；
2. 取其中一个包的数据，然后利用get_scaled_csi.m数据获得30个subcarriers的csi数据。
3. 现在得到的数据是一个1\*3\*30的数组，然后每次取出1\*1\*30的数据进行插值处理。其中x取1:30，插值的xx取0:0.25:29，之后获得一维177个元素的数组，可得到取该数组的零号元素作为zero_subcarrier的值。
4. 接后续

四、code
============
5. csitool 给定的函数read_bf_file.m,get_scaled_csi.m.
6. matlab 自带的函数squeeze和spline函数 
7. 
	>csi_trace=read_bf_file('data1/data1/018.dat')
		csi_entry=csi_trace{1}
		csi=get_scaled_csi(csi_entry)
csi_a = db(abs(csi(:,1,:)))
csi_a=squeeze(csi_a)
x=1:30
xx=0:.25:29
csi_y=spline(x,csi_a,xx)

五、截图
===
![the real of csi](https://github.com/Charliegean/laboratory/tree/master/picture/18_spline_real.jpg)

![the imag of csi](https://github.com/Charliegean/laboratory/tree/master/picture/18_spline_imag.jpg)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI1MDI4MzUzMiwxODY3NjE1MTk5XX0=
-->