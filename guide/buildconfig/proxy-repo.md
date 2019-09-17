---
title: Proxy & Repository Server
parent: Build & Configure
nav_order: 200
---
# Proxy & Repository Server
Repositories are tightly coupled with proxy servers. While a single proxy server can host multiple repositories, each repository is uniquely coupled with a single proxy server.

Repositories can reside on Direct Attached Storage (DAS), Storage Area Network (SAN) volumes or on a SMB3 Network Attached Storage (NAS) share.

## Best Practice Notes

### Repository

* Use **DAS or SAN** volumes as repository
* Repository **File System** should be chosen as **NTFS**
* Do **not enable storage encryption, dedup or compression** on the repository volume for better performance
* **Separate repositories by data type** as different types of data (Exchange, OneDrive, SharePoint) to allow higher flexibility based on the different data-change characteristics.
* **Avoid very large repositories** because handling them gets harder. Distribute the backup data, e.g. by business units over several repositories.
* Keep **10% free working space** per repository

### Proxy

* Throttle the used bandwidth per proxy on a shared network connection to not block other applications

## [More in-depth information on this item](proxy-repo-details.md)

## External Ressources
- [Veeam Helpcenter - Veeam Backup for Microsoft Office 365 User Guide](https://helpcenter.veeam.com/docs/vbo365/guide/)
    - [Backup Proxy Servers](https://helpcenter.veeam.com/docs/vbo365/guide/vbo_backup_proxy_servers.html)
    - [Backup Repositories](https://helpcenter.veeam.com/docs/vbo365/guide/vbo_backup_repositories.html)
