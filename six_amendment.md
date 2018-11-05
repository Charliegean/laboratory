---


---

<h1 id="algorithm_amendment_unwrap">algorithm_amendment_unwrap</h1>
<h2 id="charliegean-2018-11-5">charliegean 2018-11-5</h2>
<h2 id="一、思考">一、思考</h2>
<ol>
<li>利用昨天的结果，几乎不可以说明什么，几乎全部数据误差超过50%。具体见<a href="https://github.com/Charliegean/laboratory/blob/master/six_verification.md">six_verfication</a>.</li>
<li>unwrap的用法：具体见<a href="https://ww2.mathworks.cn/help/matlab/ref/unwrap.html?lang=en">matlab_unwrap</a>.可知，对于unwrap，会根据容差修正数据，而在修正的过程中，但要求必须很大，而对于spline来说，pi的数值过大，可以修正为pi/16尝试。</li>
</ol>
<h2 id="二、问题：">二、问题：</h2>
<ol start="3">
<li>
<p>对于直接使用复数修正，可能有些问题？</p>
</li>
<li>
<p>根据非unwrap的说法，可以看到，spline的相位差很少，更多是因为数据的振幅，相差较大，且根据插值的密度不同，相差不同，会出现差别大的更大，差别小得更小。接下来尝试以下规模插值模拟：</p>
<blockquote>
<p>5,10,20,50,100</p>
</blockquote>
<p>fig1：初始数据<img src="https://github.com/Charliegean/laboratory/blob/master/picture/ang_data_1.jpg" alt="初始数据" title="初始数据"><br>
fig2：插值后的数据<img src="https://github.com/Charliegean/laboratory/blob/master/picture/ang_res.jpg" alt="插值后的数据" title="插值后的数据"><br>
fig3：两者的相位差<img src="https://github.com/Charliegean/laboratory/blob/master/picture/ang_chan_unwrap.jpg" alt="相位差" title="相位差"></p>
</li>
<li>
<p>unwrap的容差应该足够小。</p>
</li>
<li>
<p>尝试使用分化模拟，即利用函数尝试将复数利用欧拉定义尝试分化为角度和振幅，然后分别模拟，在求得数值。具体方法可以考虑r=abs（）；ang_complex=angle（complex）；</p>
</li>
<li>
<p>尝试使用实部虚部分别模拟，根据模拟图像，获得结果。</p>
</li>
</ol>
<h2 id="三、试验尝试">三、试验尝试</h2>
<ol start="9">
<li>根据尝试，复数直接插值使用unwrap即使容差较小效果也不显著。</li>
<li>使用欧拉定理，分解为相位和振幅，其中相位在容错为pi/2时，模拟效果很好。但是振幅即使容差很小效果也不是很好，只有部分模拟很好。而且在最重要的28~29号数据（原因是要这附近的数据计算模拟原数据33号即0号子载波的数据）附近效果尤其差。</li>
<li>分为实部和虚部分别模拟，总体效果差于相位模拟，但远远优于振幅模拟，特别是需要的28~29号数据附近，模拟效果良好。具体结果看（四）中配图。</li>
</ol>
<h2 id="四、试验结果配图：">四、试验结果配图：</h2>
<h2 id="注：橙色线代表模拟的数据，蓝色线代表原始数据）">(<strong>注：橙色线代表模拟的数据，蓝色线代表原始数据</strong>）</h2>
<p>fig4：振幅模拟	<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/r_1000_333.jpg" alt="振幅模拟">	<br>
fig5：相位模拟<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/ang_1000.jpg" alt="相位模拟"><br>
fig6：实部模拟<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/real_1000.jpg" alt="实部模拟"><br>
fig7：虚部模拟<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/imag_1000.jpg" alt="虚部模拟"></p>
<h2 id="五、代码（仅贴模拟振幅部分且插值区间放大1000倍的代码）">五、代码（仅贴模拟振幅部分且插值区间放大1000倍的代码）</h2>
<blockquote>
<p>load(‘chanest_ex1.mat’);<br>
data=unwrap(abs(chanEst),0.1);<br>
x=1:2:60;<br>
x(15)=28;<br>
x(16:1:29)=29:2:55;<br>
x(30)=56;<br>
x=x’;<br>
xx=0.001:.001:56;<br>
xx=xx’;<br>
y=1000:1000:56000;<br>
y=y’;<br>
csi=data(x);<br>
res=interp1(x,csi,xx,‘spline’,‘extrap’);<br>
res_int=res(y);<br>
xxx=1:1:56;<br>
plot(xxx,data);<br>
hold on;<br>
plot(xxx,res_int);<br>
hold off;</p>
</blockquote>

