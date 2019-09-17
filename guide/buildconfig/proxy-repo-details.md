---
title: Proxy & Repository Server Details
parent: Build & Configure
nav_order: 2000
---
# Proxy & Repository Server Details

## Repository

### Storage Volumes
VBO stores backup data in a Microsoft Jet database in the repository. As this means random I/O on the used storage a high IOPS and bandwidth storage is preferred. In general DAS or FC-SAN block storage is preferred over ISCSI or SMB based storage.

### File System
Both NTFS and ReFS file systems are supported. When using ReFS, the data integrity features should be disabled in particular for volumes where data folders are located or at least exclude VBO Repository files. NTFS is recommended because it does not need any error-prone reconfiguration.

Storage encryption, dedup or compression does always mean added latency on I/O reqeusts, thus we recommend to disable these features for better performance.

### Separate Repositories
The maximum supported file size for the Jet DB database files (`.adb`) is 64TB. An automatic rule triggers when the repository database files reaches 59 TB at which point a new repository database file is automatically created in the same storage location. This allows to overcome the first limit.

However, handling such large repositories (e.g. for migration purposes) comes with problems like long migration times, handling very large file systems, etc. Thus we recommend to reduce the aimed repository size by separating the backup data to different repositories. Especially separation by data type (Exchange, OneDrive, SharePoint) is reasonable, as depending on the type the change characteristics (amount of data, changerate) are normally different.
While for Exchange a lot of objects might be changed, the amount of data is normally quite low, as most of it is just text. For OneDrive however, the average changed file size might be much higher because it is used to store large binary files.
Even for the same type of data (e.g. OneDrive) it might be reasonable to again separate this data only, e.g. by business unit, when the overall data size is very high.

### Working Space
Additional space for transaction protocols or database checkpoints is required per repositry. There should always 10% free workspace per repository to compensate this.

## Proxy

### Bandwidth Throttling
By default the proxy servers will take all available bandwidth to run the backups as fast as possible. As normally there is no dedicated Internet connection available just for VBO backup, it's reasonable to throttle the maximum usable bandwidth (which is done per proxy) so that other applications do not suffer (too much). Depending on the backup schedule the limit should be set to a reasonable value. It might be okay to take 90% of the bandwidth at night but if the backup runs during working hours only 40% can be consumed without affecting operations.