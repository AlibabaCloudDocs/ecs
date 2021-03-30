# Security-enhanced instance families

Security-enhanced instance families provide the trusted computing capability based on Trusted Cryptography Module \(TCM\) or Trusted Platform Module \(TPM\) chips. Some security-enhanced instance families including g7t, c7t, and r7t also provide the Software Guard Extension \(SGX\) encrypted computing capability based on Intel® SGX for a trusted confidential environment that provides a higher security level.

## Trusted computing

Security-enhanced instance families integrate TPM or TCM into the hardware platform, use TPM or TCM chips as root of trust, and use the Unified Extensible Firmware Interface \(UEFI\) firmware, vTPM or vTCM, and remote attestation service to implement instance startup measurement and integrity verification. This ensures that security-enhanced instances are secure and trusted.

For more information about the features and instructions of the trusted computing capability, see the following topics:

-   [Overview of the trusted feature for security-enhanced instances](/intl.en-US/Instance/Instance type families/Security-enhanced instance family/Overview of the trusted feature for security-enhanced instances.md)
-   [Use security-enhanced instances](/intl.en-US/Instance/Instance type families/Security-enhanced instance family/Use security-enhanced instances.md)
-   [Build a confidential computing environment by using Enclave](/intl.en-US/Instance/Instance type families/Security-enhanced instance family/Build a confidential computing environment by using Enclave.md)

## SGX encrypted computing

When you use root of trust that is based on software and the software itself has security vulnerabilities, the data security cannot be guaranteed. Root of trust of SGX contains only hardware. This further improves the security level. In addition to instance startup measurement and integrity verification, some security-enhanced instance families including g7t, c7t, and r7t transfer the encrypted computing capability of physical servers to instances based on Intel® SGX. vSGX instances are assigned encrypted memory.

SGX uses Memory Encryption Engines \(MEEs\) in CPUs to encrypt data in the encrypted memory. The encrypted data is decrypted into plaintext only after the data enters CPUs. CPUs protect your private data from being extracted by malicious code. Therefore, when you use a vSGX instance, data remains protected even if the operating system, virtualization stack, or Basic Input/Output System \(BIOS\) becomes compromised. You need only to trust CPUs to keep your private data secure. For information about how to use SGX, see [Build an SGX encrypted computing environment](/intl.en-US/Instance/Instance type families/Security-enhanced instance family/Build an SGX encrypted computing environment.md).

## Support of secure computing capabilities of instance families

|Instance family|Trusted computing|SGX encrypted computing|
|---------------|-----------------|-----------------------|
|-   [g7t, security-enhanced general purpose instance family](/intl.en-US/Instance/Instance type families/General purpose instance families.md)
-   [c7t, security-enhanced compute optimized instance family](/intl.en-US/Instance/Instance type families/Compute optimized instance families.md)
-   [r7t, security-enhanced memory optimized instance family](/intl.en-US/Instance/Instance type families/Memory optimized instance families/Memory optimized instance families.md)

|Supported|Supported|
|-   [g6t, security-enhanced general purpose instance family](/intl.en-US/Instance/Instance type families/General purpose instance families.md)
-   [c6t, security-enhanced compute optimized instance family](/intl.en-US/Instance/Instance type families/Compute optimized instance families.md)

|Supported|Not supported|

