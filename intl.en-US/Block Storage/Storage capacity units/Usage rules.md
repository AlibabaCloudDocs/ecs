---
keyword: [Alibaba Cloud, SCU, storage capacity unit, budget, cost-efficiency]
---

# Usage rules

After you purchase a storage capacity unit \(SCU\) within a region, the SCU can be automatically applied to offset the bills of eligible pay-as-you-go storage resources within that region until the SCU expires. Storage resource usage beyond the capacity of the SCU is billed on a pay-as-you-go basis.

## Deduction factors

The amount of storage capacity that an SCU can offset varies based on the resource types to which the SCU is applied. To view the deduction factors of different resource types, visit the SCU buy page.

## Order of application

Object Storage Service \(OSS\) resource plans take precedence over SCUs to offset the bills of storage resources within the same account. For example, if you have both OSS resource plans and SCUs, the OSS resource plans are applied first.

## Examples

If you purchase a 10 TiB SCU in a region, this SCU can be applied to one of the following resource types to offset pay-as-you-go bills for up to a specific amount of capacity:

-   Disks: 2.5 TiB of enhanced SSDs \(ESSDs\) at performance level 3 \(PL3 ESSDs\), 5 TiB of ESSDs at performance level 2 \(PL2 ESSDs\), 10 TiB of ESSDs at performance level 1 \(PL1 ESSDs\), 20 TiB of ESSDs at performance level 0 \(PL0 ESSDs\), 10 TiB of standard SSDs, 28 TiB of ultra disks, or 33 TiB of basic disks
-   Snapshots: 83 TiB of snapshots
-   Apsara File System NAS \(NAS\) file systems: 28 TiB of Capacity NAS file systems or 5.4 TiB of Performance NAS file systems
-   OSS: 83 TiB of OSS Standard locally redundant storage \(LRS\) capacity, 66 TiB of OSS Standard zone-redundant storage \(ZRS\) capacity, 125 TiB of OSS Infrequent Access \(IA\) LRS capacity, 100 TiB of OSS IA ZRS capacity, or 303 TiB of OSS Archive LRS capacity
-   Hybrid Backup Recovery \(HBR\): 33.89 TiB of HBR backup storage capacity

**Note:** The preceding examples are for reference only. The amount of capacity for which an SCU can offset bills is calculated based on the deduction factors of the region to which the SCU belongs.

If you purchase a 10 TiB SCU when you use multiple types of storage resources, the SCU can be applied to a combination of different storage resource types.

-   Example 1: The SCU is applied to offset the bills for 10 TiB of PL1 ESSDs.
-   Example 2: The SCU is applied to offset the bills for 10 TiB of PL0 ESSDs and 5 TiB of PL1 ESSDs.
-   Example 3: The SCU is applied to offset the bills for 1 TiB of PL3 ESSDs, 2 TiB of PL2 ESSDs, and 2 TiB of PL1 ESSDs.
-   Example 4: The SCU is applied to offset the bills for 10 TiB out of 12 TiB of standard SSDs, and the left 2 TiB of standard SSDs is billed on a pay-as-you-go basis.
-   Example 5: The SCU is applied to offset the bills for 2 TiB of PL1 ESSDs, 1 TiB of Performance NAS file systems, 16 TiB of snapshots, 20 TiB of OSS Standard LRS capacity, and 5 TiB of HBR backup storage capacity.

![Example](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3669249161/p201678.png)

