---
title: Materiály k košíku
description: Partner umístí objednávku do košíku, když zákazník chce koupit předplatné ze seznamu nabídek.
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c9372bb982528127f8870094e26465d004b1f05c75140f0ac729375f5d5f3302
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992173"
---
# <a name="cart-resources"></a>Materiály k košíku

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Partner objednává, když zákazník chce koupit předplatné ze seznamu nabídek.

## <a name="cart"></a>Košík

Popisuje košík.

| Vlastnost              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | řetězec           | Identifikátor košíku, který se dodá po úspěšném vytvoření košíku.                               |
| creationTimeStamp     | DateTime         | Datum vytvoření košíku ve formátu data a času. Použije se při úspěšném vytvoření košíku.      |
| lastModifiedTimeStamp | DateTime         | Datum poslední aktualizace košíku ve formátu data a času Použije se při úspěšném vytvoření košíku. |
| expirationTimeStamp   | DateTime         | Datum, kdy vyprší platnost košíku ve formátu data a času. Použije se při úspěšném vytvoření košíku.          |
| lastModifiedUser      | řetězec           | Uživatel, který naposledy aktualizoval košík Použije se při úspěšném vytvoření košíku.                          |
| položky řádku             | Pole objektů | Pole prostředků [CartLineItem](#cartlineitem)                                                   |
| status                | řetězec           | Stav košíku Možné hodnoty jsou Aktivní (je možné je aktualizovat nebo odeslat) a "Seřazeno" (již bylo odesláno). |

## <a name="cartlineitem"></a>CartLineItem

Představuje jednu položku obsaženou v košíku.

| Vlastnost             | Typ                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | řetězec                           | Jedinečný identifikátor řádkové položky košíku. Použije se při úspěšném vytvoření košíku.                                                                   |
| catalogItemId        | řetězec                           | Identifikátor položky katalogu.                                                                                                                          |
| Friendlyname         | řetězec                           | Nepovinný parametr. Popisný název položky definované partnerem, který pomáhá jednoznačně rozpoznat.                                                                 |
| quantity             | int                              | Počet licencí nebo instancí                                                                                                                  |
| currencyCode         | řetězec                           | Kód měny                                                                                                                                    |
| billingCycle         | Objekt                           | Typ fakturačního cyklu nastavený pro aktuální období                                                                                                 |
| termDuration         | řetězec                           | Reprezentace doby trvání období podle STANDARDu ISO 8601. Aktuální podporované hodnoty jsou P1M (1 měsíc), P1Y (1 rok) a P3Y (3 roky).                                |
| Účastníci         | Seznam párů řetězců objektů      | Kolekce PartnerId on Record (MPN ID) při nákupu.                                                                                          |
| provisioningContext  | Slovníkový<řetězec, řetězec>       | Další kontext použitý při zřizování zakoupené položky Pokud chcete zjistit, které hodnoty jsou pro konkrétní položku potřeba, podívejte se na vlastnost provisioningVariables dané SKU. |
| orderGroup           | řetězec                           | Skupina, která označuje, které položky lze odeslat společně ve stejném pořadí.                                                                          |
| addonItems           | Seznam objektů **CartLineItem** | Kolekce řádkové položky košíku pro doplňky. Tyto položky se zakoupí do základního předplatného, které je výsledkem nákupu řádkové položky kořenového košíku. |
| error                | Objekt                           | Použije se po vytvoření košíku, pokud dojde k chybě.                                                                                                    |
| renewsTo             | Pole objektů                 | Pole prostředků [RenewsTo.](#renewsto)                                                                            |
| AttestationAccepted             | bool                 | Označuje smlouvu pro podmínky nabídky nebo SKU. Vyžaduje se jenom pro nabídky nebo SKU, kde SkuAttestationProperties nebo OfferAttestationProperties enforceAttestation má hodnotu True.                                                                            |

## <a name="renewsto"></a>RenewsTo

Představuje jednu položku obsaženou v řádkové položce košíku.

| Vlastnost              | Typ             | Vyžadováno        | Popis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | řetězec           | No              | Reprezentace doby trvání období prodloužení podle ISO 8601. Aktuální podporované hodnoty jsou **P1M (1** měsíc) a **P1Y** (1 rok). |

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)

## <a name="carterror"></a>CartError

Představuje chybu, ke které dochází po vytvoření košíku.

| Vlastnost         | Typ                                   | Description                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| Errorcode        | [CareErrorCode](#carterrorcode) | Typ chyby košíku                                                                       |
| Popis chyby | řetězec                                 | Popis chyby, včetně všech poznámek k podporovaným hodnotám, výchozím hodnotám nebo omezením |


## <a name="carterrorcode"></a>CartErrorCode

Typy chyb košíku

| Name                             | ErrorCode   | Description
|----------------------------------|-------------|-----------------------------------------------------------------------------------------------|
| CurrencyIsNotSupported           | 10000   | Měna se pro daný trh nepodporuje.  |
| CatalogItemIdIsNotValid          | 10001   | ID položky katalogu není platné.  |
| QuotaNotAvailable                | 10002   | Není k dispozici dostatek kvóty  |
| InventoryNotAvailable            | 10003   | Pro vybranou nabídku není k dispozici inventář  |
| ÚčastníciIsNotSupportedForPartner  | 10004   | Nastavení účastníků se pro partnery nepodporuje  |
| UnableToProcessCartLineItem      | 10006   | Řádeková položka košíku se nepodařilo zpracovat.  |
| PředplatnéIsNotValid           | 10007   | Předplatné není platné.  |
| PředplatnéIsNotEnabledForRI    | 10008   | Pro nákup RI není povolené předplatné.  |
| SandboxLimitExceeded             | 10009   | Limit sandboxu byl překročen.  |
| Neplatný vstup                     | 10010   | Obecný vstup není platný.  |
| Předplatné není zaregistrováno        | 10011   | Předplatné není platné.  |
| AttestationNotAccepted           | 10012   | Ověření se nepřijalo.  |
| Neznámý                          | 0   | Výchozí hodnota   |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

Představuje výsledek pokladny košíku.

| Vlastnost    | Typ                                              | Description                     |
|-------------|---------------------------------------------------|---------------------------------|
| orders      | Seznam objektů [Order](order-resources.md#order)         | Kolekce objednávek.       |
| orderErrors | Seznam objektů [OrderError](#ordererror) | Kolekce chyb objednávek. |

## <a name="ordererror"></a>OrderError

Představuje chybu, ke které dochází při pokladně košíku při vytvoření objednávky.

| Vlastnost     | Typ   | Description                                     |
|--------------|--------|-------------------------------------------------|
| ID skupiny objednávek | řetězec | ID skupiny objednávek objednávky s chybou. |
| kód         | int    | Kód chyby                                 |
| description  | řetězec | Popis chyby.                   |
