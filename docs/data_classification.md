# Data Classification, Lifecycle & S3 Security Baseline

## 🎯 Data Classification Scheme
To ensure appropriate protection levels, data in the enterprise S3 bucket is classified into three tiers:

| Classification Level | Description | Examples | Access Controls | Encryption Requirement |
| :--- | :--- | :--- | :--- | :--- |
| **Public** | Non-sensitive information available to the public. | Public marketing assets, documentation. | Public Read allowed | SSE-S3 |
| **Internal** | Non-sensitive operational data for internal use. | Internal logs, project plans, reports. | Authenticated IAM Users | SSE-S3 |
| **Confidential / PII** | Highly sensitive personal or financial information. | User PII, credentials, API keys, compliance logs. | Restricted IAM / KMS Policy | Mandatory KMS (SSE-KMS) |

---

## 🛡️ S3 Security Baseline & Advanced Controls
1. **Block Public Access:** Fully enabled at the bucket level to prevent accidental exposure.
2. **Versioning:** Enabled to protect against accidental overwrites and deletion.
3. **HTTPS Enforcement:** Enforced via strict Bucket Policies (`aws:SecureTransport: false` denied).
4. **S3 Access Points:** Configured for isolated application access boundaries to restrict specific workloads to designated prefixes.
5. **IAM Access Analyzer Review:** Regularly audited via IAM Access Analyzer to confirm zero unintended public or cross-account resource exposure.

---

## 🔄 S3 Lifecycle Policy Configuration
To manage data throughout its lifecycle and reduce costs, the following retention rules are applied:
1. **Current Versions:**
   * Transition to **S3 Standard-Infrequent Access (Standard-IA)** after 30 days.
   * Transition to **S3 Glacier Flexible Retrieval** after 90 days.
2. **Noncurrent Versions:**
   * Expire / Delete noncurrent versions after 365 days.
