# 核密度估计KDE

### 1.参数估计

先假设数据属于某个分布，在估计这个分布的参数。

### 2.非参数估计

不需要先验知识。核密度估计就属于非参估计。



### 直方图到核密度估计

kernel dentisy estimation核密度估计，是通过样本估计其概率密度。

使用直方图可以直观的估计概率，但是：

- 密度函数不平滑，受宽度影响大
- 只能展示二位数据
- 如果让宽度极限趋近0，就会使得没有出现过的数据概率为0 ，密度函数不连续。

因此：核密度估计需要一个合理的邻域大小。

有分布函数和概率密度和概率的定义：

![image-20231026150805443](C:/Users/1649019876/AppData/Roaming/Typora/typora-user-images/image-20231026150805443.png)

![image-20231026150831065](C:/Users/1649019876/AppData/Roaming/Typora/typora-user-images/image-20231026150831065.png)

那么可以推导分布函数和概率密度的相互转换：

![image-20231026150915966](C:/Users/1649019876/AppData/Roaming/Typora/typora-user-images/image-20231026150915966.png)

或者用N表示样本数：

![img](https://img-blog.csdnimg.cn/20200712233224243.png)

某点x0的概率密度用极小范围h内的分布函数差值表示。

分布函数可以通过经验得到：

![image-20231026151016076](C:/Users/1649019876/AppData/Roaming/Typora/typora-user-images/image-20231026151016076.png)

该公式表示n次观测中$x_i \leq t$出现的次数和n的比值。即通过试验近似概率P($x \leq t$),即F(t)。



把该式带入概率密度（很好推）：

![image-20231026151212371](C:/Users/1649019876/AppData/Roaming/Typora/typora-user-images/image-20231026151212371.png)

h值是带宽，实际中需要比较小来满足趋近于0的条件，但也不能太小否则区间里的估计样本不够。确定带宽后去除极限值：

![image-20231026151611581](C:/Users/1649019876/AppData/Roaming/Typora/typora-user-images/image-20231026151611581.png)

将该式变形用函数K来表达试验，K有多种选择方案：

![image-20231026151542174](C:/Users/1649019876/AppData/Roaming/Typora/typora-user-images/image-20231026151542174.png)

若$0\leq \frac{|x-x_i|}{h} \leq 1$则K=1。令这个单元为t：

![image-20231026151909128](C:/Users/1649019876/AppData/Roaming/Typora/typora-user-images/image-20231026151909128.png)

需要保证概率密度积分为1：

![image-20231026152021286](C:/Users/1649019876/AppData/Roaming/Typora/typora-user-images/image-20231026152021286.png)



![image-20231026152035268](C:/Users/1649019876/AppData/Roaming/Typora/typora-user-images/image-20231026152035268.png)



因此，核函数K0只需要也是个概率密度函数就可以了，就能保证估计的概率密度是连续的。

### 核密度函数

![img](https://img-blog.csdnimg.cn/20200713102355247.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTkxMDcxMQ==,size_16,color_FFFFFF,t_70)

一些核函数：

![img](https://img-blog.csdnimg.cn/20200713102459396.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTkxMDcxMQ==,size_16,color_FFFFFF,t_70)



从上面讲述的得到的是样本中某一点的概率密度函数，那么整个样本集应该是怎么拟合的呢？将设有N个样本点，对这N个点进行上面的拟合过后，将这N个概率密度函数进行叠加便得到了整个样本集的概率密度函数。例如利用高斯核对X={x1=−2.1,x2=−1.3,x3=−0.4,x4=1.9,x5=5.1,x6=6.2} 六个点的“拟合”结果如下：
![img](https://img-blog.csdnimg.cn/20200713104255676.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTkxMDcxMQ==,size_16,color_FFFFFF,t_70)

使用高斯核，则$x_i$为正态分布的均值，方差为带宽，由h决定。
