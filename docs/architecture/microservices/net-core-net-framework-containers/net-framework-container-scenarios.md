---
title: When to choose .NET Framework for Docker containers
description: .NET Microservices Architecture for Containerized .NET Applications | When to choose .NET Framework for Docker containers
ms.date: 01/30/2020
---
# When to choose .NET Framework for Docker containers

While .NET Core offers significant benefits for new applications and application patterns, .NET Framework will continue to be a good choice for many existing scenarios.

## Migrating existing applications directly to a Windows Server container

You might want to use Docker containers just to simplify deployment, even if you are not creating microservices. For example, perhaps you want to improve your DevOps workflow with Docker—containers can give you better isolated test environments and can also eliminate deployment issues caused by missing dependencies when you move to a production environment. In cases like these, even if you are deploying a monolithic application, it makes sense to use Docker and Windows Containers for your current .NET Framework applications.

In most cases for this scenario, you will not need to migrate your existing applications to .NET Core; you can use Docker containers that include the traditional .NET Framework. However, a recommended approach is to use .NET Core as you extend an existing application, such as writing a new service in ASP.NET Core.

## Using third-party .NET libraries or NuGet packages not available for .NET Core

Third-party libraries are quickly embracing [.NET Standard](../../../standard/net-standard.md), which enables code sharing across all .NET flavors, including .NET Core. With .NET Standard 2.0 and later, the API surface compatibility across different frameworks has become significantly larger. Even more, .NET Core 2.x and newer applications can also directly reference existing .NET Framework libraries (see [.NET Framework 4.6.1 supporting .NET Standard 2.0](https://github.com/dotnet/standard/blob/master/docs/planning/netstandard-2.0/README.md#net-framework-461-supporting-net-standard-20)).

In addition, the [Windows Compatibility Pack](../../../core/porting/windows-compat-pack.md) extends the API surface available for .NET Standard 2.0 on Windows. This pack allows recompiling most existing code to .NET Standard 2.x with little or no modification, to run on Windows.

However, even with that exceptional progression since .NET Standard 2.0 and .NET Core 2.1, there might be cases where certain NuGet packages need Windows to run and might not support .NET Core. If those packages are critical for your application, then you will need to use .NET Framework on Windows Containers.

## Using .NET technologies not available for .NET Core

Some .NET Framework technologies aren't available in the current version of .NET Core (version 3.1 as of this writing). Some of them might become available in later releases, but others don't fit the new application patterns targeted by .NET Core and might never be available.

The following list shows most of the technologies that aren't available in .NET Core 3.1:

- ASP.NET Web Forms. This technology is only available on .NET Framework. Currently there are no plans to bring ASP.NET Web Forms to .NET Core.

- WCF services. Even when a [WCF-Client library](https://github.com/dotnet/wcf) is available to consume WCF services from .NET Core, as of Feb-2020, the WCF server implementation is only available on .NET Framework. This scenario might be considered for future releases of .NET Core, there are even some APIs considered for inclusion in the [Windows Compatibility Pack](../../../core/porting/windows-compat-pack.md).

- Workflow-related services. Windows Workflow Foundation (WF), Workflow Services (WCF + WF in a single service), and WCF Data Services (formerly known as ADO.NET Data Services) are only available on .NET Framework. There are currently no plans to bring them to .NET Core.

In addition to the technologies listed in the official [.NET Core roadmap](https://github.com/dotnet/core/blob/master/roadmap.md), other features might be ported to .NET Core or the new [unified .NET platform](https://devblogs.microsoft.com/dotnet/introducing-net-5/). You might consider participating in the discussions on GitHub so that your voice can be heard. And if you think something is missing, file a new issue in the [dotnet/runtime](https://github.com/dotnet/runtime/issues/new) GitHub repository.

## Using a platform or API that doesn't support .NET Core

Some Microsoft and third-party platforms don't support .NET Core. For example, some Azure services provide an SDK that isn't yet available for consumption on .NET Core. Most Azure SDK should eventually be ported to .NET Core/Standard but some might not for various reasons. You can see the available Azure SDKs in the [Azure SDK Latest Releases](https://azure.github.io/azure-sdk/releases/latest/index.html) page.

In the meantime, if any platform or service in Azure still doesn't support .NET Core with its client API, you can use the equivalent REST API from the Azure service or the client SDK on .NET Framework.

### Additional resources

- **.NET fundamentals** \
  [https://docs.microsoft.com/dotnet/fundamentals](../../../fundamentals/index.yml)

- **Porting from .NET Framework to .NET Core** \
  [https://docs.microsoft.com/dotnet/core/porting/index](../../../core/porting/index.md)

- **.NET Core on Docker Guide** \
  [https://docs.microsoft.com/dotnet/core/docker/introduction](../../../core/docker/introduction.md)

- **.NET Components Overview** \
  [https://docs.microsoft.com/dotnet/standard/components](../../../standard/components.md)

>[!div class="step-by-step"]
>[Previous](net-core-container-scenarios.md)
>[Next](container-framework-choice-factors.md)
