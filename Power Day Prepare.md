## Tech Interview
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
3. [“判定模型”和“生成模型”有什么区别](https://www.zhihu.com/question/20446337)
4. variance和bias的理解
	- variance: 度量了同样大小的训练集的变动速调值得学习性能的变化,既刻画了数据扰动所造成的的影响
	- bias: 度量了学习算法的期望预测与真实结果的偏离程度,即刻画了学习算法本身的拟合能力
5. 选择模型需要考虑的因素
	1. 数据的大小、质量和性质
	2. 拥有的计算资源和可以接收的计算时间
	3. 任务的紧迫程度
	4. 期望从数据中挖掘的内容
	5. ![速查表](https://blogs.sas.com/content/subconsciousmusings/files/2017/04/machine-learning-cheet-sheet-2.png)
6. 不同模型的优缺点、适用情况
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
	7. [Random Forest vs LR vs XGB](https://www.nowcoder.com/ta/review-ml/review?page=99)
7. 数据量超大怎么处理
	1.[Spark和Hadoop的区别和比较](https://blog.csdn.net/weixin_43520450/article/details/108740235?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.baidujs&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.baidujs)
8. 怎么让模型每天自动跑，更新
	1. online-learning:
		- [online gradient descent](https://blog.csdn.net/Losteng/article/details/51119764)
	2. shell脚本检测数据集变动:
		- 特征数量变动
		- 数据格式变动
		- 模型是否可以online-learning
	3. 为什么我们要定期更新模型
		- 当数据的label发生变化会从根本上影响我们model的性能
		- 数据的定期更新有可能导致我们一开始对于数据分布和模型部署的一些假设不再满足
		- 
9. 监测模型有没有出错
	1. 首先判断我们整个机器学习pipeline是否为e2e的，针对每一个end的位置我们都应当制定或者明确这个end的输出是什么样子的，符合什么标准的，并利用一定的程序校验来检测输出的正确性
	2. 应当有一个非常基本的baseline validation set，当我们有新的模型训练完成时，将该模型在baseline validation set上面进行inference，查看inference的结果是否存在问题。这个方法是基于这样一个假设的：我们的模型更新并不会使得我们模型丧失最基本的分类能力，因此它在简单baseline上面的表现应当变化幅度很小。
	3. 
10. [github流程](https://www.liaoxuefeng.com/wiki/896043488029600)
	1. ![Git work flow](https://user-gold-cdn.xitu.io/2019/8/12/16c84ff492a9de1a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
	2. 保证无论任何情况下master branch上面的代码是可以deploy的
	3. 冲突出现后手动check和修改冲突从而使得merge能够正常进行
11. [feature engineering](https://asialee.blog.csdn.net/article/details/84863410?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-5.baidujs&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-5.baidujs)
12. Confusion Matrix：**待补充**
13. AUC ROC：**待补充**
## Role Play
1. Features
	1. dayofweek做成categorical feature，用dummy(one-hot)来做
	2. 是否delay不能用regression，更关注是否delay>8mins，所以用binary classification -> logistic regression，关注有没有用Binary Class简历regression模型
	3. 会有一些features是高度线性相关的
		- 利用ANOVA表格来看，如果T-test结果高并且p-value小于0.05则说明我们应当支持Null Hypothesis，表明我们现有的variables的prediction是可以信赖的
		- ANOVA表格中F-test value很significant但是R^2很小这种情况需要解释：**待补充**
		- multi-colineariity的影响:
			1. Make the model unstable if it meets data beyond its training range
			2. thre coefficients of the predictors if not explainable
			3. **待补充**
		- P-value: p-valueis the probability of obtaining test results at least as extreme as the results actually observed, under the assumption that the null hypothesis is correct
		- VIF:**待补充**
	4. 加入飞机起飞地点和飞机上实际座位数量作为features，后面会有图表明这两个是有影响的
	5. 有些图标或者变量的数字并不是很合理，比如座位数量=-1这种，要注意修改
	6. 存在missing data
2. Model - Linear Regression
	1. Assumptions:
		- predictors are independent
		- noise obey the Gaussian Distribution(Normal Distribution) with 0 Mean and constant variance
		- the response(label) is linear correlated with predictors
	2. 如何解决predictor 和 response非线性关系:
		- 更换模型
		- 对response或者predictor进行非线性变换
	3. 如何解决predictors之间并不是线性无关的问题:
		- L2 penalty(ridge regression)
		- combine or remove the predictors
3. 保留图表
	- 有一个图表会表明predictors和response是有关系但是不线性的，需要注意
4. 保留predictors
	- 根据多重共线性关系来判断airplane-type已经可以涵盖很多的predictors了
## BQ
1. Questions:
	1. Most challenging project
	2. Tell me about your failure
	3. What will you do if you have a confliction with coworkers
	4. Tell me a time that you help your team
	5. 
2. Answer Structure
	- Situation: Think of a situation in which you were involved that had a positive outcome
	- Task: Describe the tasks involved in the situation
	- Action: Specify what actions you took in the situation to complete the tasks and achieve your results
	- Results: What results followed due to your actions
