## ML Model Production
1. 处理missing data
	1. 缺失值比较严重
		- 严重缺失的阈值: 10%
		- 删除该特征以避免该特征引入较大的niose，降低了variance
		- 将该特征值转化为categorical类型的特征，例如salary_change这一特征可以转化为布尔型的有或者没有
	2. 缺失值并不是很严重
		- 将缺失值作为单独的一个数字/类型来处理
		- 使用均值/众数/中位数进行填充
		- 使用前一个/后一个数值进行填充
		- 使用插值法进行填充
		- 利用模型进行填充：有一个根本缺陷，如果其他变量和缺失变量无关，则预测的结果无意义。如果预测结果相当准确，则又说明这个变量是没必要加入建模的。
		- 有的模型能够自动handle缺失值：以非missing value切割，然后分别尝试missing value走左分支还是右分支，选择gain最大的(Xgboost)
		- EM(期望最大化)
		- 把变量映射到高维空间。比如性别，有男、女、缺失三种情况，则映射成3个变量：是否男、是否女、是否缺失。连续型变量也可以这样处理，先将连续变量离散化，然后添加新的确实类别的dummy。把变量映射到高维空间。比如性别，有男、女、缺失三种情况，则映射成3个变量：是否男、是否女、是否缺失。连续型变量也可以这样处理。
2. categorical features如何处理
	1. One-Hot Encoding:
		- 优点: easy
		- 缺点: 容易产生维度灾难和稀疏矩阵
		- 注意: 在对共线性敏感的模型里使用的时候需要保证自由度为N-1，否则会产生共线性问题
	2. Label-Encoding：
		- 优点:易于理解
		- 缺点:将不同类别编码为1...N之后会有个问题，实际上类别之间是没有关系的，但model会认为他们有关系
		- 注意: 暂无
	3. Target-Encoding:
		- 用于处理high-categorical特征
		- 使用2 levels of cross-validation求出target mean
	4. [Beta Target-Encoding](https://zhuanlan.zhihu.com/p/40231966):
		- 加入了smoothing term，用 bayesian mean 来代替mean
3. variance和bias的理解
	- variance: 度量了同样大小的训练集的变动速调值得学习性能的变化,既刻画了数据扰动所造成的的影响
	- bias: 度量了学习算法的期望预测与真实结果的偏离程度,即刻画了学习算法本身的拟合能力
4. 选择模型需要考虑的因素
	1. 数据的大小、质量和性质
	2. 拥有的计算资源和可以接收的计算时间
	3. 任务的紧迫程度
	4. 期望从数据中挖掘的内容
	5. ![速查表](https://blogs.sas.com/content/subconsciousmusings/files/2017/04/machine-learning-cheet-sheet-2.png)
5. 不同模型的优缺点、适用情况
	1. 通常情况下，如果是小训练集，高偏差/低方差的分类器（例如，朴素贝叶斯NB）要比低偏差/高方差大分类的优势大（例如，KNN），因为后者会发生过拟合（overfiting）。然而，随着你训练集的增长，模型对于原数据的预测能力就越好，偏差就会降低，此时低偏差/高方差的分类器就会渐渐的表现其优势（因为它们有较低的渐近误差），而高偏差分类器这时已经不足以提供准确的模型了。
	2. Naive Bayse:
		- 对大数量训练和查询时具有较高的速度。即使使用超大规模的训练集，针对每个项目通常也只会有相对较少的特征数，并且对项目的训练和分类也仅仅是特征概率的数学运算而已
		- 对小规模的数据表现很好，能个处理多分类任务，适合增量式训练(即可以实时的对新增的样本进行训练)
		- 对缺失数据不太敏感，算法也比较简单，常用于文本分类
		- 由于使用了attribute conditional independence assumption，所以如果样本属性有关联时其效果不好
	3. [Logistic Regression](https://zhuanlan.zhihu.com/p/46831267)
	4. [线性回归](https://zhuanlan.zhihu.com/p/46831267)
	5. [KNN](https://zhuanlan.zhihu.com/p/46831267)
	6. [Decision Tree](https://zhuanlan.zhihu.com/p/46831267)
6. 数据量超大怎么处理
7. 怎么让模型每天自动跑，更新
	1. online-learning:
		- [online gradient descent](https://blog.csdn.net/Losteng/article/details/51119764)
8. 监测模型有没有出错
9. github流程
## Bussiness Case
1. Credit Card
	- Revenue Sources for Credit Card:
		1. Interchange Fees: As explained above, every time you use a credit card, the merchant pays a processing fee equal to a percentage of the transaction (MDR). The portion of that fee sent to the issuer via the payment network is called “interchange,” and is usually about 1% to 3% of the transaction. These fees are set by payment networks and vary based on the volume and value of transactions.
		2. Late Payment Fees and Revolving Interest Charges: A significant amount of card users do not pay their bills in full each month. The customer’s unpaid credit card balance starts to incur interest at rates varying roughly from 1.75% to 4% per month (APR varies between 16% to 48%). Among a card company’s customer base, majority would be “revolvers” (people who keep paying less than full amount every month), and these guys are most profitable for the bank.
		3.  Membership Fees
