---
# required metadata

title: Download Retail SDK samples and reference packages from GitHub and NuGet
description: This document explains to how to download Retail SDK samples from GitHub and reference packages from NuGet.
author: mugunthanm
manager: AnnBe
ms.date: 11/04/2020
ms.topic: article
ms.prod:
ms.service: dynamics-365-commerce
ms.technology:

# optional metadata

# ms.search.form:
# ROBOTS:
audience: Developer
# ms.devlang:
ms.reviewer: rhaertle
# ms.search.scope: Operations, Retail
# ms.tgt_pltfrm:
ms.custom:
ms.assetid:
ms.search.region: global
ms.search.industry: Retail
ms.author: mumani
ms.search.validFrom: 2020-11-10
ms.dyn365.ops.version: 10.0.16
---

# Download Retail SDK samples and reference packages from GitHub and NuGet

[!include [banner](../../includes/banner.md)]

This document explains to how to download Retail SDK samples from GitHub and reference packages from NuGet. The Retail SDK includes the code samples, templates, and tools that you need to extend or customize Dynamics 365 Commerce functionality. The SDK is published into different repos in GitHub based on the extension components. This topic applies to Retail SDK version 10.0.16 or later. For more information about downloading earlier versions of the Retail SDK, see [Retail software development kit (SDK)](retail-sdk-overview.md)

## Commerce.ScaleUnit repo

The **Commerce.ScaleUnit** repo contains the sample code customizing the Commerce runtime (CRT), Retail server (RS), and channel database.

Clone or download the repo from [Dynamics365 Commerce ScaleUnit Samples](https://github.com/microsoft/Dynamics365Commerce.ScaleUnit). To clone the **Commerce.ScaleUnit** repo, use the following command. (This command will work only if you have [Git tools](https://git-scm.com/downloads) installed.)

```DOS
git clone https://github.com/microsoft/Dynamics365Commerce.ScaleUnit.git
```

The repo contains multiple branches for each release. Use the release branch based on your go-live version. The repo contains only samples, so cloning this repo is optional.

| Release branch name | Version | Application release version |
|---|---|---|
| [Release/9.26](https://github.com/microsoft/Dynamics365Commerce.ScaleUnit/tree/release/9.26) | 9.26.\* | 10.0.16 |
| [Release/9.27](https://github.com/microsoft/Dynamics365Commerce.ScaleUnit/tree/release/9.26) | 9.27.\* | 10.0.17 |

To clone a single branch, use the following command:

```DOS
git clone --single-branch --branch release/9.26 https://github.com/microsoft/Dynamics365Commerce.ScaleUnit.git
```

### Commerce.ScaleUnit repo folders and projects

| Folder | Project | Contents | Description |
|---|---|---|---|
| Channel Database | ChannelDatabase.csproj | Contoso.ExampleTable.ChannelDatabase.sql | Sample database extension. |
| CommerceRuntime  | CommerceRuntime.csproj| Controller – Sample code for how to implement new Retail Server APIs.<br/>Entities, Messages, and RequestHandlers – Sample code for how to implement new CRT service.  | Sample CRT extensions. |
| ScaleUnit | ScaleUnit.csproj | Project required to generate the CSU package. | Project required to generate the CSU package. |

> [!NOTE]
> Repos for in-store components like Modern POS, Cloud POS, Hardware station,Retail scale unit, and other samples will be available in later releases.

## Download reference packages for creating APIs and consuming messages, request, entities, and contracts

Contracts, messages, entities, and request packages are published in the public NuGet feed. You can use the extension code to consume and customize existing functionalities or build new functionalities.

Consume the packages from [https://msazure.pkgs.visualstudio.com/D365/\_packaging/Commerce-SDK-Feed/nuget/v3/index.json](https://msazure.pkgs.visualstudio.com/D365/_packaging/Commerce-SDK-Feed/nuget/v3/index.json). You can add package source location in the **nuget.config** of your extension project file.

```xml
<packageSources>
    <add key="Commerce-SDK-Feed" value="https://msazure.pkgs.visualstudio.com/D365/_packaging/Commerce-SDK-Feed/nuget/v3/index.json" />
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>
```

## Reference packages available in the public NuGet feed

### Microsoft.Dynamics.Commerce.Sdk.Runtime package

This meta package contains all the required packages for implementing the CRT and Retail server extension. All the required contracts, messages, request/response, entities are included in this package.

Dependencies:

+ Microsoft.Dynamics.Commerce.Diagnostics
+ Microsoft.Dynamics.Commerce.Runtime.Data
+ Microsoft.Dynamics.Commerce.Runtime.DataServices.Messages
+ Microsoft.Dynamics.Commerce.Runtime.Entities
+ Microsoft.Dynamics.Commerce.Runtime.Framework
+ Microsoft.Dynamics.Commerce.Runtime.Hosting.Contracts
+ Microsoft.Dynamics.Commerce.Runtime.Messages
+ Microsoft.Dynamics.Commerce.Runtime.RealtimeServices.Messages
+ Microsoft.Dynamics.Commerce.Runtime.Services.Messages

### Microsoft.Dynamics.Commerce.Sdk.ScaleUnit package

This package is required to generate the CSU package for deployment.

Dependencies:

+ CSU Packaging dependencies.

### Microsoft.Dynamics.Commerce.Sdk.ChannelDatabase package

This package is required to generate the database packages with CSU.

Dependencies:

+ Channel database packaging dependencies.

### Package versioning

| Package version | Application release      |
|-----------------|--------------------------|
| 9.26.x_Preview  | 10.016 PEAP release      |
| 9.26.x          | 10.0.16 Customer preview |
| 9.26.x          | 10.016 GA                |

An extension project can consume the correct version by adding the package reference to the project with full version number, or it can use a wildcard to always get the latest version. We recommend that you use the full version number and update the version based on your go-live version. There are two options:

+ Without the wildcard.

    ```xml
    <PackageReference Include="Microsoft.Dynamics.Commerce.Sdk.Runtime" Version="9.26" />;
    ```

+ With the wildcard.

    ```xml
    <PackageReference Include="Microsoft.Dynamics.Commerce.Sdk.Runtime" Version="9.26.*" />;
    ```

With every hotfix and new application release a new version of the package will be published in the same public feed. Consume the package version based on the version required for your go-live. Consuming the higher version of the package than your go-live application version will result in runtime and deployment failures.

## Best practice and branching strategies

For detailed information on Git branching strategy, see [Git branching strategy](https://docs.microsoft.com/azure/devops/repos/git/git-branching-guidance) doc.

The following branching strategies are based on the way we use Git here at Microsoft.

Keep your branch strategy simple. Build your strategy from these concepts:

+ Use feature branches for all new features and bug fixes.
+ Merge feature branches into the main branch using pull requests.
+ Keep a high quality, up-to-date main branch.

For more information, see [How we use Git at Microsoft](https://docs.microsoft.com/azure/devops/learn/devops-at-microsoft/use-git-microsoft).

### Create a new feature branch for development and bug fixes

Create a new feature branch based on Dynamics 365 Commerce release/x.x.x branch. Clone the release/x.x.x branch and then create a new branch, following the proper naming convention. For more information, see [Git branching doc for sample naming convention](https://docs.microsoft.com/azure/devops/repos/git/git-branching-guidance#name-your-feature-branches-by-convention).

#### Command to clone and create a new branch

1. Create the clone.

```DOS
git clone --single-branch --branch release/9.26 https://github.com/microsoft/Dynamics365Commerce.ScaleUnit.git

git checkout -b private/{username}/{feature/description}
```

2. Add and commit new changes to the development branch.

```DOS
git -add .
git commit -m"commit message
```

3. After the development is completed, tested, and validated, push the changes to the main branch by doing `git push <remote> <branch>'.

```DOS
git push origin {private branch name}
```

### Create a release branch after development

After you push the development changes into the main branch, create a new release branch, and create the deployable packages from the release branch.

```DOS
git checkout -b release/x.x.x
```

Merge the changes from the release branch back to main branch if any changes done in the release branch.

```DOS
git checkout master git merge release/x.x.x
```

### Extension hotfix branch

Like the release branch, create hotfix branch for extension from main branch and release the fix and later merge the changes back to the main branch.

### Merge new SDK release branch to main and development branch

After a new version of the SDK samples is released, it's required to branch it with your new branch. The SDK contains only samples, so you don't have to get the updated changes from the new SDK release branch.

```DOS
git checkout master git merge release/x.x.x
```