---
title: Karta s sazbou Azure – aktuální ceny Azure
description: Zjistěte, jak pomocí karty sazeb Azure získat aktuální ceny nabídek Azure ve vaší oblasti v reálném čase. Karta sazby Azure je přístupná přes Partnerské centrum REST API.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e0b1bc9d764e2132315205653f46cef73b25e02f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974331"
---
# <a name="azure-rate-card-resources-to-get-real-time-current-azure-prices-on-azure-offers-in-your-region"></a>Prostředky karet s sazbami Azure pro získání aktuálních cen Azure v reálném čase pro nabídky Azure ve vaší oblasti

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Karta s sazbami Azure poskytuje nabídky Azure za ceny v reálném čase. Ceny Azure jsou dynamické a často se mění. Microsoft publikuje aktualizace na Partnerské centrum, ale REST API nabízí nejrychlejší způsob, jak Cloud Solution Provider partneři získat aktuální ceny.

Pokud chcete sledovat využití a pomoct s předpovídáním měsíčních faktur a faktur pro jednotlivé zákazníky, můžete zkombinovat dotaz Rate Card [(Karta sazeb)](get-prices-for-microsoft-azure.md) do oblasti Get prices for Microsoft Azure (Získat ceny za službu Microsoft Azure) s žádostí o získání záznamů o využití [zákazníka pro Azure.](get-a-customer-s-utilization-record-for-azure.md)

Ceny se liší podle trhu a měny a toto rozhraní API bere v úvahu umístění. Ve výchozím nastavení rozhraní API používá nastavení profilu partnera v Partnerské centrum a v jazyce prohlížeče a tato nastavení jsou přizpůsobitelná. Povědomí o umístění je zvlášť důležité, pokud spravujete prodeje na několika trzích z jedné centralizované kanceláře.

## <a name="azureratecard"></a>AzureRateCard

Popisuje vlastnosti prostředku karty sazeb Azure.

| Vlastnost      | Typ                                      | Description                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | řetězec                                    | Měna, ve které jsou sazby k dispozici.                     |
| isTaxIncluded | boolean                                   | Všechny sazby jsou předtaxní, takže tato vlastnost vrátí hodnotu `false` . |
| locale        | řetězec                                    | Jazyková verze, ve které jsou lokalizovány informace o prostředku.       |
| Metrů        | pole objektů                          | Pole objektů [AzureMeter](#azuremeter)                       |
| offerTerms    | pole objektů                          | Pole [objektů AzureOfferTerm](#azureofferterm)               |
| atributy    | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat. Obsahuje `"objectType": "AzureRateCard"`   |

### <a name="operations-on-the-azureratecard-resource"></a>Operace s prostředky AzureRateCard

- [Získání cen pro Microsoft Azure](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| Vlastnost         | Typ             | Description                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | řetězec           | Jedinečný identifikátor měřiče.                                                                    |
| name             | řetězec           | Popisný název měřiče.                                                                   |
| Sazby            | object           | Sazby měřičů. Klíč je množství měřiče (řetězec) a hodnota je sazba měřiče (číslo). |
| tags             | pole řetězců | Volitelné značky měřiče. Toto pole může být prázdné.                                                 |
| category         | řetězec           | Kategorie prostředku                                                                     |
| Podkategorie      | řetězec           | Podkategorie prostředku                                                                 |
| oblast           | řetězec           | Oblast ID.                                                                             |
| unit             | řetězec           | Typ množství (hodiny, bajty atd.)                                                     |
| includedQuantity | číslo           | Množství měřiče, které je zahrnuté bezplatně.                                               |
| effectiveDate    | řetězec           | Datum, kdy je tento měřič v platnosti.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| Vlastnost         | Typ             | Description                             |
|------------------|------------------|-----------------------------------------|
| name             | řetězec           | Popisný název výrazu nabídky.        |
| discount         | číslo           | Sleva použitá, pokud je k nějaké dojde.           |
| excludedMeterIds | pole řetězců | Měřiče vyloučené z nabídky, pokud nějaké jsou. |
| effectiveDate    | řetězec           | Datum, kdy nabídka platí.        |
