---
title: Consumption-based serverless offer in Azure Cosmos DB
description: Learn more about Azure Cosmos DB's consumption-based serverless offer.
author: seesharprun
ms.author: sidandrews
ms.service: cosmos-db
ms.custom: event-tier1-build-2022
ms.topic: conceptual
ms.date: 05/09/2022
ms.reviewer: thweiss
---

# Azure Cosmos DB serverless
[!INCLUDE[appliesto-all-apis](includes/appliesto-all-apis.md)]

The Azure Cosmos DB serverless offering lets you use your Azure Cosmos account in a consumption-based fashion. With serverless, you're only charged for the Request Units (RUs) consumed by your database operations and the storage consumed by your data. Serverless containers can serve thousands of requests per second with no minimum charge and no capacity planning required.

> [!IMPORTANT] 
> Do you have any feedback about serverless? We want to hear it! Feel free to drop a message to the Azure Cosmos DB serverless team: [azurecosmosdbserverless@service.microsoft.com](mailto:azurecosmosdbserverless@service.microsoft.com).

Every database operation in Azure Cosmos DB has a cost expressed in [Request Units (RUs)](request-units.md). How you're charged for this cost depends on the type of Azure Cosmos account you're using:

- In [provisioned throughput](set-throughput.md) mode, you have to commit to a certain amount of throughput (expressed in Request Units per second or RU/s) that is provisioned on your databases and containers. The cost of your database operations is then deducted from the number of Request Units available every second. At the end of your billing period, you get billed for the amount of throughput you've provisioned.
- In serverless mode, you don't have to configure provisioned throughput when creating containers in your Azure Cosmos account. At the end of your billing period, you get billed for the number of Request Units that were consumed by your database operations.

## Use-cases

Azure Cosmos DB serverless best fits scenarios where you expect **intermittent and unpredictable traffic** with long idle times. Because provisioning capacity in such situations isn't required and may be cost-prohibitive, Azure Cosmos DB serverless should be considered in the following use-cases:

- Getting started with Azure Cosmos DB
- Running applications with
    - bursty, intermittent traffic that is hard to forecast, or
    - low (<10%) average-to-peak traffic ratio
- Developing, testing, prototyping and running in production new applications where the traffic pattern is unknown
- Integrating with serverless compute services like [Azure Functions](../azure-functions/functions-overview.md)

For more information, see [choosing between provisioned throughput and serverless](throughput-serverless.md).

## Using serverless resources

Serverless is a new Azure Cosmos account type, which means that you have to choose between **provisioned throughput** and **serverless** when creating a new account. You must create a new serverless account to get started with serverless. Migrating existing accounts to/from serverless mode isn't currently supported.

Any container that is created in a serverless account is a serverless container. Serverless containers expose the same capabilities as containers created in provisioned throughput mode, so you read, write and query your data the exact same way. However serverless accounts and containers also have specific characteristics:

- A serverless account can only run in a single Azure region. It isn't possible to add more Azure regions to a serverless account after you create it.
- Provisioning throughput isn't required on serverless containers, so the following statements are applicable:
    - You can't pass any throughput when creating a serverless container and doing so returns an error.
    - You can't read or update the throughput on a serverless container and doing so returns an error.
    - You can't create a shared throughput database in a serverless account and doing so returns an error.
- Serverless containers can store a maximum of 50 GB of data and indexes.

> [!NOTE]
> Serverless containers up to 1 TB are currently in preview with Azure Cosmos DB. To try the new feature, register the *"Azure Cosmos DB Serverless 1 TB Container Preview"* [preview feature in your Azure subscription](../azure-resource-manager/management/preview-features.md).

## Monitoring your consumption

If you have used Azure Cosmos DB in provisioned throughput mode before, you'll find serverless is more cost-effective when your traffic doesn't justify provisioned capacity. The trade-off is that your costs will become less predictable because you're billed based on the number of requests your database has processed. Because of the lack of predictability, it's important to keep an eye on your current consumption.

When browsing the **Metrics** pane of your account, you'll find a chart named **Request Units consumed** under the **Overview** tab. This chart shows how many Request Units your account has consumed:

:::image type="content" source="./media/serverless/request-units-consumed.png" alt-text="Chart showing the consumed Request Units" border="false":::

You can find the same chart when using Azure Monitor, as described [here](monitor-request-unit-usage.md). Azure Monitor enables the ability to configure [alerts](../azure-monitor/alerts/alerts-metric-overview.md), which can be used to notify you when your Request Unit consumption has passed a certain threshold.

## Performance

Serverless resources yield specific performance characteristics that are different from what provisioned throughput resources deliver. Serverless containers don't offer predictable throughput or latency guarantees. If your container\[s\] requires these guarantees, use provisioned throughput. 

For more information, see [provisioned throughput](set-throughput.md).

## Next steps

Get started with serverless with the following articles:

- [Request Units in Azure Cosmos DB](request-units.md)
- [Choose between provisioned throughput and serverless](throughput-serverless.md)
- [Pricing model in Azure Cosmos DB](how-pricing-works.md)