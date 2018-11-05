---


---

<h1 id="algorithm_amendment_unwrap">algorithm_amendment_unwrap</h1>
<p>charliegean 2018-11-5<br>
一、思考</p>
<ol>
<li>利用昨天的结果，几乎不可以说明什么，几乎全部数据误差超过50%。具体见<a href="https://github.com/Charliegean/laboratory/blob/master/six_verification.md">six_verfication</a>.</li>
<li>unwrap的用法：具体见<a href="https://ww2.mathworks.cn/help/matlab/ref/unwrap.html?lang=en">matlab_unwrap</a>.可知，对于unwrap，会根据容差修正数据，而在修正的过程中，但要求必须很大，而对于spline来说，pi的数值过大，可以修正为pi/16尝试。</li>
</ol>
<p>二、问题：</p>
<ol>
<li>
<p>对于直接使用复数修正，可能有些问题？</p>
</li>
<li>
<p>根据非unwrap的说法，可以看到，spline的相位差很少，更多是因为数据的振幅，相差较大，且根据插值的密度不同，相差不同，会出现差别大的更大，差别小得更小。接下来尝试</p>
<blockquote>
<p>5,10,20,50,100</p>
</blockquote>
<p>的规模插值模拟。<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/ang_data_1.jpg" alt="初始数据"><br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/ang_res.jpg" alt="插值后的数据"><br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/ang_chan_unwrap.jpg" alt="相位差"></p>
</li>
<li>
<p>unwrap的容差应该足够小。</p>
</li>
<li>
<p>尝试使用分化模拟，即利用函数尝试将复数利用欧拉定义尝试分化为角度和振幅，然后分别模拟，在求得数值。具体方法可以考虑r=abs（）；ang_complex=angle（complex）；</p>
</li>
<li></li>
</ol>

