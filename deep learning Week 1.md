# Week 1
## 什么是神经网络
![](https://i.imgur.com/id3hmBA.png)
-  ReLU激活函数（ Rectified Linear Unit）

> 这是最简单的神经网络。其实这个小圆圈就是一个单独的神经元。接着你的网络实现了左边这个函数的功能。 

![](https://i.imgur.com/Z0gB47a.png)

> - 房屋价格预测：
>   - 房子尺寸、卧室数量-》一家人的数量
>   - 邮政编码-》步行化程度
>   - 邮政编码-》富裕程度相关
>   - 总结：基于房屋面积和卧室数量，可以估算家庭人口，基于邮编，可以估测步
行化程度或者学校的质量。最后你可能会这样想，这些决定人们乐意花费多少钱。 
对于一个房子来说，这些都是与它息息相关的事情。在这个情景里，家庭人口、步行化
程度以及学校的质量都能帮助你预测房屋的价格
> - 画的小圆圈都可以是 ReLU 的一部分，也就是指修正线性单元

![](https://i.imgur.com/2SoZuAK.png)
> - 神经网络的一部分神奇之处在于，当你实现它之后，你要做的只是输入𝑥，就能得到输出𝑦。因为它可以自己计算你训练集中样本的数目以及所有的中间过程。
> - 隐藏单元圆圈，在一个神经网络中，它们每个都从输入的四个特征获得自身输入，比如说，第一个结点代表家庭人口，而家庭人口仅仅取决于x1和x2特征，换句话说，在神经网络中，你决定在这个结点中想要得到什么，然后用所有的四个输入来计算想要得到的。
> - 神经网络给予了足够多的关于𝑥和𝑦的数据，给予了足够的训练样本有关x和y。神经网络非常擅长计算从𝑥到𝑦的精准映射函数。 

## 用神经网络进行监督学习
![](https://i.imgur.com/LN9YsAE.png)
> - 预测你是否会点开这个广告，通过向用户展示最有可能点开的广
告
> - 输入一个图像，然后想输出一个索引，范围从 1 到 1000 来试着告诉你这张照片
> - 音频片段输入神经网络，然后让它输出文本记录
> - 机器翻译，输入英语句子，接着输出一个中文句子。 
> - 自动驾驶技术，训练一个神经网络，来告诉汽车在马路上面具体的位置，这就是神经网络在自
动驾驶系统中的一个关键成分

> - 对于图像应用，我们经常在神经网络上使用卷积（Convolutional Neural Network）
> - 对于序列数据，例如音频，有一个时间组件，随着时间的推移，音频被播放
出来，所以音频是最自然的表现。作为一维时间序列.对于序列数据，经常使用 RNN，一种递归神经网（Recurrent Neural Network）语言，英语和汉语字母表或单词都是逐个出现的，所以语言也是最自然的序列数据

![](https://i.imgur.com/VK0kfF5.png)
![](https://i.imgur.com/arwoXI4.png)
> - 左图：标准的神经网络
> - 右图：卷积神经网络
> - 下图: 递归神经网络(RNN)

![](https://i.imgur.com/DduSeJQ.png)
- 结构化数据：基本数据库，对于信息都有一个定义
- 非结构化数据：音频，原始音频或者你想要识别的图像或文本中的内容。这里的特征可能是图像中的像素值或文本中的单个单词。 

> - 多亏了深度学习和神经网络，计算机现在能更好地解释非结构化数据，这是与几年前相比的结果，这为我们创造了机会。
> - 神经网络算法对于结构化和非结构化数据都有用处。 

## 为什么深度学习会兴起？
![](https://i.imgur.com/hbKFwXi.png)
> - 水平轴上画一个形状，在此绘制出所有任务的数据量，而在垂直轴上，画出机器学习算法的性能。
> - 一个传统机器学习算法的性能画出来，作为数据量的一个函数，你可能得到一个弯曲的线，就像图中这样，它的性能一开始在增加更多数据时会上升，但是一段变化后它的性能就会像一个高原一样。假设你的水平轴拉的很很长，它们不知道如何处理规模巨大的数据，而过去十年的社会里，我们遇到的很多问题只有相对较少的数据量。
> -  神经网络展现出的是，如果你训练一个小型的神经网络，那么这个性能可能会像下图黄色曲线表示那样；如果你训练一个稍微大一点的神经网络，比如说一个中等规模的神经网络（下图蓝色曲线），它在某些数据上面的性也会更好一些；如果你训练一个非常大的神经网络，它就会变成下图绿色曲线那样，并且保持变得越来越好。
> - 可以注意到两点：如果你想要获得较高的性能体现，那么你有两个条件要完成
>  - 训练一个规模足够大的神经网络，以发挥数据规模量巨大的优点
>  - 画到x轴的这个位置，所以你需要很多的数据
>  - 如今最可靠的方法来在神经网络上获得更好的性能，往往就是要么训练一个更大的神经网络，要么投入更多的数据，这只能在一定程度上起作用，因为最终你耗尽了数据，或者最终你的网络是如此大规模导致将要用太久的时间去训练

# Week 2
> - 这周我们将学习神经网络的基础知识，其中需要注意的是，当实现一个神经网络的时候，我们需要知道一些非常重要的技术和技巧。例如有一个包含m个样本的训练集，你很可能习惯于用一个 for 循环来遍历训练集中的每个样本，但是当实现一个神经网络的时候，我们通常不直接使用 for 循环来遍历整个训练集，所以在这周的课程中你将学会如何处理训练集。
> - 在神经网络的计算中，通常先有一个叫做前向暂停(forward pause)或叫做前向传播(foward propagation)的步骤，接着有一个叫做反向暂停(backward pause) 或叫做反向传播(backward propagation)的步骤。所以这周我也会向你介绍为什么神经网络的训练过程可以分为前向传播和反向传播两个独立的部分。 


## 二分分类
> 首先我们从一个问题开始说起，这里有一个二分类问题的例子，假如你有一张图片作为输入，比如这只猫，如果识别这张图片为猫，则输出标签 1 作为结果；如果识别出不是猫，那么输出标签 0 作为结果。现在我们可以用字母𝑦来表示输出的结果标签，如下图所示： 

![](https://i.imgur.com/fE27PBK.png)
> - 为了把这些像素值放到一个特征向量中，我们需要把这些像素值提取出来，然后放入一个特征向量x。如果图片的大小为 64x64 像素，那么向量x的总维度，将是 64 乘以 64 乘以 3，这是三个像素矩阵中像素的总量。在这个例子中结果为 12,288。
> - 在二分类问题中，我们的目标就是习得一个分类器，它以图片的特征向量作为输入，然后预测输出结果y为 1 还是 0，也就是预测图片中是否有猫。

![](https://i.imgur.com/sTD3q8f.png)
> - 符号定义
>  - x：表示一个nx维数据，为输入数据，维度为(nx,1)；  
>  - y：表示输出结果，取值为(0,1)；
>  - (x（i）,y（i）)：表示第𝑖组数据，可能是训练数据，也可能是测试数据，此处默认为训练数据；
>  - X = [x(1),x(2),...,x(m)]：表示所有的训练数据集的输入值，放在一个 nx × m的矩阵中，其中m表示样本数目;  
>  - Y = [y(1),y(2),...,y(m)]：对应表示所有训练数据集的输出值，维度为1 × m。 
>  - 用一对(x,y)来表示一个单独的样本，x代表nx维的特征向量，𝑦 表示标签(输出结果)只能为 0 或 1。
>  - 训练集将由𝑚个训练样本组成，其中(𝑥(1),𝑦(1))表示第一个样本的输入和输出，(𝑥(2),𝑦(2))表示第二个样本的输入和输出，直到最后一个样本(𝑥(𝑚),𝑦(𝑚))，然后所有的这些一起表示整个训练集。有时候为了强调这是训练样本的个数，会写作𝑀𝑡𝑟𝑎𝑖𝑛，当涉及到测试集的时候，我们会使用𝑀𝑡𝑒𝑠𝑡来表示测试集的样本数
>  - 𝑋是一个规模为𝑛𝑥乘以𝑚的矩阵，当你用 Python 实现的时候，你会看到 X.shape，这是一条 Python 命令，用于显示矩阵的规模，即 X.shape 等于(𝑛𝑥,𝑚)
>  - 标签𝑦放在列中将会使得后续计算非常方便，所以我们定义大写的𝑌等于𝑦(1),𝑦(𝑚),...,𝑦(𝑚)，所以在这里
是一个规模为 1 乘以𝑚的矩阵，同样地使用 Python 将表示为 Y.shape 等于(1,𝑚)

## logistic回归
![](https://i.imgur.com/5PUYPua.png)
> - 逻辑回归的 Hypothesis Function（假设函数）。 
> - 对于识别一张猫，你希望输出0代表不是猫，输出1代表是猫。如果要用一个算法来实现这个预测，我们实际上是通过预测^y=1的概率（前提条件是给定了输入特征𝑋）
> - 不同符号意义：
>  - X是一个nx维的向量
>  - w表示逻辑回归的参数
>  - b是一个实数（表示偏差）
> - 从理论上来讲，预测函数为^y=wTx+b，因为^y计算出来比1大得多，或者为一个负值，这对我们所要预测的概率是无意义的。因此，在逻辑回归中，y^因该是由上述的线性函数式子作为自变量的**sigmoid**函数中，将线性函数转换为非线性函数。 
> - 由**sigmoid**函数可知，当z非常大时，^y会趋近于1；相反，当z非常小时，^y会趋近于0.因此，在我们实现逻辑回归时，要让机器学习参数w以及b，这样蔡使得^y成为对y=1这一情况的概率的一个很好的估计。

## logistic回归代价函数（Logistic Regression Cost Function） 
![](https://i.imgur.com/WnPwWMh.png)
> - 为什么需要**代价函数**：
>   - 训练逻辑回归模型的参数参数w和参数b，需要一个代价函数，通过训练代价函数来得到参数w和参数b
> - 上述公式中的y^(i)指的是一个训练样本（带有圆括号的上标来区分索引和样本），训练样本i所对应的预测值是y（i）,是用训练样本的^y=wTx+b然后通过 sigmoid 函数来得到，上标(𝑖)来指明数据表示𝑥或者𝑦或者𝑧或者其他数据的第𝑖个训练样本，这就是上标(𝑖)的含义。 
> - 为什么需要**损失函数**？
>  - 损失函数又叫做误差函数，用来衡量算法的运行情况，Loss function:L(^y,y). 
>  - 通过L，来预测输出值和实际值有多接近
>  - 一般情况下，我们用预测值和实际值的平方差或者他们平方差的一般，但是逻辑回归中我们不这样做，因为
当我们在学习逻辑回归参数的时候，会发现我们的优化目标不是凸优化，只能找到多个局部最优值，梯度下降法很可能找不到全局最优值
>  - 逻辑回归中用到的损失函数是（可使优化目标变成凸函数）：
>        ![](https://i.imgur.com/MoWquBX.png)
>     - 在平方误差作为损失函数时，我们尽可能地让误差减小，对于这个逻辑回归损失函数，我们也尽量让它小
>        ![](https://i.imgur.com/kNdGwUZ.png)
>     - 总的来说，这个误差函数预测的值，当越接近目标值时，误差结果就越小，则达到了损失函数的功能
>     - 损失函数是在单个训练样本中定义的，它衡量的是算法在单个训练样本中表现如何
>   - 定义一个代价函数：
>    - 作用：为了用来衡量我们的算法（假设函数）的性能如何，即对训练样本的预测结果。
>    - 算法的代价函数是对𝑚个样本的损失函数求和然后除以𝑚: 
>        ![](https://i.imgur.com/XoxuuZJ.png)
>   - **代价函数**和**损失函数**的区别
>    - 损失函数适用于单个训练样本
>    - 代价函数是参数的总代价
>    - 总结：针对代价函数，在训练逻辑回归模型时，需要找到合适的w和b，来使函数J的总代价降到最低
   
## 梯度下降算法（Gradient Descent）
![](https://i.imgur.com/OfvTFt2.png)
> - 梯度下降算法的作用？
>  - 由于成本函数J（w，b）可以用来衡量参数w和b的性能，所以通过J（w，b）来训练参数w和b。梯度下降算法就是不断地更新参数w和b，从而Minimize{J（w，b）}，来求得最优参数w和b
> - 由上图可得，横轴代表空间参数w和b，在实践中，w多数情况下是高维度的，在这里为了更好地绘图，将w和b都定义为单一实数
> - 代价函数J（w，b）是一个凸函数。这是我们通过改变**损失函数**所转化而来的，若按照最初平方差来定义损失函数，那么所得到的代价函数将是一个凹凸不平的曲线，那么将无法取得全局最优值。
> - 在初始化w和b时，任意取值均可，从任意一点开始，通过梯度下降算法后，都将达到大致相同的一点。
>   - 梯度下降算法过程：
>    - 选取初始化点
>    - 朝最陡的下坡方向走一步，不断地迭代 
>    - 直到走到全局最优解或者接近全局最优解的地方 


![](https://i.imgur.com/PP4tXTu.png)

> ![](https://i.imgur.com/XddgVLl.png)
> ：=表示更新参数
> α表示学习率（learning rate），用来控制步长
> dJ（w）/dw就是函数J（w）对w求导，为斜率，在代码中我们常用dw代表这个值
> 函数图像说明，当斜率<0时，那么w将向右走；当斜率>0时，w将向左走。整个梯度下降法的迭代过程就是不断地向左（右）走，直至逼近最小值点。 

****
> ![](https://i.imgur.com/T6ev88L.png)
> - ∂表示偏导符号。![](https://i.imgur.com/jwaJBFu.png)，就是函数J（w,b）对w求偏导。在代码中，我们用dw表示这个结果。小写字母d用在函数只有一个参数的求导