---
title: Fakturovat prostředky
description: Přes rozhraní API partnerského centra jsou k dispozici více prostředků souvisejících s fakturací. Tyto prostředky souvisejí s podrobnostmi o faktuře a položkách řádků.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd2caefe4ae18c81a31083d084f1e87da1288dd9
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766719"
---
# <a name="invoice-resources"></a>Fakturovat prostředky

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Prostřednictvím rozhraní API partnerského centra jsou k dispozici následující prostředky související s fakturací.

## <a name="invoice"></a>Faktura

| Vlastnost | Typ | Description |
| -------- | ---- | ----------- |
| id | řetězec | Identifikátor faktury |
| invoiceDate | řetězec ve formátu data a času standardu UTC | Datum, kdy byla faktura vygenerována. |
| billingPeriodStartDate | řetězec ve formátu data a času standardu UTC | Počáteční datum fakturačního období ve standardu UTC |
| billingPeriodEndDate | řetězec ve formátu data a času standardu UTC   | Koncové datum fakturačního období ve standardu UTC |
| totalCharges | číslo | Celkové poplatky. Zahrnuje poplatky za transakce a jakékoli úpravy.     |
| paidAmount | číslo  | Částka placená partnerem. Záporné, pokud byla přijata platba.  |
| currencyCode | řetězec  | Kód, který označuje měnu použitou pro všechny částky a součty položek faktury. |
| currencySymbol  | řetězec | Symbol měny použitý pro všechny částky a součty položek faktury |
| pdfDownloadLink | řetězec  | Odkaz ke stažení faktury ve formátu PDF. Tento odkaz se nevrátí jako součást výsledků hledání a naplní se jenom v případě, že se k faktuře má přistup pomocí ID. Tento odkaz automaticky vyprší za 30 minut. |
| Uzlu InvoiceDetails  | pole objektů [InvoiceDetail](#invoicedetail)  | Podrobnosti faktury  |
| změn      | pole objektů [faktury](#invoice)   | Změny této faktury.  |
| documentType    | řetězec | Typ dokumentu faktury: "dobropis", "faktura". |
| amendsOf        | řetězec | Referenční číslo dokumentu, jehož změnou je tento dokument.  |
| invoiceType     | řetězec  | Typ faktury: "periodický", "jednorázový" \_ .   |
| odkazy           | [ResourceLinks](utility-resources.md#resourcelinks)  | Odkazy na prostředky.  |
| atributy      | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.  |

## <a name="invoicedetail"></a>InvoiceDetail

Faktura obsahuje kolekci fakturovaných položek a každá položka je reprezentovaná InvoiceDetail prostředkem.

| Vlastnost            | Typ                                                           | Description                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | řetězec                                                         | Typ podrobností faktury: "none", " \_ položky řádků použití \_ ", "fakturace \_ \_ položek řádků". |
| billingProvider     | řetězec                                                         | Zprostředkovatel fakturace: "none", "Office", "Azure" nebo "Azure \_ data \_ Market".         |
| odkazy               | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky.                                                               |
| atributy          | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

Každý jednotlivý poplatek v rámci faktury je reprezentován jako InvoiceLineItem.

| Vlastnost            | Typ                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | řetězec                                                         | Typ položky řádku faktury: "none", " \_ položky řádků použití \_ ", "fakturace \_ \_ položek řádků". |
| billingProvider     | řetězec                                                         | Zprostředkovatel fakturace: "none", "Office", "Azure" nebo "Azure \_ data \_ Market".            |
| atributy          | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                                                             |

## <a name="invoicesummary"></a>InvoiceSummary

Popisuje souhrn zůstatku a celkové náklady na fakturu.

| Vlastnost                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| balanceAmount            | číslo                                                         | Zůstatek faktury Toto je celková částka neplacených faktur. |
| currencyCode             | řetězec                                                         | Kód, který označuje měnu použitou pro částku zůstatku.       |
| currencySymbol           | řetězec                                                         | Použitý symbol měny                                             |
| accountingDate           | řetězec ve formátu data a času standardu UTC                                 | Datum poslední aktualizace částky zůstatku.                         |
| firstInvoiceCreationDate | řetězec ve formátu data a času standardu UTC                                 | Datum vytvoření první faktury pro zákazníka.              |
| lastPaymentDate          | řetězec ve formátu data a času standardu UTC                                 | Datum poslední platby.                                         |
| lastPaymentAmount        | číslo                                                         | Množství poslední platby.                                       |
| latestInvoiceDate        | řetězec ve formátu data a času standardu UTC                                 | Datum vytvoření poslední faktury pro zákazníka.               |
| zobrazí                  | pole objektů [InvoiceSummaryDetail](#invoicesummarydetail) | Podrobnosti o souhrnu faktury                                           |
| odkazy                    | [ResourceLinks](utility-resources.md#resourcelinks)            | Odkazy na prostředky.                                                   |
| atributy               | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atributy metadat.                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

Představuje souhrn jednotlivých podrobností typu faktury (například opakovaný, jednorázový \_ ).

| Vlastnost            | Typ                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType         | řetězec                                                         | Typ faktury: "periodický", "jednorázový" \_ .                                       |
| shrnutí             | Objekt [InvoiceSummary](#invoicesummary)                       | Souhrn faktury za typ faktury                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

Představuje kolekci typů [InvoiceSummary](#invoicesummary) , které obsahují jednotlivé podrobnosti typu faktury na měnu.

| Vlastnost            | Typ                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | pole objektů [InvoiceSummary](#invoicesummary)             | Souhrn faktury za typ faktury na jednu měnu                            |

## <a name="licensebasedlineitem"></a>LicenseBasedLineItem

Představuje položku fakturačního řádku faktury pro předplatné založené na licencích.

| Vlastnost                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| úroveň                   | řetězec                                                         | Získá nebo nastaví celkovou částku. Celková částka = Jednotková cena * množství.  |
| atributy               | řetězec                                                         | Získá atributy.                                                  |
| billingCycleType         | řetězec                                                         | Získá nebo nastaví typ fakturačního cyklu.                                  |
| billingProvider          | řetězec                                                         | Získá poskytovatele fakturace.                                            |
| chargeEndDate            | řetězec ve formátu data a času standardu UTC                                 | Získá nebo nastaví koncové datum pro poplatek.                             |
| chargeStartDate          | řetězec ve formátu data a času standardu UTC                                 | Získá nebo nastaví počáteční datum pro poplatek.                           |
| chargeType               | řetězec                                                         | Získá nebo nastaví typ poplatků.                                      |
| currency                 | řetězec                                                         | Získá nebo nastaví měnu použitou pro tuto položku řádku.                    |
| customerId               | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor zákazníka v rámci fakturační platformy Microsoftu.  |
| customerName             | řetězec ve formátu data a času standardu UTC                                 | Získá nebo nastaví název zákazníka.                                       |
| domainName               | řetězec                                                         | Získá nebo nastaví název domény.                                             |
| durableOfferId           | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor trvalé nabídky.                     |
| invoiceLineItemType      | řetězec                                                         | Získá typ položky řádku faktury.                                   |
| mpnId                    | číslo                                                         | Získá nebo nastaví ID MPN přidružené k této položce řádku. U přímých prodejců se jedná o ID MPN prodejce. U nepřímých prodejců se jedná o ID MPN přidané hodnoty pro prodejce (VAR).                                   |
| Hodnotami OfferId                  | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor nabídky.                             |
| offerName                | řetězec                                                         | Získá nebo nastaví název nabídky.                                          |
| Seskup                  | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor objednávky.                             |
| partnerId                | řetězec                                                         | Získá nebo nastaví ID tenanta partnerského služby Azure Active Directory.            |
| quantity                 | číslo                                                         | Získá nebo nastaví počet jednotek přidružených k této položce řádku.      |
| subscriptionDescription  | řetězec                                                         | Získá nebo nastaví popis předplatného.                            |
| subscriptionEndDate      | řetězec ve formátu data a času standardu UTC                                 | Získá nebo nastaví datum vypršení platnosti předplatného.                      |
| subscriptionId           | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor předplatného.                      |
| subscriptionName         | řetězec                                                         | Získá nebo nastaví název předplatného.                                   |
| subscriptionStartDate    | řetězec ve formátu data a času standardu UTC                                 | Získá nebo nastaví datum, kdy se předplatné spustí.                   |
| Jedna                 | číslo                                                         | Získá nebo nastaví hodnotu po slevě.                               |
| syndicationPartnerSubscriptionNumber | řetězec                                             | Získá nebo nastaví číslo předplatného partnera syndikace.             |
| daňových                      | číslo                                                         | Získá nebo nastaví poplatky za daň.                                       |
| tier2MpnId               | číslo                                                         | Získá nebo nastaví ID MPN partnera vrstvy 2 přidruženého k této položce řádku. |
| totalForCustomer         | číslo                                                         | Získá nebo nastaví celkovou částku po slevě a dani.                 |
| totalOtherDiscount       | číslo                                                         | Získá nebo nastaví slevu přidruženou k tomuto nákupu.              |
| unitPrice                | číslo                                                         | Získá nebo nastaví jednotkovou cenu.                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

Představuje položku řádku fakturace faktury pro odběry založené na využití.

| Vlastnost                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| atributy               | řetězec                                                         | Získá atributy.                                                  |
| billingCycleType         | řetězec                                                         | Získá nebo nastaví typ fakturačního cyklu.                                  |
| billingProvider          | řetězec                                                         | Získá poskytovatele fakturace.                                            |
| chargeEndDate            | řetězec ve formátu data a času standardu UTC                                 | Získá nebo nastaví koncové datum pro poplatek.                             |
| chargeStartDate          | řetězec ve formátu data a času standardu UTC                                 | Získá nebo nastaví počáteční datum pro poplatek.                           |
| chargeType               | řetězec                                                         | Získá nebo nastaví typ poplatků.                                      |
| consumedQuantity         | číslo                                                         | Získá nebo nastaví celkový počet spotřebovaných jednotek.                                |
| consumptionDiscount      | řetězec                                                         | Získá nebo nastaví slevu na spotřebu.                             |
| consumptionPrice         | řetězec                                                         | Získá nebo nastaví cenu spotřebovaného množství.                          |
| currency                 | řetězec                                                         | Získá nebo nastaví měnu spojenou s cenami.                 |
| customerName             | řetězec                                                         | Získá nebo nastaví název zákazníka.                                       |
| customerId               | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor zákazníka.                          |
| detailLineItemId         | číslo                                                         | Získá nebo nastaví ID položky řádku podrobností. Jednoznačně identifikuje řádkové položky pro případy, kdy se kalkulace liší pro spotřebované jednotky. Příklad: celkové spotřebované = 1338, 1024 se účtuje s jednou sazbou, cena za 314 se účtuje s jinou sazbou.        |
| domainName               | řetězec                                                         | Získá nebo nastaví název domény.                                             |
| includedQuantity         | číslo                                                         | Získá nebo nastaví jednotky zahrnuté v objednávce.                         |
| invoiceLineItemType      | řetězec                                                         | Získá typ položky řádku faktury.                                   |
| invoiceNumber            | řetězec                                                         | Získá nebo nastaví číslo faktury.                                      |
| listPrice                | číslo                                                         | Získá nebo nastaví cenu každé jednotky.                                  |
| mpnId                    | číslo                                                         | Získá nebo nastaví ID MPN přidružené k této položce řádku. U přímých prodejců se jedná o ID MPN prodejce. U nepřímých prodejců se jedná o ID MPN přidané hodnoty pro prodejce (VAR).                                   |
| Seskup                  | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor objednávky.                             |
| overageQuantity          | číslo                                                         | Získá nebo nastaví množství spotřebované nad povoleným využitím.               |
| partnerBillableAccountId | řetězec                                                         | Získá nebo nastaví fakturační ID účtu partnera.                         |
| partnerId                | řetězec                                                         | Získá nebo nastaví ID tenanta partnerského služby Azure Active Directory.            |
| partnerName              | řetězec                                                         | Získá nebo nastaví název partnera.                                      |
| postTaxEffectiveRate     | číslo                                                         | Získá nebo nastaví platnou cenu po zdanění.                         |
| postTaxTotal             | číslo                                                         | Získá nebo nastaví celkové poplatky po dani. Poplatky za Pretax a daňové částky |
| preTaxCharges            | číslo                                                         | Získá nebo nastaví cenu účtovanou před zdaněním.                          |
| preTaxEffectiveRate      | číslo                                                         | Získá nebo nastaví platnou cenu před zdaněním.                        |
| oblast                   | řetězec                                                         | Získá nebo nastaví oblast přidruženou k instanci prostředku.        |
| resourceGuid             | řetězec                                                         | Získá nebo nastaví identifikátor prostředku.                                 |
| resourceName             | řetězec                                                         | Získá nebo nastaví název prostředku. Příklad: databáze (GB/měsíc).         |
| serviceName              | řetězec                                                         | Získá nebo nastaví název služby. Příklad: Azure Data Service.           |
| serviceType              | řetězec                                                         | Získá nebo nastaví typ služby. Příklad: Azure SQL Azure DB.           |
| skladové                      | řetězec                                                         | Získá nebo nastaví SKU služby.                                         |
| subscriptionDescription  | řetězec                                                         | Získá nebo nastaví popis předplatného.                            |
| subscriptionId           | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor předplatného.                      |
| subscriptionName         | řetězec                                                         | Získá nebo nastaví název předplatného.                                   |
| taxAmount                | číslo                                                         | Získá nebo nastaví částku daně, která se účtuje.                               |
| tier2MpnId               | číslo                                                         | Získá nebo nastaví ID MPN partnera vrstvy 2 přidruženého k této položce řádku. |
| unit                     | řetězec                                                         | Získá nebo nastaví měrnou jednotku využití Azure.                     |

## <a name="invoicestatement"></a>InvoiceStatement

Představuje operace dostupné v příkazu faktury v Application/PDF.

| Vlastnost                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | ByteArrayContent s contentType = Application/PDF.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

Představuje položku fakturačního řádku faktury pro odběry na základě licencí.

| Vlastnost | Typ | Description |
| --- | --- | --- |
| PartnerId | řetězec | Získá nebo nastaví ID partnerského tenanta. |
| CustomerId | řetězec | Získá nebo nastaví ID tenanta zákazníka. |
| CustomerName | řetězec | Získá nebo nastaví název zákazníka. |
| CustomerDomainName | řetězec | Získá nebo nastaví název domény zákazníka. |
| CustomerCountry | řetězec | Získá nebo nastaví zemi zákazníka. |
| InvoiceNumber | řetězec | Získá nebo nastaví číslo faktury. |
| MpnId | řetězec | Získá nebo nastaví ID MPN přidružené k této položce řádku. |
| ResellerMpnId | int | Získá nebo nastaví jedinečný identifikátor objednávky. |
| OrderDate | DateTime | Získá nebo nastaví datum, kdy se pořadí vytvořilo. |
| ProductId | řetězec | Získá nebo nastaví jedinečný identifikátor produktu. |
| SkuId | řetězec | Získá nebo nastaví jedinečný identifikátor SKU. |
| AvailabilityId | řetězec | Získá nebo nastaví jedinečný identifikátor dostupnosti. |
| ProductName | řetězec | Získá nebo nastaví název produktu. |
| SkuName | řetězec | Získá nebo nastaví název SKU. |
| ChargeType | řetězec | Získá nebo nastaví typ poplatků. |
| UnitPrice | decimal | Získá nebo nastaví jednotkovou cenu. |
| EffectiveUnitPrice | decimal | Získá nebo nastaví efektivní jednotkovou cenu. |
| Jednotkách UnitType | řetězec | Získá nebo nastaví typ jednotky. |
| Množství | int | Získá nebo nastaví počet jednotek přidružených k této položce řádku. |
| Mezisoučet | decimal | Získá nebo nastaví hodnotu po slevě. |
| TaxTotal | decimal | Získá nebo nastaví poplatky za daň. |
| TotalForCustomer | decimal | Získá nebo nastaví celkovou částku po slevě a dani. |
| Měna | řetězec | Získá nebo nastaví měnu použitou pro tuto položku řádku. |
| Název vydavatele | řetězec | Získá nebo nastaví název vydavatele přidruženého k tomuto nákupu. |
| PublisherId | řetězec | Získá nebo nastaví ID vydavatele přidruženého k tomuto nákupu. |
| SubscriptionDescription | řetězec | Získá nebo nastaví popis předplatného přidružený k tomuto nákupu. |
| SubscriptionId | řetězec | Získá nebo nastaví ID předplatného přidruženého k tomuto nákupu. |
| ChargeStartDate | DateTime | Získá nebo nastaví počáteční datum poplatku přidružené k tomuto nákupu. |
| ChargeEndDate | DateTime | Získá nebo nastaví datum ukončení poplatku přidružené k tomuto nákupu. |
| TermAndBillingCycle | řetězec | Získá nebo nastaví termín a fakturační cyklus spojený s tímto nákupem. |
| AlternateId | řetězec | Získá nebo nastaví alternativní ID (ID nabídky). |
| PriceAdjustmentDescription | řetězec | Získá nebo nastaví popis úpravy ceny. |
| DiscountDetails | řetězec |  **Zastaralé**. Získá nebo nastaví informace o slevě přidružené k tomuto nákupu. |
| PricingCurrency | řetězec | Získá nebo nastaví kód cenové měny. |
| PCToBCExchangeRate | decimal | Získá nebo nastaví cenovou měnu směnného kurzu pro fakturační měnu. |
| PCToBCExchangeRateDate | DateTime | Získá nebo nastaví datum směnného kurzu, kdy se stanovila cenová měna pro směnný kurz fakturačních měn. |
| BillableQuantity | decimal | Získá nebo nastaví koupené jednotky. Pro každý sloupec návrhu s názvem **BillableQuantity**. |
| MeterDescription | řetězec | Získá nebo nastaví popis měřiče pro položku řádku spotřeby. |
| ReservationOrderId | řetězec | Získá nebo nastaví identifikátor objednávky rezervace pro nákup ve službě Azure RI. |
| BillingFrequency | řetězec | Získá nebo nastaví četnost fakturace. |
| InvoiceLineItemType | InvoiceLineItemType | Vrátí typ položky řádku faktury. |
| BillingProvider | BillingProvider | Vrátí zprostředkovatele fakturace. |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

Představuje nefakturovatelné a účtované položky řádku odsouhlasení pro denní hodnocené využití.

| Vlastnost | Typ | Description |
| --- | --- | --- |
| PartnerId | řetězec | Získá nebo nastaví ID partnerského tenanta. |
| PartnerName | řetězec | Získá nebo nastaví název partnera. |
| CustomerId | řetězec | Získá nebo nastaví ID tenanta zákazníka, kterému využití patří. |
| CustomerName | řetězec | Získá nebo nastaví název společnosti zákazníka, ke které je využití patří. |
| CustomerDomainName | řetězec | Získá nebo nastaví název domény zákazníka, ke kterému patří využití. |
| InvoiceNumber | řetězec | Získá nebo nastaví ID faktury, ke které je využití patří. |
| ProductId | řetězec | Získá nebo nastaví jedinečný identifikátor produktu. |
| SkuId | řetězec | Získá nebo nastaví jedinečný identifikátor SKU. |
| AvailabilityId | řetězec | Získá nebo nastaví jedinečný identifikátor dostupnosti. |
| SkuName | řetězec | Získá nebo nastaví název SKU pro službu. |
| ProductName | řetězec | Získá nebo nastaví název produktu. |
| Název vydavatele | řetězec | Získá nebo nastaví název vydavatele. |
| PublisherId | řetězec | Získá nebo nastaví ID vydavatele. |
| SubscriptionId | řetězec | Získá nebo nastaví ID předplatného. |
| SubscriptionDescription | řetězec | Získá nebo nastaví popis předplatného. |
| ChargeStartDate | DateTime | Získá nebo nastaví počáteční datum poplatku. |
| ChargeEndDate | DateTime | Získá nebo nastaví datum ukončení pro poplatek. |
| UsageDate | DateTime | Získá nebo nastaví datum využití. |
| MeterType | řetězec | Získá nebo nastaví typ měřiče. |
| MeterCategory | řetězec | Získá nebo nastaví kategorii měřiče. |
| MeterId | řetězec | Získá nebo nastaví ID měřiče (GUID). |
| MeterSubCategory | řetězec | Získá nebo nastaví podkategorii měřiče. |
| MeterName | řetězec | Získá nebo nastaví název měřiče. |
| MeterRegion | řetězec | Získá nebo nastaví oblast měřiče. |
| UnitOfMeasure | řetězec | Získá nebo nastaví měrnou jednotku. |
| ResourceLocation | řetězec | Získá nebo nastaví umístění prostředku. |
| ConsumedService | řetězec | Získá nebo nastaví spotřebovaný název služby. |
| ResourceGroup | řetězec | Získá nebo nastaví název skupiny prostředků. |
| ResourceUri | řetězec | Získá nebo nastaví identifikátor URI instance prostředku, o které se využití týká. |
| Značky | řetězec | Získá nebo nastaví značky přidané zákazníkem. |
| AdditionalInfo | řetězec | Získá nebo nastaví metadata specifická pro službu. Například typ image u virtuálního počítače. |
| ServiceInfo1 | řetězec | Získá nebo nastaví interní metadata služby Azure. |
| ServiceInfo2 | řetězec | Získá nebo nastaví informace o službě, například typ image pro virtuální počítač a název poskytovatele internetových služeb pro ExpressRoute. |
| CustomerCountry | řetězec | Získá nebo nastaví zemi zákazníka. |
| MpnId | řetězec | Získá nebo nastaví ID MPN přidružené k této položce řádku. |
| ResellerMpnId | řetězec | Získá nebo nastaví ID MPN prodejce vrstvy 2 přidruženého k této položce řádku. |
| ChargeType | řetězec | Získá nebo nastaví typ poplatků. |
| UnitPrice | decimal | Získá nebo nastaví cenu jednotky. |
| Množství | decimal | Získá nebo nastaví množství využití. |
| Jednotkách UnitType | řetězec | Získá nebo nastaví typ jednotky (například 1 hodina). |
| BillingPreTaxTotal | decimal | Získá nebo nastaví rozšířené náklady nebo celkové náklady před zdaněním v místní měně zákazníka nebo fakturační měny. |
| BillingCurrency | řetězec | Získá nebo nastaví měnu ISO, za kterou se měřič účtuje v místní měně pro zákazníka nebo fakturační měnu. |
| PricingPreTaxTotal | decimal | Získá nebo nastaví rozšířené náklady nebo celkové náklady před zdaněním v USD nebo katalogovou měnou použitou pro hodnocení. |
| PricingCurrency | řetězec | Získá nebo nastaví měnu ISO, ve které se měřič účtuje za USD nebo katalogovou měnu použitou pro hodnocení. |
| EntitlementId | řetězec | Získá nebo nastaví ID oprávnění (předplatné Azure). |
| EntitlementDescription | řetězec | Získá nebo nastaví popis oprávnění (předplatné Azure). |
| PCToBCExchangeRate | řetězec | Získá nebo nastaví cenovou měnu směnného kurzu pro fakturační měnu. |
| PCToBCExchangeRateDate | DateTime | Získá nebo nastaví cenovou měnu na datum směnného kurzu fakturační měny. |
| EffectiveUnitPrice | decimal | Získá nebo nastaví efektivní jednotkovou cenu. |
| RateOfPartnerEarnedCredit | decimal | Získá nebo nastaví počet získaných kreditů pro partnery. |
| hasPartnerEarnedCredit | bool | Get nebo set je aplikován kredit získaný partnerem. |
| InvoiceLineItemType | InvoiceLineItemType | Vrátí typ položky řádku faktury. |
| BillingProvider | BillingProvider | Vrátí zprostředkovatele fakturace. |
