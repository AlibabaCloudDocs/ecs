---
keyword: [Alibaba Cloud, SCU, storage package, storage cost, capacity package, pay-as-you-go]
---

# Storage capacity units

You can use storage capacity units \(SCUs\) to offset the pay-as-you-go bills of storage resources such as disks, Object Storage Service \(OSS\) buckets, Apsara File Storage NAS \(NAS\) file systems, and snapshots. SCUs use the subscription billing method and support the all upfront payment method.

## Billing

SCUs use the subscription billing method and are billed based on their capacity and validity periods. For more information about pricing, visit the Pricing tab on the [Storage Capacity Unit](https://www.alibabacloud.com/product/scu/pricing) page.

-   SCU capacity: For information about the capacity specifications that SCUs support, see [Overview](/intl.en-US/Block Storage/Storage capacity units/Overview.md).
-   Validity period: You can subscribe to an SCU for a period of one month, two months, three months, six months, one year, three years, or five years. For annual or multi-year subscription, you can receive some discounts.

SCUs support only the all upfront payment method. You must make a full payment at purchase.

Sum = Validity period × SCU capacity × SCU unit price. Unit: USD.

## Usage rules

After you purchase an SCU in a region, the SCU automatically matches eligible pay-as-you-go storage resources within that region to offset their bills until the SCU expires. When the deductible used capacity exceeds the SCU capacity, the excess capacity is billed on a pay-as-you-go basis.

The amount of storage capacity that an SCU can offset varies based on the types of resources to which the SCU is applied. For more information, see [Usage rules](/intl.en-US/Block Storage/Storage capacity units/Usage rules.md).

## Expiration

After an SCU expires, you cannot use it to offset the bills of pay-as-you-go storage resources. If you have no other SCUs within the same region as the expired SCU, the pay-as-you-go storage resources are billed on a pay-as-you-go basis.

## Renewal or upgrade

SCUs cannot be renewed or upgraded. You can purchase multiple SCUs based on your storage usage.

-   If an SCU is insufficient to offset the bills of pay-as-you-go storage resources, you can purchase more SCUs.
-   If an SCU is about to expire, you can purchase more SCUs and specify a time for them to take effect.

