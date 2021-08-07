---
title: Karta Azure Rate – aktuální ceny Azure
description: Naučte se, jak pomocí karty Azure Rate získat v reálném čase aktuální ceny pro nabídky Azure ve vaší oblasti. Ke kartě Azure se dostanete prostřednictvím partnerského centra REST API.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 52b9a9bea59690a8185a381647498de69a1476b1a4d4e8d632c5d13382776114
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991205"
---
# <a name="azure-rate-card-resources-to-get-real-time-current-azure-prices-on-azure-offers-in-your-region"></a>Prostředky služby Azure Rate na základě aktuálních cen Azure ve vaší oblasti v reálném čase.

**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Karta Azure Rate nabízí ceny pro Azure v reálném čase. Ceny Azure jsou dynamické a často se mění. společnost Microsoft publikuje aktualizace v partnerském centru, ale REST API poskytuje nejrychlejší způsob, jak se Cloud Solution Provider partneři dostanou k získání aktuálních cen.

pokud chcete sledovat využití a předpovídat měsíční fakturaci a faktury pro jednotlivé zákazníky, můžete zkombinovat dotaz na kartu s sazbami a [získat tak ceny pro Microsoft Azure](get-prices-for-microsoft-azure.md) s žádostí o [získání záznamů o využití zákazníka pro Azure](get-a-customer-s-utilization-record-for-azure.md).

Ceny se liší podle trhu a měny a toto rozhraní API bere v úvahu umístění. Ve výchozím nastavení používá rozhraní API nastavení partnerského profilu v partnerském centru a v jazyce prohlížeče a tato nastavení jsou přizpůsobitelná. Povědomí o poloze je obzvláště důležité, pokud spravujete prodej na více trzích z jedné centrálně centralizované kanceláře.

## <a name="azureratecard"></a>AzureRateCard

Popisuje vlastnosti prostředku služby Azure Rate Card.

| Vlastnost      | Typ                                      | Description                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | řetězec                                    | Měna, ve které jsou sazby poskytovány.                     |
| isTaxIncluded | boolean                                   | Všechny sazby jsou pretax, takže tato vlastnost vrátí jako `false` . |
| locale        | řetězec                                    | Jazyková verze, ve které jsou lokalizovány informace o prostředku.       |
| měřiče        | pole objektů                          | Pole objektů [AzureMeter](#azuremeter)                       |
| offerTerms    | pole objektů                          | Pole objektů [AzureOfferTerm](#azureofferterm)               |
| atributy    | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat. Zobrazí `"objectType": "AzureRateCard"`   |

### <a name="operations-on-the-azureratecard-resource"></a>Operace s prostředkem AzureRateCard

- [Získání cen pro Microsoft Azure](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| Vlastnost         | Typ             | Description                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | řetězec           | Jedinečný identifikátor měřiče.                                                                    |
| name             | řetězec           | Popisný název měřiče                                                                   |
| frekvencí            | object           | Tarify měřiče. Klíč je množství měřiče (řetězec) a hodnota je sazba měřiče (číslo). |
| tags             | pole řetězců | Volitelné značky měřiče. Toto pole může být prázdné.                                                 |
| category         | řetězec           | Kategorie prostředku                                                                     |
| podkategorie      | řetězec           | Podkategorie prostředku                                                                 |
| oblast           | řetězec           | Oblast ID                                                                             |
| unit             | řetězec           | Typ množství (v hodinách, bajtech atd.)                                                     |
| includedQuantity | číslo           | Množství měřiče, které je zahrnuto zdarma.                                               |
| effectiveDate    | řetězec           | Datum, kdy je toto měření v platnosti.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| Vlastnost         | Typ             | Description                             |
|------------------|------------------|-----------------------------------------|
| name             | řetězec           | Popisný název termínu nabídky        |
| discount         | číslo           | Použitá sleva, pokud nějaká existuje.           |
| excludedMeterIds | pole řetězců | Měřiče vyloučené z nabídky, pokud existují. |
| effectiveDate    | řetězec           | Datum, kdy je nabídka platná.        |
