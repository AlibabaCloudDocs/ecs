# Use RAPIDS to accelerate machine learning tasks on a GPU-accelerated instance

This topic describes how to use the NGC-based Real-time Acceleration Platform for Integrated Data Science \(RAPIDS\) libraries that are installed on a GPU-accelerated instance to accelerate tasks for data science and machine learning as well as improve the efficiency of computing resources.

RAPIDS is an open source suite of data processing and machine learning libraries developed by NVIDIA to enable GPU-acceleration for data science and machine learning. For more information about RAPIDS, visit the [RAPIDS website](https://rapids.ai/).

NVIDIA GPU Cloud \(NGC\) is a deep learning ecosystem developed by NVIDIA to provide developers with free access to deep learning and machine learning software stacks to build corresponding development environments. The [NGC website](https://ngc.nvidia.com/) provides RAPIDS Docker images, which come pre-installed with development environments.

JupyterLab is an interactive development environment that makes it easy to browse, edit, and run code files on your servers.

Dask is a lightweight big data framework that can make parallel computing more efficient.

This topic provides sample code that is modified based on the NVIDIA RAPIDS Demo code and datasets and demonstrates how to use RAPIDS to accelerate an end-to-end task from the Extract-Transform-Load \(ETL\) phase to the Machine Learning \(ML\) Training phase on a GPU-accelerated instance. The RAPIDS cuDF library is used in the ETL phase and the XGBoost model is used in the ML Training phase. The sample code is based on the Dask framework and runs on a single machine.

**Note:** To obtain the official RAPIDS Demo code of NVIDIA, visit [Mortgage Demo](https://github.com/rapidsai/notebooks-contrib).

## Procedure

If you do not use a RAPIDS pre-installed image to create a GPU-accelerated instance, perform the following steps to use RAPIDS to accelerate machine learning tasks:

-   [Step 1: Obtain the NGC API key](#section_8uv_ue4_kj4)
-   [Step 2: Obtain the RAPIDS image download command](#section_6nn_fh6_3ro)
-   [Step 3: Deploy the RAPIDS environment](#section_4tf_rho_1gy)
-   [Step 4: Run RAPIDS Demo](#section_jlv_sqz_hzk)

## Step 1: Obtain the NGC API key

1.  Create an account on the [NGC registration page](https://ngc.nvidia.com/signup/register).

2.  Log on to the [NGC website](https://ngc.nvidia.com/signin/email).

3.  In the upper-right corner, click the username and select **Setup**. On the **Setup** page, click **Get API Key**.

4.  On the **API Key** page, click **Generate API Key**.

5.  In the **Generate a New API Key** message, click **Confirm**.

    **Note:** A new NGC API key overwrites the previous API key. Before you obtain a new API key, you must make sure that the previous API key is no longer needed.

6.  Copy the API key and save it to your local storage device.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0514488951/p46989.png)


## Step 2: Obtain the RAPIDS image download command

Perform the following steps to obtain the download command of the RAPIDS image:

1.  Log on to the [NGC website](https://ngc.nvidia.com/signin/email).

2.  On the page that appears, click the **CONTAINERS** tab and search for the **RAPIDS** image.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7328031161/p46841.png)

3.  Obtain the docker pull command.

    The sample code in this topic is based on the RAPIDS v0.8 image. Therefore, use the image that is tagged with v0.8 when you run the sample code. If you use another image, the corresponding commands may differ.

    1.  On the RAPIDS page, click the Tags tab.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7328031161/p47242.png)

    2.  Copy the tag information. `0.8-cuda10.0-runtime-ubuntu16.04-gcc5-py3.6` is copied in this example.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7328031161/p47223.png)

    3.  Return to the top of the page, find the **Pull Command** section, and copy the displayed command. Paste the copied command to the text editor. Then, replace the image version with the tag information obtained in the preceding step and save the file.

        In this example, `cuda9.2-runtime-ubuntu16.04` is replaced with `0.8-cuda10.0-runtime-ubuntu16.04-gcc5-py3.6`.

        The saved docker pull command is used to download the RAPIDS image. For more information about how to download the RAPIDS image, see the [Step 3: Deploy the RAPIDS environment](#section_4tf_rho_1gy) section.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1514488951/p46842.png)


## Step 3: Deploy the RAPIDS environment

Perform the following steps to deploy the RAPIDS environment:

1.  Create a GPU-accelerated instance. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

    Configure the following parameters:

    -   **Instance Type**: RAPIDS applies only to GPU models that use the NVIDIA Pascal or a later architecture. Therefore, you must select an instance type that meets the GPU requirements. The following instance families are available: gn6i, gn6v, gn5, and gn5i. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md). We recommend that you select an instance family that has larger video memory, such as gn6i, gn6v, or gn5. The GPU-accelerated instance that has a 16 GB video memory is used in this example.
    -   **Image**: Select `NVIDIA GPU Cloud Virtual Machine Image` in the Image Marketplace dialog box.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1514488951/p46839.png)

    -   **Public IP Address**: Select **Assign Public IPv4 Address** or attach an elastic IP address \(EIP\) after you create the GPU-accelerated instance. For more information, see [Associate an EIP with an ECS instance](/intl.en-US/User Guide/Associate an EIP with a cloud instance/Associate an EIP with an ECS instance.md).
    -   **Security Group**: Select a security group for which the following ports are enabled:
        -   TCP port 22, used for SSH logon
        -   TCP port 8888, used to access JupyterLab
        -   TCP port 8786 and TCP port 8787, used to access Dask
2.  Connect to the GPU-accelerated instance. For more information, see [Connection methods](/intl.en-US/Instance/Connect to instances/Overview.md).

3.  Enter the NGC API key and press the Enter key to log on to the NGC container.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1514488951/p46840.png)

4.  Run the nvidia-smi command to view GPU information, such as the GPU model and GPU driver version.

    We recommend that you check the GPU information to identify potential issues. For example, if an earlier NGC driver version is used, it may not be supported by the Docker image.

5.  Run the docker pull command to download the RAPIDS image.

    For more information about how to obtain the docker pull command, see the [Step 2: Obtain the RAPIDS image download command](#section_6nn_fh6_3ro) section.

    ```
    docker pull nvcr.io/nvidia/rapidsai/rapidsai:0.8-cuda10.0-runtime-ubuntu16.04-gcc5-py3.6
    ```

6.  View the downloaded image.

    We recommend that you view the Docker image information to ensure that the correct image is downloaded.

    ```
    docker images
    ```

7.  Run the NGC container to deploy the RAPIDS environment.

    ```
    docker run --runtime=nvidia \
            --rm -it \
            -p 8888:8888 \
            -p 8787:8787 \
            -p 8786:8786 \
            nvcr.io/nvidia/rapidsai/rapidsai:0.8-cuda10.0-runtime-ubuntu16.04-gcc5-py3.6
    ```


## Step 4: Run RAPIDS Demo

Perform the following steps to run RAPIDS Demo:

1.  Download the dataset and the Demo file on the GPU-accelerated instance.

    ```
    # Get apt source address and download demos.
    source_address=$(curl http://100.100.100.200/latest/meta-data/source-address|head -n 1)
    source_address="${source_address}/opsx/ecs/linux/binary/machine_learning/"
    cd /rapids
    wget $source_address/rapids_notebooks_v0.8.tar.gz
    tar -xzvf rapids_notebooks_v0.8.tar.gz
    cd /rapids/rapids_notebooks_v0.8/xgboost
    wget $source_address/data/mortgage/mortgage_2000_1gb.tgz
    ```

2.  Start JupyterLab on the GPU-accelerated instance.

    We recommend that you run the commands to start JupyterLab directly.

    ```
    # Run the following command to start JupyterLab and set the password.
    cd /rapids/rapids_notebooks_v0.8/xgboost
    jupyter-lab --allow-root --ip=0.0.0.0 --no-browser --NotebookApp.token='YOUR PASSWORD'
    # Exit JupyterLab.
    sh ../utils/stop-jupyter.sh
    ```

    -   You can also run the `sh ../utils/start-jupyter.sh` script to start JupyterLab. However, you cannot set the logon password if you run the script.
    -   You can also press `Ctrl+C` twice to exit JupyterLab.
3.  Open your browser and enter `http://IP address of your GPU-accelerated instance:8888` in the address bar to access JupyterLab.

    **Note:** We recommend that you use Google Chrome.

    If you set the logon password when you start JupyterLab, you are directed to a page to enter your password.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1514488951/p46852.png)

4.  Run the NoteBook code.

    A mortgage repayment task is used in this example. For more information, see the [Code running](#section_88w_0mw_i43) section. The NoteBook code includes the following content:

    -   xgboost\_E2E.ipynb: an XGBoost Demo file. You can double-click this file to view its details, or click the Execute icon to run one cell at a time.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1514488951/p46845.png)

    -   mortgage\_2000\_1gb.tgz: a file named mortgage\_2000\_1gb.tgz, which contains the mortgage repayment training data of year 2000. Files in the perf folder are split into files of 1 GB to maximize the usage of GPU video memory.

## Code running

In this example, XGBoost is used to demonstrate the end-to-end code running process from data pre-processing to training the XGBoost data model. The process involves the following phases:

-   ETL: performed on the GPU-accelerated instance in most cases. Data is extracted, transformed, and then loaded onto the data warehouse.
-   Data Conversion: performed on the GPU-accelerated instance. Data processed in the ETL phase is converted into the DMatrix format so that it can be used by XGBoost to train the data model.
-   ML-Training: performed on the GPU-accelerated instance by default. XGBoost is used to train the gradient boosting decision tree \(GBDT\).

Perform the following steps to run the NoteBook code:

1.  Prepare the dataset.

    In this example, the shell script downloads the mortgage repayment training data of year 2000 by default, which is the mortgage\_2000\_1gb.tgz file.

    If you want to obtain more data for XGBoost model training, you can set the download\_url parameter to specify the URL. For more information, visit [Mortgage Data](https://docs.rapids.ai/datasets/mortgage-data).

    The following figure shows an example.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1514488951/p46846.png)

2.  Set relevant parameters.

    |Parameter|Description|
    |---------|-----------|
    |start\_year|Specifies the start year from which the training data is selected. In the ETL phase, data generated between the start\_year and end\_year range is processed.|
    |end\_year|Specifies the end year from which the training data is selected. In the ETL phase, data generated between the start\_year and end\_year range is processed.|
    |train\_with\_gpu|Specifies whether to use GPU for XGBoost model training. Default value: True.|
    |gpu\_count|Specifies the number of workers to be started. Default value: 1. You can set the parameter based on your actual needs but the value must be less than the number of GPUs in the GPU-accelerated instance.|
    |part\_count|Specifies the number of performance files used for data model training. Default value: 2 × gpu\_count. If the value is too large, an insufficient memory error occurs in the Data Conversion phase and the error message is stored in the background of NoteBook.|

    The following figure shows an example.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1514488951/p46847.png)

3.  Start Dask.

    The NoteBook code starts Dask Scheduler, and also starts workers based on the gpu\_count value for ETL and data model training. After you start Dask, you can monitor tasks on the Dask Dashboard. For more information about how to start Dask, see the [Dask Dashboard](#section_x15_g1t_2f7) section.

    The following figure shows an example.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1514488951/p46848.png)

4.  Start the ETL phase.

    In this phase, tables are joined, grouped, aggregated, and sliced. The data format is DataFrame of the cuDF library, which is similar to Pandas DataFrame.

    The following figure shows an example.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1514488951/p46849.png)

5.  Start the Data Conversion phase.

    In this phase, DataFrame-format data is converted into the DMatrix-format data for XGBoost model training. Each worker processes one DMatrix object.

    The following figure shows an example.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1514488951/p46850.png)

6.  Start the ML Training phase.

    In this phase, data model training is started by dask-xgboost, which supports collaborative communication among Dask workers. At the bottom layer, dask-xgboost is also called to execute data model training.

    The following figure shows an example.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2514488951/p46851.png)


## Dask Dashboard

Dask Dashboard supports task progress tracking, task performance problem identification, and fault debugging.

After Dask is started, you can enter `http://IP address of your GPU-accelerated instance:8787/status` in the address bar of your browser to go to the Dask Dashboard page.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2514488951/p57733.gif)

## Related functions

|Operation|Function name|
|---------|-------------|
|Download a file.|def download\_file\_from\_url\(url, filename\):|
|Decompress a file.|def decompress\_file\(filename, path\):|
|Obtain the number of GPUs in the current machine.|def get\_gpu\_nums\(\):|
|Manage the GPU memory.|-   def initialize\_rmm\_pool\(\):
-   def initialize\_rmm\_no\_pool\(\):
-   def run\_dask\_task\(func, \*\*kwargs\): |
|Submit a Dask task.|-   def process\_quarter\_gpu\(year=2000, quarter=1, perf\_file=""\):
-   def run\_gpu\_workflow\(quarter=1, year=2000, perf\_file="", \*\*kwargs\): |
|Use cuDF to load data from a CSV file.|-   def gpu\_load\_performance\_csv\(performance\_path, \*\*kwargs\):
-   def gpu\_load\_acquisition\_csv\(acquisition\_path, \*\*kwargs\):
-   def gpu\_load\_names\(\*\*kwargs\): |
|Process and extract characteristics of data for training machine learning models.|-   def null\_workaround\(df, \*\*kwargs\):
-   def create\_ever\_features\(gdf, \*\*kwargs\):
-   def join\_ever\_delinq\_features\(everdf\_tmp, delinq\_merge, \*\*kwargs\):
-   def create\_joined\_df\(gdf, everdf, \*\*kwargs\):
-   def create\_12\_mon\_features\(joined\_df, \*\*kwargs\):
-   def combine\_joined\_12\_mon\(joined\_df, testdf, \*\*kwargs\):
-   def final\_performance\_delinquency\(gdf, joined\_df, \*\*kwargs\):
-   def join\_perf\_acq\_gdfs\(perf, acq, \*\*kwargs\):
-   def last\_mile\_cleaning\(df, \*\*kwargs\): |

