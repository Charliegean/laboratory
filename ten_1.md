---


---

<h1 id="ten-get-the-frequency">ten: get the frequency</h1>
<h2 id="charliegean-2018-12-6">charliegean 2018-12-6</h2>
<h2 id="一、资料：">一、资料：</h2>
<ol>
<li>根据上次报告即<a href="https://github.com/Charliegean/laboratory/blob/master/nine_ex_1.md">nine</a>中的内容，接下来任务是找到对应的频率，然后转换为时域，首先先考虑频率。</li>
<li>根据国内实行的802.11n标准，在5GHz附近目前只有大概十九个信道频率可供使用。具体见下表一</li>
<li>表一：国内现行在5G附近的信道及其频率分布表（单位：MHz）
<table>
<thead>
<tr>
<th align="right">信道</th>
<th align="center">中心频率</th>
<th align="center">带宽</th>
<th align="center">信道</th>
<th align="center">中心频率</th>
<th align="center">带宽</th>
</tr>
</thead>
<tbody>
<tr>
<td align="right">36</td>
<td align="center">5180</td>
<td align="center">20</td>
<td align="center"><em><strong>62</strong></em></td>
<td align="center"><em><strong>5310</strong></em></td>
<td align="center"><em><strong>40</strong></em></td>
</tr>
<tr>
<td align="right"><em><strong>38</strong></em></td>
<td align="center"><em><strong>5390</strong></em></td>
<td align="center"><em><strong>40</strong></em></td>
<td align="center">64</td>
<td align="center">5320</td>
<td align="center">20</td>
</tr>
<tr>
<td align="right">40</td>
<td align="center">5200</td>
<td align="center">20</td>
<td align="center">149</td>
<td align="center">5745</td>
<td align="center">20</td>
</tr>
<tr>
<td align="right">44</td>
<td align="center">5220</td>
<td align="center">20</td>
<td align="center"><em><strong>151</strong></em></td>
<td align="center"><em><strong>5755</strong></em></td>
<td align="center"><em><strong>40</strong></em></td>
</tr>
<tr>
<td align="right"><em><strong>46</strong></em></td>
<td align="center"><em><strong>5230</strong></em></td>
<td align="center"><em><strong>40</strong></em></td>
<td align="center">153</td>
<td align="center">5765</td>
<td align="center">20</td>
</tr>
<tr>
<td align="right">48</td>
<td align="center">5240</td>
<td align="center">20</td>
<td align="center">157</td>
<td align="center">5785</td>
<td align="center">20</td>
</tr>
<tr>
<td align="right">52</td>
<td align="center">5260</td>
<td align="center">20</td>
<td align="center"><em><strong>159</strong></em></td>
<td align="center"><em><strong>5795</strong></em></td>
<td align="center"><em><strong>40</strong></em></td>
</tr>
<tr>
<td align="right"><em><strong>54</strong></em></td>
<td align="center"><em><strong>5270</strong></em></td>
<td align="center"><em><strong>40</strong></em></td>
<td align="center">161</td>
<td align="center">5805</td>
<td align="center">20</td>
</tr>
<tr>
<td align="right">56</td>
<td align="center">5280</td>
<td align="center">20</td>
<td align="center">165</td>
<td align="center">5825</td>
<td align="center">20</td>
</tr>
<tr>
<td align="right">60</td>
<td align="center">5300</td>
<td align="center">20</td>
<td align="center"></td>
<td align="center"></td>
<td align="center"></td>
</tr>
</tbody>
</table>
</li>
</ol>
<p>注：因为试验使用的是HT20，所以所有带宽为40MHz的信道舍去，只剩下13个信道具体有36,40,44,48,53,56,60,64,149,153,157,161,165。</p>
<h2 id="二、问题：">二、问题：</h2>
<ol start="4">
<li>在使用中国剩余定理求解答案时需要用到公式（1）：t=(&lt;hi)/(2∗pi∗fi ) mod 1/fi ，根据公式（1）需要特定的频率才能求出结果。如何找出对应的信道的频率，因为对应于即使只使用中心频率也有十三个，对应于每个包如何对应，而在实验过程中共计发送了1000个包获得998组数据，又该如何对应？</li>
<li>对于合适的信道，共计有13个，每个带宽20MHz，共计260MHz，对应于时域共计1/ 0.26G * 3 * 10^8 = 3/2.6  =    1.153846,得到的范围会超过一米。根据paper需要自己定义跳频协议，我不是很明白。</li>
<li>在解决phase offset时，每组试验需要两个csi包括接收方和发送方，但是我们试验时使用inject方法，只在接收端获得了数据，如何找到发送方的csi数据？</li>
<li>computing multipath profiles留待后续</li>
</ol>

