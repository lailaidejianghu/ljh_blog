---
layout:     post
title:     机器学习 
category: blog
description: 
---

### 监督学习 Supervised learnin
#### 先规范符合和含义：   
* x(i)表示“输入的变量值，叫`输入特征`。
* y(i)表示”输出值”，叫`目标变量`。
* $(x^{(i)},y^{(i)})$称为一组`训练样本`。
* 一个长度为m的训练样本列表$\{(x^{(i)},y^{(i)});i=1,...,m\}$，称为`数据集`,   
  也叫一个`训练合`，其中(i)表示训练样本的索引。
* 另外，用`X`表示输入空间，`Y`表示输出空间。

#### 监督学习的定义：
监督学习的严谨定义：给定一个训练集，我们的目标是让机器学习函数h:X|->Y，使得    
评估值h(x)是真实值y的一个很好的预测，出于历史原因，函数h被叫做`假设(hypothesis)`.
```
            --------------
            |Training set|
            --------------
                  ↓ 
         --------------------
         |Learning algorithm|
         --------------------
                  ↓ 
                -----               
      x   ->    | h |     -> predicted y
                -----
```

当我们试图去预测的目标变量是连续的时候，我们称这个学习问题为`回归`问题，    
如果y只能一小部分离散的值，这个学习问题被称为`分类`问题。


### Part I 线性回归 Linear Regression

有如下数据：  
``` 
Living area| #bedrooms|Price   
-----------|----------|-----          
   2104    |     3    | 400       
   1600    |     3    | 330        
   2400    |     3    | 369        
   1416    |     2    | 232        
   3000    |     4    | 540        
   ...     |    ...   | ...        
```
现在输入特征x是$R^2$向量,$x_1^{(i)}$是第i个房屋面积，$x_2^{(i)}$是第i个房间数量,   
暂时先定两个特征。要进行监督学习，我们必须决定函数（猜想）h要以怎么样的一个计算式来表达，作为一个  
初始选择，大致将y作为x的线性函数:       
<br>
$$ h_\theta(x)=\theta_0+\theta_1*x_1+\theta_2*x_2 $$    
<br>            
这里$\theta_i$'s 是参数（也叫权重），是从X到Y的线性函数映射的空间参数，在不会混肴的情况下，用h(x)来替代
<br>$h_\theta(x)$。另外，为简化公式，设$x_0=1$,然后有如下公式：   
<br>
       $$ h(x)=\sum_{i=0}^n\theta_i*x_i=\Theta^T*X $$   
<br>
            
其中$\Theta$ 和X都是向量$R^n$,n则为特征向量X的数量。   
现在给定一个训练集，如何挑选或者学习参数$theta$的值呢，合理的方法貌似是让h(x)逼近$y_i$，至少是对于已有训练集。     
用公式来表示的话，就要定义一个函数，来衡量对于每个不同的$\Theta$的值，$h(x^{(i)})$与对应的$y^{(i)}$的距离。     
这个函数称为`成本函数`(cost function)。        
<br>
      $$ J(\theta)=\frac{1}{2}\sum_{(i=1)}^m(h_\theta(x^{(i)})-y^{(i)})^2 $$   
<br>
           

#### 最小均方算法（LMS algorithm)

我们希望选择一个让$J(\theta)$最小的 $\theta$值，怎么做呢，先使用一个搜索算法，从某个$\theta$的初始值,      
然后不断的进行调整，使得$J(\theta)$逐渐变小。我们可先考虑使用`梯度下降法`Gradient descent algorithm,     
该方法从某个$\theta$值开始，然后不断的利用如下算式进行更新：   
<br>
      $$ \theta_j:=\theta_j-\alpha*\frac{\partial}{\partial\theta_j}J(\theta) $$
<br> 
对于j=0,...,n的所有值都会同时进行如上更新，这里$\alpha$也称为`学习速率`,这个算法很自然的重复的朝着J降低最快的方
<br>
向移动。要实现这个算法，需要解决右边等号的导数项，同样的先以一组训练样本(x,y)的情况来验算：
<br>
$$
\frac{\partial}{\partial\theta_j}J(\theta)
=\frac{\partial}{\partial\theta_j}\frac{1}{2}(h_\theta(x)-y)^2
  =2*\frac{1}{2}(h_\theta(x)-y)*\frac{\partial}{\partial\theta_j}(h_\theta(x)-y) 
 =(h_\theta(x)-y)*\frac{\partial}{\partial\theta_j}(\sum_{i=0}^n\theta_ix_i-y)
 =(h_\theta(x)-y)x_j
$$
<br>
对于单组训练样本，如下给出了更新规则：

<br>
$$ \theta_j:=\theta_j+\alpha(y^{(i)}-h_\theta(x^{(i)}))x_j^{(i)} $$
<br>

这个规则称为`最小均方 LMS`(LMS,least menan squares)更新规则，也被称为`Widrow-Hoff`学习规则。<br>
这个规则有几个很直观的特性：如，更新值的大小跟误差项$y(i)-h_\theta(x(i))$成比例<br>
因此，在遇到一个训练样本,我们的预测值很接近真是值$y^{(i)}$时，就没有必要改变参数的值了。<br>
相反，如果我们的预测值$h_\theta(x^{(i)})$有较大误差时(例如，它离$y^{(i)}$很远），参数将会有大的变化。
<br>
我们只推导出只有一个训练样本的LMS规则，这里有两种方法来扩展规则使适应更多的训练样本：
<br>
第一种方法如下：
<br>
Repeat until convergence{<br>
        $\theta_j:=\theta_j+\alpha\sum_{i-1}^m(y^{(i)}-h_\theta(x^{(i)}))x_j^{(i)}$       (for every j).
<br> 
}
<br>

上面更新规则中的求和项就是$\frac{\partial}{\partial\theta_j}$，这个更新规则的每一次更新都会遍历
<br>
一遍所有训练集中的样本，所以被称为`批量梯度下降法`(batch gradient descent)。
<br>
有一个批量梯度下降法的替代方法同样也能工作得很好，算法如下：
<br>
loop{<br>
   for i=1 to m{ <br>
         $\theta_j:=\theta_j+\alpha*(y^{(i)}-h_\theta(x^{(i)}))x_j^{(i)}$    (for every j).<br>
      }<br>
   }<br>
在这个算法 中，我们重复的遍历训练集，并且每次遇到训练样本的时候，根据每一个单一训练样本
<br>
的误差来对参数进行更新，这个算法叫做`随机梯度下降法`(stochastic gradient descent)，
<br>
或者叫`增量梯度下降法(incremental gradient descent)。
<br>
如下分布给出批量梯度下降法和随机梯度下降法的python实现：
<br>
暂时略过。
  
### 法线方法 The normal equations
梯度下降法是最小化J的其中一种方法，现在讨论最小化J的第二种方法,当J为最小值时，其导数为0，因此根据导数为0求得$\theta_j$的值。

#### 矩阵导数 Matrix Derivatives
对于一个函数$f:R^{m*n}$|->$R$将m\*n的矩阵映射到实数，定义f对A的导数如下：<br>

$$
\nabla_Af(A)=\begin{bmatrix}\\
             \frac{\partial}{\partial A_{11}}&\cdots&\frac{\partial}{\partial A_{1n}}\\\\
             \vdots&\ddots&\vdots\\\\
             \frac{\partial}{\partial A_{m1}}&\cdots&\frac{\partial}{\partial A_{mn}}
            \end{bmatrix}
$$
<br>
j
因此，这个梯度$\nabla_Af(A)$本身也是一个m*n的矩阵,其中第(i,j)个元素是$\frac{\partial}{\partial A_{ij}}$.
<br>

例如有矩阵$A=\begin{bmatrix} A_{11} & A_{12} \\\\ A_{21} & A_{22} \end{bmatrix}$
<br>
定义函数$f:R^{2*2}$|->$R$为$f(A)=\frac{3}{2}A_{11}+5A_{12}2+A_{21}A_{22}$.则有$\nabla_A f(A)=\begin{bmatrix}\frac{3}{2}&10A_{12}\\\\A_{22}&A_{21}\end{bmatrix}$.
<br>

迹（trace)运算：记作`tr`,对于一个n\*n的方阵A,A的迹定义为其对角线上元素之和：
$trA=\sum_{i=1}^nA_(ii)$.
<br>
一下是迹的一些性质：
* 假设a是实数，$tra=a$. 
* 矩阵A和B,若AB是方阵，则$trAB=trBA$.更一般形式:$trABC=trCAB=trBCA$,$trABCD=trBCDA=trCDAB=trDABC$.
* $trA=trA^T$
* $tr(A+B)=trA+trB$
* $traA=atrA$

矩阵导数性质： 
* $\nabla_AtrAB=B^T$                                (1)
* $\nabla_{A^T}f(A)=(\nabla Af(A))^T$               (2)
* $\nabla_AtrABA^TC=CAB+C^TAB^T$                    (3)
* $\nabla_A|A|=|A|(A^{-1})$                     (4)
<br>
其中(4)中的A为非奇异方阵(non-singular square matrices)

#### 2.2 最小二乘法回顾 Least Squares Revisited
给定训练合，定义设计矩阵X为m\*n矩阵，这个矩阵的每一行都是训练样本的一个输入值：

<br>
$X=\begin{bmatrix}\cdots&(x^{(1)})^T&\cdots\\\\\cdots&(x^{(2)})^T&\cdots\\\\ &\vdots&\ \\\\\cdots&(x^{(m)})^T&\cdots\end{bmatrix}$
     ,其中，$x^{(i)}=\begin{bmatrix}x_0^{(i)}\\\\\vdots\\\\x_n^{(i)}\end{bmatrix}$
<br>

令$\vec y$为包含训练集所有目标值的m维向量：
<br>

$\vec y=\begin{bmatrix}y^{(1)}\\\\y^{(2)}\\\\ \vdots\\\\y^{(m)}\end{bmatrix}$
<br>

由$h_\theta(x^{(i)})=(x^{(i)})^T\theta$得，
<br>

$$
X\theta-\vec y
=\begin{bmatrix}(x^{(1)})^T\\\\ \vdots\\\\(x^{(m)})^T\end{bmatrix}-\begin{bmatrix}y^{(1)}\\\\ \vdots\\\\y^{(m)}\end{bmatrix}
=\begin{bmatrix}(x^{(1)})^T\theta-y^{(1)}\\\\ \vdots\\\\(x^{(m)})^T\theta-y^{(m)}\end{bmatrix}
=\begin{bmatrix}h_\theta(x^{(1)})-y^{(1)}\\\\ \vdots\\\\h_\theta(x^{(m)})-y^{(m)}\end{bmatrix}
$$

<br>

对于向量z，有$z^Tz=\sum_iz_i^2$,利用这个性质可推出：
<br>

$\frac{1}{2}(X\theta-\vec y)^T(X\theta-\vec y)=\frac{1}{2}\sum_{i=1}^m(h_\theta(x^{(i)})-y^{(i)})^2=J(\theta)$
<br>

最终，为了最小化J,我们来看一下关于$\theta$的导数,结合(2),(3)可得到：
<br>
$\nabla_{A^T}trABA^TC=B^TA^TC^T+BA^TC$                     (5)          
<br>
因此，

<br>
$$ 
\nabla_\theta J(\theta)
 ={\nabla_\theta\frac{1}{2}(X\theta-\vec y)^T(X\theta-\vec y)} 
 =\frac{1}{2}\nabla_\theta(\theta^TX^TX\theta-\theta^TX^T\vec y+{\vec y}^TX\theta+{\vec y}^T\vec y)
 =\frac{1}{2}\nabla_\theta tr(\theta^TX^TX\theta-\theta^TX^T\vec y+{\vec y}^TX\theta+{\vec y}^T\vec y)
 =\frac{1}{2}\nabla_\theta (tr\theta^TX^TX\theta-2tr{\vec y}^TX\theta)
 =\frac{1}{2}(X^TX\theta+X^TX\theta-2X^T\vec y)
 =X^TX\theta-X^T\vec y
$$
<br>

在第三步，我们应用了一个实数的迹就是它自身这个事实；第四步应用了$trA=trA^T$；第五步应用了等式(5)，其中$A^T=\theta,B=B^T=X^TX,C=I$和等式(1)
<br>
为了最小化J，我们使他的导数为0，并且得到法线方程(normal equations):
<br>

$$
X^TX\theta=X^T\vec y
$$

<br>
因此使$J(\theta)$最小化的$\theta$的值为：
<br>

$$
\theta=(X^TX)^{-1}X^T i\vec y
$$

<br>

#### 概率观点解释 Probabilistic interpertation
在面对回归问题时候，为什么选择线性回归，特别是最小二乘法的成本函数J是一个合理的选择呢？接下来，我们给出一系列概率
<br>
假设，基于这些假设可以很容易推出最小二乘法回归是很自然的算法。
<br>
假设目标变量和输入值存在如下等量关系：
<br>

$y^{(i)}=\theta^Tx^{(i)}+\epsilon^{(i)}$

<br>
其中，$\epsilon^{(i)}$是误差项，用来捕获未建模的变量(如有些对房价预测影响大但是在回归时忽略掉的特征)或者随机噪音信息，
<br>
进一步假设$\epsilon^{(i)}$是独立同分布的(i.i.d.,independently and identically distributed),服从高斯分布(Gaussian distribution),
<br>也叫正态分布(Normal distribution)，其均值为0，方差为$\sigma^2$.我们可以把假设写成这种形式:"$\epsilon^{(i)}$~$N(0,\sigma^2)$".$\epsilon^{(i)}$的密度函数为：
<br>

$$
p(\epsilon^{(i)})=\frac{1}{\sqrt{2\pi\sigma}}e^{-\frac{\epsilon^{(i)}}{2\sigma^T}}
$$

<br>
即
<br>

$$
p(y^{(i)}|x^{(i)};\theta)=\frac{1}{\sqrt{2\pi\sigma}}e^{-\frac{(y^{(i)}-\theta^Tx^{(i)})^2}{2\sigma^2}}
$$

记号$p(y^{(i)}|x^{(i)};\theta)$表示这是一个给定$x^{(i)}$和$\theta$参数化的$y^{(i)}$的分布。
<br>
因为$\theta$不是一个随机变量。这个$y^{(i)}$还可以写成$y^{(i)}|x^{(i)};\theta$~$N(\theta^Tx^{(i)},\sigma^2)$。
给定X（包含所有$x^{(i)}$的设计矩阵）和$\theta$，$y^{(i)}$的分布是怎样的呢？
<br>
数据的概率由$p(vec y|X;\theta)$给出。
<br>
对于给定的$\theta$，这个等式可以看作是一个$vec y$的函数(或者是X的函数)。当我们要把当作$\theta$的函数时，就称为`似然函数`(likelihood function):

<br>
$L(\theta)=L(\theta;X,vec y)=p(vec y|X;\theta)$
<br>

结合之前对于$\epsilon^{(i)}$的独立性假设（这里对$y^{(i)}$已经给定$x^{(i)}$也都作同样假设),就可以把上面等式改写为：
<br>

$$
L(\theta)=\prod_{i=1}^mP(y^{(i)}|x^{(i)};\theta)
=\prod_{i=1}^m\frac{1}{\sqrt{2\pi\sigma}}e^{-\frac{(y^{(i)}-\theta^Tx^{(i)})^2}{2\sigma^2}}
$$
<br>

现在给定了$y^{(i)}$和$x^{(i)}$关系的概率模型，用什么可行的方法来选择对参数$\theta$的最佳猜测呢？最大似然法（maximum likelihood)
<br>
告诉我们要选择能让数据的似然函数尽可能大的$\theta$，也就是说，要找到使函数$L(\theta)$最大的$\theta$值。
<br>
除了最大化$L(\theta)$，我们还可以最大化$L(\theta)$的任何严格单调递增的函数。特别的，最大化`对数似然`(log likelihood)$l(\theta)$,
<br>
它的求导会更简单一点。
<br>

$$
l(\theta)=\log{L(\theta)}
=\log\prod_{i=1}^m\frac{1}{\sqrt{2\pi\sigma}}e^{-\frac{(y^{(i)}-\theta^Tx^{(i)})^2}{2\sigma^2}}
=\sum_{i=1}^m\log\frac{1}{\sqrt{2\pi\sigma}}e^{-\frac{(y^{(i)}-\theta^Tx^{(i)})^2}{2\sigma^2}}
=mlog\frac{1}{\sqrt{2\pi\sigma}}-\frac{1}{\sigma^2}\frac{1}{2}\sum_{i=1}^m(y^{(i)}-\theta^Tx^{(i)})^2
$$

<br>
因此，最大化$l(\theta)$也同样是最小化
<br>

$$
\frac{1}{2} \sum_{i=1}^m (y^{(i)}-\theta^T x^{(i)})^2,
$$
<br>
这个式子实际上就是$J(\theta)$,也就是最原始的最小二乘成本函数。

#### 4 局部加权函数 Locally Weighted Linear Regression
考虑从实数域内取值的$x\in R$，左下角的图显示使用$y=\theta_0+\theta_1 x$来对一个数据集进行模拟。从中可看出数据的趋势
<br>
并不是严格的直线，所以用直线进行拟合不是方法。
<br>
如果我们增加一个额外的特征$x^2$，并且用$y=\theta_0+\theta_1 x+\theta_2 x^2$来拟合，（看中间的图）很明显，补充的特征越多，
<br>
效果越好，但是增加过多特征也会造成危险，右下角的图就是使用了五次多项式$y=\sum_{j=0}^5\theta_j x^j$来拟合，虽然能够完美拟合
<br>
当前数据，但是明显这不是一个适合的预测工具。简单来说左下角的图像是一个`欠拟合`(under fitting)的例子，右下角的图像是一个
`过拟合`(over fitting)的例子。
<table>
    <tr>
        <th>
            <div id="chart1" style="width: 280px;height:300px;"></div>
            <script type="text/javascript"> 
                var myChart = echarts.init(document.getElementById('chart1'));
                var data =[ [0,2.6],
                    [1,3.4],
                    [2,4.3],
                    [3,4.7],
                    [4,5],
                    [5,7.2],
                    [6,8.4],
                    [7,8.4],
                    [8,10.7],
                    [9,11.3],
                    [10,12.6]
                    ];
                        // See https://github.com/ecomfe/echarts-stat
                        var myRegression = ecStat.regression('polynomial', data, 1);
                        myRegression.points.sort(function(a, b) {
                            return a[0] - b[0];
                        });
                        option = {
                            tooltip: {
                                trigger: 'axis',
                                axisPointer: {
                                    type: 'cross'
                                }
                            },
                            title: {
                                text: '图1',
                                subtext: 'underfitting',
                                sublink: 'https://github.com/ecomfe/echarts-stat',
                                left: 'center',
                                top: 16
                            },
                            xAxis: {
                                type: 'value',
                                splitLine: {
                                    lineStyle: {
                                        type: 'dashed'
                                    }
                                },
                                splitNumber:1 
                            },
                            yAxis: {
                                type: 'value',
                                min: 0,
                                splitLine: {
                                    lineStyle: {
                                        type: 'dashed'
                                    }
                                }
                            },
                            grid: {
                                top: 90
                            },
                            series: [{
                                name: 'scatter',
                                type: 'scatter',
                                label: {
                                    emphasis: {
                                        show: true,
                                        position: 'right',
                                        textStyle: {
                                            color: 'blue',
                                            fontSize: 16
                                        }
                                    }
                                },
                                data: data
                            }, {
                                name: 'line',
                                type: 'line',
                                smooth: true,
                                showSymbol: false,
                                data: myRegression.points,
                                markPoint: {
                                    itemStyle: {
                                        normal: {
                                            color: 'transparent'
                                        }
                                    },
                                    label: {
                                        normal: {
                                            show: true,
                                            position: 'left',
                                            formatter: myRegression.expression,
                                            textStyle: {
                                                color: '#333',
                                                fontSize: 14
                                            }
                                        }
                                    },
                                    data: [{
                                        coord: myRegression.points[myRegression.points.length - 1]
                                    }]
                                }
                            }]
                        };
                myChart.setOption(option);
            </script>
        </th>
        <th>
            <div id="chart2" style="width: 280px;height:300px;"></div>
            <script type="text/javascript"> 
                var myChart = echarts.init(document.getElementById('chart2'));
                var data = [
                    [0,1.2],
                    [1,2.45],
                    [2,5],
                    [3,6.85],
                    [4,7.6],
                    [5,8.25],
                    [6,8.7],
                    [7,10.65],
                    [8,10.9],
                    [9,9.65],
                    [10,9.9]
                    ];
                        // See https://github.com/ecomfe/echarts-stat
                        var myRegression = ecStat.regression('polynomial', data, 2);
                        myRegression.points.sort(function(a, b) {
                            return a[0] - b[0];
                        });
                        option = {
                            tooltip: {
                                trigger: 'axis',
                                axisPointer: {
                                    type: 'cross'
                                }
                            },
                            title: {
                                text: '图2',
                                subtext: '',
                                sublink: 'https://github.com/ecomfe/echarts-stat',
                                left: 'center',
                                top: 16
                            },
                            xAxis: {
                                type: 'value',
                                splitLine: {
                                    lineStyle: {
                                        type: 'dashed'
                                    }
                                },
                                splitNumber:1 
                            },
                            yAxis: {
                                type: 'value',
                                min: 0,
                                splitLine: {
                                    lineStyle: {
                                        type: 'dashed'
                                    }
                                }
                            },
                            grid: {
                                top: 90
                            },
                            series: [{
                                name: 'scatter',
                                type: 'scatter',
                                label: {
                                    emphasis: {
                                        show: true,
                                        position: 'right',
                                        textStyle: {
                                            color: 'blue',
                                            fontSize: 16
                                        }
                                    }
                                },
                                data: data
                            }, {
                                name: 'line',
                                type: 'line',
                                smooth: true,
                                showSymbol: false,
                                data: myRegression.points,
                                markPoint: {
                                    itemStyle: {
                                        normal: {
                                            color: 'transparent'
                                        }
                                    },
                                    label: {
                                        normal: {
                                            show: true,
                                            position: 'left',
                                            formatter: myRegression.expression,
                                            textStyle: {
                                                color: '#333',
                                                fontSize: 14
                                            }
                                        }
                                    },
                                    data: [{
                                        coord: myRegression.points[myRegression.points.length - 1]
                                    }]
                                }
                            }]
                        };
                myChart.setOption(option);
            </script>
        </th>
        <th>
            <div id="chart3" style="width: 280px;height:300px;"></div>
            <script type="text/javascript"> 
                var myChart = echarts.init(document.getElementById('chart3'));
                var data = [
                    [0,30],
                    [1,10],
                    [1.5,1],
                    [3,16],
                    [4,18],
                    [5,19],
                    [6,19.5],
                    [7,21],
                    [8,24],
                    [9,27],
                    [10,10]
                        ];
                        // See https://github.com/ecomfe/echarts-stat
                        var myRegression = ecStat.regression('polynomial', data, 5);
                        myRegression.points.sort(function(a, b) {
                            return a[0] - b[0];
                        });
                        option = {
                            tooltip: {
                                trigger: 'axis',
                                axisPointer: {
                                    type: 'cross'
                                }
                            },
                            title: {
                                text: '图3',
                                subtext: 'overfitting',
                                sublink: 'https://github.com/ecomfe/echarts-stat',
                                left: 'center',
                                top: 16
                            },
                            xAxis: {
                                type: 'value',
                                splitLine: {
                                    lineStyle: {
                                        type: 'dashed'
                                    }
                                },
                                splitNumber:1 
                            },
                            yAxis: {
                                type: 'value',
                                min: 0,
                                splitLine: {
                                    lineStyle: {
                                        type: 'dashed'
                                    }
                                }
                            },
                            grid: {
                                top: 90
                            },
                            series: [{
                                name: 'scatter',
                                type: 'scatter',
                                label: {
                                    emphasis: {
                                        show: true,
                                        position: 'right',
                                        textStyle: {
                                            color: 'blue',
                                            fontSize: 16
                                        }
                                    }
                                },
                                data: data
                            }, {
                                name: 'line',
                                type: 'line',
                                smooth: true,
                                showSymbol: false,
                                data: myRegression.points,
                                markPoint: {
                                    itemStyle: {
                                        normal: {
                                            color: 'transparent'
                                        }
                                    },
                                    label: {
                                        normal: {
                                            show: true,
                                            position: 'left',
                                            formatter: myRegression.expression,
                                            textStyle: {
                                                color: '#333',
                                                fontSize: 14
                                            }
                                        }
                                    },
                                    data: [{
                                        coord: myRegression.points[myRegression.points.length - 1]
                                    }]
                                }
                            }]
                        };
                myChart.setOption(option);
            </script>
        </th>
    </tr>
</table>

在原始的线性回归算法中，要对一个查询点x进行预测，比如要衡量h(x)，要经过以下步骤：
1. 使用参数$\theta$进行拟合，使得$\sum_i(y^{(i)}-\theta^Tx^{(i)})^2$最小.
2. 输出$\theta^Tx$

相反的，局部加权线性回归算法的步骤如下：
1. 使用参数$\theta$进行拟合，使得加权距离$\sum_i\omega^{(i)}(y^{(i)}=\theta^Tx^{(i)})^2$最小。
2. 输出$\theta^Tx$
这里的$\omega^{(i)}$是非负的重值，很直观的，如果对于某个i的$\omega^{(i)}$特别大，那么在选择拟合参数$\theta$的       
时候，就要尽量让这一点的$(y^{(i)}-\theta^Tx^{(i)})^2$小，如果$\omega^{(i)}$小，那么这一点的$(y^{(i)}-\theta^Tx^{(i)})^2$      
的误差项在拟合过程中基本可以忽略。
较常见的权值公式是：
$$
    \omega^{(i)}=e^{(-\frac{(x^{(i)}-x)^2}{2\tau^2})}
$$
要注意，权值是依赖每个我们需要评估的的特定点x，此外，如果$|x^{(i)}-x|$值是小的，那么$\omega^{(i)}$的值趋近1，反之,         
$\omega^{(i)}$趋近0，因此，当训练样本趋近查询点x时，$\theta$拥有更高的权重。参数$\tau$控制训练样本权重随着训练样本           
和查询点x之间距离增大而衰减的速度,$\tau$被称为`带宽`参数。          

局部加权线性回归是第一个`非参数`算法的例子，无权重的线性回归算法是一种`参数`算法。因为有固定的有限数量的参数(也就是$\theta^{(i)})$）           
拟合数据。。一旦拟合了$\theta^{(i)}$'s,就将它们保存下来，我们就不需要将样本数据保存下来用于以后的预测。相反，用加权           
线性回归，我们需要保存整个样本数据。这里的非参数算法是指为了呈现假设h随数据集规模的增长而线性增长，我们需要顺序保存一些          
数据的规模。         


### Part II 分类和逻辑回归(Classification and logistic regression)
    分类问题和之前的回归问题很像，只是现在y的值局限于少数的若干个离散值。现在我们将关注的是y只有两个值，0和1的`二元`分类问题。       
    （这里讲到的大部分内容都可以扩展到多种类情况。）例如我们要建立一个垃圾邮件筛选器，那么$x^{(i)}$表示的是邮件的一些特征，         
    y取值为1表示的是垃圾邮件，其他情况y值为0,0也称为`负向类`,1称为`正向类`,有时候分别用符号'-'和'+'表示。对于给定的$x^{(i)}$          
    和对应的$y^{(i)}$也称为训练样本的`标签`。              

#### 5 逻辑回归
    忽略掉y是一个散列值，就可以用之前的线性回归算法根据给定的x来预测y,然而这样构建的例子很容易遭遇性能问题，这个方法的执行效率       
    非常低。直观来看，当已知$y\in(0,1)$候，$h_\theta(x)$的值如果大于1或者小于0就没有意义了。         
    为了解决这个问题，我们将假设$h_\theta(x)$的形式作一些改变。我们选择          
    $$
        h_\theta(x)=g(\theta^Tx)=\frac{1}{1+e^{-\theta^Tx}}
    $$
    其中，       
    $$
        g(z)=\frac{1}{1+e^{-z}}
    $$
    g(z)被称为'逻辑函数`，或者`s型函数`。如下是g(z)
