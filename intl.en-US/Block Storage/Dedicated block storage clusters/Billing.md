# Billing

This topic describes the billing of dedicated block storage clusters when you purchase or renew a dedicated block storage cluster or handle refunds.

## Purchase

Dedicated block storage clusters support only the subscription billing method.

Fees for a dedicated block storage cluster = Cluster capacity × Subscription duration × Unit price. The following table describes the cluster capacity, subscription duration, and unit price.

|Item|Description|
|----|-----------|
|Cluster capacity \(TiB\)|-   Minimum capacity: 72 TiB
-   Maximum capacity: 2,304 TiB

**Note:** The cluster capacity can only be increased by an increment of 12 TiB, and cannot be customized. |
|Subscription duration|The subscription duration ranges from six months to three years.|
|Unit price|The unit price displayed on the buy page prevails.|

## Renewal

Dedicated block storage clusters can be manually or automatically renewed.

-   When you manually renew a dedicated block storage cluster, the renewal duration ranges from three months to three years.
-   When you configure a dedicated block storage cluster to be automatically renewed, the dedicated block storage cluster is automatically renewed based on the purchase duration. For example, if you set the duration to 12 months when you purchase a dedicated block storage cluster, the cluster is automatically renewed by 12 months.

## Post-expiration processing of resources

Before your dedicated block storage cluster expires, the ECS console prompts you to determine whether to migrate your disk resources.

-   If you do not want to renew the dedicated block storage cluster after it expires, and if you do not need to retain the data in the cloud disks in the dedicated block storage cluster, you can configure the cloud disks to be automatically released when the dedicated block storage cluster expires.
-   If you do not want to renew the dedicated block storage cluster after it expires, but you want to retain the data in the cloud disks in the dedicated block storage cluster, you can migrate the cloud disks to the public cloud by using the ECS console.

