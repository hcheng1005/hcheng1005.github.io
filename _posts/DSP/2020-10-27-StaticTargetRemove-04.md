---
layout: post
title: 静态目标剔除
category: 'DSP'
order: 4
---

本小节介绍如何进行**静态目标剔除**。

$$ X_{nr} = \frac{1}{N}\sum_{c=1}^{N_{c}}X_{ncr} $$

- - -

<br>
### **处理流程一览**

<div align=center>
<img src="{{site.url}}/images/static-01.png" div align=center />
</div>

<br>
基于上图的处理流程，可以大致将**静态剔除算法**分为以下步骤：

1 首先对所有chirp进行距离维FFT；

2 每个距离维点（point）减去该点所有chirp的均值（mean）；

3 对该点的所有chirp数据再次进行FFT计算（Doppler—FFT）；

4 该二维频谱图即剔除静态目标后的RDM（Range_Doppler_MAP）

<br>
**部分代码如下**
```matlab
% Static cluster Removal
for i=1:8
	% calculate meanValue
	for j=1:Range_FFT_N
		staticmeandata(j,i) = mean(rec1_data(j,1:Velocity_FFT_N,i));
	end
	% subtract meanValue
	for k=1:Velocity_FFT_N
		rec1_data(1:Range_FFT_N,k,i) = rec1_data(1:Range_FFT_N,k,i) -  staticmeandata(1:Range_FFT_N,i) ;
	end
end
```

结果如下：

<div align=center>
<img src="{{site.url}}/images/static-02.png" div align=center />
</div>

<br>
**参考资料**

[1. PeopleCounting]({{site.url}}/pdfs/People Tracking and Counting Reference Design Using mmWave Radar Sensor.pdf)





