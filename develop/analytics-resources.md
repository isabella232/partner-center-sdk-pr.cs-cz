---
title: Analytické prostředky
description: Partnerské centrum prostředky obsahují data o využití, nasazení a spotřebě. Zahrnuje přehledy o nasazení licencí a jejich využití partnery a zákazníky.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: fc665e8e4468648f71f242992780fbc66a02522a0b8b957a5ce68147ab33eaac
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993193"
---
# <a name="analytics-api-resources-that-help-you-report-on-license-usage-deployment-and-consumption"></a>Analytické prostředky rozhraní API, které vám pomůžou nahlásit využití, nasazení a využití licencí

Zde definované prostředky obsahují data používaná k hlášení o využití, nasazení a spotřebě.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

Prostředek **PartnerLicensesDeploymentInsights** obsahuje přehledy o nasazení licencí na úrovni partnera.

| Vlastnost                  | Typ                                                           | Description                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | číslo                                                         | Procento nasazených licencí                                                |
| licensesSold              | číslo                                                         | Počet prodaných licencí                                                        |
| processedDateTime         | řetězec ve formátu data a času UTC                                 | Datum a čas, kdy byla data agregována.                                     |
| Název_služby               | řetězec                                                         | Název služby (například o365, crm).                                                  |
| Kanál                   | řetězec                                                         | Název kanálu služby (například prodejce).                                    |
| atributy                | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat. Zahrnuje objectType: PartnerLicensesDeploymentInsights. |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

Prostředek **PartnerLicensesUsageInsights** obsahuje přehledy o využití licencí na úrovni partnera.

| Vlastnost                     | Typ                                                           | Description                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | číslo                                                         | Procento nasazených licencí                                           |
| název úlohy                 | řetězec                                                         | Název úlohy (například exchange)                                             |
| processedDateTime            | řetězec ve formátu data a času UTC                                 | Datum a čas, kdy byla data agregována.                                |
| Název_služby                  | řetězec                                                         | Název služby (například o365, crm).                                             |
| Kanál                      | řetězec                                                         | Název kanálu služby (například prodejce).                               |
| atributy                   | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat. Zahrnuje objectType: PartnerLicensesUsageInsights. |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

Prostředek **CustomerLicensesDeploymentInsights** obsahuje přehledy o nasazení licencí na úrovni zákazníka.

| Vlastnost          | Typ                                                           | Description                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | číslo                                                         | Počet nasazených licencí                                                     |
| licensesSold      | číslo                                                         | Počet prodaných licencí                                                         |
| deploymentPercent | číslo                                                         | Upravené procento nasazených licencí.                                        |
| customerId        | řetězec                                                         | Identifikátor zákazníka.                                                             |
| customerName      | řetězec                                                         | Jméno zákazníka.                                                                   |
| Productname       | řetězec                                                         | Název produktu.                                                                    |
| serviceCode (kód služby)       | řetězec                                                         | Kód služby licence.                                                     |
| processedDateTime | řetězec ve formátu data a času UTC                                 | Datum a čas, kdy byla data agregována.                                      |
| Název_služby       | řetězec                                                         | Název služby (například o365, crm).                                                   |
| Kanál           | řetězec                                                         | Název kanálu služby (například prodejce).                                     |
| atributy        | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat. Zahrnuje objectType: CustomerLicensesDeploymentInsights. |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

Prostředek **CustomerLicensesUsageInsights** obsahuje přehledy o využití licencí na úrovni zákazníka.

| Vlastnost          | Typ                                                           | Description                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode (kód úlohy)      | řetězec                                                         | Kód úlohy.                                                              |
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