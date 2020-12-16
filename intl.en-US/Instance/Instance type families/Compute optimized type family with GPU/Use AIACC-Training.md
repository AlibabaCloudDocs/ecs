---
keyword: [X-Dragon, AI accelerator, accelerated inference, accelerated training, AIACC-Training, AIACC-Inference]
---

# Use AIACC-Training

Apsara AI Accelerator \(AIACC\) is an artificial intelligence \(AI\) accelerator developed by Alibaba Cloud. It consists of a training accelerator \(AIACC-Training\) and an inference accelerator \(AIACC-Inference\). AIACC-Training can accelerate major AI computing frameworks such as TensorFlow, PyTorch, MxNet, and Caffe to achieve significant gains in training performance.

Conda is an open source package management system and environment management system that can run on different platforms. Miniconda is a small installer of conda. When you create a GPU-accelerated instance, you can configure a conda environment that contains AIACC-Training to be installed automatically. You can use Miniconda to select a conda environment. Then, in the conda environment, you can install and switch between deep learning frameworks and use AIACC-Training to improve training performance.

AIACC-Training has the following acceleration features:

-   Gradient fusion communication: supports adaptive multi-stream fusion and adaptive gradient fusion to improve the training performance of bandwidth-intensive network models by up to 300%.
-   Decentralized gradient-based negotiation: reduces the traffic of gradient-based negotiation on large-scale nodes by up to two orders of magnitude.
-   Hierarchical Allreduce algorithm: supports FP16 gradient compression and mixed precision compression.
-   NaN check: You can enable NaN check during the training process and determine the gradient from which the NaN comes on an SM60 or later platform.
-   API extensions for MXNet: support data parallelism and model parallelism of the InsightFace type.
-   Deep optimization for remote direct memory access \(RDMA\) networks.

## Automatically install AIACC-Training

AIACC-Training depends on the GPU driver, CUDA, and cuDNN. When you create a GPU-accelerated instance, select **Auto-install GPU Driver** and then select **Auto-install AIACC-Training**. For more information about how to create a GPU-accelerated instance, see [Create an NVIDIA GPU-accelerated instance](/intl.en-US/Instance/Instance type families/Compute optimized type family with GPU/Create an NVIDIA GPU-accelerated instance.md).

![install-aiacc-training](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1900808061/p185328.png)

Conda environments contain dependency packages such as AIACC-Training and OpenMPI, but do not contain deep learning frameworks. For more information about how to install a deep learning framework, see [Select a conda environment and install a deep learning framework](#section_742_vx6_d1i).

CUDA versions determine the versions of deep learning frameworks that can be installed. The following table describes the mappings between CUDA versions and versions of deep learning frameworks.

|CUDA version|Default conda environment|Version of the deep learning framework that can be installed|
|------------|-------------------------|------------------------------------------------------------|
|CUDA 10.1|tf2.1\_cu10.1\_py36|Tensorflow 2.1|
|CUDA 10.0|tf1.15\_tr1.4.0\_mx1.5.0\_cu10.0\_py36|-   Tensorflow 1.15 + Pytorch 1.4.0 + MXNet 1.5.0
-   Tensorflow 1.14 + Pytorch 1.3.0 + MXNet 1.4.0 |
|CUDA 9.0|tf1.12\_tr1.3.0\_mx1.5.0\_cu9.0\_py36|Tensorflow 1.12 + Pytorch 1.3.0 + MXNet 1.5.0|

## Select a conda environment and install a deep learning framework

1.  Connect to the instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using VNC.md).

2.  Select a conda environment.

    1.  Initialize Miniconda.

        ```
        . /root/miniconda/etc/profile.d/conda.sh
        ```

    2.  View all conda environments.

        ```
        conda env list
        ```

        The following figure shows an example command output.

        ![aiacc-training-envlist](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0879997061/p185296.png)

    3.  Select a conda environment.

        ```
        conda activate [environments_name]
        ```

        The following figure shows an example command output.

        ![aiacc-training-activate](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0879997061/p185299.png)

        aiacct\_tf2.1\_cu10.1\_py36 indicates:

        -   Tensorflow 2.1
        -   CUDA 10.1
        -   Python 3.6
3.  Install a deep learning framework.

    ```
    install_frameworks.sh
    ```

    The install\_frameworks.sh script includes the commands used to install deep learning frameworks that are compatible with the selected conda environment. The following figure shows a sample script.

    ![install-frameworks-script](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0879997061/p185541.png)

    The following figure shows an example script output.

    ![install-frameworks](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0879997061/p185310.png)

4.  Test the demo.

    By default, the ali-perseus-demos.tgz demo file is located in the /root directory. In this example, the TensorFlow demo is tested.

    -   For TensorFlow 2.1, perform the following operations:
        1.  Decompress the demo test package.

            ```
            tar -xvf ali-perseus-demos.tgz
            ```

        2.  Go to the directory of the TensorFlow demo.

            ```
            cd ali-perseus-demos/tensorflow2-examples
            ```

        3.  Run the test script in the directory.

            Sample command:

            ```
            python tensorflow2_keras_mnist_perseus.py
            ```

            This demo uses Modified National Institute of Standards and Technology \(MNIST\) datasets for training to improve training performance and ensure that the same level of precision is achieved as that of your benchmark code. The following figure shows an example training result.

            ![tf2.1-demo](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0879997061/p185425.png)

    -   For TensorFlow 1.14, perform the following operations:
        1.  Decompress the demo test package.

            ```
            tar -xvf ali-perseus-demos.tgz
            ```

        2.  Go to the directory of the TensorFlow demo.

            ```
            cd ali-perseus-demos/tensorflow-benchmarks
            ```

        3.  View the test command in README.txt.
        4.  Go to the directory where the test script of the corresponding version resides.

            Sample command:

            ```
            cd benchmarks-tf1.14
            ```

        5.  Modify and run the test command based on the number of GPUs with which the specified instance type is equipped.

            Sample command:

            ```
            mpirun --allow-run-as-root --bind-to none -np 1 -npernode 1  \
                   --mca btl_tcp_if_include eth0  \
                   --mca orte_keep_fqdn_hostnames t   \
                   -x NCCL_SOCKET_IFNAME=eth0   \
                   -x LD_LIBRARY_PATH   \
                   ./config-fp16-tf.sh
            ```

            This demo uses synthetic data for training to test the training speed. The following figure shows an example training result.

            ![tf1.14-demo](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0879997061/p185351.png)


## Delete Miniconda

You can delete Miniconda if you no longer need AIACC-Training. By default, the root user can install and delete Miniconda.

1.  Delete the miniconda folder.

    ```
    rm -rf /root/miniconda
    ```

2.  Delete relevant environment variables and output.

    1.  Modify the /root/.bashrc file and comment out the environment variables and output related to Miniconda and AIACC-Training, as shown in the following figure.

        ![bashrc-file](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0879997061/p185524.png)

    2.  Make the changes to the environment variables take effect.

        ```
        source /root/.bashrc
        ```


