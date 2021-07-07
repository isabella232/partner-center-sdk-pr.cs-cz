---
title: Prostředky převodu
description: Přečtěte si informace o použití prostředků pro převod z partnerského centra rozhraní API, které vám pomůžou převést zkušební předplatné na placené předplatné.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1863c365627807d8de2534a2d3116807a5de70e1
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973889"
---
# <a name="conversion-resources-to-convert-trial-subscriptions-to-paid"></a>Převod prostředků na převod předplatných zkušební verze na placené

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Převod prostředků podporuje převod zkušebního předplatného na placené předplatné.

## <a name="conversion"></a>Převod

Obsahuje informace, které slouží k převodu zkušebního předplatného na placené předplatné.

| Vlastnost | Typ | Description |
| -------- | ---- | ----------- |
| Hodnotami OfferId | řetězec | Identifikátor nabídky původní nabídky zkušební verze. |
| targetOfferId | řetězec | Identifikátor nabídky cílové nabídky |
| Seskup | řetězec | Identifikátor objednávky. |
| quantity | int | Počet licencí. Výchozí hodnota je počet licencí ve zkušebním předplatném. |
| billingCycle | řetězec | Určuje, jak často se má partner účtovat za předplatné. Možné hodnoty: **měsíčně** (partner se účtuje měsíčně), **roční** (účtuje se za rok) nebo **žádné** (partner se fakturuje). Používá se pro zkušební verze předplatného. |

## <a name="conversionerror"></a>ConversionError

Představuje chybu, k níž došlo během převodu.

| Vlastnost | Typ | Description |
| -------- | ---- | ----------- |
| kód | řetězec | Kód chyby přidružený k problému. Možné hodnoty: **jiné** (obecná chyba), **ConversionsNotFound** (nejdou najít žádné převody zkušebního předplatného, na které se má převést).
| description | řetězec | Popisný text popisující problém. |

## <a name="conversionresult"></a>ConversionResult

Představuje výsledek provádění převodu předplatného.

| Vlastnost       | Typ                                | Description                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | řetězec                              | Identifikátor předplatného.                                           |
| Hodnotami OfferId        | řetězec                              | Původní identifikátor nabídky                                         |
| targetOfferId  | řetězec                              | Identifikátor nabídky cílové nabídky                             |
| error          | [ConversionError](#conversionerror) | Došlo k chybě při pokusu o převod, pokud je to možné. |