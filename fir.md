---


---

<h1 id="前期试验总结并修正">前期试验总结并修正</h1>
<p>一、数据处理面临的问题：</p>
<ol>
<li>带宽选择：<br>
在2.401GHz ~ 2.495GHz共计95MHz带宽有14个信道，国内能够使用的是13个，但是相互之间有重叠；<br>
在5GHz附近国内能够使用的一共是24个信道，但是国内 能够使用的只有19个信道包括13个20MHz带宽和6个40GHz带宽；<br>
在避免重叠的情况下，根据inject的限制，只能选择5G附近的13个作为数据参与计算。</li>
<li>之前的算法只能模拟单纯的相位，但是根据单纯的计算相位在利用NDFT时不够，所以我修正了之前的算法，采用实虚部分别模拟，根据画出的图可以看出最大误差不超过0.25/ 6.5  * 100% &lt;= 3.7%,不大于相位的误差，而且相对而言信息更准确，所以采用实虚部模拟法。</li>
<li>初步计算：<br>
根据inject中使用的函数，在发送端和接收端使用的是64号信道，对应的中心频率为5320MHz，信道宽度为20MHZ，使用中心频率计算。<br>
对于公式t=(&lt;hi)/(2∗pi∗fi ) mod 1/fi，有fi为5320MHZ， 对应于T0 = 1/fi =   (1/5.32) * 10^-9 = 0.1879699248120300075 * 10 ^-9 ,取T1 = 1/(2∗pi∗fi ) = 0.02991634268644452276448034269546 * 10 ^ -9. 于是2中等式可以化简为 t = &lt;hi * T1 mod T0.其中：T0 = 0.18797 * 10 ^ -9; T1 = 0.0299163 * 10 ^-9.<br>
根据上述计算表达式，t的结果最大是T0，即使如此，最远的测量距离为T0 * V = 0.056391m ，其中V是光速，显然较小，若是考虑中国剩余定理，计算记过可能略大，具体没有详细计算，因为中国剩余定理无法计算小数。</li>
</ol>
<h2 id="二、接下来的问题：">二、接下来的问题：</h2>
<ol start="4">
<li>设计实验适用于13个信道的过程，通过新的模拟算法，计算相应子信道CSI数值，然后对于100组数据求数值平均获得较为可信的数据，然后带入下一步继续计算。</li>
<li>根据4中获得的数据，应该是2 * 13 * 4 * 100组数据，将数据数值平均获得2 * 13 * 4 * 1个数据，然后将正反数据相乘即可得到h<sub>i,0</sub> <sup>2</sup>，假设DFT的组数为13，利用相应的算法可以求出t * f的值，然后计算可以获得时间，因为NDFT是一个欠定系统，所以组数是未知的，所以需调用paper 中 的alg1计算相应的结果，即可获得TOF。</li>
</ol>
<h2 id="三、实虚部模拟zero-subcarriers的csi图像">三、实虚部模拟zero-subcarriers的CSI图像</h2>
<ol start="6">
<li>实部整体模拟<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/ten/real.png" alt="fig1"></li>
<li>实部放大处理<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/ten/real_big.png" alt="fig2"></li>
<li>虚部整体模拟<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/ten/imag_big.png" alt="fig3"></li>
<li>虚部放大处理<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/ten/imag.png" alt="fig4"></li>
</ol>

