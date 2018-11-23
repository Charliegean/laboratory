---


---

<h1 id="plan——nine">Plan——nine</h1>
<p>charliegean 2018-11-23</p>
<h3 id="一二是之前写的计划三是接下来我对工作的一个认识">一二是之前写的计划三是接下来我对工作的一个认识</h3>
<h2 id="一、处理过程">一、处理过程</h2>
<p>第一步：处理实验数据，获得三个天线的CSI</p>
<p>第二步：获取每组数据的zero-subcarriers的phase，方法（cubic spline interpolation)</p>
<p>第三步：resolving phase offset（方法直接CSIrx 与CSItx相乘）</p>
<p>第四步：获得TOF（方法，利用上步得到的数据处理，得到time-power图像，获得第一个peak）</p>
<p>第五步：获得distance 和location（方法：利用三个distance获得location）</p>
<h2 id="二、具体数据类型">二、具体数据类型</h2>
<p>1、试验获得的直接数据是的n*1cell数据</p>
<p>2、利用插值法，即cubic spline interpolation求出zero-subcarriers missing phase然后可以获得csi: [1×3×30 double]，包括三个antenna的csi数据，输入是n*1 cell，输出 csi: [1×3×30 double]。</p>
<p>3、利用2获得的 csi: [1×3×30 double]数据（应该是两个包括CSIrx和CSItx），将对应天线的对应数据相乘，获得h^2数据，输入是两组 csi: [1×3×30 double]，输出是一组 [1×3×30 double]数据。</p>
<p>4、利用3中[1×3×30 double]画出power-time profile，输入是 一组 [1×3×30 double]，输出应该是TOF*2。</p>
<p>5、利用4中获得的TOF*2获得distance，利用三组distance计算得到location。输入三个TOF，输出，三个距离以及一个坐标（相对于三组antenna）。</p>
<h2 id="三、接下来的工作">三、接下来的工作</h2>
<p>根据之前所做的工作，我已经获得了zero-subcarrrier的值，根据论文中的处理过程，下一步处理假设单路径的TOF，处理方法：根据一组数据（或者继续采用模拟数据），假设其是单路径的，然后根据多组数据的zero-subcarrier值求出LCM（least common multiple）将排列获得TOF。</p>

