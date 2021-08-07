---
title: Využití Azure zaznamenávat prostředky
description: Záznam o využití Azure obsahuje podrobnosti o využití prostředku předplatného Azure.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: eb905dd41d5ab177a29bc1bd949c5eb865e4614e204250709d91f1a31304b267
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992275"
---
# <a name="azure-utilization-record-resources"></a>Využití Azure zaznamenávat prostředky

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Záznam o využití Azure obsahuje podrobnosti o využití prostředku předplatného Azure. Pokud jste partner poskytovatele cloudových služeb, který vlastní fakturační vztah pro předplatná Azure vašich zákazníků, můžete pomocí této služby REST API poskytnout škálovatelný způsob sledování využití v předplatných, abyste mohli zákazníkům odeslat fakturu na konci každého fakturačního cyklu.

Pokud chcete sledovat využití a pomoct s předpovídáním měsíčních faktur a faktur pro jednotlivé zákazníky, můžete zkombinovat dotaz Rate Card [(Karta sazeb)](get-prices-for-microsoft-azure.md) do oblasti Get prices for Microsoft Azure (Získat ceny za službu Microsoft Azure) s žádostí o získání záznamů o využití [zákazníka pro Azure.](get-a-customer-s-utilization-record-for-azure.md)

Ceny se liší podle trhu a měny a toto rozhraní API bere v úvahu umístění. Ve výchozím nastavení rozhraní API používá nastavení profilu partnera v Partnerské centrum a v jazyce prohlížeče a tato nastavení jsou přizpůsobitelná. Povědomí o umístění je zvlášť důležité, pokud spravujete prodeje na několika trzích z jedné centralizované kanceláře.

## <a name="azureutilizationrecord"></a>Záznam azureutilization

Popisuje vlastnosti prostředku záznamu využití Azure.

| Vlastnost       | Typ                                      | Vyžadováno | Popis                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | řetězec                                    | Yes      | Začátek časového rozsahu agregace využití Odpověď se seskupí podle času spotřeby (kdy byl prostředek použit vs. kdy byl nahlášen fakturačnímu systému). |
| usageEndTime   | řetězec                                    | Yes      | Konec časového rozsahu agregace využití Odpověď se seskupí podle času spotřeby. To znamená, kdy se prostředek použil vs. kdy se nahlásil fakturačnímu systému.   |
| prostředek       | object                                    | Yes      | Obsahuje [objekt AzureResource.](#azureresource)                                                                                                                                     |
| quantity       | číslo                                    | Yes      | Množství spotřebované službou [AzureResource.](#azureresource)                                                                                                                           |
| unit           | řetězec                                    | No       | Typ množství (hodiny, bajty atd.) Tato vlastnost je volitelná.                                                                                                                     |
| infoFields     | object                                    | Yes      | Páry klíč-hodnota podrobností na úrovni instance. Tento objekt může být prázdný.                                                                                                                    |
| instanceData   | object                                    | No       | Obsahuje objekt [AzureInstanceData,](#azureinstancedata) který obsahuje páry klíč-hodnota s podrobnostmi na úrovni instance. Tato vlastnost je volitelná a nemusí být zahrnuta.                  |
| atributy     | [Atributy prostředků](utility-resources.md#resourceattributes) | Yes      | Atributy metadat. Obsahuje objectType: AzureUtilizationRecord.                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>Operace s prostředky AzureUtilizationRecord

- [Získání záznamů o využití Azure zákazníkem](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>Prostředek Azure

Popisuje vlastnosti prostředku Azure.

| Vlastnost    | Typ   | Vyžadováno | Popis                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | řetězec | Yes      | Jedinečný identifikátor prostředku Azure Označuje se také jako resourceID nebo GUID prostředku. |
| name        | řetězec | No       | Popisný název spotřebovaného prostředku. Tato vlastnost je nepovinná.            |
| category    | řetězec | No       | Kategorie spotřebovaného prostředku. Tato vlastnost je nepovinná.                   |
| Podkategorie | řetězec | No       | Podkategorie spotřebovaného prostředku. Tato vlastnost je nepovinná.               |
| oblast      | řetězec | No       | Oblast spotřebovaného prostředku. Tato vlastnost je nepovinná.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Popisuje vlastnosti prostředku dat instance Azure.

| Vlastnost       | Typ             | Vyžadováno | Popis                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| identifikátor URI prostředku    | řetězec           | Yes      | Plně kvalifikované ID prostředku Azure, které zahrnuje skupiny prostředků a název instance.                   |
| location       | řetězec           | Yes      | Oblast, ve které byla služba spuštěna.                                                                               |
| partNumber     | object           | Yes      | Jedinečný obor názvů, pomocí kterého se dá identifikovat prostředek pro komerční použití třetích stran Tato vlastnost může být prázdný řetězec. |
| orderNumber    | číslo           | Yes      | Jedinečný obor názvů, který slouží k identifikaci objednávky třetí strany pro komerční tržiště. Tato vlastnost může být prázdný řetězec.          |
| tags           | pole řetězců | No       | Značky prostředků zadané uživatelem Tato vlastnost je volitelná a nemusí být zahrnutá.                            |
| additionalInfo | pole řetězců | No       | Další data pro prostředek Azure. Tato vlastnost je volitelná a nemusí být zahrnutá.                          |