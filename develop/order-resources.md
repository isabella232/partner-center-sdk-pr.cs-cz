---
title: Objednání prostředků
description: Partner objednává, když zákazník chce koupit předplatné ze seznamu nabídek.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 128c9e041cacc1c15f6187c4d99690d5c5fa4183
ms.sourcegitcommit: 59950cf131440786779c8926be518c2dc4bc4030
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/31/2021
ms.locfileid: "115009165"
---
# <a name="order-resources"></a>Objednání prostředků

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Partner objednává, když zákazník chce koupit předplatné ze seznamu nabídek.

>[!NOTE]
>Prostředek Order (Objednávka) má omezení rychlosti 500 požadavků za minutu na identifikátor tenanta.

## <a name="order"></a>Objednávka

Popisuje objednávku partnera.

| Vlastnost           | Typ                                               | Description                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| id                 | řetězec                                             | Identifikátor objednávky zadaný po úspěšném vytvoření objednávky.                                   |
| alternativní ID        | řetězec                                             | Popisný identifikátor objednávky.                                                                          |
|referenčníCustomerId | řetězec                                             | Identifikátor zákazníka. |
| billingCycle       | řetězec                                             | Určuje frekvenci, s jakou se partner účtuje za tuto objednávku. Podporované hodnoty jsou názvy členů, které najdete v [části BillingCycleType](product-resources.md#billingcycletype). Výchozí hodnota je "Měsíčně" nebo "OneTime" při vytváření objednávky. Toto pole se použije při úspěšném vytvoření objednávky. |
| Transactiontype    | řetězec                                             | Jen pro čtení. Typ transakce objednávky. Podporované hodnoty jsou UserPurchase, SystemPurchase nebo SystemBilling. |
| položky řádku          | pole prostředků [OrderLineItem](#orderlineitem) | Itemized list of the offers the customer is purchasing including the quantity.        |
| currencyCode       | řetězec                                             | Jen pro čtení. Měna použitá při zadávání objednávky. Použije se při úspěšném vytvoření objednávky.           |
| Currencysymbol     | řetězec                                             | Jen pro čtení. Symbol měny přidružený k kódu měny. |
| datum vytvoření       | datetime                                           | Jen pro čtení. Datum vytvoření objednávky ve formátu data a času. Použije se při úspěšném vytvoření objednávky.                                   |
| status             | řetězec                                             | Jen pro čtení. Stav objednávky  Podporované hodnoty jsou názvy členů, které najdete v [**OrderStatus**](#orderstatus).        |
| Odkazy              | [OrderLinks](utility-resources.md#resourcelinks)           | Propojení prostředků odpovídající objednávce            |
| atributy         | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat odpovídající order.       |

## <a name="orderlineitem"></a>OrderLineItem (PoložkaŘádku Objednávky)

Objednávka obsahuje seznam nabídek s položkami a každá položka je reprezentovaná jako OrderLineItem.

| Vlastnost             | Typ                                      | Description                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int                                       | Každá položka řádku v kolekci získá jedinečné číslo řádku, počítá se od 0 do count-1.                                                                                                                                                 |
| ID nabídky              | řetězec                                    | ID nabídky.                                                                                                                                                                                                                       |
| subscriptionId       | řetězec                                    | ID předplatného.                                                                                                                                                                                                                |
| PARENTSubscriptionId | řetězec                                    | Nepovinný parametr. ID nadřazeného předplatného v nabídce doplňku. Platí jenom pro PATCH.                                                                                                                                                     |
| Friendlyname         | řetězec                                    | Nepovinný parametr. Popisný název předplatného definovaného partnerem, který pomáhá jednoznačně rozpoznat.                                                                                                                                              |
| quantity             | int                                       | Počet licencí nebo instancí                                                                                                                                                                                |
| termDuration         | řetězec                                    | Reprezentace doby trvání období podle STANDARDu ISO 8601. Aktuální podporované hodnoty jsou **P1M (1** měsíc), **P1Y** (1 rok) a **P3Y** (3 roky).                               |
| Transactiontype      | řetězec                                    | Jen pro čtení. Typ transakce řádkové položky. Podporované hodnoty jsou "new", "renew", "addQuantity", "removeQuantity", "cancel", "convert" nebo "customerCredit". |
| id partneraZáznam    | řetězec                                    | Když nepřímý poskytovatel zadá objednávku jménem nepřímého prodejce, zadejte do tohoto pole pouze ID MPN nepřímého prodejce **(nikdy** ID nepřímého poskytovatele). Tím se zajistí správné účtování pobídek. |
| provisioningContext  | Slovníkový<řetězec, řetězec>            | Informace požadované pro zřizování některých položek v katalogu. Vlastnost provisioningVariables v SKU indikuje, které vlastnosti jsou požadovány pro konkrétní položky v katalogu.                                                                                                                                               |
| odkazy                | [OrderLineItemLinks](#orderlineitemlinks) | Jen pro čtení. Odkazy na prostředky odpovídající položce řádku objednávky.                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |Údaje o době platnosti obnovení.                                                                           |
| AttestationAccepted             | bool                 | Označuje smlouvu o nabídkách nebo podmínkách SKU. Vyžaduje se jenom pro nabídky nebo skladové položky, kde SkuAttestationProperties nebo OfferAttestationProperties enforceAttestation má hodnotu true.                                                                            |

## <a name="renewsto"></a>RenewsTo

Představuje údaje o době platnosti obnovení.

| Vlastnost              | Typ             | Vyžadováno        | Popis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | řetězec           | No              | ISO 8601 představuje dobu trvání období obnovy. Aktuální podporované hodnoty jsou **P1M** (1 měsíc) a **P1Y** (1 rok). |

## <a name="orderlinks"></a>OrderLinks

Představuje odkazy na prostředky odpovídající objednávce.

| Vlastnost           | Typ                                         | Description                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [Propojit](utility-resources.md#link)            | Po naplnění se zobrazí odkaz pro načtení stavu zřizování pro objednávku.       |
| samorozbalující               | [Propojit](utility-resources.md#link)            | Odkaz pro načtení prostředku objednávky.                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

Představuje úplné předplatné přidružené k objednávce.

| Vlastnost           | Typ                                         | Description                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [Propojit](utility-resources.md#link)            | Po vyplnění odkaz pro načtení [stavu zřizování](#orderlineitemprovisioningstatus) položky řádku.       |
| skladové                | [Propojit](utility-resources.md#link)            | Odkaz pro načtení informací o SKU pro zakoupenou položku katalogu                    |
| předplatné       | [Propojit](utility-resources.md#link)            | Po vyplnění se zobrazí odkaz na úplné informace o odběru.                       |
| activationLinks    | [Propojit](utility-resources.md#link)            | Po naplnění na odkaz získat prostředek pro aktivaci předplatného.             |

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
| status                          | řetězec                              | Stav zřizování položky řádku objednávky Mezi tyto hodnoty patří:</br>**Splněno**: plnění objednávky je úspěšně dokončeno a uživatel bude moci použít rezervace.</br>**Nesplněno**: není splněné kvůli zrušení.</br>**PrefulfillmentPending**: vaše žádost se pořád zpracovává, plnění ještě není dokončené. |
| quantityProvisioningInformation | Seznam<[QuantityProvisioningStatus](#quantityprovisioningstatus)> | Seznam informací o stavu zřizování pro položku řádku objednávky. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

Představuje stav zřizování podle množství.

| Vlastnost                           | Typ                                         | Description                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | int                                          | Počet položek                                 |
| status                             | řetězec                                       | Stav počtu položek                   |
