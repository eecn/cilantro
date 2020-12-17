## 精简高效的点云数据处理库
`cilantro`是一个精简高效的C++库，用于处理点云数据，重点放在了3D案例上。它包括针对各种常见操作的高效实现，提供了一个简洁的API，并尝试最大程度地减少样板代码的数量。该库具有广泛的模板化功能，可对任意数值类型和维数（如果适用）的数据进行操作，并具有更复杂过程的模块化/可扩展设计。同时为最常见方法提供了方便的别名/包装器案例。你还可以在我们的[技术报告](https://arxiv.org/abs/1807.00399)中找到对`cilantro`的高级描述。

## 支持的功能
#### 基础操作:
- 通用维度kd树(使用了捆绑的[nanoflann](https://github.com/jlblancoc/nanoflann))
- 根据原始点云的表面法线和曲率估算(稳健)
- 基于通用尺寸网格的点云重采样
- PCA主成分分析
- 用于3D点云的基础I/O实用程序操作(采用PLY格式, 使用捆绑的[tinyply](https://github.com/ddiakopoulos/tinyply))
- RGBD图像对与点云之间转换的实用程序

#### 凸包和空间推理:
- 从顶点或半空间相交输入计算(使用捆绑的[Qhull](http://www.qhull.org/))的通用尺寸凸多面体表示，并允许在各个表示之间轻松切换
- 将通用(通用尺寸)空间区域，表示为实现设置操作的凸多面体的并集检测运算

#### 聚类:
- 通用维度k均值聚类，支持[nanoflann](https://github.com/jlblancoc/nanoflann)支持的所有距离度量
- 基于各种图拉普拉斯算子类型的光谱聚类(使用捆绑的[Spectra](https://github.com/yixuan/spectra))
- 支持自定义内核的均值漂移聚类算法
- 基于联通性的点云分割，支持任意逐点相似度函数

#### 几何配准:
- 支持以下任意点特征空间中的任意对应搜索方法的多个通用迭代最近点实现:
    - 点对点度量(常规尺寸), 点对平面度量(2D或3D)或其任意组合下的**刚性**或**仿射**对准
    - 在点对点和点对平面度量的任意组合下，通过鲁棒的正则化，**局部刚性**或**局部仿射**变换对2D或3D点集进行***非刚性对齐**; 提供了*密集*和*稀疏*(通过嵌入式变形图)支持的点云变换的实现
#### 稳健的模型估算:
- 通用尺寸的RANSAC估算器模板及其实例:
    - 稳健的超平面估计
    - 给定噪声对应的刚性点云配准

#### 可视化
- 经典多维缩放(使用捆绑的[Spectra](https://github.com/yixuan/spectra)进行特征分解)
- 是一个功能强大，可扩展且易于使用的3D可视化工具

## 依赖
- [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page) (3.3版或更高版本)[ **必需** ]
- [Pangolin](https://github.com/stevenlovegrove/Pangolin) (built with Eigen enabled) [ **可选**; 可视化模块和大多数示例所需的]

## Build编译
`cilantro`是使用[CMake](https://cmake.org/)在Ubuntu变体(16.04及更高版本)上开发和测试的。要克隆和构建库(带有捆绑的示例)，请在终端中执行以下操作:

```
git clone https://github.com/kzampog/cilantro.git
cd cilantro
mkdir build
cd build
cmake ..
make -j
```
## 文档资料
文档([readthedocs.io](http://cilantro.readthedocs.io/en/latest/?badge=latest), [Doxygen API reference](https://codedocs.xyz/kzampog/cilantro/))正在进行中。提供的简短示例(默认情况下构建)涵盖了库功能的重要部分。大多数都期望有一个命令行参数(PLY格式的点云文件的路径). 点云输入可以在examples/test_clouds下进行快速测试。

## License
该库是根据 [MIT license](https://github.com/kzampog/cilantro/blob/master/LICENSE)许可发布的。如果您使用 `cilantro`用于你的研究，请引用我们的[技术报告](https://arxiv.org/abs/1807.00399):
```
@inproceedings{zampogiannis2018cilantro,
    author = {Zampogiannis, Konstantinos and Fermuller, Cornelia and Aloimonos, Yiannis},
    title = {cilantro: A Lean, Versatile, and Efficient Library for Point Cloud Data Processing},
    booktitle = {Proceedings of the 26th ACM International Conference on Multimedia},
    series = {MM '18},
    year = {2018},
    isbn = {978-1-4503-5665-7},
    location = {Seoul, Republic of Korea},
    pages = {1364--1367},
    doi = {10.1145/3240508.3243655},
    publisher = {ACM},
    address = {New York, NY, USA}
}
```