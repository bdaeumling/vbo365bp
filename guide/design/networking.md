---
title: Networking
parent: Design
nav_order: 90
---
# Networking


## Best Practise

{: .veeam-bp }
* Static IPv4 for VBO server
* Static IPv4 for VBO proxy/repo server
* Create A and PTR records in DNS
* Prefer IPv4 over IPv6
* VBO server and proxies need to be part of the same (or trusted) Active Directory domain

## Explanation

{: .veeam-why }
Working communication between the components with working DNS name resolution is key to prevent hard to trace errors.
