---
keyword: [Alibaba Cloud, SCU, storage capacity unit, budget, cost-efficiency]
---

# Usage rules

After you purchase a storage capacity unit \(SCU\) in a region, the SCU can be automatically applied to offset bills of eligible pay-as-you-go storage resources within that region until the SCU expires. Storage resource usage beyond the capacity of the SCU is billed on a pay-as-you-go basis.

## Deduction factors

The amount of storage capacity that an SCU can offset varies based on the types of resources to which the SCU is applied. See the buy page for deduction factors of different resource types.

## Order of application

OSS resource plans take precedence over SCUs to offset bills of storage resources in the same account. For example, if you have both OSS resource plans and SCUs, the OSS resource plans are applied first.

## Examples

If you purchase a 10 TiB SCU in a region, the SCU can be applied to one of the following resource types to offset pay-as-you-go bills up to a specific amount of capacity:

-   Disks: 2.5 TiB of ESSDs at performance level 3 \(PL3 ESSDs\), 5 TiB of ESSDs at performance level 2 \(PL2 ESSDs\), 10 TiB of ESSDs at performance level 1 \(PL1 ESSDs\), 10 TiB of standard SSDs, 28 TiB of ultra disks, or 33 TiB of basic disks
-   Snapshots: 83 TiB of snapshots
-   NAS: 28 TiB of Capacity NAS file systems or 5.4 TiB of Performance NAS file systems
-   OSS: 83 TiB of OSS Standard \(locally redundant storage\) storage capacity

If you have purchased a 10 TiB SCU and are using multiple types of storage resources, the SCU can be applied to a combination of different types of storage resources.

-   Examples of how the SCU is applied to a combination of different categories of disks:

    -   Example 1: The SCU is applied to offset the bills for 10 TiB of PL1 ESSDs.
    -   Example 2: The SCU is applied to offset the bills for 5 TiB of PL1 ESSDs and 5 TiB of standard SSDs.
    -   Example 3: The SCU is applied to offset the bills for 1 TiB of PL3 ESSDs, 2 TiB of PL2 ESSDs, and 2 TiB of PL1 ESSDs.
    -   Example 4: The SCU is applied to offset the bills for 10 TiB out of 12 TiB of standard SSDs, and the left 2 TiB is billed on a pay-as-you-go basis.
    ![Examples of how the SCU is applied to offset disk bills](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4725714951/p63169.png)

-   Example of how the SCU is applied to a combination of resources of different storage services

    For example, the SCU is applied to offset the bills for 2 TiB of PL1 ESSDs, 1 TiB of Performance NAS file systems, 16 TiB of snapshots, and 33 TiB of OSS Standard storage capacity.

    ![Example of how the SCU is applied to offset bills of multiple resources](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4725714951/p114834.png)


