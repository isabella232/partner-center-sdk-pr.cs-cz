---
title: Analýzy partnerského centra
description: Partnerské centrum k veřejnému rozhraní API služby Partnerské centrum Analytics.
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 03d7d252a415524c6573c1bf62b8b9c1518a1b9f
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548086"
---
# <a name="partner-center-analytics---resources"></a>Analýzy Partnerského centra – prostředky

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Analytické rozhraní API umožňuje programově přistupovat k datům, která se prezentuje v uživatelském prostředí.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tyto scénáře podporují ověřování pouze pomocí přihlašovacích údajů uživatele.

## <a name="csp-program-azure-usage-analytics"></a>Program CSP: Analýza využití Azure

Následující scénář ukazuje, jak pomocí rozhraní API pro analýzu načíst všechny informace o Partnerské centrum azure pro analýzu využití.

- [Získání všech analytických informací o využití Azure](get-all-azure-usage-analytics.md)

Tento scénář vrátí analytické informace v kolekci prostředků [využití](#azure-usage-resource) Azure.

## <a name="azure-usage-resource"></a>Prostředek využití Azure

Představuje všechna analytická data pro využití Azure.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| CustomerTenantId | řetězec | Identifikátor tenanta zákazníka. |
| customerName | řetězec | Jméno zákazníka. |
| subscriptionId | řetězec | Identifikátor předplatného. |
| subscriptionName | řetězec | Název předplatného. |
| usageDate | řetězec | Datum použití |
| resourceLocation | řetězec | Například umístění datového centra západní Evropa. |
| meterCategory | řetězec | Například kategorie měřiče, správa dat. |
| meterSubcategory | řetězec | Podkategorie měřiče, například geograficky redundantní. |
| meterUnit | řetězec | Jednotka měřiče, například gigabajty nebo hodiny. |
| reservationOrderId | řetězec | Objednávka rezervace rezervované instance virtuálního počítače Azure |
| reservationId | řetězec | Rezervované instance v rámci konkrétní objednávky rezervovaných instancí. |
| Servicetype | řetězec | Určuje typ virtuálního počítače. Příklad: Standard_E4s_v3. |
| quantity | long | Označuje čísla použitá v jednotce měřiče. |

## <a name="csp-program-indirect-resellers-analytics"></a>Program CSP: Analýza nepřímých prodejců

Následující scénář ukazuje, jak pomocí rozhraní Api pro analýzu načíst všechny analytické informace Partnerské centrum nepřímých prodejců.

- [Získání všech analytických informací o nepřímých prodejcích](get-all-indirect-resellers-analytics.md)

Tento scénář vrátí analytické informace v kolekci prostředků [nepřímých prodejců.](#indirect-resellers-resource)

## <a name="indirect-resellers-resource"></a>Prostředek nepřímých prodejců

Představuje všechna analytická data pro nepřímé prodejce.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| partnerTenantId | řetězec | ID tenanta partnera, pro kterého chcete načíst data nepřímých prodejců. |
| id | řetězec | ID nepřímého prodejce. |
| name | řetězec | Název partnera, pro kterého chcete načíst data nepřímých prodejců. |
| Trhu | řetězec | Trh partnera, pro kterého chcete načíst data nepřímých prodejců. |
| firstSubscriptionCreationDate | řetězec ve formátu data a času UTC | Datum vytvoření prvního předplatného, na základě kterého chcete načíst data nepřímých prodejců. |
| latestSubscriptionCreationDate | řetězec ve formátu data a času UTC | Datum vytvoření nejnovějšího předplatného. |
| firstSubscriptionEndDate | řetězec ve formátu data a času UTC | Při prvním ukončení předplatného. |
| latestSubscriptionEndDate | řetězec ve formátu data a času UTC | Nejnovější datum ukončení libovolného předplatného |
| firstSubscriptionSuspendedDate | řetězec ve formátu data a času UTC | Při prvním pozastavení libovolného předplatného. |
| latestSubscriptionSuspendedDate | řetězec ve formátu data a času UTC | Nejnovější datum pozastavení libovolného předplatného |
| firstSubscriptionDeprovisionedDate | řetězec ve formátu data a času UTC | Při prvním rušení zřízení libovolného předplatného. |
| latestSubscriptionDeprovisionedDate | řetězec ve formátu data a času UTC | Poslední datum, kdy bylo zrušeno zřízení nějakého předplatného. |
| subscriptionCount | double | Počet předplatných pro všechny přidané hodnoty pro prodejce |
| licenseCount | double | Počet licencí pro všechny přidané hodnoty pro prodejce |
| indirectResellerCount | double | Počet nepřímých prodejců |

## <a name="csp-program-subscription-analytics"></a>Program CSP: analýza předplatných

V následujících scénářích se dozvíte, jak pomocí rozhraní API Analytics načíst všechny informace o analýze předplatného partnerského centra, filtrovat je pomocí vyhledávacího dotazu nebo je seskupit podle kalendářních dat nebo termínů.

- [Získání všech analytických informací o předplatných](get-all-subscription-analytics.md)
- [Získání analytických informací o předplatných filtrovaných podle vyhledávacího dotazu](get-subscription-analytics-by-search-query.md)
- [Získání analytických informací o předplatných seskupených podle dat nebo podmínek](get-subscription-analytics-grouped-by-dates-or-terms.md)

Všechny tyto scénáře vrátí vaše analytické informace v kolekci prostředků [předplatného](#subscription-resource) .

## <a name="subscription-resource"></a>Prostředek odběru

Představuje všechna analytická data pro předplatné.

|         Vlastnost          |              Typ              |                                                                      Description                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     customerTenantId      |             řetězec             |                                              Řetězec ve formátu GUID, který identifikuje tenanta zákazníka.                                              |
|       customerName        |             řetězec             |                                                               Jméno zákazníka.                                                                |
|      customerMarket       |             řetězec             |                                                 Země nebo oblast, ve které má zákazník obchodní oddělení                                                 |
|            id             |             řetězec             |                                                              Identifikátor předplatného.                                                              |
|          status           |             řetězec             |                                          Stav předplatného: "aktivní", "pozastaveno" nebo "zrušeno zřízení".                                           |
|        NázevVýrobku        |             řetězec             |                                                                Název produktu.                                                                |
|     subscriptionType      |             řetězec             |       Typ předplatného. **Poznámka**: Toto pole rozlišuje velká a malá písmena. podporované hodnoty jsou: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".       |
|     autoRenewEnabled      |            boolean             |                                         Hodnota, která označuje, jestli se předplatné obnovuje automaticky.                                          |
|         partnerId         |             řetězec             | ID Microsoft Partner Network (MPN). U přímého prodejce bude tento parametr ID MPN partnera. Pro nepřímý prodejce tento parametr bude ID MPN nepřímého prodejce. |
|       friendlyName        |             řetězec             |                                                             Název předplatného.                                                              |
|        partnerName        |             řetězec             |                                              Název partnera, pro kterého se předplatné zakoupilo                                               |
|       providerName        |             řetězec             |            Pokud je transakce předplatného určena pro nepřímý prodejce, jméno poskytovatele je nepřímým poskytovatelem, který si zakoupil předplatné.             |
|    effectiveStartDate     | řetězec ve formátu data a času UTC |                                                           Datum, kdy se předplatné spustí.                                                            |
|     commitmentEndDate     | řetězec ve formátu data a času UTC |                                                            Datum ukončení předplatného                                                             |
|    currentStateEndDate    | řetězec ve formátu data a času UTC |                                           Datum, kdy se změní aktuální stav předplatného.                                            |
| trialToPaidConversionDate | řetězec ve formátu data a času UTC |                                 Datum, kdy se předplatné převede ze zkušební verze na placené. Výchozí hodnotou je hodnota null.                                 |
|      trialStartDate       | řetězec ve formátu data a času UTC |                                Datum, kdy se začalo zkušební období předplatného. Výchozí hodnotou je hodnota null.                                 |
|       trialEndDate        | řetězec ve formátu data a času UTC |                                  Datum, kdy se ukončí zkušební období předplatného. Výchozí hodnotou je hodnota null.                                  |
|       lastUsageDate       | řetězec ve formátu data a času UTC |                                        Datum posledního použití předplatného Výchozí hodnotou je hodnota null.                                        |
|     deprovisionedDate     | řetězec ve formátu data a času UTC |                                      Datum zrušení zřízení předplatného. Výchozí hodnotou je hodnota null.                                      |
|      lastRenewalDate      | řetězec ve formátu data a času UTC |                                       Datum poslední obnovy odběru Výchozí hodnotou je hodnota null.                                       |
|       licenseCount        |             číslo             |                                                             Celkový počet licencí.                                                              |
|     subscriptionCount     |             číslo             |                        Počet předplatných Poznámka: Tato hodnota se zobrazí pouze v odpovědi agregačního dotazu.                         |

## <a name="search-analytics"></a>Analýza vyhledávání

> [!NOTE]
> K získání analýzy vyhledávání se členství v programu CSP nevyžaduje.

Následující scénář ukazuje, jak pomocí rozhraní API pro analýzu načíst všechny analytické informace Partnerské centrum vyhledávání.

- [Získání všech analytických informací o hledání](get-all-search-analytics.md)

Tento scénář vrátí analytické informace v kolekci prostředků [služby Search.](#search-resource)

## <a name="search-resource"></a>Hledání prostředku

Představuje všechna analytická data pro vyhledávání.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| Companyname | řetězec | Název fakturační společnosti. |
| contactButtonClicked | Logická hodnota | Označuje, jestli se klikli na tlačítko kontaktu. |
| keywordCountry | řetězec | Země zadaná při hledání. |
| detailsViewed (Zobrazení podrobností) | Logická hodnota | Určuje, jestli se prohlížely podrobnosti hledání. |
| keywordIndustryFocus | řetězec | Obor, ve které se má vyhledávat, například zdravotnictví. |
| ID mpn | řetězec | ID Microsoft Partner Network (MPN). Pro přímého prodejce bude tento parametr ID MPN partnera. Pro nepřímého prodejce bude tento parametr ID MPN nepřímého prodejce. |
| partnerMarket | řetězec | Národní prostředí, ve kterém partner podniká. |
| keywordProduct | řetězec | Produkt zadaný při hledání. |
| referenční_odkazSubmitted | Logická hodnota | Určuje, jestli se odeslal referenční seznam. |
| datum hledání | řetězec ve formátu data a času UTC | Datum, kdy došlo k vyhledávacímu dotazu |
| keywordSearchText | řetězec | Text zadaný při hledání. |
| searchResultPageViews | long | Počet, kolikrát partner ve výsledku hledání objevil. Část odpovědi pouze pro agregaci.
| kontaktní kliknutí | long | Počet kliknutí na tlačítko kontaktu Část odpovědi pouze pro agregaci.
| referenční_počet | long | Počet referenčních odkazů vygenerované při hledání Část odpovědi pouze pro agregaci.
| zobrazení profilu | long | Počet zobrazení partnerského profilu Část odpovědi pouze pro agregaci.

## <a name="referrals-analytics"></a>Analýzy referenčních odkazů

> [!NOTE]
> K získání analýzy referenčních doporučení se členství v programu CSP nevyžaduje.

Následující scénář ukazuje, jak pomocí rozhraní Api pro analýzu načíst všechny analytické informace Partnerské centrum referenčních seznamech.

- [Získání všech analytických informací o referencích](get-all-referrals-analytics.md)

Tento scénář vrátí analytické informace v kolekci prostředků [referenčních](#referrals-resource) seznamů.

> [!NOTE]
> Analýzy referenčních doporučení nejsou k dispozici pro Partnerské centrum provozované společností 21Vianet.

## <a name="referrals-resource"></a>Prostředek referenčních odkazů

Představuje všechna analytická data referenčního seznamu.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| id | řetězec | Identifikátor tenanta zákazníka.  |
| status | řetězec | Určuje, jestli referenční seznam vedl k zákazníkovi.  |
| customerMarket | řetězec | Země nebo oblast, ve které zákazník obchoduje. |
| customerName | řetězec | Jméno zákazníka. |
| customerOrgSize | řetězec | Rozsah označující počet zaměstnanců v organizaci zákazníka. Například "10to50employees". |
| acceptedDate (datum přijetí) | řetězec ve formátu data a času UTC | Datum přijetí referenčního odkazu |
| datum potvrzení | řetězec ve formátu data a času UTC | Datum potvrzení referenčního odkazu. |
| archivedDate | řetězec ve formátu data a času UTC | Datum archivace referenčního odkazu. |
| declinedDate | řetězec ve formátu data a času UTC | Datum, kdy byl odkaz odmítnut. |
| expiredDate | řetězec ve formátu data a času UTC | Datum, kdy platnost odkazu vypršela. |
| lostDate | řetězec ve formátu data a času UTC | Datum, kdy byl odkaz ztracen. |
| missedDate | řetězec ve formátu data a času UTC | Datum, kdy byl odkaz vynechán. |
| createdDate | řetězec ve formátu data a času UTC | Datum vytvoření odkazu. |
| skippedDate | řetězec ve formátu data a času UTC | Datum, kdy byl odkaz přeskočen. |
| wonDate | řetězec ve formátu data a času UTC | Datum, kdy byl odkaz získán. |
| partnerMarket | řetězec |  Země nebo oblast, ve které má partner firmy. |
