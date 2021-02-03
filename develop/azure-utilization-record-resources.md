---
title: Zdroje záznamů využití Azure
description: Záznam využití Azure obsahuje podrobnosti o využití prostředku předplatného Azure.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 21d39c4497c00f5abeeeb771dfe20cd1e2b1c13a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766695"
---
# <a name="azure-utilization-record-resources"></a>Zdroje záznamů využití Azure

**Platí pro:**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Záznam využití Azure obsahuje podrobnosti o využití prostředku předplatného Azure. Pokud jste partner poskytovatele cloudové služby, který je vlastníkem fakturačního vztahu pro předplatná Azure vašich zákazníků, můžete tento REST API využít k tomu, abyste zajistili škálovatelný způsob, jak sledovat využití vyplývající z předplatných za účelem odeslání faktury zákazníkům na konci každého fakturačního cyklu.

Pokud chcete sledovat využití a předpovídat měsíční fakturaci a faktury pro jednotlivé zákazníky, můžete zkombinovat dotaz na kartu s sazbami a [získat tak ceny pro Microsoft Azure](get-prices-for-microsoft-azure.md) s žádostí o [získání záznamů o využití zákazníka pro Azure](get-a-customer-s-utilization-record-for-azure.md).

Ceny se liší podle trhu a měny a toto rozhraní API bere v úvahu umístění. Ve výchozím nastavení používá rozhraní API nastavení partnerského profilu v partnerském centru a v jazyce prohlížeče a tato nastavení jsou přizpůsobitelná. Povědomí o poloze je obzvláště důležité, pokud spravujete prodej na více trzích z jedné centrálně centralizované kanceláře.

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Popisuje vlastnosti prostředku záznamu využití Azure.

| Vlastnost       | Typ                                      | Vyžadováno | Popis                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | řetězec                                    | Yes      | Začátek časového rozsahu agregace využití Odpověď je seskupená podle času spotřeby (kdy se prostředek skutečně použil vs. kdy byl nahlášen do fakturačního systému). |
| usageEndTime   | řetězec                                    | Yes      | Konec agregace časového rozsahu použití Odpověď je seskupena podle času spotřeby. To znamená, že když se prostředek skutečně použil vs. kdy byl hlášený k fakturačnímu systému.   |
| prostředek       | object                                    | Yes      | Obsahuje objekt [AzureResource](#azureresource) .                                                                                                                                     |
| quantity       | číslo                                    | Yes      | Množství spotřebované v [AzureResource.](#azureresource)                                                                                                                           |
| unit           | řetězec                                    | No       | Typ množství (v hodinách, bajtech atd.) Tato vlastnost je nepovinná.                                                                                                                     |
| infoFields     | object                                    | Yes      | Páry klíč-hodnota podrobností úrovně instance. Tento objekt může být prázdný.                                                                                                                    |
| instanceData   | object                                    | No       | Obsahuje objekt [AzureInstanceData](#azureinstancedata) , který obsahuje páry klíč-hodnota podrobností na úrovni instance. Tato vlastnost je volitelná a nemusí být zahrnutá.                  |
| atributy     | [ResourceAttributes](utility-resources.md#resourceattributes) | Yes      | Atributy metadat. Obsahuje objectType: "AzureUtilizationRecord"                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>Operace s prostředkem AzureUtilizationRecord

- [Získání záznamů o využití Azure zákazníkem](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Popisuje vlastnosti prostředku Azure.

| Vlastnost    | Typ   | Vyžadováno | Popis                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | řetězec | Yes      | Jedinečný identifikátor prostředku Azure Označuje se také jako resourceID nebo GUID prostředku. |
| name        | řetězec | No       | Popisný název spotřebovaného prostředku Tato vlastnost je nepovinná.            |
| category    | řetězec | No       | Kategorie spotřebovaného prostředku. Tato vlastnost je nepovinná.                   |
| podkategorie | řetězec | No       | Podkategorie spotřebovaného prostředku. Tato vlastnost je nepovinná.               |
| oblast      | řetězec | No       | Oblast spotřebovaného prostředku. Tato vlastnost je nepovinná.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Popisuje vlastnosti prostředku dat instance Azure.

| Vlastnost       | Typ             | Vyžadováno | Popis                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri    | řetězec           | Yes      | Plně kvalifikované ID prostředku Azure, které zahrnuje skupiny prostředků a název instance.                   |
| location       | řetězec           | Yes      | Oblast, ve které byla služba spuštěna.                                                                               |
| partNumber     | object           | Yes      | Jedinečný obor názvů, pomocí kterého se dá identifikovat prostředek pro komerční použití třetích stran Tato vlastnost může být prázdný řetězec. |
| orderNumber    | číslo           | Yes      | Jedinečný obor názvů, který slouží k identifikaci objednávky třetí strany pro komerční tržiště. Tato vlastnost může být prázdný řetězec.          |
| tags           | pole řetězců | No       | Značky prostředků zadané uživatelem Tato vlastnost je volitelná a nemusí být zahrnutá.                            |
| additionalInfo | pole řetězců | No       | Další data pro prostředek Azure. Tato vlastnost je volitelná a nemusí být zahrnutá.                          |