---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# GPU-accelerated compute optimized instance families

This topic describes the features of GPU-accelerated compute optimized instance families and lists the instance types of each family.

-   Recommended instance families
    -   [vgn6i, lightweight GPU-accelerated compute optimized instance family](#section_dti_hon_urw)
    -   [gn6i, GPU-accelerated compute optimized instance family](#section_e88_tau_vwf)
    -   [gn6e, GPU-accelerated compute optimized instance family](#section_8gr_min_yk3)
    -   [gn6v, GPU-accelerated compute optimized instance family](#section_698_e4v_7rh)
-   Other available instance families
    -   [vgn5i, lightweight GPU-accelerated compute optimized instance family](#section_lip_fsm_g9e)
    -   [gn5, GPU-accelerated compute optimized instance family](#section_8ir_i5x_nvl)
    -   [gn5i, GPU-accelerated compute optimized instance family](#section_ye9_eyj_ek2)

## vgn6i, lightweight GPU-accelerated compute optimized instance family

vgn6i is in invitational preview. To use vgn6i, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Uses NVIDIA T4 GPU computing accelerators.
-   Contains virtual GPUs generated from GPU slice virtualization.
    -   Supports the 1/4 and 1/2 computing capacity of NVIDIA Tesla T4 GPUs.
    -   Supports 4 GB and 8 GB of GPU video memory.
-   Offers a CPU-to-memory ratio of 1:5.
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors.
-   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   Real-time rendering for cloud games
    -   Real-time rendering for AR and VR applications
    -   AI \(deep learning and machine learning\) inference for elastic Internet service deployment
    -   Educational environment of deep learning
    -   Modeling experiment environment of deep learning

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:--|:----------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.vgn6i-m4.xlarge|4|23.0|None|T4\*1/4|4|3.0|500|Yes|2|4|10|
|ecs.vgn6i-m8.2xlarge|10|46.0|None|T4\*1/2|8|4.0|800|Yes|4|5|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn6i, GPU-accelerated compute optimized instance family

Features

-   Is an instance family in which all instances are I/O optimized.
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors.
-   Supports enhanced SSDs \(ESSDs\) that deliver millions of IOPS, standard SSDs, and ultra disks.
-   Uses NVIDIA T4 GPU computing accelerators that feature:
    -   New NVIDIA Turing architecture
    -   16 GB memory \(320 GB/s bandwidth\) per GPU
    -   Up to 2,560 CUDA cores per GPU
    -   Up to 320 Turing Tensor cores per GPU
    -   Mixed-precision Tensor cores that support 65 FP16 TFLOPS, 130 INT8 TOPS, and 260 INT4 TOPS
-   Provides high network performance based on large computing capacity.
-   Suitable for the following scenarios:
    -   AI \(deep learning and machine learning\) inference for computer vision, speech recognition, speech synthesis, natural language processing \(NLP\), machine translation, and recommendation systems
    -   Real-time rendering for cloud games
    -   Real-time rendering for AR and VR applications
    -   Graphics workstations or overloaded graphics computing
    -   GPU-accelerated databases
    -   High-performance computing

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:--|:----------------|--------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.gn6i-c4g1.xlarge|4|15.0|None|T4\*1|16|4.0|500|Yes|2|2|10|
|ecs.gn6i-c8g1.2xlarge|8|31.0|None|T4\*1|16|5.0|800|Yes|2|2|10|
|ecs.gn6i-c16g1.4xlarge|16|62.0|None|T4\*1|16|6.0|1,000|Yes|4|3|10|
|ecs.gn6i-c24g1.6xlarge|24|93.0|None|T4\*1|16|7.5|1,200|Yes|6|4|10|
|ecs.gn6i-c24g1.12xlarge|48|186.0|None|T4\*2|32|15.0|2,400|Yes|12|6|10|
|ecs.gn6i-c24g1.24xlarge|96|372.0|None|T4\*4|64|30.0|4,800|Yes|24|8|10|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn6e, GPU-accelerated compute optimized instance family

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Uses NVIDIA V100 \(32 GB NVLink\) GPU processors.
-   Offers a CPU-to-memory ratio of 1:8.
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors.
-   Uses NVIDIA V100 GPU computing accelerators \(SXM2-based\) that feature:
    -   New NVIDIA Volta architecture
    -   32 GB HBM2 GPU memory \(900 GB/s bandwidth\) per GPU
    -   Up to 5,120 CUDA cores per GPU
    -   Up to 640 Tensor cores per GPU
    -   Support for up to six NVLink connections and a total bandwidth of 300 GB/s \(25 GB/s per connection\)
-   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   Deep learning applications such as training and inference applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications such as fluid dynamics, finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:--|:----------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.gn6e-c12g1.3xlarge|12|92.0|None|V100\*1|32|5.0|800|Yes|8|6|10|
|ecs.gn6e-c12g1.12xlarge|48|368.0|None|V100\*4|128|16.0|2,400|Yes|8|8|20|
|ecs.gn6e-c12g1.24xlarge|96|736.0|None|V100\*8|256|32.0|4,800|Yes|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn6v, GPU-accelerated compute optimized instance family

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Uses NVIDIA V100 GPU processors.
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors.
-   Uses NVIDIA V100 GPU computing accelerators \(SXM2-based\) that feature:
    -   New NVIDIA Volta architecture
    -   16 GB HBM2 GPU memory \(900 GB/s bandwidth\) per GPU
    -   Up to 5,120 CUDA cores per GPU
    -   Up to 640 Tensor cores per GPU
    -   Support for up to six NVLink connections and a total bandwidth of 300 GB/s \(25 GB/s per connection\)
-   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   Deep learning applications such as training and inference applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications such as fluid dynamics, finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:--|:----------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.gn6v-c8g1.2xlarge|8|32.0|None|1 \* NVIDIA V100|1 \* 16|2.5|800|Yes|4|4|10|
|ecs.gn6v-c8g1.8xlarge|32|128.0|None|4 \* NVIDIA V100|4 \* 16|10.0|2,000|Yes|8|8|20|
|ecs.gn6v-c8g1.16xlarge|64|256.0|None|8 \* NVIDIA V100|8 \* 16|20.0|2,500|Yes|16|8|20|
|ecs.gn6v-c10g1.20xlarge|82|336.0|None|8 \* NVIDIA V100|8 \* 16|32.0|4,500|Yes|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## vgn5i, lightweight GPU-accelerated compute optimized instance family

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Uses NVIDIA P4 GPU computing accelerators.
-   Contains virtual GPUs generated from GPU slice virtualization.
    -   Supports the 1/8, 1/4, 1/2, and 1/1 computing capacity of NVIDIA Tesla P4 GPUs.
    -   Supports 1 GB, 2 GB, 4 GB, and 8 GB of GPU video memory.
-   Offers a CPU-to-memory ratio of 1:3.
-   Uses 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) processors.
-   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   Real-time rendering for cloud games
    -   Real-time rendering for AR and VR applications
    -   AI \(deep learning and machine learning\) inference for elastic Internet service deployment
    -   Educational environment of deep learning
    -   Modeling experiment environment of deep learning

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:--|:----------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.vgn5i-m1.large|2|6.0|None|P4\*1/8|1|1.0|300|Yes|2|2|6|
|ecs.vgn5i-m2.xlarge|4|12.0|None|P4\*1/4|2|2.0|500|Yes|2|3|10|
|ecs.vgn5i-m4.2xlarge|8|24.0|None|P4\*1/2|4|3.0|800|Yes|2|4|10|
|ecs.vgn5i-m8.4xlarge|16|48.0|None|P4\*1|8|5.0|1,000|Yes|4|5|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn5, GPU-accelerated compute optimized instance family

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Uses NVIDIA P100 GPU processors.
-   Offers multiple CPU-to-memory ratios.
-   Supports high-performance local NVMe SSDs.
-   Uses 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) processors.
-   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   Deep learning
    -   Scientific computing applications such as fluid dynamics, finance, genomics, and environmental analysis
    -   Server-side GPU compute workloads such as high-performance computing, rendering, and multi-media encoding and decoding

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:--|:----------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.gn5-c4g1.xlarge|4|30.0|440|1 \* NVIDIA P100|1 \* 16|3.0|300|No|1|3|10|
|ecs.gn5-c8g1.2xlarge|8|60.0|440|1 \* NVIDIA P100|1 \* 16|3.0|400|No|1|4|10|
|ecs.gn5-c4g1.2xlarge|8|60.0|880|2 \* NVIDIA P100|2 \* 16|5.0|1,000|No|2|4|10|
|ecs.gn5-c8g1.4xlarge|16|120.0|880|2 \* NVIDIA P100|2 \* 16|5.0|1,000|No|4|8|20|
|ecs.gn5-c28g1.7xlarge|28|112.0|440|1 \* NVIDIA P100|1 \* 16|5.0|1,000|No|8|8|20|
|ecs.gn5-c8g1.8xlarge|32|240.0|1760|4 \* NVIDIA P100|4 \* 16|10.0|2,000|No|8|8|20|
|ecs.gn5-c28g1.14xlarge|56|224.0|880|2 \* NVIDIA P100|2 \* 16|10.0|2,000|No|14|8|20|
|ecs.gn5-c8g1.14xlarge|54|480.0|3520|8 \* NVIDIA P100|8 \* 16|25.0|4,000|No|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn5i, GPU-accelerated compute optimized instance family

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Uses NVIDIA P4 GPU processors.
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) processors.
-   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   Deep learning inference
    -   Server-side GPU compute workloads such as multi-media encoding and decoding

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:--|:----------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.gn5i-c2g1.large|2|8.0|None|1 \* NVIDIA P4|1 \* 8|1.0|100|Yes|2|2|6|
|ecs.gn5i-c4g1.xlarge|4|16.0|None|1 \* NVIDIA P4|1 \* 8|1.5|200|Yes|2|3|10|
|ecs.gn5i-c8g1.2xlarge|8|32.0|None|1 \* NVIDIA P4|1 \* 8|2.0|400|Yes|4|4|10|
|ecs.gn5i-c16g1.4xlarge|16|64.0|None|1 \* NVIDIA P4|1 \* 8|3.0|800|Yes|4|8|20|
|ecs.gn5i-c16g1.8xlarge|32|128.0|None|2 \* NVIDIA P4|2 \* 8|6.0|1,200|Yes|8|8|20|
|ecs.gn5i-c28g1.14xlarge|56|224.0|None|2 \* NVIDIA P4|2 \* 8|10.0|2,000|Yes|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

