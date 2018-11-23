---


---

<h1 id="去掉cfo模拟情况分析">去掉CFO模拟情况分析</h1>
<p>charliegean 	2018-11-22</p>
<h2 id="一、原因：">一、原因：</h2>
<p>前期使用模拟过程，在处理时忽略了数据中的CFO，在处理过程中目标信道值与0值相差较大。现在分析去掉CFO的结果与加上CFO的结果对比，并分别测试使用unwrap对模拟效果的影响。</p>
<h2 id="二、实验过程">二、实验过程</h2>
<ol>
<li>设置对照，模拟生成六组数据，前三组是带有CFO的，后三组是不带CFO的，利用spline处理并画出图像分析效果。截取一组作为实例见fig1，fig2.</li>
<li>设置对照，利用1中的数据，分别用和不用unwrap对数据进行模拟，同时改变容差然后画出图像，分析结果，实例见fig2.</li>
</ol>
<h2 id="三、分析">三、分析</h2>
<ol start="3">
<li>根据结果进行分析，在待求的结果区间内，模拟效果较好，但是在其他部分效果较差，使用unwrap之后，即使改变容差，变化不是很大，故，unwrap对结果的影响不是很大。</li>
<li>考虑去掉cfo的数据，可以看到，两端的弧度差大概在0.4，而待求区间的模拟数据在0.01左右，故相对误差在0.01/0.4 * 100% = 2.5%。</li>
<li>考虑加上cfo的数据处理，在目标区间为0.07685（28号）~0.08863（29号）两端极差大于等于0.4，相对误差在（0.08863-0.07685）/ 0.4 * 100%= 2.9%，左端即1号信道的数据在0.1附近，右端即56号信道的数据在-0.3附近，考虑为cfo带来的误差，cfo大致在0.09，将目标区间的数据减去CFO带来的影响在0 ~ 0.01内.</li>
<li>分析不是零的原因：三维线条差值受区间两端的影响，而28号和29号信道的数据收到sfo的影响，所以在处理时回叙会造成一定的偏差。</li>
</ol>
<h2 id="四、截图">四、截图</h2>
<ol start="7">
<li>fig1：带 cfo的数据模拟分析<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/eight/cfo_0_angle.png" alt="fig1"><br>
fig2:带CFO的局部放大图像<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/eight/c_angle_1.png" alt="fig2"><br>
fig3:使用unwrap之后的结果<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/eight/cfo_0_angle_unwrap.png" alt="fig3"><br>
fig4:使用unwrap后的局部放大<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/eight/cfo_0_angle_unwrap_1.png" alt="fig4"><br>
fig5：不带CFO的数据模拟分析<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/eight/c_angle.png" alt="fig5"><br>
fig6:不带CFO的局部放大<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/eight/c_angle_unwrap_1.png" alt="fig6"><br>
fig7：使用unwrap之后的结果<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/eight/c_angle_unwrap.png" alt="fig7"><br>
fig8：使用unwrap之后的局部放大<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/eight/c_angle_unwrap_1.png" alt="fig8"></li>
<li></li>
</ol>

