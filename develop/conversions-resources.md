---
title: Převod prostředků
description: Seznamte se s Partnerské centrum rozhraní API pro převod, které vám pomůžou převést zkušební předplatné na placené předplatné.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9e7f8985fa15f4959f3cb5a729e492bbb9f3f624a5812f5b87fc119f841dc87e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991867"
---
# <a name="conversion-resources-to-convert-trial-subscriptions-to-paid"></a>Převod prostředků pro převod zkušebních předplatných na placené

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Převod prostředků podporuje převod zkušebního předplatného na placené předplatné.

## <a name="conversion"></a>Převod

Obsahuje informace použité k převodu zkušebního předplatného na placené předplatné.

| Vlastnost | Typ | Description |
| -------- | ---- | ----------- |
| ID nabídky | řetězec | Identifikátor původní zkušební nabídky. |
| targetOfferId (ID cílové nabídky) | řetězec | Identifikátor nabídky pro cílovou nabídku. |
| Kódobjednávky | řetězec | Identifikátor objednávky. |
| quantity | int | Počet licencí Výchozí hodnota je počet licencí ve zkušebním předplatném. |
| billingCycle | řetězec | Určuje, jak často se partnerovi účtuje předplatné. Možné hodnoty: **Měsíční** (partner se fakturuje měsíčně), **Roční** (partner se fakturuje ročně) nebo Žádný **(partner** se neúčtuje. Používá se pro zkušební předplatná). |

## <a name="conversionerror"></a>Chyba převodu

Představuje chybu, ke které došlo během převodu.

| Vlastnost | Typ | Description |
| -------- | ---- | ----------- |
| kód | řetězec | Kód chyby související s problémem. Možné hodnoty: **Jiné** (obecná chyba), **ConversionsNotFound** (nelze najít žádné převody pro zkušební předplatné, na které se má převést).
| description | řetězec | Popisný text popisující problém |

## <a name="conversionresult"></a>Převodvýsledek

Představuje výsledek provedení převodu předplatného.

| Vlastnost       | Typ                                | Description                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | řetězec                              | Identifikátor předplatného.                                           |
| ID nabídky        | řetězec                              | Původní identifikátor nabídky.                                         |
| targetOfferId (ID cílové nabídky)  | řetězec                              | Identifikátor nabídky pro cílovou nabídku.                             |
| error          | [Chyba převodu](#conversionerror) | Chyba, ke které došlo při pokusu o převod, pokud je k mání |