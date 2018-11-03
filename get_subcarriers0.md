---


---

<h1 id="get-zero_sub-carrier-s-data">Get zero_sub carrier 's data</h1>
<h2 id="date10-28--author-charliegean">date:10-28 	author: charliegean</h2>
<h1 id="一、reason：">一、Reason：</h1>
<p>在chronos测量TOF过程中，需要测量zero-subcarriers的值，但是在80211n标准中，zero-subcarrier不携带任何信号，所以，但是幸运的是，我们可以利用信号的物理性质计算出它的值。</p>
<h1 id="二、way：">二、Way：</h1>
<p><a href="https://baike.baidu.com/item/%E4%B8%89%E6%AC%A1%E6%A0%B7%E6%9D%A1%E6%8F%92%E5%80%BC/3476729?fr=aladdin">cubic spline interpolation.(三次样条插值)</a></p>
<p><a href="https://www.cnblogs.com/xpvincent/archive/2013/01/26/2878092.html">CODE</a></p>
<h1 id="三、detail：">三、Detail：</h1>
<ol>
<li>利用read_bf_file.m文件读取.dat数据；</li>
<li>取其中一个包的数据，然后利用get_scaled_csi.m数据获得30个subcarriers的csi数据。</li>
<li>现在得到的数据是一个1*3*30的数组，然后每次取出1*1*30的数据进行插值处理。其中x取1:30，插值的xx取0:0.25:29，之后获得一维177个元素的数组，可得到取该数组的零号元素作为zero_subcarrier的值。</li>
<li>接后续</li>
</ol>
<h1 id="四、code">四、code</h1>
<ol start="5">
<li>csitool 给定的函数read_bf_file.m,get_scaled_csi.m.</li>
<li>matlab 自带的函数squeeze和spline函数</li>
<li>
<blockquote>
<p>csi_trace=read_bf_file(‘data1/data1/018.dat’)<br>
csi_entry=csi_trace{1}csi=get_scaled_csi(csi_entry)<br>
csi_a = db(abs(csi(:,1,:)))<br>
csi_a=squeeze(csi_a)<br>
x=1:30<br>
xx=0:.25:29<br>
csi_y=spline(x,csi_a,xx)<br>
plot(x,csi_a,‘o’'o',xx,csi_y)</p>
</blockquote>
</li>
<li></li>
</ol>
<h1 id="五、截图">五、截图</h1>
<p><img src="
8.

==
ealocsihttps://github.com/Charliegean/laboratory/tree/master/picture/18_spline_real.jpg" alt="the real of csi"></p>
<p><img src="https://github.com/Charliegean/laboratory/tree/master/picture/18_spline_imag.jpg" alt="the imag of csi"></p>)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEwMTk1OTYzNl19
-->