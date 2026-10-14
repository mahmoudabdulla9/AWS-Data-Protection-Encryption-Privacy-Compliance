# Data Classification & Lifecycle Policy

## 🎯 Data Classification Scheme
To ensure appropriate protection levels, data in the enterprise S3 bucket is classified into three tiers:

| Classification Level | Description | Examples | Access Controls | Encryption Requirement |
| :--- | :--- | :--- | :--- | :--- |
| **Public** | Non-sensitive information available to the public. | Public marketing assets, documentation. | Public Read allowed | SSE-S3 |
| **Internal** | Non-sensitive operational data for internal use. | Internal logs, project plans, reports. | Authenticated IAM Users | SSE-S3 |
| **Confidential / PII** | Highly sensitive personal or financial information. | User PII, credentials, API keys, compliance logs. | Restricted IAM / KMS Policy | Mandatory KMS (SSE-KMS) |

---

## 🔄 S3 Lifecycle Policy Configuration
To manage data throughout its lifecycle and reduce costs, the following retention rules are applied:

1. **Current Versions:**
   * Transition to **S3 Standard-Infrequent Access (Standard-IA)** after 30 days.
   * Transition to **S3 Glacier Flexible Retrieval** after 90 days.
2. **Noncurrent Versions:**
   * Expire / Delete noncurrent versions after 365 days.
