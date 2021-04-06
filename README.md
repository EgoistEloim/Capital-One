# Capital-One
## Start Self Introduction
1. Basic information: 
    - Graduate time: this May
    - major courses: Artificial Intelligence, Deep Learning, NLP, Computer Vision, Machine Learning, Big Data, Algorithm, Database
    - interested: Deep Learning, Machine Learning related techniques
3. Professional experience: MEGVII-design deep learning and machine learning algorithms to solve credit card detection and recognition problem
4. Why Capital One:
    - 我有一个朋友在Capital One担任Data Scientist并且告诉我Capital One有很多的growth opportunities
    - Capital One有extensive use of data science to provide customers with better service in financial services我想把我的expertise和experience to this process
    - 之前我申请了一个CV的岗位，但是那个岗位was filled by internal hire了，所以HR推荐我和你聊一下，我比较感兴趣的几个点是：
    - 你们team目前的projects
    - what are the goals and functionalities of your team in Capital One

## Related Project
1. Computer Vision STN(Computer Vision & Deep Learning):这个项目中我主要负责信用卡文字识别相关的工作。通过对目前已有的pipeline的分析和探索后我发现模型对于大角度拍摄的信用卡的识别效果不好。于是为了解决这一问题，我设计了两种算法。第一种就是STN模块。它是基于Google的一篇空间矫正研究设计的可以自动的学习一个空间变换矩阵的网络结构。这个矩阵能够对现有图片进行旋转、平移、缩放等等操作，从而将大角度拍摄的图片矫正回正常角度。第二个方法就是Fake Generator + Focal Loss，大角度拍摄的图片属于长尾问题，仅在总数据集中占据很少一部分。为了提升模型对这类长尾问题的处理能力，我设计了一个fake generator来生成大角度拍摄的图片用于模型训练，同时利用Focal Loss来提高hard sample的权重。除此以外，模型并没有达到很理想的识别效果，于是我修改了模型结构，使用了双向LSTM+CTC Loss替换掉原来的CNN+Smooth L1 Loss，这样也使得模型最终的识别效果提升了很多。
2. 
3. Kaggle WSDM (Big Data):这是一个Kaggle平台的比赛项目。这个项目有一个非常有意思的点，数据量非常巨大，所以我使用了一些大数据的处理和分析技术例如spark和MapReduce来进行特征工程。特征工程阶段我利用了conditional probability构建了一系列的feature使得模型效果获得了很大的提升。模型方面我使用了LightGBM模型，该模型的很多优化使得它在大规模数据集上面的表现非常优秀
4. 
5. Code Search Engine(NLP & Deep Learning):在这个比赛中我的任务是构建一个模型来判别一段代码和一段代码注释是否匹配。我使用了Transformer作为代码和注释的encoder，然后利用encoder的结果作为特征来计算两者的匹配程度，从而构建了比赛的模型。
6. 
7. Objects 365(Dataset):
## Questions
1. As you can tell, most of my past professional experience has strong focus towards computer vision and deep learning, how would you think my experience and expertise can fit into the current projects of the team or some potential opportunities in the near future?

2. In terms of NLP, I'm particular interested in the application of some SOTA modeling techniques and research, for example Transformer and BERT. Will there be opportinuties to utilize these SOTA models?

3. As a data scientist at Capital One, will there be opportunities to learn? Such as academic conferences to learn about the newest research.
