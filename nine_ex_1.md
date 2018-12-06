---


---

<h1 id="nine_first_try">nine_first_try</h1>
<p>charliegean 2018-11-25</p>
<h2 id="一、目标：">一、目标：</h2>
<p>根据试验测出的数据，获取对应的csi，根据csi利用三维插值法求出zero-subcarrier，然后求出其对应的频率，获得LCM（假设其没有multipath和phase offset），然后求出TOF</p>
<h2 id="二、方法">二、方法</h2>
<ol>
<li>现行的802.11协议的频率是2.4GHz~5GHz，我是用的是频率是5GHz附近，频率间隔是20MHz。</li>
<li>试验采取每组距离发送1000个包，每个包receiver获得998组数据，然后每组数据包含一个包含一个结构体，然后可以根据这个结构获得三组天线对应30个信道的csi，其信道对应结果见<a href="https://github.com/Charliegean/laboratory/blob/master/six_verification.md">report_six</a> 。然后利用三维插值法模拟器其角度求出zero-subcarrier的角度，具体可见<a href="https://github.com/Charliegean/laboratory/blob/master/eight.md">report_seven</a>。每组数据获得三个天线对应的zero-subcarrier的角度，然后对于每个天线每组数据共可以获得998个zero-subcarriers。</li>
<li>取a天线为例说明接下来的数据处理，b，c同理。然后根据论文中讲的处理t的方法，有公式（1）：t=(&lt;hi)/(2∗pi∗fi ) mod  1/fi ，可以计算出t。</li>
</ol>
<blockquote>
<p>1、预处理数据，获得A组30个子信道的csi；<br>
2、利用插值法求出0号子信道的csi角度即公式（1）中需要的&lt;hi；<br>
3、找出对应的fi（不会，具体见问题）<br>
4、利用公式（1）获得t</p>
</blockquote>
<ol start="4">
<li>对于每一个天线，我们可以获得998组满足公式（1），使用中国剩余定理解决的话，我提出一个假设解：所有的值保留适当的位数设为m，保证所有的使用的值小数点之后的位数相同均为m，然后左右同时乘于10^m变成自然数，利用中国剩余定理求解之后获得待求的时间t，然后除以10 ^m即可获得目标t。</li>
<li>paper给出的利用NDFT求解的算法我没看懂。</li>
</ol>
<h2 id="三、问题：">三、问题：</h2>
<ol start="6">
<li>根据3中的公式，我们首先需要确定fi，那么fi是自己定义的协议选择频率还是既定的频率，若是前者，如何定义协议，若是后者，会引出问题7.或者我理解出现错误，每一个数据都是用的同一组频率，或者分段每段的频率是相同的。</li>
<li>根据现行的IEEE802.11n协议，我查到在全球各地的5G信道，再国内大概只有19个频率可用，如何确定每个包发送时使用的频率以满足公式（1）的需要求t。<br>
世界各个地区5G信道一览表：<br>
<img src="https://github.com/Charliegean/laboratory/blob/master/picture/nine/wifi5GHz.jpg" alt="fig1"></li>
</ol>
<h2 id="四、代码">四、代码</h2>
<pre><code>clear;
clc;
csi_trace=read_bf_file('../data1_lu/008.dat');%读取data
csi_entry = csi_trace{121};%预处理
csi = get_scaled_csi(csi_entry);%get csi
csi_a =  squeeze(csi(1,1,:));
csi_b =  squeeze(csi(1,2,:));
csi_c =  squeeze(csi(1,3,:));%分别取出三个天线对应的csi
%ang_a = unwrap(angle(csi_a),pi/2);
%ang_b = unwrap(angle(csi_b),pi/2);
%ang_c = unwrap(angle(csi_c),pi/2);%使用unwrap获得angle
ang_a = angle(csi_a);
ang_b = angle(csi_b);
ang_c = angle(csi_c);%不使用unwrap获得angle
x= 1:1:30;
xx = 0.01:0.01: 56;
res_a =  interp1(x,ang_a,xx,'spline','extrap');
res_b =  interp1(x,ang_b,xx,'spline','extrap');
res_c =  interp1(x,ang_c,xx,'spline','extrap');
%res_csi_a = mod(res_a(2850),pi/2);
%res_csi_b = mod(res_b(2850),pi/2);
%res_csi_c = mod(res_c(2850),pi/2);
res_csi_a = mod(res_a(2850),pi);
res_csi_b = mod(res_b(2850),pi);
res_csi_c = mod(res_c(2850),pi);%分别求出对应的zero-subcarrier
</code></pre>

