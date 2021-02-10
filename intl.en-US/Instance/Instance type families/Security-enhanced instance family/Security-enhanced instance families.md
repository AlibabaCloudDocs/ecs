# Security-enhanced instance families

The g6t and c6t security-enhanced instance families are provided by Alibaba Cloud to implement trusted boot based on Trusted Cryptography Module \(TCM\) or Trusted Platform Module \(TPM\) chips. During a trusted boot, each module in the boot chain from the underlying hardware to the guest OS is measured and verified. This topic describes how a security-enhanced instance works and the basic concepts of trusted computing technology.

## How a security-enhanced instance works

Trusted computing is one of the main features used to achieve the high-level security of underlying computing environments for cloud tenants. TPM or TCM is integrated into the hardware platform to build a trusted chain that covers system startup and user-specified applications and implement a remote attestation mechanism. In this way, a trusted environment can be guaranteed for users in all aspects during the startup and running phases. The trust verification of systems and applications reduces vulnerability to attacks due to the use of unknown or tampered systems or software.

The g6t and c6t security-enhanced instance families use trusted computing technologies to verify the integrity of each module. This ensures that instances are not compromised by startup-level or kernel-level malware or rootkits. Based on the TPM or TCM trusted hardware, the g6t and c6t instance families can implement instance startup measurement and Integrity verification by using the Unified Extensible Firmware Interface \(UEFI\) firmware, vTPM or vTCM, and remote attestation service. This ensures that security-enhanced instances are secure and trustful. For more information about instance type parameters, see [g6t, security-enhanced general purpose instance family](/intl.en-US/Instance/Instance type families/General purpose instance families.md) and [c6t, security-enhanced compute optimized instance family](/intl.en-US/Instance/Instance type families/Compute optimized instance families.md). For more information about how to create a security-enhanced instance, see [Create a security-enhanced instance]().

## TPM or TCM hardware

Trusted computing relies on TPM or TCM chips. TPM is standardized by ISO as ISO/IEC 11889, and TCM is standardized as GM/T 0012-2020 in China. TPM or TCM chips used as the Trusted Computing Base \(TCB\) have the following advantages:

-   TPM or TCM uses its own internal firmware and logic circuits to process instructions. It does not rely on operating systems and is insulated from external software vulnerabilities.
-   Attacking TPM or TCM chips require physical access to the computer.
-   Security-enhanced instances are equipped with TPM or TCM chips, startup firmware, and system software, so that a server can build a chain of trust.

## vTPM or vTCM

Alibaba Cloud also provides virtual TCB \(vTPM or vTCM\) for ECS instances to extend the trust system of servers to the ECS virtualization layer on a trusted hardware base. A comprehensive security system is built based on hardware and virtual TCB.

vTPM or vTCM is a virtualized and trusted platform module, which can be used to transmit a chain of trust from the trusted server hardware to the trusted instance. vTPM or vTCM is fully compatible with the trusted computing specification \(TPM2.0/TCM2.0\). Security-enhanced instances enable vTPM or vTCM to build virtual TCB within these instances and implement a startup chain of trust and remote attestation mechanism similarly to the host layer. The integrity measurement benchmark is generated when an instance is created. The measurement values collected on subsequent instance startups are compared with the benchmark measurement value to determine whether the instance has changed. The comparison result indicates the trusted status of the instance and is displayed in the Security Center console.

## UEFI firmware

Security-enhanced instances use trusted boot firmware that meets the UEFI for system boot. The UEFI firmware can measure the integrity of system firmware, system boot loader, and system kernel modules during the boot process of the operating system to build a chain of trust for system startup.

## Start measurement

Components are measured grade-by-grade. The components started first measure the components started next. A successful measurement indicates that a chain of trust is transmitted from the previous grade to the next grade.

When you start an instance, the trusted firmware calculates the hash value of a component when the firmware loads the component. The trusted firmware concatenates the calculated hash value with the hash values of all loaded components, and then recalculates the hash value. The values are transferred grade by grade to form a chain of trust.

## Verify integrity

Integrity verification helps you to learn the trusted status of instances and make decisions.

When an instance is started for the first time, the trusted components create the first set of hash values as integrity benchmark data and store the data securely. After that, these measurement and storage operations are performed each time the instance starts. You can measure and verify the integrity of the instance by comparing the latest measurement data with the benchmark data to determine whether the instance is running in the expected trusted state.

Integrity verification compares the startup measurement information with the integrity benchmark data of an instance. If the information is matched, a pass result is returned, which indicates that the instance is trusted. If the information is not matched, a failure result is returned, which indicates that the instance is untrusted.

If an expected integrity verification failure occurs, for example, if the system of the ECS instance was upgraded, you can update the instance integrity benchmark data by adding the trusted event to the whitelist. Subsequent integrity measurements are performed against the latest integrity benchmark data. For more information, see [Handle trusted exceptions](). If an unexpected integrity verification failure occurs, you must find the cause of the failure based on the trusted event details to prevent instances from running in an untrusted environment.

