# Use Analytics Zoo to implement bfloat16 acceleration for AI applications on ECS instances

This topic describes how to use Analytics Zoo and the bfloat16 capability provided by third-generation Intel® Xeon® scalable processors to accelerate the performance of artificial intelligence \(AI\) applications on ECS instances. This topic is applicable to seventh-generation high frequency ECS instances \(also called ECS instances with high clock speeds\).

-   Seventh-generation high frequency ECS instances are built on the third-generation SHENLONG architecture and powered by Intel® Xeon® scalable processors. These instances can deliver a compute performance up to 260% higher than the sixth-generation high frequency instances can. When you use Analytics Zoo on ECS instances, you can leverage advanced pipeline features such as the TensorFlow and PyTorch deep learning frameworks optimized by Intel to develop deep learning applications.
-   Third-generation Intel® Xeon® scalable processors provide an industry-leading workload-optimized platform and have enhanced Intel® Deep Learning Boost \(Intel® DL Boost\) built in to take AI performance to the next level. Enhanced Intel® DL Boost features the industry's first x86 support for bfloat16 to drive better AI inference and training performance.

    Third-generation intelligent Intel® Xeon® scalable processors can cope with complex AI workloads. Enhanced Intel® DL Boost can increase AI training performance by up to 1.93×, image classification performance by up to 1.87×, natural language processing \(NLP\) training performance by up to 1.7×, and inference performance by up to 1.9×. Support for bfloat16 makes it much more efficient to handle AI training workloads for the healthcare, financial services, and retail industries.

-   Analytics Zoo is a unified, open source big data analytics and AI platform developed by Intel. It can seamlessly scale AI programs such as TensorFlow, Keras, and PyTorch to adapt to distributed big data environments such as Spark, Flink, and Ray. Analytics Zoo provides the following features:

    -   An end-to-end pipeline for running AI models based on TensorFlow, PyTorch, or OpenVINO on big data platforms. For example, developers can embed TensorFlow or PyTorch code into Spark code for distributed training and inference. Developers can also use the native support for deep learning frameworks such as TensorFlow, Keras, PyTorch, and BigDL in Spark machine learning \(ML\) pipelines.
    -   Support for high-level ML workflows to automate ML tasks, such as Cluster Serving for automatically distributed TensorFlow, PyTorch, Caffe, and OpenVINO model inference, and scalable AutoML for time series prediction.
    -   Built-in common models for applications such as Recommendation, Time Series, CV, and NLP.
    ![ZOO](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5909755061/p175741.jpg)

-   Bfloat16 is a data format widely used in neural networks.
-   ResNet-50 is a convolutional neural network that is 50 layers deep. It is used in fields such as object classification.

## Procedure

To use Analytics Zoo to implement bfloat16 acceleration for AI applications on an ECS instance, perform the following steps:

1.  [Step 1: Create a high frequency ECS instance](#section_yzf_2l0_625)
2.  [Step 2: Prepare an Analytics Zoo environment that provides enhanced support for bfloat16 on the ECS instance](#section_odn_pxr_3qj)
3.  [Step 3: Train ResNet-50 models and implement bfloat16 acceleration for better performance on the ECS instance](#section_4hb_eid_lb1)

## Step 1: Create a high frequency ECS instance

To create a high frequency ECS instance, perform the following operations:

1.  Go to the [Custom Launch](https://ecs-buy.aliyun.com/wizard/#/) tab of the instance buy page in the ECS console.

2.  Create a high frequency instance. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

    When you configure parameters to create the high frequency instance, you can select the hfc7 or hfg7 instance family. In this example, select the hfc7 instance family. For information about specific instance types, see [Instance families with high clock speeds](/intl.en-US/Instance/Instance type families/Instance families with high clock speeds.md).

3.  On the Instances page, find the instance that you created in the previous step and click the ID of the instance. Confirm that the instance is of the hfc7 instance type.

    ![Confirm the instance type](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3724945061/p175789.png)


## Step 2: Prepare an Analytics Zoo environment that provides enhanced support for bfloat16 on the ECS instance

Analytics Zoo provides a precreated Docker image that supports bfloat16. You can use method 1 to obtain this Docker image in Alibaba Cloud ECS. Alternatively, you can use method 2 to obtain a nightly build of Analytics Zoo that supports bfloat16. For information about the related code, see [Sample code for using bfloat16 to accelerate the training of deep learning models in Analytics Zoo](#section_o85_jd0_p6m).

-   Method 1: Obtain the Docker image provided by Analytics Zoo in ECS
    1.  Connect to the ECS instance. For more information, see [Connect to an ECS instance]().
    2.  Run the following commands to install and run Docker:

        ```
        yum install docker-io -y
        systemctl start docker
        ```

    3.  Run the following command to obtain the Docker image provided by Analytics Zoo that supports bfloat16:

        ```
        docker pull intelanalytics/analytics-zoo:0.8.1-bigdl_0.10.0-spark_2.4.3-bf16
        ```

    4.  Run the following command to run the Docker container that corresponds to the Docker image:

        ```
        docker run -itd --name az1 --net=host  --privileged intelanalytics/analytics-zoo:0.8.1-bigdl_0.10.0-spark_2.4.3-bf16
        ```

    5.  Run the following command to access the container:

        ```
        docker exec -it az1 bash
        ```

-   Method 2: Use a nightly build of Analytics Zoo that supports bfloat16 to manually create an Analytics Zoo environment
    1.  Connect to the ECS instance. For more information, see [Connect to an ECS instance]().
    2.  Run the following commands to download and decompress the latest Analytics Zoo prebuilt release and nightly build package:

        ```
        wget https://oss.sonatype.org/content/repositories/snapshots/com/intel/analytics/zoo/analytics-zoo-bigdl_0.11.1-spark_2.4.3/0.9.0-SNAPSHOT/analytics-zoo-bigdl_0.11.1-spark_2.4.3-0.9.0-20201026.210040-51-dist-all.zip
        unzip analytics-zoo-bigdl_0.11.1-spark_2.4.3-0.9.0-{datetime}-dist-all.zip -d analytics-zoo
        ```

    3.  Run the following command to install Git:

        ```
        yum -y install git
        ```

    4.  Run the following commands to download TensorFlow source code:

        ```
        git clone https://github.com/Intel-tensorflow/tensorflow.git
        git checkout v1.15.0up1
        ```

    5.  Run the following commands to compile TensorFlow:

        ```
        bazel build --cxxopt=-D_GLIBCXX_USE_CXX11_ABI=0 --copt=-O3 --copt=-Wformat
        --copt=-Wformat-security --copt=-fstack-protector --copt=-fPIC
        --copt=-fpic --linkopt=-znoexecstack --linkopt=-zrelro
        --linkopt=-znow --linkopt=-fstack-protector --config=mkl --define
        build_with_mkl_dnn_v1_only=true --copt=-DENABLE_INTEL_MKL_BFLOAT16
        --copt=-march=native
        //tensorflow/tools/lib_package:libtensorflow_jni.tar.gz
        //tensorflow/java:libtensorflow.jar
        //tensorflow/java:libtensorflow-src.jar
        //tensorflow/tools/lib_package:libtensorflow_proto.zip
        ```

    6.  Run the following commands to organize the library files required by Analytics Zoo:

        ```
        cd bazel-bin/tensorflow/tools/lib_package
        mkdir linux-x86_64
        tar -xzvf libtensorflow_jni.tar.gz -C linux_x86-64
        rm libtensorflow_framework.so
        rm libtensorflow_framework.so.1
        mv libtensorflow_framework.so.1.15.0 libtensorflow_framework-zoo.so
        cp .. /.. /.. /../_solib_k8/_U@mkl_Ulinux_S_S_Cmkl_Ulibs_Ulinux___Uexternal_Smkl_Ulinux_Slib/* . /
        ```

    7.  Run the following command to update the Analytics Zoo Jar folder:

        ```
        cd ~/analytics-zoo/lib/
        cp ~/tensorflow/bazel-bin/tensorflow/tools/lib_package/linux-x86_64 ./
        jar -ufanalytics-zoo-bigdl_0.11.1-spark_2.4.3-0.9.0-SNAPSHOT-jar-with-dependencies.jar linux-x86_64/*
        ```


## Step 3: Train ResNet-50 models and implement bfloat16 acceleration for better performance on the ECS instance

1.  Run the following command to access the Analytic Zoo Docker container:

    ```
    docker exec -it az1 bash
    ```

2.  Run the following commands to configure Spark and modify the /opt/work/spark-2.4.3/conf/spark-defaults.conf file:

    ```
    spark.authenticate=false
    spark.ui.killEnabled=true
    spark.eventLog.enabled=true
    spark.history.ui.port=18080
    spark.eventLog.dir=file:///var/log/spark/spark-events
    spark.history.fs.logDirectory=file:///var/log/spark/spark-events
    spark.shuffle.service.port=7337
    spark.master=spark://$(hostname):7077
    ```

3.  Run the following commands to start the Spark master:

    ```
    cd /opt/work/spark-2.4.3
    ./sbin/start-master.sh
    ```

4.  Run numactl commands to start eight Spark workers and bind each Spark worker to 12 vCPUs. Then, create the following script in the /opt/work/spark-2.4.3/bin directory:

    ```
    numactl -C 0-11 ./spark-class org.apache.spark.deploy.worker.Worker spark://$(hostname):7077 &
    numactl -C 12-23 ./spark-class org.apache.spark.deploy.worker.Worker spark://$(hostname):7077 &
    numactl -C 24-35 ./spark-class org.apache.spark.deploy.worker.Worker spark://$(hostname):7077 &
    numactl -C 36-47 ./spark-class org.apache.spark.deploy.worker.Worker spark://$(hostname):7077 &
    numactl -C 48-59 ./spark-class org.apache.spark.deploy.worker.Worker spark://$(hostname):7077 &
    numactl -C 60-71 ./spark-class org.apache.spark.deploy.worker.Worker spark://$(hostname):7077 &
    numactl -C 72-83 ./spark-class org.apache.spark.deploy.worker.Worker spark://$(hostname):7077 &
    numactl -C 84-95 ./spark-class org.apache.spark.deploy.worker.Worker spark://$(hostname):7077 &
    ```

5.  Run the following commands to check how many Spark workers are started. If `8` is displayed in the command output, eight Spark workers are started.

    ```
    jps | grep Worker | wc -l
    ```

6.  Run the following commands to download ResNet-50 sample code from Github:

    ```
    git clone https://github.com/yangw1234/models-1.git
    git checkout branch-1.6.1-zoo
    ```

7.  Run the run.sh script in the models-1/models/image\_recognition/tensorflow/resnet50v1\_5/training/mlperf\_resnet directory and enable bfloat16 training by adding the --use\_bfloat16 option. If the --use\_bfloat16 option is not added, float32 training is used.

    ```
    # Register the model as a source root
    export PYTHONPATH="$(pwd):${PYTHONPATH}"
    export KMP_BLOCKTIME=0
    # 8 instances
    export OMP_NUM_THREADS=6
    export KMP_AFFINITY=granularity=fine,compact,1,0
    export KMP_SETTINGS=1
    export ANALYTICS_ZOO_HOME=/opt/work/analytics-zoo/dist
    export SPARK_HOME=/opt/work/spark-2.4.3
    bash $ANALYTICS_ZOO_HOME/bin/spark-submit-python-with-zoo.sh --master
    spark://$(hostname):7077 \
    --executor-cores 1 --total-executor-cores 8 --driver-memory 20g --executor-memory 18g \
    --conf spark.network.timeout=10000000 --conf spark.executor.heartbeatInterval=100000 \
    imagenet_main.py 1 --model_dir ./logs --batch_size 128 --version 1 \
    --resnet_size 50 --train_epochs 90 --data_dir /opt/ILSVRC2012/ --use_bfloat16
    ```

    The following table describes the training test results.

    |ResNet-50 model training|Float32|Bfloat16|Performance improvement achieved by bfloat16 over float32|
    |------------------------|-------|--------|---------------------------------------------------------|
    |Throughput\(images/sec\)|119.636|212.315|1.775|


## Sample code for using bfloat16 to accelerate the training of deep learning models in Analytics Zoo

The following code provides an example of how to use bfloat16 to accelerate the training of deep learning models such as ResNet-50 models. The code is for reference only. It is already included in the Docker image provided by Analytics Zoo, and does not require manual operations.

1.  Use the following code to convert input images into the bfloat16 format:

    ```
    if use_bfloat16 == True:
    dtype = tf.bfloat16
    features = tf.cast(features, dtype)
    ```

2.  Use the following code to compile custom\_dtype\_getter:

    ```
    DEFAULT_DTYPE = tf.float32
    CASTABLE_TYPES = (tf.float16,tf.bfloat16)
    def _custom_dtype_getter(getter, name, shape=None, dtype=DEFAULT_DTYPE,     
          *args, **kwargs):
        if dtype in CASTABLE_TYPES:
          var = getter(name, shape, tf.float32, *args, **kwargs)
          return tf.cast(var, dtype=dtype, name=name + '_cast')
        else:
          return getter(name, shape, dtype, *args, **kwargs)
    ```

3.  Use the following code to create a variable\_scope and build a model under the variable\_scope:

    ```
    def _model_variable_scope():
        return tf.compat.v1.variable_scope('resnet_model',
                        custom_getter=_custom_dtype_getter)
    
    with _model_variable_scope():
        logits = _resnet_50_model(features)
    ```

4.  Use the following code to cast logits to the float32 format and then calculate loss to ensure numerical stability:

    ```
    logits = tf.cast(logits, tf.float32)
    ```

5.  Use Analytics TFPark for distributed training. For more information, see [TFPark Overview](https://analytics-zoo.github.io/master/#ProgrammingGuide/TFPark/tensorflow/).


