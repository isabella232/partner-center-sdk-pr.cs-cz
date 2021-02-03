---
title: Objednat prostředky
description: Partner umístí objednávku, když chce zákazník koupit předplatné ze seznamu nabídek.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9db07337a98214b4aaa93e2c8b43b84702249b77
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766828"
---
# <a name="order-resources"></a>Objednat prostředky

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Partner umístí objednávku, když chce zákazník koupit předplatné ze seznamu nabídek.

>[!NOTE]
>Zdroj objednávky má omezení frekvence 500 požadavků za minutu na identifikátor tenanta.

## <a name="order"></a>Objednávka

Popisuje objednávku partnera.

| Vlastnost           | Typ                                               | Description                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| id                 | řetězec                                             | Identifikátor objednávky, který je zadán po úspěšném vytvoření objednávky.                                   |
| alternateId        | řetězec                                             | Popisný identifikátor pro objednávku.                                                                          |
|referenceCustomerId | řetězec                                             | Identifikátor zákazníka. |
| billingCycle       | řetězec                                             | Určuje četnost, s jakou se má partner fakturovat v této objednávce. Podporované hodnoty jsou názvy členů nalezené v [BillingCycleType](product-resources.md#billingcycletype). Výchozí hodnota je "Month" nebo "jednorázová" při vytváření objednávky. Toto pole se použije po úspěšném vytvoření objednávky. |
| transactionType    | řetězec                                             | Jen pro čtení. Typ transakce objednávky. Podporované hodnoty jsou "UserPurchase", "SystemPurchase" nebo "SystemBilling" |
| Položky řádku          | pole prostředků [OrderLineItem](#orderlineitem) | Seznam položek nabídek, které zákazník kupuje, včetně množství.        |
| currencyCode       | řetězec                                             | Jen pro čtení. Měna použitá při umístění objednávky Použito po úspěšném vytvoření objednávky.           |
| currencySymbol     | řetězec                                             | Jen pro čtení. Symbol měny přidružený k kódu měny. |
| creationDate       | datetime                                           | Jen pro čtení. Datum vytvoření objednávky ve formátu data a času. Použito po úspěšném vytvoření objednávky.                                   |
| status             | řetězec                                             | Jen pro čtení. Stav objednávky.  Podporované hodnoty jsou názvy členů nalezené v [**OrderStatus**](#orderstatus).        |
| odkazy              | [OrderLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky odpovídající objednávce.            |
| atributy         | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající pořadí.       |

## <a name="orderlineitem"></a>OrderLineItem

Objednávka obsahuje seřazený seznam nabídek a každá položka je reprezentována jako OrderLineItem.

| Vlastnost             | Typ                                      | Description                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int                                       | Každá položka řádku v kolekci získá jedinečné číslo řádku, počítáno od 0 do Count-1.                                                                                                                                                 |
| Hodnotami OfferId              | řetězec                                    | ID nabídky                                                                                                                                                                                                                       |
| subscriptionId       | řetězec                                    | ID předplatného                                                                                                                                                                                                                |
| parentSubscriptionId | řetězec                                    | Nepovinný parametr. ID nadřazeného odběru v nabídce doplňku Platí pouze pro opravu.                                                                                                                                                     |
| friendlyName         | řetězec                                    | Nepovinný parametr. Popisný název předplatného definovaného partnerem, který vám umožní určit nejednoznačnost.                                                                                                                                              |
| quantity             | int                                       | Počet licencí nebo instancí.                                                                                                                                                                                |
| termDuration         | řetězec                                    | ISO 8601 reprezentace doby trvání období. Aktuální podporované hodnoty jsou **P1M** (1 měsíc), **P1Y** (1 rok) a **P3Y** (3 roky).                               |
| transactionType      | řetězec                                    | Jen pro čtení. Typ transakce položky řádku Podporovány jsou hodnoty "New", "Renew", "addQuantity", "removeQuantity", "Cancel", "Convert" nebo "customerCredit". |
| partnerIdOnRecord    | řetězec                                    | Když nepřímý poskytovatel umístí objednávku jménem nepřímého prodejce, naplňte toto pole do ID MPN **nepřímého prodejce** (nikdy ID nepřímého poskytovatele). To zajišťuje správné účetnictví pro motivaci. |
| provisioningContext  | Řetězec<slovníku, řetězec>            | Informace požadované pro zřizování některých položek v katalogu. Vlastnost provisioningVariables v SKU indikuje, které vlastnosti jsou požadovány pro konkrétní položky v katalogu.                                                                                                                                               |
| odkazy                | [OrderLineItemLinks](#orderlineitemlinks) | Jen pro čtení. Odkazy na prostředky odpovídající položce řádku objednávky.                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |Údaje o době platnosti obnovení.                                                                           |

## <a name="renewsto"></a>RenewsTo

Představuje údaje o době platnosti obnovení.

| Vlastnost              | Typ             | Vyžadováno        | Popis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | řetězec           | No              | ISO 8601 představuje dobu trvání období obnovy. Aktuální podporované hodnoty jsou **P1M** (1 měsíc) a **P1Y** (1 rok). |

## <a name="orderlinks"></a>OrderLinks

Představuje odkazy na prostředky odpovídající objednávce.

| Vlastnost           | Typ                                         | Description                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [Odkaz](utility-resources.md#link)            | Po naplnění se zobrazí odkaz pro načtení stavu zřizování pro objednávku.       |
| samorozbalující               | [Odkaz](utility-resources.md#link)            | Odkaz pro načtení prostředku objednávky.                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

Představuje úplné předplatné přidružené k objednávce.

| Vlastnost           | Typ                                         | Description                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [Odkaz](utility-resources.md#link)            | Po vyplnění odkaz pro načtení [stavu zřizování](#orderlineitemprovisioningstatus) položky řádku.       |
| skladové                | [Odkaz](utility-resources.md#link)            | Odkaz pro načtení informací o SKU pro zakoupenou položku katalogu                    |
| předplatné       | [Odkaz](utility-resources.md#link)            | Po vyplnění se zobrazí odkaz na úplné informace o odběru.                       |
| activationLinks    | [Odkaz](utility-resources.md#link)            | Po naplnění na odkaz získat prostředek pro aktivaci předplatného.             |

## <a name="orderstatus"></a>OrderStatus

[Enum/dotnet/API/System. Enum) s hodnotami, které označují stav objednávky.

| Hodnota              | Pozice     | Description                                     |
|--------------------|--------------|-------------------------------------------------|
| Neznámý            | 0            | Inicializátor výčtu.                               |
| kompletní          | 1            | Indikuje, že je objednávka dokončená.          |
| pending            | 2            | Indikuje, že objednávka stále čeká na vyřízení.      |
| stornován          | 3            | Indikuje, že objednávka byla zrušena.    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

Představuje stav zřizování [OrderLineItem](#orderlineitem).

| Vlastnost                        | Typ                                | Description                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber                  | int                                 | Jedinečné číslo řádku položky řádku objednávky Hodnoty jsou v rozsahu od 0 do Count-1.             |
| status                          | řetězec                              | Stav zřizování položky řádku objednávky Mezi tyto hodnoty patří:</br>"Splněno": plnění objednávky je úspěšně dokončeno a uživatel bude moci použít rezervace</br>"Nesplněno": nedodrženo v důsledku zrušení</br>"PrefulfillmentPending": vaše žádost se pořád zpracovává, plnění ještě není dokončené. |
| quantityProvisioningInformation | Seznam<[QuantityProvisioningStatus](#quantityprovisioningstatus)> | Seznam informací o stavu zřizování pro položku řádku objednávky. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

Představuje stav zřizování podle množství.

| Vlastnost                           | Typ                                         | Description                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | int                                          | Počet položek                                 |
| status                             | řetězec                                       | Stav počtu položek                   |
