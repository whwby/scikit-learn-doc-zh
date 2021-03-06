
==========================================================================
机器学习: scikit-learn 中的设置以及预估对象
==========================================================================

数据集
=========

Scikit-learn从可以从一个或者多个数据集中学习信息，这些数据集合必须是2维阵列，也可以认为是一个列表。列表的第一个维度代表 **样本** ，第二个维度代表 **特征** （每一行代表一个样本，每一列代表一种特征）。

.. topic:: 样例: iris 数据集（鸢尾花卉数据集）

    ::

        >>> from sklearn import datasets
        >>> iris = datasets.load_iris()
        >>> data = iris.data
        >>> data.shape
        (150, 4)

    这个数据集包含150个样本，每个样本包含4个特征：花萼长度，花萼宽度，花瓣长度，花瓣宽度，详细数据可以通过``iris.DESCR``查看。

如果原始数据并不是``(n_samples, n_features)``的形状，在使用之前必须进行预处理。

.. topic:: 数据预处理样例:digits数据集(手写数字数据集)

    .. image:: /auto_examples/datasets/images/sphx_glr_plot_digits_last_image_001.png
        :target: ../../auto_examples/datasets/plot_digits_last_image.html
        :align: right
        :scale: 60

    digits数据集包含1797个手写数字的图像，每个图像为8*8像素 ::

        >>> digits = datasets.load_digits()
        >>> digits.images.shape
        (1797, 8, 8)
        >>> import matplotlib.pyplot as plt #doctest: +SKIP
        >>> plt.imshow(digits.images[-1], cmap=plt.cm.gray_r) #doctest: +SKIP
        <matplotlib.image.AxesImage object at ...>

    为了在scikit中使用这一数据集，需要将8×8的图像转换成长度为64的一维列表 ::

        >>> data = digits.images.reshape((digits.images.shape[0], -1))


预估对象
===================

.. Some code to make the doctests run

   >>> from sklearn.base import BaseEstimator
   >>> class Estimator(BaseEstimator):
   ...      def __init__(self, param1=0, param2=0):
   ...          self.param1 = param1
   ...          self.param2 = param2
   ...      def fit(self, data):
   ...          pass
   >>> estimator = Estimator()

**拟合数据**: scikit-learn实现最重要的一个API是`estimator`。拟合模型（estimators object）可以基于数据进行学习，拟合模型可以是一个分类器，回归或者是一个聚类算法，或者只是一个*映射*关系。

所有的拟合模型对象拥有一个名为``fit``的方法，参数是一个数据集（通常是一个2维列表）:

    >>> estimator.fit(data)

**拟合模型对象构造参数**: 在创建一个拟合模型时，可以设置相关参数，在创建之后也可以修改对应的参数::

    >>> estimator = Estimator(param1=1, param2=2)
    >>> estimator.param1
    1

**拟合参数**: 当拟合模型完成对数据的拟合之后，可以从拟合模型中获取拟合的参数结果，所有拟合完成的参数均以下划线(_)作为结尾::

    >>> estimator.estimated_param_ #doctest: +SKIP
