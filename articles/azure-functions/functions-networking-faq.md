---
title: Frequently asked questions about networking in Azure Functions
description: Answers to some of the most common questions and scenarios for networking with Azure Functions.
services: functions
author: alexkarcher-msft
manager: jeconnoc
ms.service: azure-functions
ms.topic: troubleshooting
ms.date: 4/11/2019
ms.author: alkarche, glenga

---
# Frequently asked questions about networking in Azure Functions

This article lists frequently asked questions about networking in Azure Functions. For a more comprehensive overview, see [Functions networking options](functions-networking-options.md).

## How do I set a static IP in Functions?

Deploying a function in an App Service Environment is currently the only way to have a static inbound and outbound IP for your function. For details on using an App Service Environment, start with the article [Create and use an internal load balancer with an App Service Environment](../app-service/environment/create-ilb-ase.md).

## How do I restrict internet access to my function?

You can restrict internet access in a couple of ways:

* [IP restrictions](../app-service/app-service-ip-restrictions.md): Restrict inbound traffic to your function app by IP range.
* Removal of all HTTP triggers. For some applications, it's enough to simply avoid HTTP triggers and use any other event source to trigger your function.

Keep in mind that the Azure portal editor requires direct access to your running function. Any code changes through the Azure portal will require the device you're using to browse the portal to have its IP whitelisted. But you can still use anything under the platform features tab with network restrictions in place.

## How do I restrict my function app to a virtual network?

The only way to totally restrict a function such that all traffic flows through a virtual network is to use an internally load-balanced App Service Environment. This option deploys your site on a dedicated infrastructure inside a virtual network and sends all triggers and traffic through the virtual network. 

For details on using an App Service Environment, start with the article [Create and use an internal load balancer with an App Service Environment](../app-service/environment/create-ilb-ase.md).

## How can I access resources in a virtual network from a function app?

You can access resources in a virtual network from a running function by using virtual network integration. For more information, see [Virtual network integration](functions-networking-options.md#virtual-network-integration).

## How do I access resources protected by service endpoints?

By using virtual network integration (currently in preview), you can access service-endpoint-secured resources from a running function. For more information, see [Preview virtual network integration](functions-networking-options.md#preview-version-of-virtual-network-integration).

## How can I trigger a function from a resource in a virtual network?

You can trigger a function from a resource in a virtual network only by deploying your function app to an App Service Environment. For details on using an App Service Environment, see [Create and use an internal load balancer with an App Service Environment](../app-service/environment/create-ilb-ase.md).


## How can I deploy my function app in a virtual network?

Deploying to an App Service Environment is the only way to create a function app that's wholly inside a virtual network. For details on using an internal load balancer with an App Service Environment, start with the article [Create and use an internal load balancer with an App Service Environment](https://docs.microsoft.com/azure/app-service/environment/create-ilb-ase).

For scenarios where you need only one-way access to virtual network resources, or less comprehensive network isolation, see the [Functions networking overview](functions-networking-options.md).

## Next steps

To learn more about networking and functions: 

* [Follow the tutorial about getting started with virtual network integration](./functions-create-vnet.md)
* [Learn more about the networking options in Azure Functions](./functions-networking-options.md)
* [Learn more about virtual network integration with App Service and Functions](../app-service/web-sites-integrate-with-vnet.md)
* [Learn more about virtual networks in Azure](../virtual-network/virtual-networks-overview.md)
* [Enable more networking features and control with App Service Environments](../app-service/environment/intro.md)