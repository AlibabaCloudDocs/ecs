---
keyword: [神龙, AI加速, 加速推理, 加速训练, AIACC-Training, AIACC-Inference]
---

# 使用AIACC-Training

神龙AI加速引擎AIACC是阿里云自研的AI加速器，包括神龙AI加速训练引擎AIACC-Training和神龙AI加速推理引擎AIACC-Inference。其中AIACC-Training支持统一加速AI主流计算框架TensorFlow、PyTorch、MxNet和Caffe，可以显著提升训练性能。

Conda是一款开源跨平台的软件包和环境管理系统，Miniconda是一款小巧的Conda环境部署工具。创建GPU实例时支持自动安装包含AIACC-Training的Conda环境，您可以使用Miniconda快速选择不同的Conda环境，一键安装和切换深度学习框架，并通过AIACC-Training显著提升训练性能。

AIACC-Training包括以下加速特性：

-   梯度融合通信支持自适应多流、自适应梯度融合，显著提升带宽密集的网络模型的训练性能，约提速50%至300%。
-   采用去中心化梯度协商机制，将大规模节点下梯度协商的通信量降低1到2个数量级。
-   采用分级的Allreduce方法，支持FP16梯度压缩及混合精度压缩。
-   支持在训练过程中开启NaN检查，支持定位NaN来自于哪个梯度（需要为SM60及更新平台）。
-   提供针对MXNet的API扩展，支持insightface类型的数据和模型并行。
-   提供针对RDMA网络的深度优化。

## 自动安装AIACC-Training

AIACC-Training依赖GPU驱动、CUDA和cuDNN，请在创建GPU实例时配置自动安装GPU驱动，然后选中**AIACC-Training**。具体操作，请参见[创建配备NVIDIA GPU的实例](/cn.zh-CN/实例/选择实例规格/GPU计算型/创建配备NVIDIA GPU的实例.md)。

![install-aiacc-training](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2809736061/p185328.png)

Conda环境包括AIACC-Training及OpenMPI等依赖包，但不包括深度学习框架。安装深度学习框架的具体操作，请参见[选择Conda环境并安装深度学习框架](#section_742_vx6_d1i)。

CUDA版本决定支持安装的深度学习框架版本，对应关系如下表所示。

|CUDA版本|默认进入的Conda环境|支持安装的深度学习框架版本|
|------|------------|-------------|
|CUDA 10.1|tf2.1\_cu10.1\_py36|Tensorflow 2.1|
|CUDA 10.0|tf1.15\_tr1.4.0\_mx1.5.0\_cu10.0\_py36|-   Tensorflow 1.15 + Pytorch 1.4.0 + MXNet 1.5.0
-   Tensorflow 1.14 + Pytorch 1.3.0 + MXNet 1.4.0 |
|CUDA 9.0|tf1.12\_tr1.3.0\_mx1.5.0\_cu9.0\_py36|Tensorflow 1.12 + Pytorch 1.3.0 + MXNet 1.5.0|

## 选择Conda环境并安装深度学习框架

1.  [远程连接实例](/cn.zh-CN/实例/连接实例/连接Linux实例/通过Workbench远程连接Linux实例.md)。

2.  选择Conda环境。

    1.  初始化Miniconda。

        ```
        . /root/miniconda/etc/profile.d/conda.sh
        ```

    2.  查看已有的Conda环境列表。

        ```
        conda env list
        ```

        示例如下图所示。

        ![aiacc-training-envlist](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2809736061/p185296.png)

    3.  选择Conda环境。

        ```
        conda activate [environments_name]
        ```

        示例如下图所示。

        ![aiacc-training-activate](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2809736061/p185299.png)

        其中，aiacct\_tf2.1\_cu10.1\_py36代表：

        -   Tensorflow 2.1
        -   CUDA 10.1
        -   Python 3.6
3.  安装深度学习框架。

    ```
    install_frameworks.sh
    ```

    install\_frameworks.sh脚本中包括了在安装适用当前Conda环境的深度学习框架的命令，脚本内容示例如下图所示。

    ![install-frameworks-script](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9243836061/p185541.png)

    执行脚本后安装过程示例如下图所示。

    ![install-frameworks](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2809736061/p185310.png)

4.  测试demo。

    demo文件ali-perseus-demos.tgz默认位于/root下，本文以测试TensorFlow的demo为例。

    -   如果TensorFlow版本为2.1：
        1.  解压demo测试包。

            ```
            tar -xvf ali-perseus-demos.tgz
            ```

        2.  进入TensorFlow的demo目录。

            ```
            cd ali-perseus-demos/tensorflow2-examples
            ```

        3.  执行目录下的测试脚本。

            示例命令如下：

            ```
            python tensorflow2_keras_mnist_perseus.py
            ```

            该demo使用MNIST数据集进行训练，在提升训练性能的同时，保证和您的基准代码达到相同的精度。训练结果示例如下图所示。

            ![tf2.1-demo](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2809736061/p185425.png)

    -   如果TensorFlow版本为1.14：
        1.  解压demo测试包。

            ```
            tar -xvf ali-perseus-demos.tgz
            ```

        2.  进入TensorFlow的demo目录。

            ```
            cd ali-perseus-demos/tensorflow-benchmarks
            ```

        3.  查看README.txt中的测试命令。
        4.  进入对应版本的测试脚本目录。

            示例命令如下：

            ```
            cd benchmarks-tf1.14
            ```

        5.  根据实例规格的GPU数量修改并执行测试命令。

            示例命令如下：

            ```
            mpirun --allow-run-as-root --bind-to none -np 1 -npernode 1  \
                   --mca btl_tcp_if_include eth0  \
                   --mca orte_keep_fqdn_hostnames t   \
                   -x NCCL_SOCKET_IFNAME=eth0   \
                   -x LD_LIBRARY_PATH   \
                   ./config-fp16-tf.sh
            ```

            该demo使用合成数据进行训练，测试训练速度。训练结果示例如下图所示。

            ![tf1.14-demo](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2809736061/p185351.png)


## 删除Miniconda

如果您不需要使用AIACC-Training，可以删除Miniconda。默认为root用户安装Miniconda，为root用户删除Miniconda即可。

1.  删除miniconda文件夹。

    ```
    rm -rf /root/miniconda
    ```

2.  删除相关环境变量和回显。

    1.  修改文件/root/.bashrc，注释Miniconda、AIACC-Training相关的环境变量和回显。

        示例如下图所示。

        ![bashrc-file](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0343836061/p185524.png)

    2.  使环境变量修改生效。

        ```
        source /root/.bashrc
        ```


