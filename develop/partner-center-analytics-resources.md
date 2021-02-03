---
title: Analýzy partnerského centra
description: Dokumentace k veřejnému rozhraní API služby partner Center Analytics
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4b14ee929f3020079f409be8817e077673d3219f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766700"
---
# <a name="partner-center-analytics---resources"></a>Analýzy Partnerského centra – prostředky

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Rozhraní API pro analýzu umožňuje programově přistupovat k datům, která se zobrazují v uživatelském prostředí.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tyto scénáře podporují ověřování pouze pomocí přihlašovacích údajů uživatele.

## <a name="csp-program-azure-usage-analytics"></a>CSP program: Analýza využití Azure

V následujícím scénáři se dozvíte, jak pomocí rozhraní API pro analýzu načíst informace o analýze využití Azure v partnerském centru.

- [Získání všech analytických informací o využití Azure](get-all-azure-usage-analytics.md)

Tento scénář vrátí vaše analytické informace v kolekci prostředků [využití Azure](#azure-usage-resource) .

## <a name="azure-usage-resource"></a>Prostředek využití Azure

Představuje všechna analytická data pro využití Azure.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| CustomerTenantId | řetězec | Identifikátor tenanta zákazníka |
| customerName | řetězec | Jméno zákazníka. |
| subscriptionId | řetězec | Identifikátor předplatného. |
| subscriptionName | řetězec | Název předplatného. |
| usageDate | řetězec | Datum využití |
| resourceLocation | řetězec | Umístění datového centra, západní Evropa, například. |
| meterCategory | řetězec | Kategorie měřiče, například Správa dat |
| meterSubcategory | řetězec | Podkategorie měřiče, například geograficky redundantní. |
| meterUnit | řetězec | Jednotka měření, například gigabajty nebo hodiny. |
| reservationOrderId | řetězec | Pořadí rezervace rezervované instance virtuálního počítače Azure. |
| reservationId | řetězec | Rezervované instance v rámci konkrétní objednávky vyhrazené instance. |
| serviceType | řetězec | Označuje typ virtuálního počítače. Například Standard_E4s_v3. |
| quantity | long | Označuje čísla použitá v jednotce měřičů. |

## <a name="csp-program-indirect-resellers-analytics"></a>Program CSP: analýzy nepřímých prodejců

V následujícím scénáři se dozvíte, jak pomocí rozhraní API pro analýzu načíst všechny informace o analýze nepřímých prodejců v partnerském centru.

- [Získání všech analytických informací o nepřímých prodejcích](get-all-indirect-resellers-analytics.md)

Tento scénář vrátí vaše analytické informace v kolekci [nepřímých prodejců](#indirect-resellers-resource) prostředků.

## <a name="indirect-resellers-resource"></a>Prostředky nepřímých prodejců

Představuje všechna analytická data pro nepřímé prodejce.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| partnerTenantId | řetězec | ID tenanta partnera, pro který chcete načíst data nepřímých prodejců. |
| id | řetězec | ID nepřímého prodejce |
| name | řetězec | Název partnera, pro který chcete načíst data nepřímých prodejců. |
| uvádět | řetězec | Trh partnera, pro který chcete načíst data nepřímých prodejců. |
| firstSubscriptionCreationDate | řetězec ve formátu data a času UTC | Datum vytvoření prvního předplatného, na základě kterého chcete načíst data nepřímých prodejců. |
| latestSubscriptionCreationDate | řetězec ve formátu data a času UTC | Datum vytvoření posledního předplatného. |
| firstSubscriptionEndDate | řetězec ve formátu data a času UTC | První ukončení předplatného. |
| latestSubscriptionEndDate | řetězec ve formátu data a času UTC | Poslední datum, kdy bylo ukončeno nějaké předplatné. |
| firstSubscriptionSuspendedDate | řetězec ve formátu data a času UTC | Při prvním pozastavení předplatného. |
| latestSubscriptionSuspendedDate | řetězec ve formátu data a času UTC | Poslední datum, kdy se nějaké předplatné pozastavilo. |
| firstSubscriptionDeprovisionedDate | řetězec ve formátu data a času UTC | Při prvním zrušení zřízení předplatného. |
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
|     subscriptionType      |             řetězec             |       Typ předplatného. **Poznámka**: Toto pole rozlišuje velká a malá písmena. Podporované hodnoty jsou: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".       |
|     autoRenewEnabled      |            boolean             |                                         Hodnota, která označuje, jestli se předplatné obnovuje automaticky.                                          |
|         partnerId         |             řetězec             | ID MPN U přímého prodejce bude tento parametr ID MPN partnera. Pro nepřímý prodejce tento parametr bude ID MPN nepřímého prodejce. |
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
|      lastRenewalDate      | řetězec ve formátu data a času UTC |                                       Datum, kdy bylo předplatné naposledy obnoveno, má výchozí hodnotu null.                                       |
|       licenseCount        |             číslo             |                                                             Celkový počet licencí.                                                              |
|     subscriptionCount     |             číslo             |                        Počet předplatných. Poznámka: Tato hodnota se zobrazí pouze v odpovědi agregačního dotazu.                         |

## <a name="search-analytics"></a>Vyhledávání analýz

> [!NOTE]
> Pro získání analýzy vyhledávání není nutné členství v programu CSP.

V následujícím scénáři se dozvíte, jak pomocí rozhraní Analytics API načíst všechny informace o analýze vyhledávání v partnerském centru.

- [Získání všech analytických informací o hledání](get-all-search-analytics.md)

Tento scénář vrátí vaše analytické informace v kolekci prostředků [vyhledávání](#search-resource) .

## <a name="search-resource"></a>Hledat prostředek

Představuje všechna analytická data pro hledání.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| Společnosti | řetězec | Název fakturační společnosti |
| contactButtonClicked | Logická hodnota | Indikuje, jestli se kliklo na tlačítko kontaktu. |
| keywordCountry | řetězec | Země zadaná ve vyhledávání |
| detailsView | Logická hodnota | Indikuje, jestli se zobrazily podrobnosti hledání. |
| keywordIndustryFocus | řetězec | Obor, ve kterém se má hledat například zdravotnictví. |
| mpnId | řetězec | ID Microsoft Partner Network (MPN). U přímého prodejce bude tento parametr ID MPN partnera. Pro nepřímý prodejce tento parametr bude ID MPN nepřímého prodejce. |
| partnerMarket | řetězec | Národní prostředí, ve kterém se partneři obchodují. |
| keywordProduct | řetězec | Produkt určený ve vyhledávání |
| referralSubmitted | Logická hodnota | Určuje, zda byl odeslán odkaz. |
| searchDate | řetězec ve formátu data a času UTC | Datum, kdy došlo k vyhledávacímu dotazu. |
| keywordSearchText | řetězec | Text zadaný ve vyhledávání |
| searchResultPageViews | long | Počet pokusů, kolikrát byl partner ve výsledku hledání. Část odpovědi pouze pro agregaci.
| contactClicks | long | Počet kliknutí na tlačítko kontaktu Část odpovědi pouze pro agregaci.
| referralCount | long | Počet odkazů generovaných z hledání. Část odpovědi pouze pro agregaci.
| profileViews | long | Počet, kolikrát byl partnerský profil zobrazen. Část odpovědi pouze pro agregaci.

## <a name="referrals-analytics"></a>Analýzy odkazů

> [!NOTE]
> Pro získání analýz odkazů není nutné členství v programu CSP.

V následujícím scénáři se dozvíte, jak pomocí rozhraní API pro analýzu načíst informace o analýze odkazů v partnerském centru.

- [Získání všech analytických informací o referencích](get-all-referrals-analytics.md)

Tento scénář vrátí vaše analytické informace v kolekci prostředků [odkazů](#referrals-resource) .

> [!NOTE]
> Analýzy referencí nejsou k dispozici partnerskému centru provozovanému společností 21Vianet.

## <a name="referrals-resource"></a>Prostředek odkazů

Představuje všechna analytická data pro odkaz.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| id | řetězec | Identifikátor tenanta zákazníka  |
| status | řetězec | Určuje, zda odkaz vedl na zákazníka.  |
| customerMarket | řetězec | Země nebo oblast, ve které má zákazník obchodní oddělení |
| customerName | řetězec | Jméno zákazníka. |
| customerOrgSize | řetězec | Rozsah udávající počet zaměstnanců v organizaci zákazníka. Například "10to50employees". |
| acceptedDate | řetězec ve formátu data a času UTC | Datum, kdy byl odkaz přijat. |
| acknowledgedDate | řetězec ve formátu data a času UTC | Datum, kdy byl odkaz potvrzen. |
| archivedDate | řetězec ve formátu data a času UTC | Datum, kdy byl odkaz archivován. |
| declinedDate | řetězec ve formátu data a času UTC | Datum, kdy byl odkaz odmítnut. |
| expiredDate | řetězec ve formátu data a času UTC | Datum, kdy platnost odkazu vypršela. |
| lostDate | řetězec ve formátu data a času UTC | Datum, kdy byl odkaz ztracen. |
| missedDate | řetězec ve formátu data a času UTC | Datum, kdy byl odkaz vynechán. |
| createdDate | řetězec ve formátu data a času UTC | Datum vytvoření odkazu. |
| skippedDate | řetězec ve formátu data a času UTC | Datum, kdy byl odkaz přeskočen. |
| wonDate | řetězec ve formátu data a času UTC | Datum, kdy byl odkaz získán. |
| partnerMarket | řetězec |  Země nebo oblast, ve které má partner firmy. |
