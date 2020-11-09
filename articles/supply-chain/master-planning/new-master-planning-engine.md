---
# required metadata

title: Migration to Planning Optimization for master planning
description: This topic provides information about the new master planning engine, Planning Optimization, and about migration from the existing engine. 
author: ChristianRytt
manager: tfehr
ms.date: 05/11/2020
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

ms.search.form: 
# ROBOTS: 
audience: Application User
# ms.devlang: 
ms.reviewer: kamaybac
ms.search.scope: Core, Operations
# ms.tgt_pltfrm: 
ms.custom: 19311
ms.assetid: 5ffb1486-2e08-4cdc-bd34-b47ae795ef0f
ms.search.region: Global
ms.search.industry: 
ms.author: crytt
ms.search.validFrom: 2020-11-05
ms.dyn365.ops.version: 

---

# Migration to Planning Optimization for master planning

[!include [banner](../includes/banner.md)]

The built-in master planning engine is scheduled to be made obsolete (deprecated). It's being replaced by the Planning Optimization Add-in for Microsoft Dynamics 365 Supply Chain Management. This topic provides information about the impact on new and existing deployments. It includes information about required actions.

Planning Optimization enables master planning calculations to occur outside Supply Chain Management and its Azure SQL database. The benefits that are associated with Planning Optimization include improved performance and minimized impact on the SQL database during master planning runs. Because quick planning runs can be done even during office hours, planners can immediately react to demand or parameter changes.

For more information about Planning Optimization, see [Planning Optimization overview](planning-optimization/planning-optimization-overview.md).

## Obsolescence of the existing master planning engine

Microsoft is in the process of making the built-in planning engine obsolete in favor of Planning Optimization. This change affects all cloud environments. On-premises installations aren't affected. In version 10.0.16 and later, you will receive an error message if you run the built-in master planning without generating planned production orders. However, the master planning run will be successfully completed despite the error message.

For more information about the obsolescence of the built-in planning engine, see the announcements in [Removed or deprecated features in Dynamics 365 Supply Chain Management](../get-started/removed-deprecated-features-scm-updates.md).

## Migration, messages, and exceptions

Owners of existing environments who run the built-in master planning engine without generating planned production orders will receive an email that provides details about the exception process. We recommend that you work with a partner to evaluate and plan the migration to Planning Optimization.

As has been mentioned, you will receive an error message in version 10.0.16 and later if you run the built-in master planning without generating planned production orders. This error message includes guidance about migration and instructions for requesting an exception.

### New deployments

Planning Optimization should be considered the default master planning engine for all new deployments in the cloud. In general, Planning Optimization should be used for all new deployments that don't generate planned production orders during master planning. If a new deployment depends on functionality that Planning Optimization doesn't currently support, you can request an exception so that you can continue to use the built-in master planning engine.

### Existing deployments

Owners of existing cloud-based deployments that depend on master planning should plan to migrate to Planning Optimization. If your implementation depends on functionality that Planning Optimization doesn't currently support, you can request an exception so that you can continue to use the built-in master planning engine.

For environments that currently use master planning processes that are being made obsolete, Microsoft will send an email to the environment admin. This email will provide information about the actions that are required to migrate or to request an exception.

## The exception process

You can request an exception if you must continue to use the built-in master planning engine because your business processes depends heavily on at least one feature that isn't currently implemented in Planning Optimization. For a list of available features, see [Planning Optimization fit analysis](planning-optimization/planning-optimization-fit-analysis.md).

Currently, exceptions for Planning Optimization migration are provided only if your master planning process doesn't include production (that is, planned production orders that are generated by master planning), and you require the built-in master planning engine beyond version 10.0.15.

After the required features become available, Microsoft will provide a grace period until the exception expires. The environment admin will be informed when the required features have become available and the grace period has started.

## Frequently asked questions

### On-premises environments

My environment is on-premises. Do I need an exception?

**Answer:** No. An exception isn't required for on-premises environments. You can continue to use the built-in master planning. Your environment admin will be informed if any action is required.

### Production scenarios

We use planned production orders, but I'm concerned about what will happen when we upgrade to version 10.0.16. Should I take any action?

**Answer:** You should not be concerned. You can continue to use the built-in master planning in version 10.0.16. However, we recommend that you evaluate whether migration to Planning Optimization can start with the current functionality. We also recommend that you remain informed about new functionality.

### Email from Microsoft

Our environment admin received an email from Microsoft. This email states that we should migrate to Planning Optimization or request an exception. Do I need to take any action?

**Answer:** Yes. Your environment will be affected unless you follow the instructions in the email. You can either migrate to Planning Optimization by the date specified or request an exception by using the link in the email. This link opens a questionnaire. After you've completed and submitted this questionnaire, you will receive a reply via email. Although this process is manual, Microsoft tries to reply within a week after the questionnaire is submitted.

### Error messages

I'm using version 10.0.16 or later, and I receive the following error message when I run master planning. Is master planning blocked?

> You receive this error message because the built-in master planning engine was used for scenarios supported by Planning Optimization. You should migrate to Planning Optimization now, as the current built-in master planning will be deprecated. Note that this master planning run did complete successfully.
>
> In case your migration has strong dependencies on pending features, an exception to continued usage of the built-in master planning engine can be requested.
>
> Please complete the following questionnaire to get started and if relevant request exception from migration to Planning Optimization.

**Answer:** No, master planning isn't blocked. Your master planning run was successfully completed, and you can use the result in the usual way. However, to avoid receiving this error message during future master planning runs, you must either migrate to Planning Optimization immediately or request an exception by using the link in the error message.