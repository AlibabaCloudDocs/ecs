# API概览

云服务器ECS提供以下相关API接口。

## 实例

|API|描述|
|---|--|
|[RunInstances](/intl.zh-CN/API参考/实例/RunInstances.md)|调用RunInstances创建一台或多台按量付费或者包年包月ECS实例。|
|[CreateInstance](/intl.zh-CN/API参考/实例/CreateInstance.md)|调用CreateInstance创建一台包年包月或者按量付费ECS实例。|
|[StartInstance](/intl.zh-CN/API参考/实例/StartInstance.md)|调用StartInstance启动一台实例。|
|[StopInstance](/intl.zh-CN/API参考/实例/StopInstance.md)|调用StopInstance停止运行一台实例。|
|[RebootInstance](/intl.zh-CN/API参考/实例/RebootInstance.md)|当一台ECS实例处于运行中（Running）状态时，调用RebootInstance可以重启这台实例。|
|[DeleteInstance](/intl.zh-CN/API参考/实例/DeleteInstance.md)|调用DeleteInstance释放一台按量付费实例或者到期的包年包月实例。|
|[StartInstances](/intl.zh-CN/API参考/实例/StartInstances.md)|调用StartInstances启动一台或多台处于已停止（Stopped）状态的ECS实例。|
|[RebootInstances](/intl.zh-CN/API参考/实例/RebootInstances.md)|调用RebootInstances重启一台或多台处于运行中（Running）状态的ECS实例。|
|[StopInstances](/intl.zh-CN/API参考/实例/StopInstances.md)|调用StopInstances停止一台或多台运行中（Running）的ECS实例。|
|[AttachInstanceRamRole](/intl.zh-CN/API参考/实例/AttachInstanceRamRole.md)|调用AttachInstanceRamRole为一台或多台ECS实例授予实例RAM角色。如果实例已有RAM角色，则报错提示您不能附加新的角色。|
|[DetachInstanceRamRole](/intl.zh-CN/API参考/实例/DetachInstanceRamRole.md)|调用DetachInstanceRamRole收回一台或多台ECS实例的实例RAM角色。|
|[DescribeInstanceStatus](/intl.zh-CN/API参考/实例/DescribeInstanceStatus.md)|调用DescribeInstanceStatus获取一台或多台ECS实例的状态信息。|
|[DescribeInstances](/intl.zh-CN/API参考/实例/DescribeInstances.md)|调用DescribeInstances查询一台或多台ECS实例的详细信息。|
|[DescribeInstanceVncUrl](/intl.zh-CN/API参考/实例/DescribeInstanceVncUrl.md)|调用DescribeInstanceVncUrl查询一台ECS实例的Web管理终端地址。|
|[DescribeUserData](/intl.zh-CN/API参考/实例/DescribeUserData.md)|调用DescribeUserData查询一台ECS实例的自定义数据。|
|[DescribeInstanceAutoRenewAttribute](/intl.zh-CN/API参考/实例/DescribeInstanceAutoRenewAttribute.md)|调用DescribeInstanceAutoRenewAttribute查询一台或多台包年包月ECS实例自动续费状态。|
|[DescribeInstanceRamRole](/intl.zh-CN/API参考/实例/DescribeInstanceRamRole.md)|调用DescribeInstanceRamRole查询一台或者多台ECS实例上的已赋予的实例RAM角色。|
|[DescribeSpotPriceHistory](/intl.zh-CN/API参考/实例/DescribeSpotPriceHistory.md)|调用DescribeSpotPriceHistory查询抢占式实例近30天内的历史价格。|
|[DescribeSpotAdvice](/intl.zh-CN/API参考/实例/DescribeSpotAdvice.md)|调用DescribeSpotAdvice查询指定地域下，抢占式实例近30天的实例平均释放率、平均折扣率等信息。|
|[DescribeInstanceTypeFamilies](/intl.zh-CN/API参考/实例/DescribeInstanceTypeFamilies.md)|调用DescribeInstanceTypeFamilies查询云服务器ECS提供的实例规格族资源。|
|[DescribeInstanceTypes](/intl.zh-CN/API参考/实例/DescribeInstanceTypes.md)|调用DescribeInstanceTypes查询云服务器ECS提供的实例规格资源。|
|[ModifyInstanceAttribute](/intl.zh-CN/API参考/实例/ModifyInstanceAttribute.md)|调用ModifyInstanceAttribute修改一台ECS实例的部分信息，包括实例密码、名称、描述、主机名和自定义数据等。如果是突发性能实例，可以切换这台实例的性能突发模式。|
|[ModifyInstanceVncPasswd](/intl.zh-CN/API参考/实例/ModifyInstanceVncPasswd.md)|调用ModifyInstanceVncPasswd修改一台ECS实例的Web管理终端密码。|
|[ModifyInstanceAutoReleaseTime](/intl.zh-CN/API参考/实例/ModifyInstanceAutoReleaseTime.md)|调用ModifyInstanceAutoReleaseTime为一台按量付费ECS实例设定或者取消自动释放时间。设置自动释放时请谨慎操作，配置的时间到期后将自动释放ECS实例。|
|[ModifyInstanceAutoRenewAttribute](/intl.zh-CN/API参考/实例/ModifyInstanceAutoRenewAttribute.md)|调用ModifyInstanceAutoRenewAttribute设置一台或多台包年包月实例的自动续费状态。为了减少您的资源到期维护成本，包年包月ECS实例可以设置自动续费。|
|[ModifyInstanceChargeType](/intl.zh-CN/API参考/实例/ModifyInstanceChargeType.md)|调用ModifyInstanceChargeType更换一台或者多台ECS实例的计费方式。支持在按量付费实例和包年包月实例间相互转换，同时可以将实例挂载的所有按量付费云盘转换为包年包月云盘。|
|[ModifyInstanceSpec](/intl.zh-CN/API参考/实例/ModifyInstanceSpec.md)|调用ModifyInstanceSpec调整一台按量付费ECS实例的实例规格和公网带宽大小。|
|[ModifyPrepayInstanceSpec](/intl.zh-CN/API参考/实例/ModifyPrepayInstanceSpec.md)|调用ModifyPrepayInstanceSpec升级或者降低一台包年包月ECS实例的实例规格，新实例规格将会覆盖实例的整个生命周期。|
|[ModifyInstanceMetadataOptions](/intl.zh-CN/API参考/实例/ModifyInstanceMetadataOptions.md)|调用ModifyInstanceMetadataOptions修改一台实例的元数据信息。|
|[RenewInstance](/intl.zh-CN/API参考/实例/RenewInstance.md)|调用RenewInstance续费一台包年包月ECS实例。|
|[ReactivateInstances](/intl.zh-CN/API参考/实例/ReActivateInstances.md)|重新启动一台已过期或欠费回收中的按量付费ECS实例。|
|[DeleteInstances](/intl.zh-CN/API参考/实例/DeleteInstances.md)|调用DeleteInstances释放一台或多台按量付费ECS实例或者到期的包年包月ECS实例。|

## 专有宿主机

|API|描述|
|---|--|
|[AllocateDedicatedHosts](/intl.zh-CN/API参考/专有宿主机/AllocateDedicatedHosts.md)|调用AllocateDedicatedHosts创建一台或多台按量付费或者包年包月专有宿主机。专有宿主机是单租户独享的物理机资源，您可以在专有宿主机上自行创建ECS实例和获取物理服务器属性等信息。|
|[CreateDedicatedHostCluster](/intl.zh-CN/API参考/专有宿主机/CreateDedicatedHostCluster.md)|调用CreateDedicatedHostCluster创建一个专有宿主机集群。|
|[DescribeDedicatedHostClusters](/intl.zh-CN/API参考/专有宿主机/DescribeDedicatedHostClusters.md)|调用DescribeDedicatedHostClusters查询一个或多个专有宿主机集群的详细信息。|
|[ModifyDedicatedHostClusterAttribute](/intl.zh-CN/API参考/专有宿主机/ModifyDedicatedHostClusterAttribute.md)|调用ModifyDedicatedHostClusterAttribute修改一台专有宿主机集群的部分信息，包括专有宿主机集群的名称、描述信息、属性等。|
|[DeleteDedicatedHostCluster](/intl.zh-CN/API参考/专有宿主机/DeleteDedicatedHostCluster.md)|调用DeleteDedicatedHostCluster删除一个专有宿主机集群。|
|[RenewDedicatedHosts](/intl.zh-CN/API参考/专有宿主机/RenewDedicatedHosts.md)|调用RenewDedicatedHosts续费一台或者多台包年包月专有宿主机。|
|[ReleaseDedicatedHost](/intl.zh-CN/API参考/专有宿主机/ReleaseDedicatedHost.md)|调用ReleaseDedicatedHost释放一台按量付费专有宿主机。|
|[RedeployDedicatedHost](/intl.zh-CN/API参考/专有宿主机/RedeployDedicatedHost.md)|调用RedeployDedicatedHost执行专有宿主机的故障迁移。|
|[DescribeDedicatedHosts](/intl.zh-CN/API参考/专有宿主机/DescribeDedicatedHosts.md)|调用DescribeDedicatedHosts查询一台或多台专有宿主机的详细信息，包括专有宿主机的物理性能指标、机器码、使用状态和已创建的ECS实例列表等。|
|[DescribeDedicatedHostTypes](/intl.zh-CN/API参考/专有宿主机/DescribeDedicatedHostTypes.md)|调用DescribeDedicatedHostTypes查询指定地域下支持的专有宿主机规格详细参数，或者查询专有宿主机支持的ECS实例规格族。|
|[DescribeDedicatedHostAutoRenew](/intl.zh-CN/API参考/专有宿主机/DescribeDedicatedHostAutoRenew.md)|调用DescribeDedicatedHostAutoRenew查询一台或多台包年包月专有宿主机自动续费状态。|
|[ModifyInstanceDeployment](/intl.zh-CN/API参考/专有宿主机/ModifyInstanceDeployment.md)|调用ModifyInstanceDeployment修改ECS实例的宿主机。ECS实例与目标宿主机必须位于同一地域。|
|[ModifyDedicatedHostAttribute](/intl.zh-CN/API参考/专有宿主机/ModifyDedicatedHostAttribute.md)|调用ModifyDedicatedHostAttribute修改一台专有宿主机的部分信息，包括专有宿主机的名称、描述和服务不可用属性等。|
|[ModifyDedicatedHostAutoReleaseTime](/intl.zh-CN/API参考/专有宿主机/ModifyDedicatedHostAutoReleaseTime.md)|调用ModifyDedicatedHostAutoReleaseTime为一台按量付费专有宿主机设定自动释放时间，或者取消自动释放一台按量付费专有宿主机。|
|[ModifyDedicatedHostAutoRenewAttribute](/intl.zh-CN/API参考/专有宿主机/ModifyDedicatedHostAutoRenewAttribute.md)|调用ModifyDedicatedHostAutoRenewAttribute为一台或多台包年包月专有宿主机设置自动续费，也可以取消已设定的自动续费。|
|[ModifyDedicatedHostsChargeType](/intl.zh-CN/API参考/专有宿主机/ModifyDedicatedHostsChargeType.md)|调用ModifyDedicatedHostsChargeType修改专有宿主机的付费类型。|

## 启动模板

|API|描述|
|---|--|
|[CreateLaunchTemplate](/intl.zh-CN/API参考/启动模板/CreateLaunchTemplate.md)|调用CreateLaunchTemplate创建一个实例启动模板，简称模板。实例启动模板能免除您每次创建实例时都需要填入大量配置参数。|
|[CreateLaunchTemplateVersion](/intl.zh-CN/API参考/启动模板/CreateLaunchTemplateVersion.md)|调用CreateLaunchTemplateVersion根据指定的实例启动模板创建一个版本。|
|[DeleteLaunchTemplate](/intl.zh-CN/API参考/启动模板/DeleteLaunchTemplate.md)|调用DeleteLaunchTemplate删除一个实例启动模板。|
|[DeleteLaunchTemplateVersion](/intl.zh-CN/API参考/启动模板/DeleteLaunchTemplateVersion.md)|调用DeleteLaunchTemplateVersion删除指定实例启动模板的一个版本。不支持删除默认版本，您需要通过DeleteLaunchTemplate删除整个实例启动模板才能删除默认版本。|
|[DescribeLaunchTemplates](/intl.zh-CN/API参考/启动模板/DescribeLaunchTemplates.md)|调用DescribeLaunchTemplates查询一个或多个可用的实例启动模板。|
|[DescribeLaunchTemplateVersions](/intl.zh-CN/API参考/启动模板/DescribeLaunchTemplateVersions.md)|调用DescribeLaunchTemplateVersions查询实例启动模板版本。|
|[ModifyLaunchTemplateDefaultVersion](/intl.zh-CN/API参考/启动模板/ModifyLaunchTemplateDefaultVersion.md)|调用ModifyLaunchTemplateDefaultVersion切换启动模板的某个版本为该模板的默认版本。如果您在创建实例（RunInstances）时不指定模板版本号，会采用默认版本。|

## 资源保障

|API|描述|
|---|--|
|[CreateElasticityAssurance](/intl.zh-CN/API参考/资源保障/CreateElasticityAssurance.md)|调用CreateElasticityAssurance创建弹性保障服务。|
|[CreateCapacityReservation](/intl.zh-CN/API参考/资源保障/CreateCapacityReservation.md)|调用CreateCapacityReservation创建容量预定服务。|
|[DescribeElasticityAssurances](/intl.zh-CN/API参考/资源保障/DescribeElasticityAssurances.md)|调用DescribeElasticityAssurances查询弹性保障服务的详细信息。|
|[DescribeElasticityAssuranceInstances](/intl.zh-CN/API参考/资源保障/DescribeElasticityAssuranceInstances.md)|调用DescribeElasticityAssuranceInstances查询弹性保障服务已匹配的运行状态的实例列表。|
|[DescribeCapacityReservations](/intl.zh-CN/API参考/资源保障/DescribeCapacityReservations.md)|调用DescribeCapacityReservations查询一个或多个容量预定服务的详细信息。|
|[DescribeCapacityReservationInstances](/intl.zh-CN/API参考/资源保障/DescribeCapacityReservationInstances.md)|调用DescribeCapacityReservationInstances查询容量预定服务已匹配的实例列表。|
|[DescribeInstanceAttachmentAttributes](/intl.zh-CN/API参考/资源保障/DescribeInstanceAttachmentAttributes.md)|调用DescribeInstanceAttachmentAttributes查询实例匹配的私有池信息。|
|[ModifyElasticityAssurance](/intl.zh-CN/API参考/资源保障/ModifyElasticityAssurance.md)|调用ModifyElasticityAssurance修改一个弹性保障服务的名称与描述信息。|
|[ModifyCapacityReservation](/intl.zh-CN/API参考/资源保障/ModifyCapacityReservation.md)|调用ModifyCapacityReservation修改一个容量预定服务的部分信息，包括容量预定服务的名称、描述信息、失效方式以及预留的实例总数量。|
|[ModifyInstanceAttachmentAttributes](/intl.zh-CN/API参考/资源保障/ModifyInstanceAttachmentAttributes.md)|调用ModifyInstanceAttachmentAttributes修改实例的私有池的属性。|
|[ReleaseCapacityReservation](/intl.zh-CN/API参考/资源保障/ReleaseCapacityReservation.md)|调用ReleaseCapacityReservation释放容量预定服务。|

## 弹性供应组

|API|描述|
|---|--|
|[CreateAutoProvisioningGroup](/intl.zh-CN/API参考/弹性供应组/CreateAutoProvisioningGroup.md)|调用CreateAutoProvisioningGroup接口创建一个弹性供应组。|
|[ModifyAutoProvisioningGroup](/intl.zh-CN/API参考/弹性供应组/ModifyAutoProvisioningGroup.md)|调用ModifyAutoProvisioningGroup接口修改一个弹性供应组的设置。|
|[DeleteAutoProvisioningGroup](/intl.zh-CN/API参考/弹性供应组/DeleteAutoProvisioningGroup.md)|调用DeleteAutoProvisioningGroup接口删除一个弹性供应组。|
|[DescribeAutoProvisioningGroupInstances](/intl.zh-CN/API参考/弹性供应组/DescribeAutoProvisioningGroupInstances.md)|调用DescribeAutoProvisioningGroupInstances查询指定弹性供应组下的实例。|
|[DescribeAutoProvisioningGroups](/intl.zh-CN/API参考/弹性供应组/DescribeAutoProvisioningGroups.md)|调用DescribeAutoProvisioningGroups接口查询弹性供应组。|
|[DescribeAutoProvisioningGroupHistory](/intl.zh-CN/API参考/弹性供应组/DescribeAutoProvisioningGroupHistory.md)|调用DescribeAutoProvisioningGroupHistory接口查询弹性供应组的调度任务信息。|

## 块存储

|API|描述|
|---|--|
|[CreateDisk](/intl.zh-CN/API参考/磁盘/CreateDisk.md)|调用CreateDisk创建一块按量付费或包年包月数据盘。云盘类型包括普通云盘、高效云盘、SSD云盘和ESSD云盘。|
|[DeleteDisk](/intl.zh-CN/API参考/磁盘/DeleteDisk.md)|调用DeleteDisk释放一块按量付费数据盘。磁盘类型包括普通云盘、高效云盘、SSD云盘和ESSD云盘。|
|[DescribeDisks](/intl.zh-CN/API参考/磁盘/DescribeDisks.md)|调用DescribeDisks查询一块或多块您已经创建的云盘以及本地盘。|
|[AttachDisk](/intl.zh-CN/API参考/磁盘/AttachDisk.md)|调用AttachDisk为一台ECS实例挂载一块按量付费数据盘。|
|[DetachDisk](/intl.zh-CN/API参考/磁盘/DetachDisk.md)|调用DetachDisk从一台实例上卸载一块按量付费磁盘。磁盘类型包括普通云盘、高效云盘和SSD云盘。|
|[ModifyDiskAttribute](/intl.zh-CN/API参考/磁盘/ModifyDiskAttribute.md)|调用ModifyDiskAttribute修改您的磁盘的属性或者明细。|
|[ReplaceSystemDisk](/intl.zh-CN/API参考/磁盘/ReplaceSystemDisk.md)|调用ReplaceSystemDisk更换一台ECS实例的系统盘或者操作系统。|
|[ReInitDisk](/intl.zh-CN/API参考/磁盘/ReInitDisk.md)|调用ReInitDisk重新初始化一块云盘到创建时的初始状态。|
|[ResetDisk](/intl.zh-CN/API参考/磁盘/ResetDisk.md)|调用ResetDisk使用磁盘的历史快照回滚至某一阶段的磁盘状态。|
|[ResizeDisk](/intl.zh-CN/API参考/磁盘/ResizeDisk.md)|调用ResizeDisk扩容一块云盘，支持扩容系统盘和数据盘。|
|[ModifyDiskChargeType](/intl.zh-CN/API参考/磁盘/ModifyDiskChargeType.md)|调用ModifyDiskChargeType修改一台实例上挂载的一块或最多16块云盘的计费方式。|
|[ModifyDiskSpec](/intl.zh-CN/API参考/磁盘/ModifyDiskSpec.md)|调用ModifyDiskSpec升级一块ESSD云盘的性能等级。|

## 预留实例券

|API|描述|
|---|--|
|[PurchaseReservedInstancesOffering](/intl.zh-CN/API参考/预留实例券/PurchaseReservedInstancesOffering.md)|调用PurchaseReservedInstancesOffering购买一张预留实例券。预留实例券可以自动匹配对应的ECS实例，抵扣按量付费实例账单。|
|[DescribeReservedInstances](/intl.zh-CN/API参考/预留实例券/DescribeReservedInstances.md)|调用DescribeReservedInstances查询已经购买的预留实例券。|
|[ModifyReservedInstances](/intl.zh-CN/API参考/预留实例券/ModifyReservedInstances.md)|您可以通过ModifyReservedInstances更改预留实例券。|

## 存储容量单位包

|API|描述|
|---|--|
|[PurchaseStorageCapacityUnit](/intl.zh-CN/API参考/存储容量单位包/PurchaseStorageCapacityUnit.md)|调用PurchaseStorageCapacityUnit购买一个或多个存储容量单位包SCU（Storage Capacity Unit）。|
|[ModifyStorageCapacityUnitAttribute](/intl.zh-CN/API参考/存储容量单位包/ModifyStorageCapacityUnitAttribute.md)|调用ModifyStorageCapacityUnitAttribute修改一个存储容量单位包SCU的名称或者描述信息。|
|[DescribeStorageCapacityUnits](/intl.zh-CN/API参考/存储容量单位包/DescribeStorageCapacityUnits.md)|调用DescribeStorageCapacityUnits查询一个或多个存储容量单位包SCU的详细信息。|

## 镜像

|API|描述|
|---|--|
|[CreateImage](/intl.zh-CN/API参考/镜像/CreateImage.md)|调用CreateImage创建一份自定义镜像。您可以使用创建的自定义镜像创建ECS实例（RunInstances）或者更换实例的系统盘（ReplaceSystemDisk）。|
|[ImportImage](/intl.zh-CN/API参考/镜像/ImportImage.md)|调用ImportImage导入您已有的镜像文件到云服务器ECS，并作为自定义镜像出现在相应地域中。|
|[ExportImage](/intl.zh-CN/API参考/镜像/ExportImage.md)|调用ExportImage导出您的自定义镜像到与该自定义镜像同一地域的OSS Bucket里。|
|[CopyImage](/intl.zh-CN/API参考/镜像/CopyImage.md)|调用CopyImage复制一个地域下的自定义镜像到其他地域。复制镜像可以实现跨地域部署ECS实例、跨地域复制ECS实例等目的。|
|[CancelCopyImage](/intl.zh-CN/API参考/镜像/CancelCopyImage.md)|调用CancelCopyImage取消正在进行中的复制镜像（CopyImage）任务。|
|[DescribeImages](/intl.zh-CN/API参考/镜像/DescribeImages.md)|调用DescribeImages查询您可以使用的镜像资源。|
|[DeleteImage](/intl.zh-CN/API参考/镜像/DeleteImage.md)|调用DeleteImage删除一份自定义镜像。|
|[DescribeImageSharePermission](/intl.zh-CN/API参考/镜像/DescribeImageSharePermission.md)|调用DescribeImageSharePermission查询一份自定义镜像已经共享的所有用户。返回结果支持分页显示，每页的信息条目默认为10条。|
|[ModifyImageAttribute](/intl.zh-CN/API参考/镜像/ModifyImageAttribute.md)|调用ModifyImageAttribute修改一份自定义镜像的名称或描述信息。|
|[ModifyImageSharePermission](/intl.zh-CN/API参考/镜像/ModifyImageSharePermission.md)|调用ModifyImageSharePermission管理镜像共享权限。您可以将自己的自定义镜像共享给其他阿里云用户，该用户可以使用共享的自定义镜像创建ECS实例（RunInstances）或者更换实例的系统盘（ReplaceSystemDisk）。|
|[DescribeImageSupportInstanceTypes](/intl.zh-CN/API参考/镜像/DescribeImageSupportInstanceTypes.md)|调用DescribeImageSupportInstanceTypes查询指定镜像支持的实例规格。|
|[DescribeImageFromFamily](/intl.zh-CN/API参考/镜像/DescribeImageFromFamily.md)|调用DescribeImageFromFamily查询指定镜像族系内最新创建的可用自定义镜像。|

## 快照

|API|描述|
|---|--|
|[CreateSnapshot](/intl.zh-CN/API参考/快照/CreateSnapshot.md)|调用CreateSnapshot为一块云盘创建一份快照。|
|[CreateAutoSnapshotPolicy](/intl.zh-CN/API参考/快照/CreateAutoSnapshotPolicy.md)|调用CreateAutoSnapshotPolicy创建一条自动快照策略。|
|[CreateSnapshotGroup](/intl.zh-CN/API参考/快照/CreateSnapshotGroup.md)|调用CreateSnapshotGroup为指定ECS实例中的云盘创建实例快照。实例快照包含一个或多个云盘对应的快照。|
|[ApplyAutoSnapshotPolicy](/intl.zh-CN/API参考/快照/ApplyAutoSnapshotPolicy.md)|调用ApplyAutoSnapshotPolicy为一块或者多块云盘应用自动快照策略。目标云盘已经应用了自动快照策略时，调用ApplyAutoSnapshotPolicy可以更换云盘当前应用的自动快照策略。|
|[CopySnapshot](/intl.zh-CN/API参考/快照/CopySnapshot.md)|调用CopySnapshot将一份普通快照从一个地域复制到另一个地域。|
|[ResetDisks](/intl.zh-CN/API参考/快照/ResetDisks.md)|调用ResetDisks通过实例快照回滚一个或多个云盘。|
|[DeleteSnapshot](/intl.zh-CN/API参考/快照/DeleteSnapshot.md)|调用DeleteSnapshot删除指定的快照。如果需要取消正在创建的快照，也可以调用该接口删除快照，即取消创建快照任务。|
|[CancelAutoSnapshotPolicy](/intl.zh-CN/API参考/快照/CancelAutoSnapshotPolicy.md)|调用CancelAutoSnapshotPolicy取消一块或者多块云盘的自动快照策略。|
|[DeleteAutoSnapshotPolicy](/intl.zh-CN/API参考/快照/DeleteAutoSnapshotPolicy.md)|删除一条自动快照策略。如果目标自动快照策略已经被应用到磁盘上，删除自动快照策略后，这些磁盘不再执行该策略。|
|[DeleteSnapshotGroup](/intl.zh-CN/API参考/快照/DeleteSnapshotGroup.md)|调用DeleteSnapshotGroup删除指定的实例快照。|
|[DescribeAutoSnapshotPolicyEX](/intl.zh-CN/API参考/快照/DescribeAutoSnapshotPolicyEX.md)|调用DescribeAutoSnapshotPolicyEX查询您已创建的自动快照策略。|
|[DescribeSnapshots](/intl.zh-CN/API参考/快照/DescribeSnapshots.md)|调用DescribeSnapshots查询一台ECS实例或一块云盘所有的快照列表。InstanceId、DiskId和SnapshotIds不是必需参数，但是可以构建过滤器逻辑，参数之间为逻辑与（And）关系。|
|[DescribeSnapshotLinks](/intl.zh-CN/API参考/快照/DescribeSnapshotLinks.md)|调用DescribeSnapshotLinks查询云盘快照链。快照链是一块云盘所有快照组成的关系链，一块云盘对应一条快照链。|
|[DescribeSnapshotGroups](/intl.zh-CN/API参考/快照/DescribeSnapshotGroups.md)|调用DescribeSnapshotGroups查询一个或多个实例快照的信息。|
|[DescribeSnapshotsUsage](/intl.zh-CN/API参考/快照/DescribeSnapshotsUsage.md)|调用DescribeSnapshotsUsage查询您在一个地域下的快照数量以及快照容量。|
|[ModifyAutoSnapshotPolicyEx](/intl.zh-CN/API参考/快照/ModifyAutoSnapshotPolicyEx.md)|调用ModifyAutoSnapshotPolicyEx修改一条自动快照策略。修改自动快照策略后，之前已应用该策略的云盘随即执行修改后的自动快照策略。|
|[ModifySnapshotAttribute](/intl.zh-CN/API参考/快照/ModifySnapshotAttribute.md)|调用ModifySnapshotAttribute修改一份快照的名称或描述。|
|[ModifySnapshotGroup](/intl.zh-CN/API参考/快照/ModifySnapshotGroup.md)|调用ModifySnapshotGroup修改指定实例快照的名称与描述信息。|

## 前缀列表

|API|描述|
|---|--|
|[CreatePrefixList](/intl.zh-CN/API参考/前缀列表/CreatePrefixList.md)|调用CreatePrefixList创建一个前缀列表。|
|[DescribePrefixLists](/intl.zh-CN/API参考/前缀列表/DescribePrefixLists.md)|调用DescribePrefixLists查询一个或多个前缀列表的信息。|
|[DescribePrefixListAssociations](/intl.zh-CN/API参考/前缀列表/DescribePrefixListAssociations.md)|调用DescribePrefixListAssociations查询指定前缀列表已关联的资源信息。|
|[DescribePrefixListAttributes](/intl.zh-CN/API参考/前缀列表/DescribePrefixListAttributes.md)|调用DescribePrefixListAttributes查询指定前缀列表的详细信息，包含前缀列表的名称、地址族、最大条目容量以及条目的详细信息等。|
|[ModifyPrefixList](/intl.zh-CN/API参考/前缀列表/ModifyPrefixList.md)|调用ModifyPrefixList修改指定前缀列表的名称、描述和条目。|
|[DeletePrefixList](/intl.zh-CN/API参考/前缀列表/DeletePrefixList.md)|调用DeletePrefixList删除指定的前缀列表，同时删除前缀列表中的所有条目。|

## 安全组

|API|描述|
|---|--|
|[CreateSecurityGroup](/intl.zh-CN/API参考/安全组/CreateSecurityGroup.md)|调用CreateSecurityGroup新建一个安全组。新建的安全组，默认只允许安全组内的实例互相访问，安全组外的一切通信请求会被拒绝。若您想允许其他安全组实例的通信请求，或者来自互联网的访问请求，需要授权安全组权限（AuthorizeSecurityGroup）。|
|[AuthorizeSecurityGroup](/intl.zh-CN/API参考/安全组/AuthorizeSecurityGroup.md)|调用AuthorizeSecurityGroup增加一条安全组入方向规则。指定安全组入方向的访问权限，允许或者拒绝其他设备发送入方向流量到安全组里的实例。|
|[AuthorizeSecurityGroupEgress](/intl.zh-CN/API参考/安全组/AuthorizeSecurityGroupEgress.md)|调用AuthorizeSecurityGroupEgress增加一条安全组出方向规则。指定安全组出方向的访问权限，允许或者拒绝安全组里的实例发送出方向流量到其他设备。|
|[RevokeSecurityGroup](/intl.zh-CN/API参考/安全组/RevokeSecurityGroup.md)|调用RevokeSecurityGroup删除一条安全组入方向规则，撤销安全组入方向的权限设置。|
|[RevokeSecurityGroupEgress](/intl.zh-CN/API参考/安全组/RevokeSecurityGroupEgress.md)|调用RevokeSecurityGroupEgress删除一条安全组出方向规则，撤销安全组出方向的访问权限。|
|[JoinSecurityGroup](/intl.zh-CN/API参考/安全组/JoinSecurityGroup.md)|调用JoinSecurityGroup将一台ECS实例加入到指定的安全组。|
|[LeaveSecurityGroup](/intl.zh-CN/API参考/安全组/LeaveSecurityGroup.md)|调用LeaveSecurityGroup将一台ECS实例移出指定的安全组。|
|[DeleteSecurityGroup](/intl.zh-CN/API参考/安全组/DeleteSecurityGroup.md)|调用DeleteSecurityGroup删除一个安全组。|
|[DescribeSecurityGroupAttribute](/intl.zh-CN/API参考/安全组/DescribeSecurityGroupAttribute.md)|调用DescribeSecurityGroupAttribute查询一个安全组的安全组规则。|
|[DescribeSecurityGroups](/intl.zh-CN/API参考/安全组/DescribeSecurityGroups.md)|调用DescribeSecurityGroups查询您创建的安全组的基本信息，例如安全组ID和安全组描述等。返回列表按照安全组ID降序排列。|
|[DescribeSecurityGroupReferences](/intl.zh-CN/API参考/安全组/DescribeSecurityGroupReferences.md)|调用DescribeSecurityGroupReferences查询一个安全组和其他哪些安全组有安全组级别的授权行为。|
|[ModifySecurityGroupAttribute](/intl.zh-CN/API参考/安全组/ModifySecurityGroupAttribute.md)|调用ModifySecurityGroupAttribute修改指定安全组的属性，包括修改安全组名称和描述。|
|[ModifySecurityGroupPolicy](/intl.zh-CN/API参考/安全组/ModifySecurityGroupPolicy.md)|调用ModifySecurityGroupPolicy修改安全组内网连通策略。|
|[ModifySecurityGroupRule](/intl.zh-CN/API参考/安全组/ModifySecurityGroupRule.md)|调用ModifySecurityGroupRule修改安全组入方向规则的描述信息。如果您还没有增加过安全组规则，可以调用AuthorizeSecurityGroup增加。|
|[ModifySecurityGroupEgressRule](/intl.zh-CN/API参考/安全组/ModifySecurityGroupEgressRule.md)|调用ModifySecurityGroupEgressRule修改安全组出方向规则的描述信息。如果您还没有增加过安全组规则，可以调用AuthorizeSecurityGroupEgress增加。|

## 部署集

|API|描述|
|---|--|
|[CreateDeploymentSet](/intl.zh-CN/API参考/部署集/CreateDeploymentSet.md)|调用CreateDeploymentSet在指定的地域内创建一个部署集。|
|[DeleteDeploymentSet](/intl.zh-CN/API参考/部署集/DeleteDeploymentSet.md)|调用DeleteDeploymentSet删除一个部署集。|
|[ModifyDeploymentSetAttribute](/intl.zh-CN/API参考/部署集/ModifyDeploymentSetAttribute.md)|调用ModifyDeploymentSetAttribute修改一个部署集的名称和描述信息。|
|[DescribeDeploymentSets](/intl.zh-CN/API参考/部署集/DescribeDeploymentSets.md)|调用DescribeDeploymentSets查询一个或多个部署集的属性列表。|
|[DescribeDeploymentSetSupportedInstanceTypeFamily](/intl.zh-CN/API参考/部署集/DescribeDeploymentSetSupportedInstanceTypeFamily.md)|调用DescribeDeploymentSetSupportedInstanceTypeFamily查询支持部署集的实例规格族。|

## SSH密钥对

|API|描述|
|---|--|
|[CreateKeyPair](/intl.zh-CN/API参考/SSH 密钥对/CreateKeyPair.md)|调用CreateKeyPair创建一对SSH密钥对。我们会为您保管密钥的公钥部分，并返回未加密的PEM编码的PKCS\#8格式私钥。您需要自行妥善保管私钥部分。|
|[ImportKeyPair](/intl.zh-CN/API参考/SSH 密钥对/ImportKeyPair.md)|调用ImportKeyPair导入由其他工具产生的RSA密钥对的公钥部分。导入密钥对后，阿里云为您保管公钥部分，您需要自行妥善保存密钥对的私钥部分。|
|[AttachKeyPair](/intl.zh-CN/API参考/SSH 密钥对/AttachKeyPair.md)|调用AttachKeyPair绑定一个SSH密钥对到一台或多台Linux实例。|
|[DetachKeyPair](/intl.zh-CN/API参考/SSH 密钥对/DetachKeyPair.md)|调用DetachKeyPair为一台或者多台Linux实例解绑SSH密钥对。|
|[DeleteKeyPairs](/intl.zh-CN/API参考/SSH 密钥对/DeleteKeyPairs.md)|调用DeleteKeyPairs删除一对或者多对SSH密钥对。删除SSH密钥对后，我们不再为您保存该SSH密钥对，但是已经绑定的实例可以正常使用该SSH密钥对，其SSH密钥对名称仍然显示在实例详情中。|
|[DescribeKeyPairs](/intl.zh-CN/API参考/SSH 密钥对/DescribeKeyPairs.md)|调用DescribeKeyPairs查询一个或多个密钥对。|

## 网络

|API|描述|
|---|--|
|[ModifyInstanceVpcAttribute](/intl.zh-CN/API参考/网络/ModifyInstanceVpcAttribute.md)|调用ModifyInstanceVpcAttribute修改一台ECS实例的专有网络VPC属性。|
|[AllocatePublicIpAddress](/intl.zh-CN/API参考/网络/AllocatePublicIpAddress.md)|调用AllocatePublicIpAddress为一台ECS实例分配一个公网IP地址。|
|[ConvertNatPublicIpToEip](/intl.zh-CN/API参考/网络/ConvertNatPublicIpToEip.md)|调用ConvertNatPublicIpToEip将一台网络类型为专有网络VPC的ECS实例的公网IP（PublicIp）转化为弹性公网IP（EIP）。|
|[AttachClassicLinkVpc](/intl.zh-CN/API参考/网络/AttachClassicLinkVpc.md)|调用AttachClassicLinkVpc将一台经典网络类型实例连接到专有网络VPC中，使经典网络类型实例可以和VPC中的云资源私网互通。|
|[DetachClassicLinkVpc](/intl.zh-CN/API参考/网络/DetachClassicLinkVpc.md)|调用DetachClassicLinkVpc取消经典网络类型实例与专有网络VPC的连接（ClassicLink）。取消ClassicLink后，经典网络类型实例无法与VPC互通。|
|[DescribeBandwidthLimitation](/intl.zh-CN/API参考/网络/DescribeBandwidthLimitation.md)|调用DescribeBandwidthLimitation查询带宽资源列表。|
|[DescribeClassicLinkInstances](/intl.zh-CN/API参考/网络/DescribeClassicLinkInstances.md)|调用DescribeClassicLinkInstances查询一台或多台与专有网络VPC建立了连接的经典网络类型实例。|
|[ModifyInstanceNetworkSpec](/intl.zh-CN/API参考/网络/ModifyInstanceNetworkSpec.md)|调用ModifyInstanceNetworkSpec修改实例的带宽配置。当实例现有网络规格不满足要求时，可以通过修改实例的带宽配置提高网络性能。|

## 弹性网卡

|API|描述|
|---|--|
|[CreateNetworkInterface](/intl.zh-CN/API参考/弹性网卡/CreateNetworkInterface.md)|调用CreateNetworkInterface创建一个弹性网卡（ENI）。|
|[AttachNetworkInterface](/intl.zh-CN/API参考/弹性网卡/AttachNetworkInterface.md)|调用AttachNetworkInterface附加弹性网卡（ENI）到专有网络（VPC）类型实例上。|
|[DetachNetworkInterface](/intl.zh-CN/API参考/弹性网卡/DetachNetworkInterface.md)|调用DetachNetworkInterface从一台实例上分离一个弹性网卡（ENI）。|
|[DeleteNetworkInterface](/intl.zh-CN/API参考/弹性网卡/DeleteNetworkInterface.md)|调用DeleteNetworkInterface删除一个弹性网卡（ENI）。|
|[DescribeNetworkInterfaces](/intl.zh-CN/API参考/弹性网卡/DescribeNetworkInterfaces.md)|调用DescribeNetworkInterfaces查看弹性网卡（ENI）列表。|
|[ModifyNetworkInterfaceAttribute](/intl.zh-CN/API参考/弹性网卡/ModifyNetworkInterfaceAttribute.md)|调用ModifyNetworkInterfaceAttribute修改一个弹性网卡（ENI）的属性。例如，弹性网卡名称、描述以及所属安全组等。|
|[AssignPrivateIpAddresses](/intl.zh-CN/API参考/弹性网卡/AssignPrivateIpAddresses.md)|调用AssignPrivateIpAddresses为一块弹性网卡分配一个或多个辅助私有IP地址。可以为网卡指定在所属虚拟交换机（VSwitch）的CIDR私有IP地址，或者通过指定私有网络地址数量自动创建私有IP地址。|
|[UnassignPrivateIpAddresses](/intl.zh-CN/API参考/弹性网卡/UnassignPrivateIpAddresses.md)|调用UnassignPrivateIpAddresses从一块弹性网卡删除一个或多个辅助私有IP地址。|

## 系统事件

|API|描述|
|---|--|
|[DescribeDisksFullStatus](/intl.zh-CN/API参考/系统事件/DescribeDisksFullStatus.md)|调用DescribeDisksFullStatus查询一块或多块块存储的全部状态信息。|
|[DescribeInstancesFullStatus](/intl.zh-CN/API参考/系统事件/DescribeInstancesFullStatus.md)|调用DescribeInstancesFullStatus查询一台或多台实例的全状态信息。全状态信息包括实例状态和实例系统事件状态，其中，实例状态为实例的生命周期状态，实例系统事件为维护事件的健康状态。|
|[DescribeInstanceHistoryEvents](/intl.zh-CN/API参考/系统事件/DescribeInstanceHistoryEvents.md)|调用DescribeInstanceHistoryEvents查询指定实例的系统事件信息，默认查询处于非活跃状态的历史系统事件。|
|[CancelSimulatedSystemEvents](/intl.zh-CN/API参考/系统事件/CancelSimulatedSystemEvents.md)|调用CancelSimulatedSystemEvents取消一件或多件处于Scheduled（计划中）或Executing（执行中）状态的模拟系统事件。取消系统事件后，模拟事件变为Canceled（已取消）状态。|
|[CreateSimulatedSystemEvents](/intl.zh-CN/API参考/系统事件/CreateSimulatedSystemEvents.md)|调用CreateSimulatedSystemEvents为一台或多台ECS实例预约模拟系统事件。模拟系统事件相当于事件演习，不会真正执行事件，也不会对ECS实例产生影响。|
|[AcceptInquiredSystemEvent](/intl.zh-CN/API参考/系统事件/AcceptInquiredSystemEvent.md)|调用AcceptInquiredSystemEvent接受并授权执行系统事件操作。对问询中（Inquiring）状态的系统事件，接受系统事件的默认操作，授权系统执行默认操作。|

## 高性能集群

|API|描述|
|---|--|
|[DeleteHpcCluster](/intl.zh-CN/API参考/高性能集群/DeleteHpcCluster.md)|调用DeleteHpcCluster删除一个HPC集群。|
|[CreateHpcCluster](/intl.zh-CN/API参考/高性能集群/CreateHpcCluster.md)|调用CreateHpcCluster创建一个HPC集群。|
|[DescribeHpcClusters](/intl.zh-CN/API参考/高性能集群/DescribeHpcClusters.md)|调用DescribeHpcClusters查询您可用的HPC集群。请求参数作为筛选器（Filter）使用，筛选关系为逻辑与（&&）关系，参数之间无依赖关系。|
|[ModifyHpcClusterAttribute](/intl.zh-CN/API参考/高性能集群/ModifyHpcClusterAttribute.md)|调用ModifyHpcClusterAttribute修改一个HPC集群的描述信息。|

## 运维与监控

|API|描述|
|---|--|
|[GetInstanceScreenshot](/intl.zh-CN/API参考/运维与监控/GetInstanceScreenshot.md)|调用GetInstanceScreenshot获取实例的截屏信息。|
|[GetInstanceConsoleOutput](/intl.zh-CN/API参考/运维与监控/GetInstanceConsoleOutput.md)|调用GetInstanceConsoleOutput获取一台实例的系统命令行输出，数据以Base64编码后返回。|
|[DescribeDiskMonitorData](/intl.zh-CN/API参考/运维与监控/DescribeDiskMonitorData.md)|调用DescribeDiskMonitorData查询一块云盘指定时间内的使用信息。|
|[DescribeInstanceMonitorData](/intl.zh-CN/API参考/运维与监控/DescribeInstanceMonitorData.md)|调用DescribeInstanceMonitorData查询一台ECS实例的监控信息。可查询的指标包括ECS实例的vCPU使用率、突发性能实例积分、接收的数据流量、发送的数据流量、平均带宽等。|
|[DescribeEniMonitorData](/intl.zh-CN/API参考/运维与监控/DescribeEniMonitorData.md)|调用DescribeEniMonitorData查询一块辅助网卡在指定时间段内使用的流量信息。|
|[DescribeSnapshotMonitorData](/intl.zh-CN/API参考/运维与监控/DescribeSnapshotMonitorData.md)|调用DescribeSnapshotMonitorData查询一个地域下近30天内的快照容量变化监控数据。|
|[DescribeInstanceMaintenanceAttributes](/intl.zh-CN/API参考/运维与监控/DescribeInstanceMaintenanceAttributes.md)|调用DescribeInstanceMaintenanceAttributes查询实例的维护属性。|
|[ModifyInstanceMaintenanceAttributes](/intl.zh-CN/API参考/运维与监控/ModifyInstanceMaintenanceAttributes.md)|调用ModifyInstanceMaintenanceAttributes修改实例的维护属性。|
|[RedeployInstance](/intl.zh-CN/API参考/运维与监控/RedeployInstance.md)|当ECS实例收到系统事件通知时，调用RedeployInstance可以重新部署这台ECS实例。|
|[ReportInstancesStatus](/intl.zh-CN/API参考/运维与监控/ReportInstancesStatus.md)|调用ReportInstancesStatus反馈一台或者多台ECS实例的异常问题。您可以反馈多台ECS实例发生的相同问题，也可以反馈一台ECS实例的多块磁盘发生的相同问题。|

## 云助手

|API|描述|
|---|--|
|[CreateCommand](/intl.zh-CN/API参考/云助手/CreateCommand.md)|调用CreateCommand新建一条云助手命令。|
|[InvokeCommand](/intl.zh-CN/API参考/云助手/InvokeCommand.md)|调用InvokeCommand为一台或多台ECS实例触发一条云助手命令。|
|[StopInvocation](/intl.zh-CN/API参考/云助手/StopInvocation.md)|调用StopInvocation停止一台或多台ECS实例中一条正在进行中（Running）的云助手命令进程。|
|[DisableActivation](/intl.zh-CN/API参考/云助手/DisableActivation.md)|调用DisableActivation手动禁用指定的激活码。|
|[ModifyCommand](/intl.zh-CN/API参考/云助手/ModifyCommand.md)|调用ModifyCommand修改一条云助手命令相关参数以及命令内容。|
|[DeleteCommand](/intl.zh-CN/API参考/云助手/DeleteCommand.md)|调用DeleteCommand删除一条云助手命令。|
|[DeregisterManagedInstance](/intl.zh-CN/API参考/云助手/DeregisterManagedInstance.md)|调用DeregisterManagedInstance注销一个托管实例。注销后您将无法再使用云助手向实例发送命令或文件。|
|[DescribeCommands](/intl.zh-CN/API参考/云助手/DescribeCommands.md)|调用DescribeCommands查询您已经创建的云助手命令。只输入参数Action和RegionId，不输入其他任何请求参数，则默认查询您所有可用的命令（CommandId）。|
|[DescribeInvocations](/intl.zh-CN/API参考/云助手/DescribeInvocations.md)|调用DescribeInvocations查询最近两周云助手脚本的执行列表和状态。|
|[DescribeInvocationResults](/intl.zh-CN/API参考/云助手/DescribeInvocationResults.md)|调用DescribeInvocationResults查看云助手命令的执行结果，在指定ECS实例中的实际执行结果。|
|[DescribeCloudAssistantStatus](/intl.zh-CN/API参考/云助手/DescribeCloudAssistantStatus.md)|调用DescribeCloudAssistantStatus查询一台或者多台实例是否安装了云助手客户端。|
|[DescribeActivations](/intl.zh-CN/API参考/云助手/DescribeActivations.md)|调用DescribeActivations查询已创建的激活码以及激活码的使用情况。|
|[DescribeManagedInstances](/intl.zh-CN/API参考/云助手/DescribeManagedInstances.md)|调用DescribeManagedInstances查询托管实例列表。|
|[InstallCloudAssistant](/intl.zh-CN/API参考/云助手/InstallCloudAssistant.md)|调用InstallCloudAssistant为一台或多台实例安装云助手客户端。|
|[RunCommand](/intl.zh-CN/API参考/云助手/RunCommand.md)|调用RunCommand新建一份Shell、PowerShell或者Bat类型的云助手脚本，然后在一台或多台ECS实例中执行该脚本。|
|[SendFile](/intl.zh-CN/API参考/云助手/SendFile.md)|调用SendFile向一台或多台ECS实例下发远程文件。|
|[DescribeSendFileResults](/intl.zh-CN/API参考/云助手/DescribeSendFileResults.md)|调用DescribeSendFileResults查询云助手下发文件列表及状态。|
|[DeleteActivation](/intl.zh-CN/API参考/云助手/DeleteActivation.md)|调用DeleteActivation删除一个未被使用的激活码。|

## 标签

|API|描述|
|---|--|
|[TagResources](/intl.zh-CN/API参考/标签/TagResources.md)|调用TagResources为指定的ECS资源列表统一创建并绑定标签。|
|[ListTagResources](/intl.zh-CN/API参考/标签/ListTagResources.md)|调用ListTagResources查询一个或多个ECS资源已经绑定的标签列表。|
|[UntagResources](/intl.zh-CN/API参考/标签/UntagResources.md)|调用UntagResources为指定的ECS资源列表统一解绑并删除标签。|

## 地域

|API|描述|
|---|--|
|[DescribeRegions](/intl.zh-CN/API参考/地域/DescribeRegions.md)|调用DescribeRegions查询您可以使用的阿里云地域。|
|[DescribeZones](/intl.zh-CN/API参考/地域/DescribeZones.md)|调用DescribeZones查询一个阿里云地域下的可用区。|
|[DescribeAvailableResource](/intl.zh-CN/API参考/地域/DescribeAvailableResource.md)|调用DescribeAvailableResource查询某一可用区的资源列表。例如，您可以在某一可用区创建实例（RunInstances）或者修改实例规格（ModifyInstanceSpec）时查询该可用区的资源列表。|
|[DescribeResourcesModification](/intl.zh-CN/API参考/地域/DescribeResourcesModification.md)|调用DescribeResourcesModification查询升级和降配实例规格或者系统盘时，某一可用区的可用资源信息。|

## 询价

|API|描述|
|---|--|
|[DescribePrice](/intl.zh-CN/API参考/询价/DescribePrice.md)|调用DescribePrice查询云服务器ECS资源的最新价格。|
|[DescribeRenewalPrice](/intl.zh-CN/API参考/询价/DescribeRenewalPrice.md)|调用DescribeRenewalPrice查询云服务器ECS资源的续费价格。仅支持查询包年包月资源的续费价格。|
|[DescribeInstanceModificationPrice](/intl.zh-CN/API参考/询价/DescribeInstanceModificationPrice.md)|调用DescribeInstanceModificationPrice查询未到期的包年包月ECS实例升配时目标实例规格的价格信息、新增包年包月数据盘的价格信息。|

## 其他接口

|API|描述|
|---|--|
|[CancelTask](/intl.zh-CN/API参考/其他接口/CancelTask.md)|调用CancelTask取消一件正在运行的任务。目前，您能取消正在运行的导入镜像任务（ImportImage）和导出镜像任务（ExportImage）。|
|[DescribeTasks](/intl.zh-CN/API参考/其他接口/DescribeTasks.md)|调用DescribeTasks查询一个或多个异步请求的进度。|
|[DescribeTaskAttribute](/intl.zh-CN/API参考/其他接口/DescribeTaskAttribute.md)|调用DescribeTaskAttribute查询异步任务的详细信息。目前，可以查询的异步任务有导入镜像（ImportImage）和导出镜像（ExportImage）两种。|
|[DescribeAccountAttributes](/intl.zh-CN/API参考/其他接口/DescribeAccountAttributes.md)|调用DescribeAccountAttributes查询您在一个阿里云地域下能创建的ECS资源配额。包括您能创建的安全组数量、弹性网卡数量、按量付费vCPU核数、抢占式实例vCPU核数、专用宿主机数量、地域网络类型以及账号是否已完成实名认证。|
|[JoinResourceGroup](/intl.zh-CN/API参考/其他接口/JoinResourceGroup.md)|调用JoinResourceGroup将一个ECS资源或者服务加入另一个资源组。|
|[DescribeDemands](/intl.zh-CN/API参考/其他接口/DescribeDemands.md)|调用DescribeDemands查询报备资源的交付及使用状态。|

