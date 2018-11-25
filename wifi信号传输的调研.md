---


---

<h1 id="wifi信号传输的调研">WiFi信号传输的调研</h1>
<p>charliegean 2018-11-25</p>
<h2 id="一、目的：">一、目的：</h2>
<p>研究chronos中，对于整个系统模块间传递的信号形式有一定的了解。对现行的wifi AP 与client之间传输信号的形式调研。</p>
<h2 id="二、wifi是什么：">二、wifi是什么：</h2>
<p>wifi是一种允许电子设备连接到WLAN的技术，由WI-FI联盟所有，目的是改善基于IEEE802.11标准的无线网路产品之间的互通性。无线网络在无线局域网的范畴是指“无线相容性认证”，实质上是一种商业认证，同时也是一种无线联网技术。WIFI相较于蓝牙数据安全性和传输质量较低，但是传输速度很快。</p>
<h2 id="三、wi-fi的组成结构：">三、WI-FI的组成结构：</h2>
<p>包括硬件设备和WIF协议，一般架设无线网络的基本配备是无线网卡以及一台AP<br>
<strong>硬件方面：</strong></p>
<blockquote>
<p>通信接口方面：一般多采用USB接口，也包括PCIE和SDIO接口。<br>
供电方面：一般是直接供电或者利用主板中的电源供电。<br>
天线的处理形式：内置的PCB板载天线或者陶瓷天线，也可以采用I-PEX接头，链接天线延长线，然后天线外置。<br>
与主板链接的形式：直接SMT或者通过2.54的排针作为插件。</p>
</blockquote>
<p><strong>网络协议</strong>：</p>
<blockquote>
<p>一个WI-FI链接点网络和结构站点是网络最基本的组成部分。基本服务单元（BSS）是网络最基本的服务单元，最简单的服务单元可以只有两个站点组成，站点可以动态的联结(associate)到基本服务单元中。分配系统(DS)用于链接不同的基本服务单元，接入点（AP）即有普通站点的身份，也有接入到分配系统的功能。扩展服务单元（ESS）有分配系统和基本服务单元组成，这种组合是逻辑上的。关口（Portal)是一个逻辑成分，用于将无线局域网和有限局域网或其他网络联系起来。</p>
</blockquote>
<h2 id="三、ieee802.11的功能">三、IEEE802.11的功能</h2>
<p>IEEE802.11只负责在站点使用的无线网络的媒介上的寻址，而且没有具体定义分配系统，只定义了分配系统应该提供的服务（Service),共包括九种：五种服务属于分配系统的工作，具体有：联接(Association)，结束联接(Disassociation)，分配(Distribution)，集成(Integration)，再联接(Reassociation)。四种服务属于站点的任务，具体有鉴权(Authentication)，结束鉴权(Deauthentication)，隐私(Privacy)，MAC数据传输(MSDU delivery)。</p>
<h2 id="四、802.11系列频率：">四、802.11系列频率：</h2>
<p><a href="https://www.radio-electronics.com/info/wireless/wi-fi/80211-channels-number-frequencies-bandwidth.php">Wi-Fi / WLAN Channels, Frequencies, Bands &amp; Bandwidths</a></p>

