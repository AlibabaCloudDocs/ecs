# Overview of the trusted feature for security-enhanced instances

Security-enhanced instance families are provided by Alibaba Cloud to implement trusted boot based on Trusted Cryptography Module \(TCM\) or Trusted Platform Module \(TPM\) chips. During a trusted boot, each module in the boot chain from the underlying hardware to the guest OS is measured and verified. This topic describes how a security-enhanced instance works and basic concepts of the trusted computing technology.

## How a security-enhanced instance works

Trusted computing is one of the main features used to achieve the high-level security of underlying computing environments for cloud tenants. TPM or TCM is integrated into the hardware platform to build a trusted chain that covers system startup and user-specified applications and implement a remote attestation mechanism. This guarantees a trusted environment for users in all aspects during the startup and running phases. The trust verification of systems and applications reduces vulnerability to attacks due to the use of unknown or tampered systems or software.

Security-enhanced instance families use the trusted computing technology to verify the integrity of each module. This ensures that instances are not compromised by startup-level or kernel-level malware or rootkits. Based on the TPM or TCM trusted hardware, the security-enhanced instance families can achieve measured boot and integrity verification by using the Unified Extensible Firmware Interface \(UEFI\) firmware, vTPM or vTCM, and remote attestation service. This ensures that security-enhanced instances are secure and trusted.

## TPM or TCM hardware

Trusted computing relies on TPM or TCM chips. TPM is standardized by ISO as ISO 11889, and TCM is standardized as GM/T 0012-2020 in China. TPM or TCM chips used as the root of trust has the following benefits:

-   TPM or TCM uses its own internal firmware and logic circuits to process instructions. It does not rely on operating systems and is insulated from external software vulnerabilities.
-   Attackers must have physical access to computers before they can attack TPM or TCM chips.
-   Security-enhanced instances are equipped with TPM or TCM chips, startup firmware, and system software to build a chain of trust.

## Firmware security

Alibaba Cloud supports secure firmware updates. Before firmware is updated, firmware signatures are verified to ensure that only authorized firmware can be updated. This can prevent malicious firmware from attacking the cloud infrastructure.

## vTPM or vTCM

Alibaba Cloud also provides virtual root of trust \(vTPM or vTCM\) for ECS instances to extend the trust system of servers to the ECS virtualization layer on a trusted hardware base. A comprehensive security system is built based on hardware and virtual root of trust.

vTPM or vTCM is a virtualized and trusted platform module, which can be used to transmit a chain of trust from the trusted server hardware to the trusted instance. vTPM or vTCM is fully compatible with the trusted computing specification \(TPM2.0/TCM2.0\). Security-enhanced instances enable vTPM or vTCM to build virtual root of trust within these instances and implement a startup chain of trust and remote attestation mechanism similar to the host layer. The baseline measurement is generated when an instance is created. The measurement values collected on subsequent instance startups are compared with the baseline measurement to determine whether the instance has changed. The comparison result indicates the trusted status of the instance and is displayed in the Security Center console.

## UEFI firmware

Security-enhanced instances use trusted boot firmware that meets the UEFI for system boot. The UEFI firmware can measure the integrity of system firmware, system boot loader, and system kernel modules during the boot process of the operating system to build a chain of trust for system startup.

## Measured boot

Components are measured stage by stage. The components started first measure the next stage components before starting them. If the measurement is successful, the chain of trust is extended to the next stage.

Each module in the boot chain from the underlying hardware to the guest OS is measured during the boot process of an instance. When these modules are loaded, trusted components calculate the hash value for each module and securely store the calculated values to the root of trust to form a chain of trust. Stage-by-stage measurement and verification of all modules in the boot chain ensures that the system has not changed since the last boot.

## Integrity verification

Integrity verification helps you to learn the trusted status of instances and make decisions.

When an instance is started for the first time, the trusted components create the first set of hash values as baseline measurement and securely store the data. Then, these measurement and storage operations are performed each time the instance starts. Trusted components send the measurement values to the trusted service by using remote attestation. You can measure and verify the integrity of the instance by comparing the latest measurement data with the baseline measurement to determine whether the instance is running in the expected trusted state.

Integrity verification compares the startup measurement information with the baseline measurement of an instance. If the information is matched, a pass result is returned, which indicates that the instance is trusted. If the information is not matched, a failure result is returned, which indicates that the instance is untrusted.

If an expected integrity verification failure occurs in specific scenarios such as when the system of the ECS instance was updated, you can update the instance baseline measurement by adding the trusted event to the whitelist. Subsequent integrity measurements are performed against the latest baseline measurement. For more information, see [Handle trusted exceptions](/intl.en-US/Instance/Instance type families/Security-enhanced instance family/Use security-enhanced instances.md). If an unexpected integrity verification failure occurs, you must find the cause of the failure based on the trusted event details to prevent instances from running in an untrusted environment.

