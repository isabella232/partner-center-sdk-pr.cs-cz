---
title: Objednání prostředků
description: Partner objednává, když zákazník chce koupit předplatné ze seznamu nabídek.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c2b841b73921c9727180e5649ec6a6213081442a8047c6b088e5f9fc6428ef0b
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997851"
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
| provisioningContext  | Slovníkový<řetězec, řetězec>            | Informace vyžadované pro zřizování některých položek v katalogu. Vlastnost provisioningVariables ve SKU určuje, které vlastnosti jsou vyžadovány pro konkrétní položky v katalogu.                                                                                                                                               |
| Odkazy                | [OrderLineItemLinks](#orderlineitemlinks) | Jen pro čtení. Propojení prostředků odpovídající položce řádku objednávky.                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |Podrobnosti o době trvání období obnovení                                                                           |
| AttestationAccepted             | bool                 | Označuje smlouvu pro podmínky nabídky nebo SKU. Vyžaduje se jenom pro nabídky nebo SKU, kde SkuAttestationProperties nebo OfferAttestationProperties enforceAttestation má hodnotu True.                                                                            |

## <a name="renewsto"></a>RenewsTo

Představuje podrobnosti o době trvání období prodloužení.

| Vlastnost              | Typ             | Vyžadováno        | Popis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | řetězec           | No              | Reprezentace doby trvání období prodloužení podle ISO 8601. Aktuální podporované hodnoty jsou **P1M (1** měsíc) a **P1Y** (1 rok). |

## <a name="orderlinks"></a>OrderLinks

Představuje propojení prostředků odpovídající objednávce.

| Vlastnost           | Typ                                         | Description                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| stav zřizování | [Odkaz](utility-resources.md#link)            | Po naplnění se zobrazí odkaz na načtení stavu zřizování pro objednávku.       |
| Vlastní               | [Odkaz](utility-resources.md#link)            | Odkaz pro načtení prostředku objednávky.                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

Představuje úplné předplatné přidružené k objednávce.

| Vlastnost           | Typ                                         | Description                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| stav zřizování | [Odkaz](utility-resources.md#link)            | Po naplnění se zobrazí odkaz pro načtení [stavu zřizování](#orderlineitemprovisioningstatus) řádkové položky.       |
| Sku                | [Odkaz](utility-resources.md#link)            | Odkaz na načtení informací o SKU zakoupené položky katalogu                    |
| předplatné       | [Odkaz](utility-resources.md#link)            | Po vyplnění se zobrazí odkaz na úplné informace o předplatném.                       |
| aktivační odkazy    | [Odkaz](utility-resources.md#link)            | Po naplnění prostředku GET pro odkazy aktivujte předplatné.             |

## <a name="orderstatus"></a>Stav objednávky

[Enum/dotnet/api/system.enum) s hodnotami, které označují stav objednávky.

| Hodnota              | Pozice     | Description                                     |
|--------------------|--------------|-------------------------------------------------|
| Neznámý            | 0            | Inicializátor výčtu.                               |
| Dokončena          | 1            | Označuje, že se objednávka dokončila.          |
| pending            | 2            | Označuje, že objednávka stále čeká na vyřízení.      |
| Zrušena          | 3            | Označuje, že objednávka byla zrušena.    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

Představuje stav zřizování [OrderLineItem](#orderlineitem).

| Vlastnost                        | Typ                                | Description                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber                  | int                                 | Jedinečné číslo řádku položky řádku objednávky. Hodnoty jsou v rozsahu od 0 do count-1.             |
| status                          | řetězec                              | Stav zřizování řádkové položky objednávky. Mezi tyto hodnoty patří:</br>**Splněno:** Plnění objednávky se úspěšně dokončilo a uživatel bude moct využívat rezervace.</br>**Nevyplněné:** Nesplněn kvůli zrušení</br>**PrefulfillmentPending:** Vaše žádost se stále zpracovává, plnění ještě není dokončené |
| quantityProvisioningInformation | Seznam<[QuantityProvisioningStatus](#quantityprovisioningstatus)> | Seznam informací o stavu zřizování množství pro položku řádku objednávky. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

Představuje stav zřizování podle množství.

| Vlastnost                           | Typ                                         | Description                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | int                                          | Počet položek                                 |
| status                             | řetězec                                       | Stav počtu položek                   |
