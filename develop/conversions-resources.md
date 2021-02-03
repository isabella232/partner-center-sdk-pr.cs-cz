---
title: Prostředky převodu
description: Přečtěte si informace o použití prostředků pro převod z partnerského centra rozhraní API, které vám pomůžou převést zkušební předplatné na placené předplatné.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d3ade5a5af76e7c637962b6bfe076ac806f337bf
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2020
ms.locfileid: "97767107"
---
# <a name="conversion-resources-to-convert-trial-subscriptions-to-paid"></a>Převod prostředků na převod předplatných zkušební verze na placené

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

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
| error          | [ConversionError](#conversionerror) | Došlo k chybě při pokusu o převod, pokud je k dispozici.. |