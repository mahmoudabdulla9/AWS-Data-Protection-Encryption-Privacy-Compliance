# Encryption at Rest & KMS Key Management Policy

## 🔒 Overview
This document outlines the Key Management Service (KMS) strategy for enforcing Encryption at Rest across all sensitive data stored within the AWS environment.

## 🗝️ Customer Managed Key (CMK) Specifications
* **Key Alias:** `alias/depi-data-protection-key`
* **Key Type:** Symmetric (AES-256)
* **Key Usage:** Encrypt and Decrypt
* **Automatic Key Rotation:** Enabled (365-day rotation cycle)

---

## 🛡️ Access Control & Key Policy
The KMS Key policy adheres to the principle of least privilege:
1. **Key Administrators:** Authorized to manage, disable, and rotate the key material.
2. **Key Users:** Authorized only for `kms:GenerateDataKey` and `kms:Decrypt` operations required for S3 object interactions.

---

## 🔍 Audit & Lifecycle Tracking
* All key operations (creation, encryption, decryption, rotation) are logged continuously via **AWS CloudTrail**.
* Deletion safety: Scheduled key deletion includes a mandatory 30-day waiting period.
