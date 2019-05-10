---
title: include file
description: include file
services: data-factory
author: linda33wj
ms.service: data-factory
ms.topic: include
ms.date: 1/10/2019
ms.author: jingwang
ms.custom: include file
---

Azure Data Factory is a multitenant service that has the following default limits in place to make sure customer subscriptions are protected from each other's workloads. To raise the limits up to the maximum for your subscription, contact support.

### Version 2

| Resource | Default limit | Maximum limit |
| -------- | ------------- | ------------- |
| Data factories in an Azure subscription |	50 | [Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Total number of entities, such as pipelines, data sets, triggers, linked services, and integration runtimes, within a data factory | 5,000 | [Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Total CPU cores for Azure-SSIS Integration Runtimes under one subscription | 256 | [Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Concurrent pipeline runs per data factory that's shared among all pipelines in the factory | 10,000  | [Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Maximum activities per pipeline, which includes inner activities for containers | 40 | 40 |
| Maximum number of linked integration runtimes that can be created against a single self-hosted integration runtime | 20 | [Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Maximum parameters per pipeline | 50 | 50 |
| ForEach items | 100,000 | 100,000 |
| ForEach parallelism | 20 | 50 |
| Characters per expression | 8,192 | 8,192 |
| Minimum tumbling window trigger interval | 15 min | 15 min |
| Maximum timeout for pipeline activity runs | 7 days | 7 days |
| Bytes per object for pipeline objects<sup>1</sup> | 200 KB | 200 KB |
| Bytes per object for dataset and linked service objects<sup>1</sup> | 100 KB | 2,000 KB |
| Data integration units per copy activity run<sup>3</sup> | 256 | [Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Write API calls | 2,500/h<br/><br/> This limit is imposed by Azure Resource Manager, not Azure Data Factory. | [Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Read API calls | 12,500/h<br/><br/> This limit is imposed by Azure Resource Manager, not Azure Data Factory. | [Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Monitoring queries per minute | 1,000 | [Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Entity CRUD operations per minute | 50 | [Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |


### Version 1

| **Resource** | **Default limit** | **Maximum limit** |
| --- | --- | --- |
| Data factories in an Azure subscription |50 |[Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Pipelines within a data factory |2,500 |[Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Data sets within a data factory |5,000 |[Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Concurrent slices per data set |10 |10 |
| Bytes per object for pipeline objects<sup>1</sup> |200 KB |200 KB |
| Bytes per object for data set and linked service objects<sup>1</sup> |100 KB |2,000 KB |
| Azure HDInsight on-demand cluster cores within a subscription<sup>2</sup> |60 |[Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Cloud data movement units per copy activity run<sup>3</sup> |32 |[Contact support](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/). |
| Retry count for pipeline activity runs |1,000 |MaxInt (32 bit) |

<sup>1</sup>Pipeline, data set, and linked service objects represent a logical grouping of your workload. Limits for these objects don't relate to the amount of data you can move and process with Azure Data Factory. Data Factory is designed to scale to handle petabytes of data.

<sup>2</sup>On-demand HDInsight cores are allocated out of the subscription that contains the data factory. As a result, the previous limit is the Data Factory-enforced core limit for on-demand HDInsight cores. It's different from the core limit that's associated with your Azure subscription.

<sup>3</sup>The data integration unit (DIU) for version 2 or the cloud data movement unit (DMU) for version 1 is used in a cloud-to-cloud copy operation. It's a measure that represents the power of a single unit in Data Factory. It combines the CPU, memory, and network resource allocations. You can achieve higher copy throughput by using more DMUs for some scenarios. For more information, see [Data integration units (version 2)](../articles/data-factory/copy-activity-performance.md#data-integration-units) and [Cloud data movement units (version 1)](../articles/data-factory/v1/data-factory-copy-activity-performance.md#cloud-data-movement-units). For information on billing, see [Azure Data Factory pricing](https://azure.microsoft.com/pricing/details/data-factory/).

<sup>4</sup>The integration runtime (IR) is the compute infrastructure used by Azure Data Factory to provide data integration capabilities across different network environments, such as data movement, dispatching activities to compute services, and execution of SSIS packages. For more information, see [Integration runtime overview](../articles/data-factory/concepts-integration-runtime.md).

| **Resource** | **Default lower limit** | **Minimum limit** |
| --- | --- | --- |
| Scheduling interval |15 minutes |15 minutes |
| Interval between retry attempts |1 second |1 second |
| Retry timeout value |1 second |1 second |

#### Web service call limits
Azure Resource Manager has limits for API calls. You can make API calls at a rate within the [Azure Resource Manager API limits](../articles/azure-subscription-service-limits.md#resource-group-limits).