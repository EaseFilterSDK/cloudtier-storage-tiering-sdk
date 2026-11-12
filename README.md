# CloudTier Storage Tiering Filter Driver SDK

[![Platform](https://img.shields.io/badge/Platform-Windows-blue.svg)](https://www.easefilter.com/cloud/cloudtier-storage-tiering-sdk.htm)
[![Languages](https://img.shields.io/badge/Languages-C%23%20%7C%20C%2B%2B%20%7C%20Java%20%7C%20Python%20%7C%20Go%20%7C%20Rust-brightgreen.svg)](https://www.easefilter.com/cloud/cloudtier-storage-tiering-sdk.htm)

The **CloudTier Storage Tiering Filter Driver SDK** by EaseFilter is a comprehensive Hierarchical Storage Management (HSM) development kit. It provides a robust, kernel-level framework designed to implement transparent data migration between high-cost (hot) local storage and low-cost (cold) remote storage media (like AWS S3, Azure Blob, or secondary NAS).

By seamlessly replacing migrated files with **Stub Files**, the SDK enables organizations to optimize storage efficiency, reduce CapEx/OpEx, and enforce data lifecycles—all without disrupting existing end-user applications or changing how files appear in Windows Explorer.
A storage tiering example was implemented with CloudTier Storage Tiering SDK. The CloudTier Storage Tiering SDK provides you a simple solution to develop the cloud archiving software, it allows you to integrate your existing on-premises applications with the remote cloud storage infrastructure in a seamless, secure, and transparent fashion. The cloud tiering is a data storage technique which automatically moves data between high-cost on-premise storage and low-cost remote cloud storage, it provides a native cloud storage tier, it allows you to free up on-premise storage capacity, by moving out cooler data to the cloud storage, thereby reducing capital and operational expenditures.

![loudTier Storage Tiering Architecture](https://www.easefilter.com/images/cloudtier-storage-tiering-architecture.jpg)

## 🚀 Key Features

*   **Transparent Stub Files:** Migrated files are replaced with sparse files (stubs) tagged with reparse points. They consume zero local disk space but retain 100% of the original metadata (name, size, timestamps, ACLs).
*   **Block-Level Archive Recall (Hydration):** Optimized for high performance and low egress costs. If an application requests only a specific byte-range of a massive file, the driver fetches only the required blocks on-demand, not the entire file.
*   **Storage Provider Agnostic:** The kernel driver manages local NTFS/ReFS blocks, leaving the cloud provider logic to you. Easily integrate with **Amazon S3, Microsoft Azure Blob Storage, Google Cloud Storage**, or any on-premise object storage.
*   **Policy-Driven Migration:** Automate tiering based on access frequency (e.g., `LastAccessTime`), file size, extension, or custom application tags.
*   **WORM & Compliance Readiness:** Native support for "Write Once Read Many" workflows to meet regulatory standards like HIPAA, FINRA, and GDPR.

---

## 💡 Common Use Cases

*   **Enterprise File Archival:** Automatically offload old medical imaging (DICOM), media assets, or logs to cloud storage after 30+ days of inactivity. When a user opens the file, it streams instantly.
*   **Infinite Local File Systems:** Present petabytes of cloud object storage as a standard local drive letter to legacy applications that only understand NTFS.
*   **Disaster Recovery (DR):** Keep light, metadata-rich stubs on-premise while the bulk of the data is safely secured and versioned in the cloud.

---

## 🏗️ A CloudTier S3 Intelligent-Tiering Example 
This C# demo project demonstrates how to connect Amazon S3 Intelligent-Tiering as a secondary storage tier for on-premises storage using the **CloudTier Storage Tiering SDK**. 

The CloudTier SDK enables Hierarchical Storage Management (HSM) by automatically tiering infrequently used on-premises data to cost-effective S3 storage, and moving it back transparently when accessed by local applications.
The example can generate some stub files. To handle the read request of the stub file, we need to register the callback function for the file system filter driver. When the stub file was accessed, the callback function will be invoked, the callback function will retrieve the data from the remote server and send back to the filter driver.
![loudTier Storage Tiering Architecture](https://www.easefilter.com/images/cloudtier-s3-architecture.jpg)

### Key Features

* **Transparent File Access:** Local applications can read/write to S3 objects without knowing the files are stored in the cloud.
* **Stub File Technology:** Replaces local files with 0-byte "stub files" that retain all original metadata, attributes, and security permissions.
* **Automated Data Recall:** When a stub file is accessed, the SDK automatically downloads the required data from S3 to a local cache and serves it to the application.
* **Customizable Filter Driver:** Granular control over process exclusions, connection threads, timeouts, and cache management.
* **Built-in S3 Explorer:** Includes a UI to browse S3 buckets, upload/download files, and generate stub files on your local drive.

### Architecture & How It Works

This solution is built on a File System Filter Driver. Here is the lifecycle of a tiered file:

1. **Tiering:** A physical file on the local server is uploaded to Amazon S3.
2. **Stubbing:** The local physical file is replaced by a **Stub File**.
   * *A stub file acts exactly like the regular file. It maintains the file size, creation time, last write time, and security descriptors, but it consumes 0 bytes of physical disk space.*
3. **Recall (Read Request):** An application attempts to read the stub file.
4. **Interception:** The CloudTier Filter Driver intercepts the read request.
5. **Retrieval:** The requested data is retrieved from S3 to a local cache folder.
6. **Completion:** The data is returned to the application seamlessly.


## EaseFilter File System Filter Driver SDK Reference
| Product Name | Description |
| --- | --- |
| [Cloud File System SDK](https://www.easefilter.com/cloud/cloud-file-system-sdk.htm) | EaseFilter Cloud File System SDK Introduction. |
| [CloudTier Storage Tiering SDK](https://www.easefilter.com/cloud/storage-tiering-sdk.htm) | EaseFilter Storage Tiering Filter Driver SDK Introduction. |
| [File Monitor SDK](https://www.easefilter.com/kb/file-monitor-filter-driver-sdk.htm) | EaseFilter File Monitor Filter Driver SDK Introduction. |
| [File Control SDK](https://www.easefilter.com/kb/file-control-file-security-sdk.htm) | EaseFilter File Control Filter Driver SDK Introduction. |
| [File Encryption SDK](https://www.easefilter.com/kb/transparent-file-encryption-filter-driver-sdk.htm) | EaseFilter Transparent File Encryption Filter Driver SDK Introduction. |
| [Registry Filter SDK](https://www.easefilter.com/kb/registry-filter-drive-sdk.htm) | EaseFilter Registry Filter Driver SDK Introduction. |
| [Process Filter SDK](https://www.easefilter.com/kb/process-filter-driver-sdk.htm) | EaseFilter Process Filter Driver SDK Introduction. |
| [EaseFilter SDK Programming](https://www.easefilter.com/kb/programming.htm) | EaseFilter Filter Driver SDK Programming. |

## EaseFilter SDK Sample Projects
| Sample Project | Description |
| --- | --- |
| [CloudTier Storage Tiering Demo](https://www.easefilter.com/cloud/cloudtier-storage-tiering-demo.htm) | A HSM File System Filter Driver Demo. |
| [CloudTier S3 Tiering Demo](https://www.easefilter.com/cloud/cloudtier-s3-intelligent-tiering-demo.htm) | CloudTier S3 Intelligent Tiering Demo. |
| [Cloud File DR S3 Demo](https://www.easefilter.com/cloud/cloud-file-dr-demo.htm) | Cloud File DR S3 Demo. |
| [Amazon S3 File Explorer Demo](https://www.easefilter.com/cloud/s3-browser-demo.htm) | Amazon S3 File Explorer Demo. |
| [Auto File DRM Encryption](https://www.easefilter.com/kb/auto-file-drm-encryption-tool.htm) | Auto file encryption with DRM data embedded. |
| [Transparent File Encrypt](https://www.easefilter.com/kb/AutoFileEncryption.htm) | Transparent on access file encryption. |
| [Secure File Sharing with DRM](https://www.easefilter.com/kb/DRM_Secure_File_Sharing.htm) | Secure encrypted file sharing with digital rights management. |
| [File Monitor Example](https://www.easefilter.com/kb/file-monitor-demo.htm) | Monitor file system I/O in real time, tracking file changes. |
| [File Protector Example](https://www.easefilter.com/kb/file-protector-demo.htm) | Prevent sensitive files from being accessed by unauthorized users or processes. |
| [FolderLocker Example](https://www.easefilter.com/kb/FolderLocker.htm) | Lock file automatically in a FolderLocker. |
| [Process Monitor](https://www.easefilter.com/kb/Process-Monitor.htm) | Monitor the process creation and termination, block unauthorized process running. |
| [Registry Monitor](https://www.easefilter.com/kb/RegMon.htm) | Monitor the Registry activities, block the modification of the Registry keys. |
| [Secure Sandbox Example](https://www.easefilter.com/kb/Secure-Sandbox.htm) |A secure sandbox example, block the processes accessing the files out of the box. |
| [FileSystemWatcher Example](https://www.easefilter.com/kb/FileSystemWatcher.htm) | File system watcher, logging the file I/O events. |
| [ZeroTrust Example](https://www.easefilter.com/kb/zero-trust-file-access-control-demo.htm) | Zero trust file access control with encryption feature. |

## Filter Driver Reference

* [Understand MiniFilter Driver](https://www.easefilter.com/kb/understand-minifilter.htm)
* [Understand File I/O](https://www.easefilter.com/kb/File_IO.htm)
* [Understand I/O Request Packets(IRPs)](https://www.easefilter.com/kb/understand-irps.htm)
* [Filter Driver Developer Guide](https://www.easefilter.com/kb/DeveloperGuide.htm)
* [MiniFilter Filter Driver Framework](https://www.easefilter.com/kb/minifilter-framework.htm)
* [Isolation Filter Driver](https://www.easefilter.com/kb/Isolation_Filter_Driver.htm)

## License

This repository contains two distinct licensing categories:

1. **Wrapper/Implementation Code (MIT License):** 
   The source code, scripts, and configuration files provided directly in this repository are licensed under the [MIT License](LICENSE). You are free to modify, distribute, and use this specific integration code.

2. **EaseFilter SDK (Commercial License):**
   This project requires the EaseFilter SDK (including its binaries, filter drivers, and core libraries) to function. The EaseFilter SDK is **proprietary commercial software** and is strictly excluded from the MIT License.   
   To use the EaseFilter SDK for commercial purposes or in a production environment, you must obtain a valid commercial license directly from [EaseFilter](https://www.easefilter.com/license.pdf).

## Support
If you have questions or need help, please contact support@easefilter.com 

[Home](https://www.easefilter.com/) | [Solution](https://www.easefilter.com/solutions.htm) | [Download](https://www.easefilter.com/download.htm) | [Demos](https://www.easefilter.com/online-fileio-test.aspx) | [Blog](https://blog.easefilter.com/) | [Programming](https://www.easefilter.com/kb/programming.htm)
