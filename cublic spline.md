---


---

<h1 id="第七次报告">第七次报告</h1>
<h5 id="吴浩天-2018-11-19">吴浩天 2018-11-19</h5>
<h2 id="一、-反思与分析">一、 反思与分析</h2>
<p>64个子信道只有五十六个可用的数据，对应于0号子信道的应该是模拟的33号子信道，对应的数据应该在28号和29号信道之间，但是，我尝试将原始数据画图，使用角度和实部虚部作图，但结果都是相差不大，即根据28,29两点的平均数均与零点有较大偏差，角度处理见fig1.</p>
<h2 id="二、修正与误差解释">二、修正与误差解释</h2>
<ol>
<li>在尝试修改之后，拟合效果反而相差更大，回到第六次结果，尝试使用matlab的图像放大功能，发现在放大接近二十倍的情况下，原始曲线与模拟曲线的重合程度依然非常好，可以说是同一条线，几乎没有区别，至于为什么模上pi之后会与0有较大误差我尝试解释了一下，见3</li>
<li>利用三次样条插值方法，可以看出，在插值处理某两点时，与两个端点的关系很大，给定的56组数组构成55个区间，假定分别是A1，……，A55，其中Ai表示i与i+1构成的区间，所以目标是尽可能的提高A28的模拟效果，但是在给定的数据中，A28的两个端点即28号和29号的平均值与0值有较大误差，而我们的目标又是求出在A28中点的值，利用三次样条插值法在A28号产生的三次多项式在区间中点的取值就与0有较大偏差。实验图像见fig2，fig3.</li>
</ol>
<h2 id="三、结论">三、结论</h2>
<ol start="3">
<li>之前采用的方法<a href="https://github.com/Charliegean/laboratory/blob/master/six_amendment.md">三次样条</a>对角度模拟良好。</li>
</ol>
<h2 id="四、处理截图">四、处理截图</h2>
<p><img src="https://github.com/Charliegean/laboratory/blob/master/picture/seven/ex7_ang_1.png" alt="fig1:原始数据角度"><br>
<strong>fig1</strong><br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/seven/ex7_index_1.png" alt="fig2:模拟信号原始信号与index的关系图像"><br>
<strong>fig2</strong><br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/seven/ex7_ang_1.png" alt="fig3:A28区间局部放大"><br>
<strong>fig3</strong></p>

