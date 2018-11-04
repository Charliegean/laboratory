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
<p>三、修正算法：</p>
<ol>
<li>对于64个subcarriers的值已知56个，对于其中，其中对应于有</li>
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
</ol>

