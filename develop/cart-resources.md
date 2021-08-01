---
title: Prostředky košíku
description: Když si zákazník chce koupit předplatné ze seznamu nabídek, zařadí objednávku do košíku.
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ebe6e628d5bb3b66186d5c4f428f69e46415892b
ms.sourcegitcommit: 59950cf131440786779c8926be518c2dc4bc4030
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/31/2021
ms.locfileid: "115009135"
---
# <a name="cart-resources"></a>Prostředky košíku

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Partner umístí objednávku, když chce zákazník koupit předplatné ze seznamu nabídek.

## <a name="cart"></a>Košík

Popisuje košík.

| Vlastnost              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | řetězec           | Identifikátor košíku, který se zadal po úspěšném vytvoření košíku.                               |
| creationTimeStamp     | DateTime         | Datum, kdy byl košík vytvořen, ve formátu data a času. Použito po úspěšném vytvoření košíku.      |
| lastModifiedTimeStamp | DateTime         | Datum poslední aktualizace košíku ve formátu data a času. Použito po úspěšném vytvoření košíku. |
| expirationTimeStamp   | DateTime         | Datum, kdy vyprší platnost košíku, ve formátu data a času. Použito po úspěšném vytvoření košíku.          |
| lastModifiedUser      | řetězec           | Uživatel, který kartu naposledy aktualizoval. Použito po úspěšném vytvoření košíku.                          |
| Položky řádku             | Pole objektů | Pole prostředků [CartLineItem](#cartlineitem)                                                   |
| status                | řetězec           | Stav košíku. Možné hodnoty jsou "aktivní" (může být aktualizováno/odesláno) a "seřazené" (již bylo odesláno). |

## <a name="cartlineitem"></a>CartLineItem

Představuje jednu položku obsaženou v košíku.

| Vlastnost             | Typ                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | řetězec                           | Jedinečný identifikátor položky řádku košíku Použito po úspěšném vytvoření košíku.                                                                   |
| catalogItemId        | řetězec                           | Identifikátor položky katalogu                                                                                                                          |
| friendlyName         | řetězec                           | Nepovinný parametr. Popisný název položky definované partnerem, který vám umožní určit nejednoznačnost.                                                                 |
| quantity             | int                              | Počet licencí nebo instancí.                                                                                                                  |
| currencyCode         | řetězec                           | Kód měny.                                                                                                                                    |
| billingCycle         | Objekt                           | Typ fakturačního cyklu nastaveného pro aktuální období.                                                                                                 |
| termDuration         | řetězec                           | ISO 8601 reprezentace doby trvání období. Aktuální podporované hodnoty jsou P1M (1 měsíc), P1Y (1 rok) a P3Y (3 roky).                                |
| členům         | Seznam párů řetězců objektů      | Kolekce PartnerId na záznamu (MPN ID) na nákupu.                                                                                          |
| provisioningContext  | Řetězec<slovníku, řetězec>       | Další kontext, který se používá při zřizování koupené položky Chcete-li zjistit, které hodnoty jsou nutné pro konkrétní položku, přečtěte si vlastnost provisioningVariables skladové položky. |
| pořadí           | řetězec                           | Skupina, která označuje, které položky lze odeslat společně ve stejném pořadí.                                                                          |
| addonItems           | Seznam objektů **CartLineItem** | Kolekce položek řádků košíku pro Doplňky Tyto položky se zakoupí do základního předplatného, které je výsledkem nákupu položky řádku kořenového košíku. |
| error                | Objekt                           | Používá se po vytvoření košíku, pokud došlo k chybě.                                                                                                    |
| renewsTo             | Pole objektů                 | Pole prostředků [RenewsTo](#renewsto)                                                                            |
| AttestationAccepted             | bool                 | Označuje smlouvu o nabídkách nebo podmínkách SKU. Vyžaduje se jenom pro nabídky nebo skladové položky, kde SkuAttestationProperties nebo OfferAttestationProperties enforceAttestation má hodnotu true.                                                                            |

## <a name="renewsto"></a>RenewsTo

Představuje jednu položku obsaženou v položce řádku košíku.

| Vlastnost              | Typ             | Vyžadováno        | Popis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | řetězec           | No              | ISO 8601 představuje dobu trvání období obnovy. Aktuální podporované hodnoty jsou **P1M** (1 měsíc) a **P1Y** (1 rok). |

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

## <a name="carterror"></a>CartError

Představuje chybu, která nastane po vytvoření košíku.

| Vlastnost         | Typ                                   | Description                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [CareErrorCode](#carterrorcode) | Typ chyby košíku                                                                       |
| errorDescription | řetězec                                 | Popis chyby včetně všech poznámek o podporovaných hodnotách, výchozích hodnotách nebo omezeních. |


## <a name="carterrorcode"></a>CartErrorCode

Typy chyb košíku.

| Name                             | ErrorCode   | Description
|----------------------------------|-------------|-----------------------------------------------------------------------------------------------|
| CurrencyIsNotSupported           | 10000   | Měna není pro daný trh podporovaná.  |
| CatalogItemIdIsNotValid          | 10001   | ID položky katalogu je neplatné.  |
| QuotaNotAvailable                | 10002   | Není k dispozici dostatečná kvóta.  |
| InventoryNotAvailable            | 10003   | Inventář není pro vybranou nabídku k dispozici.  |
| ParticipantsIsNotSupportedForPartner  | 10004   | Nastavení účastníků není pro partnera podporováno.  |
| UnableToProcessCartLineItem      | 10006   | Nelze zpracovat položku řádku košíku.  |
| SubscriptionIsNotValid           | 10007   | Předplatné je neplatné.  |
| SubscriptionIsNotEnabledForRI    | 10008   | U předplatného není povolený nákup na rezervované instance.  |
| SandboxLimitExceeded             | 10009   | Překročil se limit izolovaného prostoru (sandbox).  |
| InvalidInput                     | 10010   | Obecný vstup není platný.  |
| SubscriptionNotRegistered        | 10011   | Předplatné je neplatné.  |
| AttestationNotAccepted           | 10012   | Ověření identity nebylo přijato.  |
| Neznámý                          | 0   | Výchozí hodnota   |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

Představuje výsledek rezervace košíku.

| Vlastnost    | Typ                                              | Description                     |
|-------------|---------------------------------------------------|---------------------------------|
| orders      | Seznam objektů [objednávky](order-resources.md#order)         | Kolekce objednávek.       |
| orderErrors | Seznam objektů [OrderError](#ordererror) | Kolekce chyb pořadí. |

## <a name="ordererror"></a>OrderError

Představuje chybu, ke které dojde během rezervace košíku při vytvoření objednávky.

| Vlastnost     | Typ   | Description                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | řetězec | ID skupiny objednávek objednávky s chybou. |
| kód         | int    | Kód chyby                                 |
| description  | řetězec | Popis chyby.                   |
