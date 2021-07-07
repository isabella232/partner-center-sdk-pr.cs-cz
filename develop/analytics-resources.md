---
title: Zdroje analýzy
description: Prostředky partnerského centra obsahují data o využití, nasazení a spotřebě. Zahrnuje přehledy o nasazení a využití licencí pro partnery a zákazníky.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: 69c6c195ba1a0d657a91320b2f9b08b5269a8499
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025594"
---
# <a name="analytics-api-resources-that-help-you-report-on-license-usage-deployment-and-consumption"></a>Prostředky rozhraní API pro analýzy, které vám pomůžou ohlásit využití licencí, nasazení a spotřebu

Zde definované prostředky obsahují data, která se používají k hlášení o využití, nasazení a spotřebě.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

Prostředek **PartnerLicensesDeploymentInsights** obsahuje přehled o nasazení licence na úrovni partnera.

| Vlastnost                  | Typ                                                           | Description                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | číslo                                                         | Procento nasazených licencí                                                |
| licensesSold              | číslo                                                         | Počet prodaných licencí.                                                        |
| processedDateTime         | řetězec ve formátu data a času standardu UTC                                 | Datum a čas, kdy byla data agregována.                                     |
| serviceName               | řetězec                                                         | Název služby (například: O365, CRM).                                                  |
| kanál                   | řetězec                                                         | Název kanálu služby (například prodejce).                                    |
| atributy                | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat. Zahrnuje objectType: "PartnerLicensesDeploymentInsights" |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

Prostředek **PartnerLicensesUsageInsights** obsahuje přehled o využití licencí na úrovni partnerů.

| Vlastnost                     | Typ                                                           | Description                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | číslo                                                         | Procento nasazených licencí                                           |
| úloha úlohy                 | řetězec                                                         | Název úlohy (například: Exchange).                                             |
| processedDateTime            | řetězec ve formátu data a času standardu UTC                                 | Datum a čas, kdy byla data agregována.                                |
| serviceName                  | řetězec                                                         | Název služby (například: O365, CRM).                                             |
| kanál                      | řetězec                                                         | Název kanálu služby (například prodejce).                               |
| atributy                   | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat. Zahrnuje objectType: "PartnerLicensesUsageInsights" |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

Prostředek **CustomerLicensesDeploymentInsights** obsahuje přehled o nasazení licencí na úrovni zákazníka.

| Vlastnost          | Typ                                                           | Description                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | číslo                                                         | Počet nasazených licencí.                                                     |
| licensesSold      | číslo                                                         | Počet prodaných licencí.                                                         |
| deploymentPercent | číslo                                                         | Upravené procento nasazených licencí.                                        |
| customerId        | řetězec                                                         | Identifikátor zákazníka.                                                             |
| customerName      | řetězec                                                         | Jméno zákazníka.                                                                   |
| NázevVýrobku       | řetězec                                                         | Název produktu                                                                    |
| serviceCode       | řetězec                                                         | Kód služby licence                                                     |
| processedDateTime | řetězec ve formátu data a času standardu UTC                                 | Datum a čas, kdy byla data agregována.                                      |
| serviceName       | řetězec                                                         | Název služby (například: O365, CRM).                                                   |
| kanál           | řetězec                                                         | Název kanálu služby (například prodejce).                                     |
| atributy        | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat. Zahrnuje objectType: "CustomerLicensesDeploymentInsights" |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

Prostředek **CustomerLicensesUsageInsights** obsahuje přehled o využití licencí na úrovni zákazníka.

| Vlastnost          | Typ                                                           | Description                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | řetězec                                                         | Kód úlohy.                                                              |
| název úlohy      | číslo                                                         | Název úlohy (například Exchange).                                              |
| usagePercent      | číslo                                                         | Upravené procento použitých licencí.                                       |
| licensesActive    | číslo                                                         | Počet aktivních licencí                                                  |
| licensesQualified | číslo                                                         | Počet kvalifikovaných licencí                                               |
| customerId        | řetězec                                                         | Identifikátor zákazníka.                                                        |
| customerName      | řetězec                                                         | Jméno zákazníka.                                                              |
| Productname       | řetězec                                                         | Název produktu.                                                               |
| serviceCode (kód služby)       | řetězec                                                         | Kód služby licence.                                                |
| processedDateTime | řetězec ve formátu data a času UTC                                 | Datum a čas, kdy byla data agregována.                                 |
| Název_služby       | řetězec                                                         | Název služby (například o365, crm).                                              |
| Kanál           | řetězec                                                         | Název kanálu služby (například prodejce).                                |
| atributy        | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat. Zahrnuje objectType: CustomerLicensesUsageInsights. |