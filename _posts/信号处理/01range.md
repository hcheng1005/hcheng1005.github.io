---
title: 距离解算
category: 信号处理
order: 1
---
<img src="{{site.url}}/images/bg1.png"/>

毫米波 (mmWave) 是一类使用短波长电磁波的特殊雷达技术。雷达系统发射的电磁波信号被其发射路径上的物体阻挡继而会发生反射。通过捕捉反射的信号，雷达系统可以确定物体的**距离**、**速度**和**角度**。

Key words:

1. 带宽
2. 脉宽
3. 距离分辨率

- - -
#### 距离测量
在雷达系统中，其基本概念是指电磁信号发射过程中被其发射路径上的物体阻挡进行的反射。FMCW雷达系统所用信号的频率随时间变化呈线性升高。这种类型的信号也称为**线性调频脉冲**。图1以幅度（振幅）相对时间的函数，显示了线性调频脉冲信号表示。
<div align=center>
<img src="{{site.url}}/images/range-01.png" width="300" height="200" div align=center />
</div>

图2为同一个线性调频脉冲信号（频率作为时间的函数）。该线性调频脉冲具有**起始频率 (fc)**、**带宽(B)**和**持续时间(Tc)**。该线性调频脉冲的斜率(S)捕捉频率的变化率。在例子中图2提供的示例中，fc = 77 GHz，B = 4 GHz，Tc = 40 µs，S = 100 MHz/µs.
<div align=center>
<img src="{{site.url}}/images/range-02.png" width="300" height="200" />
</div>

雷达TX脉冲在遇到目标时会反射回接收机，混频器通过将RX和TX信号合并到一起，生成一个**中频(IF)信号**，通过计算中频信号的频率即可得出目标的距离位置（这里暂时假定不存在相对速度）。
<div align=center>
<img src="{{site.url}}/images/range-03.png" width="300" height="200" />
</div>

由图可知:

$$ \tau =\frac{2d}{c} $$

其中d是与被检测物体的距离，c是光速。
根据三角函数关系可得：

$$ \frac{f_0}{\tau} = \frac{B}{T_c} $$

因此可得:

$$ d = \frac{f_0c}{2s}$$

因此只要计算出差频$f_0$即可得出目标的距离。
另外，IF信号的初始相位($\varphi_0$)是IF信号起点对应的时间点的TX线性调频脉冲相位与RX线性调频脉冲相位之差。

$$ \varphi_0 = 2pif_c\tau $$

可以得出：

$$ \varphi_0 = \frac{4pid}{\lambda} $$

总结：对于与雷达相距d的物体，IF信号将是一个正弦波：

$$ Asin(2pif_0t+\varphi_0) $$

其中$ f_0 = \frac{S2d}{c} $和$ \varphi_0 = \frac{4pid}{\lambda} $

#### 距离分辨率
距离分辨率是辨别两个或更多物体的能力。当两个物体靠近到某个位置时，雷达系统将不再能够将二者区分开物体。傅里叶变换理论指出，通过延长IF信号，可以提高分辨率。而延长IF信号，会按比例增加带宽。
同时、傅里叶变换理论指出，观测窗口(T)可以分辨间隔超过1/THz的频率分量。因此，当两个频率频差满足如下关系时，便可以分辨出来：

$$ \Delta f > \frac{1}{T_c} $$

其中Tc是观测时间长度。
由于

$$ \Delta f = \frac{S2\Delta d}{c} $$

可得

$$ \Delta d>\frac{c}{2ST_C}=\frac{c}{2B}  (由于B = STc)$$

因此距离分辨率$d_{Res}$仅取决于系统的带宽：

$$ d_{res} = \frac{c}{2B} $$








