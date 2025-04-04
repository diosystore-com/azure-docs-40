---
title: Availability zone migration guidance overview for Microsoft Azure products and services
description: Availability zone migration guidance overview for Microsoft Azure products and services
author: anaharris-ms
ms.service: reliability
ms.subservice: availability-zones
ms.topic: conceptual
ms.date: 11/08/2022
ms.author: anaharris
ms.custom: subject-reliability
---

# Availability zone migration guidance overview for Microsoft Azure products and services

Azure services that support availability zones, including zonal and zone-redundant offerings, are continually expanding.  For that reason, resources that don't currently have availability zone support, may have an opportunity to gain that support. The Migration Guides section offers a collection of guides for each service that requires certain procedures in order to move a resource from non-availability zone support to availability support. You'll find information on prerequisites for migration, download requirements, important migration considerations and recommendations.

The table below lists each product that offers migration guidance and/or information. 

## Azure services migration guides

### ![An icon that signifies this service is foundational.](media/icon-foundational.svg) Foundational services 

| **Products**  | 
| --- | 
| [Azure Application Gateway (V2)](migrate-app-gateway-v2.md) |
| [Azure Backup and Azure Site Recovery](migrate-recovery-services-vault.md)  | 
| [Azure Storage account: Blob Storage, Azure Data Lake Storage, Files Storage](migrate-storage.md) |
| [Azure Storage: Managed Disks](migrate-vm.md)|
| [Azure Virtual Machines and Azure Virtual Machine Scale Sets](migrate-vm.md)|  

\*VMs that support availability zones: AV2-series, B-series, DSv2-series, DSv3-series, Dv2-series, Dv3-series, ESv3-series, Ev3-series, F-series, FS-series, FSv2-series, and M-series.

### ![An icon that signifies this service is mainstream.](media/icon-mainstream.svg) Mainstream services

| **Products**   | 
| --- | 
| [Azure API Management](migrate-api-mgt.md)|
| [Azure App Configuration](migrate-app-configuration.md)|
| [Azure App Service](migrate-app-service.md)|
| [Azure App Service: App Service Environment](migrate-app-service-environment.md)|
| [Azure Cache for Redis](migrate-cache-redis.md)|
| [Azure Cognitive Search](migrate-search-service.md)|
| [Azure Container Instances](migrate-container-instances.md)|
| [Azure Database for MySQL - Flexible Server](migrate-database-mysql-flex.md)|
| [Azure Monitor: Log Analytics](migrate-monitor-log-analytics.md)|

## Workload and general guidance
| **Workloads**   | 
| --- | 
| [Azure Kubernetes Service (AKS) and MySQL Flexible Server](migrate-workload-aks-mysql.md)|

## Next steps


> [!div class="nextstepaction"]
> [Azure services and regions with availability zones](availability-zones-service-support.md)

> [!div class="nextstepaction"]
> [Availability of service by category](availability-service-by-category.md)

> [!div class="nextstepaction"]
> [Microsoft commitment to expand Azure availability zones to more regions](https://azure.microsoft.com/blog/our-commitment-to-expand-azure-availability-zones-to-more-regions/)

> [!div class="nextstepaction"]
> [Build solutions for high availability using availability zones](/azure/architecture/high-availability/building-solutions-for-high-availability)
