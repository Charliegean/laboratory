---


---

<h1 id="checkout-whether-the-cubic-spline-interpolation">checkout whether the cubic spline interpolation</h1>
<h3 id="charliegean--2018-11-3">charliegean  2018-11-3</h3>
<p>一、目标：</p>
<ol>
<li>
<p>利用已知的一组数据，标号连续，从中抽取一些数据，共计三十个，然后利用这三十个数据调用cubic spline interpolation算法，根据得到的结果验证最后的算法是否正确。<br>
二、算法.</p>
</li>
<li>
<p>读取每一个mat文件中的数值，挑选 其中特定序列的三十个数据。</p>
</li>
<li>
<p>根据数据调用cubic spline interpolation 算法，模拟得到在0处的取值，与实际值进行比较</p>
</li>
<li>
<p>根据查表可知对于20MHz的数据若采集30个信号需要-28，-26，-24，-22，-20，-18，-16，-14，-12，-10，-8，-6，-4，-2，-1,1，3,5,7，9，11,13,15,17,19,21,23,25,27,28.</p>
</li>
<li>
<p>根据上述算法，有几个问题，</p>
</li>
</ol>
<blockquote>
<p>（1）0处的值本来就不知道，如何比较<br>
（2）还是我理解错了，应该将30个插值获得56个数据，然后逐一进行比较，然后验证算法<br>
（3）利用不同的插值获得不同的数据，可以在某两点之间获得多个插值点，根据这几个插值的点对应的值，获得一个三次函数，求得对应位置的解对应于0号子信道。以师兄给我的数据为例，一共有56个数据，我可以尝试获得168个插值数据，然后因为56个数据对应有28.5信道是zero-subcarrier，1和-1两个信道对应于28和29，对应于168个插值数据对应于84,85,86.根据这三个数值可以获得一个方程的解，然后可以求出0号对应的位置即代入方程可以准确求解，然后估计zero-subcarrier的值。</p>
</blockquote>
<p>三、初步修正：<br>
因为不知道0号子载波的值，所以采用下述算法进行计算：</p>
<pre><code>1. 读取每一个mat文件中的数值，挑选 其中特定序列的三十个数据。
2. 调用cubic spline interpolation 算法，获得56组数据
3. 对比每一组数据的值，若误差不大，可以直接获得在0号子载波左右的四个
   数据，根据这四个数据列出在0号附近的模拟三次方程，解出对应0号子载波
   的值。
</code></pre>
<p>三、修正算法：</p>
<ol>
<li>
<p>对于64个subcarriers的值已知56个，对于其中，其中对应于有</p>
</li>
<li>

<table>
<thead>
<tr>
<th>number</th>
<th align="center">index</th>
<th align="center">number</th>
<th align="center">index</th>
<th align="center">number</th>
<th align="center">index</th>
<th align="center">number</th>
<th align="right">index</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td align="center">/</td>
<td align="center">17</td>
<td align="center">data</td>
<td align="center">33</td>
<td align="center">0</td>
<td align="center">49</td>
<td align="right">data</td>
</tr>
<tr>
<td>2</td>
<td align="center">/</td>
<td align="center">18</td>
<td align="center">data</td>
<td align="center">34</td>
<td align="center">data</td>
<td align="center">50</td>
<td align="right">data</td>
</tr>
<tr>
<td>3</td>
<td align="center">/</td>
<td align="center">19</td>
<td align="center">data</td>
<td align="center">35</td>
<td align="center">data</td>
<td align="center">51</td>
<td align="right">data</td>
</tr>
<tr>
<td>4</td>
<td align="center">/</td>
<td align="center">20</td>
<td align="center">data</td>
<td align="center">36</td>
<td align="center">data</td>
<td align="center">52</td>
<td align="right">data</td>
</tr>
<tr>
<td>5</td>
<td align="center">data</td>
<td align="center">21</td>
<td align="center">data</td>
<td align="center">37</td>
<td align="center">data</td>
<td align="center">53</td>
<td align="right">data</td>
</tr>
<tr>
<td>6</td>
<td align="center">data</td>
<td align="center">22</td>
<td align="center">data</td>
<td align="center">38</td>
<td align="center">data</td>
<td align="center">54</td>
<td align="right">polit</td>
</tr>
<tr>
<td>7</td>
<td align="center">data</td>
<td align="center">23</td>
<td align="center">data</td>
<td align="center">39</td>
<td align="center">data</td>
<td align="center">55</td>
<td align="right">data</td>
</tr>
<tr>
<td>8</td>
<td align="center">data</td>
<td align="center">24</td>
<td align="center">data</td>
<td align="center">40</td>
<td align="center">polit</td>
<td align="center">56</td>
<td align="right">data</td>
</tr>
<tr>
<td>9</td>
<td align="center">data</td>
<td align="center">25</td>
<td align="center">data</td>
<td align="center">41</td>
<td align="center">data</td>
<td align="center">57</td>
<td align="right">data</td>
</tr>
<tr>
<td>10</td>
<td align="center">data</td>
<td align="center">26</td>
<td align="center">polit</td>
<td align="center">42</td>
<td align="center">data</td>
<td align="center">58</td>
<td align="right">data</td>
</tr>
<tr>
<td>11</td>
<td align="center">data</td>
<td align="center">27</td>
<td align="center">data</td>
<td align="center">43</td>
<td align="center">data</td>
<td align="center">59</td>
<td align="right">data</td>
</tr>
<tr>
<td>12</td>
<td align="center">polit</td>
<td align="center">28</td>
<td align="center">data</td>
<td align="center">44</td>
<td align="center">data</td>
<td align="center">60</td>
<td align="right">data</td>
</tr>
<tr>
<td>13</td>
<td align="center">data</td>
<td align="center">29</td>
<td align="center">data</td>
<td align="center">45</td>
<td align="center">data</td>
<td align="center">61</td>
<td align="right">data</td>
</tr>
<tr>
<td>14</td>
<td align="center">data</td>
<td align="center">30</td>
<td align="center">data</td>
<td align="center">36</td>
<td align="center">data</td>
<td align="center">62</td>
<td align="right">/</td>
</tr>
<tr>
<td>15</td>
<td align="center">data</td>
<td align="center">31</td>
<td align="center">data</td>
<td align="center">47</td>
<td align="center">data</td>
<td align="center">63</td>
<td align="right">/</td>
</tr>
<tr>
<td>16</td>
<td align="center">data</td>
<td align="center">32</td>
<td align="center">data</td>
<td align="center">48</td>
<td align="center">data</td>
<td align="center">64</td>
<td align="right">/</td>
</tr>
</tbody>
</table></li>
<li>
<p>对于已知的数据，根据number of matrices and carrier grouping 可知，对于64个 数据应该是20MHz，采取Ng=2时Ns=30，即取值为</p>
<blockquote>
<p>-28, -26, -24, -22, -20, -18, -16, -14, -12, -10, -8, -6, -4, -2, -1, 1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 28.</p>
</blockquote>
<p>写出对应关系，</p>
<blockquote>
<p>28-&gt; 61 , …… , 1 -&gt; 34, -1 -&gt;32,-28-&gt;5.</p>
</blockquote>
<p>所以待抽取的数值下表应该是：</p>
</li>
</ol>

<table>
<thead>
<tr>
<th>init</th>
<th align="center">now/true</th>
<th align="center">init</th>
<th align="center">now/true</th>
<th align="center">init</th>
<th align="center">now/true</th>
<th align="center">init</th>
<th align="center">now/true</th>
<th align="center">init</th>
<th align="center">now/true</th>
</tr>
</thead>
<tbody>
<tr>
<td>28</td>
<td align="center">61/56</td>
<td align="center">15</td>
<td align="center">48/43</td>
<td align="center">1</td>
<td align="center">34/29</td>
<td align="center">-12</td>
<td align="center">21/17</td>
<td align="center">-26</td>
<td align="center">7/3</td>
</tr>
<tr>
<td>27</td>
<td align="center">60/55</td>
<td align="center">13</td>
<td align="center">46/41</td>
<td align="center">-1</td>
<td align="center">32/28</td>
<td align="center">-14</td>
<td align="center">19/15</td>
<td align="center">-28</td>
<td align="center">5/1</td>
</tr>
<tr>
<td>25</td>
<td align="center">58/53</td>
<td align="center">11</td>
<td align="center">44/39</td>
<td align="center">-2</td>
<td align="center">31/27</td>
<td align="center">-16</td>
<td align="center">17/13</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>23</td>
<td align="center">56/51</td>
<td align="center">9</td>
<td align="center">42/37</td>
<td align="center">-4</td>
<td align="center">29/25</td>
<td align="center">-18</td>
<td align="center">15/11</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>21</td>
<td align="center">54/49</td>
<td align="center">7</td>
<td align="center">40/35</td>
<td align="center">-6</td>
<td align="center">27/23</td>
<td align="center">-20</td>
<td align="center">13/9</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>19</td>
<td align="center">52/47</td>
<td align="center">5</td>
<td align="center">38/33</td>
<td align="center">-8</td>
<td align="center">25/21</td>
<td align="center">-22</td>
<td align="center">11/7</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>17</td>
<td align="center">50/45</td>
<td align="center">3</td>
<td align="center">36/31</td>
<td align="center">-10</td>
<td align="center">23/19</td>
<td align="center">-24</td>
<td align="center">9/5</td>
<td align="center"></td>
<td align="center"></td>
</tr>
</tbody>
</table><pre><code>figure 2 数值对应关系
</code></pre>
<ol start="4">
<li>根据三维插值法，需要根据30个数据获得56个数据对于算法</li>
</ol>
<blockquote>
<p>res = spline（x_a，data，xx）;<br>
x=-28, -26, -24, -22, -20, -18, -16, -14, -12, -10, -8, -6, -4, -2, -1, 1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 28.<br>
x_a可以根据f.2获得对应的数值。<br>
xx=1:1:56;是1~56对应的整数值<br>
data是对应于下标为x_a的值</p>
</blockquote>
<ol start="5">
<li>调用spline算法，获得结果，根据比较，结果相差较大，后分为实部和虚部依次处理，结果同样有较大误差，误差大到可以直接舍弃。不知道错误在那。</li>
</ol>

