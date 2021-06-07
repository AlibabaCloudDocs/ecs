---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# GPU-accelerated compute optimized instance types

This topic describes the features of GPU-accelerated compute optimized instance families and lists the instance types of each family.

-   Recommended instance families
    -   [gn7, GPU-accelerated compute optimized instance family](#section_4xh_rvo_jxy)
    -   [vgn6i, lightweight GPU-accelerated compute optimized instance family](#section_dti_hon_urw)
    -   [gn6i, GPU-accelerated compute optimized instance family](#section_e88_tau_vwf)
    -   [gn6e, GPU-accelerated compute optimized instance family](#section_8gr_min_yk3)
    -   [gn6v, GPU-accelerated compute optimized instance family](#section_698_e4v_7rh)
-   Other available instance families
    -   [vgn5i, lightweight GPU-accelerated compute optimized instance family](#section_lip_fsm_g9e)
    -   [gn5, GPU-accelerated compute optimized instance family](#section_8ir_i5x_nvl)
    -   [gn5i, GPU-accelerated compute optimized instance family](#section_ye9_eyj_ek2)

## gn7, GPU-accelerated compute optimized instance family

This instance family is in invitational preview and unavailable for purchase.

Features

-   Compute:
    -   Uses NVIDIA A100 GPUs. NVSwitches are used to establish connections between NVIDIA A100 GPUs. The GPUs have the following features:
        -   Innovative Ampere architecture
        -   40 GB HBM2 memory per GPU
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports enhanced SSDs \(ESSDs\), standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning applications such as training applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications that have high GPU workloads such as computational fluid dynamics, computational finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|
|:------------|:----|:-------------|:---|:---------|--------------------|:------------------------------|:---------|:---|
|ecs.gn7-c12g1.3xlarge|12|95.0|NVIDIA A100 × 1|40 GB × 1|4.0|2,500|4|8|
|ecs.gn7-c13g1.13xlarge|52|380.0|NVIDIA A100 × 4|40 GB × 4|15.0|9,000|16|8|
|ecs.gn7-c13g1.26xlarge|104|760.0|NVIDIA A100 × 8|40 GB × 8|30.0|18,000|16|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## vgn6i, lightweight GPU-accelerated compute optimized instance family

Features

-   If you want your vgn6i instance to support graphics features such as Open Graphics Library \(OpenGL\), you must purchase a GRID license from [NVIDIA](https://www.nvidia.com/object/nvidia-enterprise-account.html). Then, you must create an instance and manually install a GRID driver and activate the license after the instance is created.
-   Compute:
    -   Uses NVIDIA T4 GPUs.
    -   Is equipped with vGPUs that are generated from GPU virtualization with mediated pass-through.
        -   Supports the 1/4 and 1/2 computing capacity of NVIDIA Tesla T4 GPUs.
        -   Supports 4 GB and 8 GB of GPU video memory.
    -   Offers a CPU-to-memory ratio of 1:5.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Real-time rendering for cloud games
    -   Real-time rendering for AR and VR applications
    -   AI \(deep learning and machine learning\) inference for elastic Internet service deployment
    -   Educational environment of deep learning
    -   Modeling experiment environment of deep learning

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:---|:---------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.vgn6i-m4.xlarge|4|23.0|NVIDIA T4 × 1/4|16 GB × 1/4|3.0|500|2|4|10|
|ecs.vgn6i-m8.2xlarge|10|46.0|NVIDIA T4 × 1/2|16GB × 1/2|4.0|800|4|5|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn6i, GPU-accelerated compute optimized instance family

Features

-   Compute:
    -   Uses NVIDIA T4 GPUs that have the following features:
        -   Innovative NVIDIA Turing architecture
        -   16 GB memory per GPU \(320 GB/s bandwidth\)
        -   2,560 CUDA cores per GPU
        -   Up to 320 Turing Tensor cores per GPU
        -   Mixed-precision Tensor cores that support 65 FP16 TFLOPS, 130 INT8 TOPS, and 260 INT4 TOPS
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports standard SSDs, ultra disks, and ESSDs that deliver millions of IOPS.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   AI \(deep learning and machine learning\) inference for computer vision, speech recognition, speech synthesis, natural language processing \(NLP\), machine translation, and recommendation systems
    -   Real-time rendering for cloud games
    -   Real-time rendering for AR and VR applications
    -   Graphics workstations or overloaded graphics computing
    -   GPU-accelerated databases
    -   High-performance computing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|Baseline storage IOPS|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:---|:---------|--------------------|:------------------------------|---------------------|:---------|:---|----------------------------|
|ecs.gn6i-c4g1.xlarge|4|15.0|NVIDIA T4 × 1|16 GB × 1|4.0|500|None|2|2|10|
|ecs.gn6i-c8g1.2xlarge|8|31.0|NVIDIA T4 × 1|16 GB × 1|5.0|800|None|2|2|10|
|ecs.gn6i-c16g1.4xlarge|16|62.0|NVIDIA T4 × 1|16 GB × 1|6.0|1,000|None|4|3|10|
|ecs.gn6i-c24g1.6xlarge|24|93.0|NVIDIA T4 × 1|16 GB × 1|7.5|1,200|None|6|4|10|
|ecs.gn6i-c24g1.12xlarge|48|186.0|NVIDIA T4 × 2|16 GB × 2|15.0|2,400|None|12|6|10|
|ecs.gn6i-c24g1.24xlarge|96|372.0|NVIDIA T4 × 4|16 GB × 4|30.0|4,800|250,000|24|8|10|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn6e, GPU-accelerated compute optimized instance family

Features

-   Compute:
    -   Uses NVIDIA V100 GPUs that each have 32 GB of GPU memory and support NVLink.
    -   Uses NVIDIA V100 GPUs \(SXM2-based\) that have the following features:
        -   Innovative Volta architecture
        -   32 GB HBM2 memory per GPU \(900 GB/s bandwidth\)
        -   5,120 CUDA cores per GPU
        -   640 Tensor cores per GPU
        -   Up to six NVLink links and a total bandwidth of 300 GB/s \(25 GB/s per NVlink link per direction\)
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning applications such as training and inference applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications such as fluid dynamics, finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:---|:---------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.gn6e-c12g1.3xlarge|12|92.0|NVIDIA V100 × 1|32 GB× 1|5.0|800|8|6|10|
|ecs.gn6e-c12g1.12xlarge|48|368.0|NVIDIA V100 × 4|32 GB × 4|16.0|2,400|8|8|20|
|ecs.gn6e-c12g1.24xlarge|96|736.0|NVIDIA V100 × 8|32 GB × 8|32.0|4,800|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn6v, GPU-accelerated compute optimized instance family

Features

-   Compute:
    -   Uses NVIDIA V100 GPUs.
    -   Uses NVIDIA V100 GPUs \(SXM2-based\) that have the following features:
        -   Innovative Volta architecture
        -   16 GB HBM2 memory per GPU \(900 GB/s bandwidth\)
        -   5,120 CUDA cores per GPU
        -   640 Tensor cores per GPU
        -   Up to six NVLink links and a total bandwidth of 300 GB/s \(25 GB/s per NVlink link per direction\)
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning applications such as training and inference applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications such as fluid dynamics, finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|Baseline storage IOPS|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:---|:---------|:-------------------|:------------------------------|---------------------|:---------|:---|----------------------------|
|ecs.gn6v-c8g1.2xlarge|8|32.0|NVIDIA V100 × 1|16 GB × 1|2.5|800|None|4|4|10|
|ecs.gn6v-c8g1.8xlarge|32|128.0|NVIDIA V100 × 4|16 GB × 4|10.0|2,000|None|8|8|20|
|ecs.gn6v-c8g1.16xlarge|64|256.0|NVIDIA V100 × 8|16 GB × 8|20.0|2,500|None|16|8|20|
|ecs.gn6v-c10g1.20xlarge|82|336.0|NVIDIA V100 × 8|16 GB × 8|32.0|4,500|250,000|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## vgn5i, lightweight GPU-accelerated compute optimized instance family

Features

-   If you want your vgn5i instance to support graphics features such as Open Graphics Library \(OpenGL\), you must purchase a GRID license from [NVIDIA](https://www.nvidia.com/object/nvidia-enterprise-account.html). Then, you must create an instance, and manually install a GRID driver and activate the license after the instance is created.
-   Compute:
    -   Uses NVIDIA P4 GPUs.
    -   Is equipped with vGPUs that are generated from GPU virtualization with mediated pass-through.
        -   Supports the 1/8, 1/4, 1/2, and 1/1 computing capacity of NVIDIA Tesla P4 GPUs.
        -   Supports 1 GB, 2 GB, 4 GB, and 8 GB of GPU memory.
    -   Offers a CPU-to-memory ratio of 1:3.
    -   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Real-time rendering for cloud games
    -   Real-time rendering for AR and VR applications
    -   AI \(deep learning and machine learning\) inference for elastic Internet service deployment
    -   Educational environment of deep learning
    -   Modeling experiment environment of deep learning

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:---|:---------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.vgn5i-m1.large|2|6.0|NVIDIA P4 × 1/8|8 GB × 1/8|1.0|300|2|2|6|
|ecs.vgn5i-m2.xlarge|4|12.0|NVIDIA P4 × 1/4|8 GB × 1/4|2.0|500|2|3|10|
|ecs.vgn5i-m4.2xlarge|8|24.0|NVIDIA P4 × 1/2|8 GB × 1/2|3.0|800|2|4|10|
|ecs.vgn5i-m8.4xlarge|16|48.0|NVIDIA P4 × 1|8 GB × 1|5.0|1,000|4|5|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn5, GPU-accelerated compute optimized instance family

Features

-   Compute:
    -   Uses NVIDIA P100 GPUs.
    -   Offers multiple CPU-to-memory ratios.
    -   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors.
-   Storage:
    -   Supports high-performance local NVMe SSDs.
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning
    -   Scientific computing applications, such as fluid dynamics, finance, genomics, and environmental analysis
    -   Server-side GPU compute workloads such as high-performance computing, rendering, and multi-media encoding and decoding

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|GPUs|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:--------------------|:---|:---------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.gn5-c4g1.xlarge|4|30.0|440|NVIDIA P100 × 1|16 GB × 1|3.0|300|1|3|10|
|ecs.gn5-c8g1.2xlarge|8|60.0|440|NVIDIA P100 × 1|16 GB × 1|3.0|400|1|4|10|
|ecs.gn5-c4g1.2xlarge|8|60.0|880|NVIDIA P100 × 2|16 GB × 2|5.0|1,000|2|4|10|
|ecs.gn5-c8g1.4xlarge|16|120.0|880|NVIDIA P100 × 2|16 GB × 2|5.0|1,000|4|8|20|
|ecs.gn5-c28g1.7xlarge|28|112.0|440|NVIDIA P100 × 1|16 GB × 1|5.0|1,000|8|8|20|
|ecs.gn5-c8g1.8xlarge|32|240.0|1,760|NVIDIA P100 × 4|16 GB × 4|10.0|2,000|8|8|20|
|ecs.gn5-c28g1.14xlarge|56|224.0|880|NVIDIA P100 × 2|16 GB × 2|10.0|2,000|14|8|20|
|ecs.gn5-c8g1.14xlarge|54|480.0|3,520|NVIDIA P100 × 8|16 GB × 8|25.0|4,000|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn5i, GPU-accelerated compute optimized instance family

Features

-   Compute:
    -   Uses NVIDIA P4 GPUs.
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning inference
    -   Server-side GPU compute workloads such as multi-media encoding and decoding

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:---|:---------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.gn5i-c2g1.large|2|8.0|NVIDIA P4 × 1|8 GB × 1|1.0|100|2|2|6|
|ecs.gn5i-c4g1.xlarge|4|16.0|NVIDIA P4 × 1|8 GB × 1|1.5|200|2|3|10|
|ecs.gn5i-c8g1.2xlarge|8|32.0|NVIDIA P4 × 1|8 GB × 1|2.0|400|4|4|10|
|ecs.gn5i-c16g1.4xlarge|16|64.0|NVIDIA P4 × 1|8 GB × 1|3.0|800|4|8|20|
|ecs.gn5i-c16g1.8xlarge|32|128.0|NVIDIA P4 × 2|8 GB × 2|6.0|1,200|8|8|20|
|ecs.gn5i-c28g1.14xlarge|56|224.0|NVIDIA P4 × 2|8 GB × 2|10.0|2,000|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

