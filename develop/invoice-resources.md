---
title: Fakturovat prostředky
description: Přes rozhraní API partnerského centra jsou k dispozici více prostředků souvisejících s fakturací. Tyto prostředky souvisejí s podrobnostmi o faktuře a položkách řádků.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d2e801dc3b082411e140b88cd495807b1381ef915e8f5f06803d64ca2cca1c6b
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996542"
---
# <a name="invoice-resources"></a>Fakturovat prostředky

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

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
| balanceAmount            | číslo                                                         | Zůstatek faktury Jedná se o celkovou částku nezaplacené faktury. |
| currencyCode             | řetězec                                                         | Kód, který označuje měnu použitou pro zůstatek.       |
| Currencysymbol           | řetězec                                                         | Použitý symbol měny.                                             |
| accountingDate           | řetězec ve formátu data a času UTC                                 | Datum poslední aktualizace zůstatku                         |
| firstInvoiceCreationDate | řetězec ve formátu data a času UTC                                 | Datum vytvoření první faktury pro zákazníka              |
| lastPaymentDate          | řetězec ve formátu data a času UTC                                 | Datum poslední platby                                         |
| lastPaymentAmount        | číslo                                                         | Částka poslední platby                                       |
| latestInvoiceDate        | řetězec ve formátu data a času UTC                                 | Datum vytvoření poslední faktury pro zákazníka               |
| Podrobnosti                  | pole objektů [InvoiceSummaryDetail](#invoicesummarydetail) | Podrobnosti o souhrnu faktury                                           |
| Odkazy                    | [Odkazy na prostředky](utility-resources.md#resourcelinks)            | Odkazy na prostředky.                                                   |
| atributy               | [Atributy prostředků](utility-resources.md#resourceattributes)  | Atributy metadat.                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

Představuje souhrn jednotlivých podrobností pro typ faktury (například jednou \_ opakovaně).

| Vlastnost            | Typ                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType (typ faktury)         | řetězec                                                         | Typ faktury: "opakující se", \_ "jednou".                                       |
| shrnutí             | [Objekt InvoiceSummary](#invoicesummary)                       | Souhrn faktury podle typu faktury                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

Představuje kolekci typu [InvoiceSummary,](#invoicesummary) která obsahuje jednotlivé podrobnosti pro typ faktury podle měny.

| Vlastnost            | Typ                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | pole objektů [InvoiceSummary](#invoicesummary)             | Souhrn faktury podle typu faktury podle měny                            |

## <a name="licensebasedlineitem"></a>LicenseBasedLineItem

Představuje řádkovou položku fakturace faktury pro licencovaná předplatná.

| Vlastnost                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| Částka                   | řetězec                                                         | Získá nebo nastaví celkovou částku. Celková částka = jednotková cena * množství.  |
| atributy               | řetězec                                                         | Získá atributy.                                                  |
| billingCycleType         | řetězec                                                         | Získá nebo nastaví typ fakturačního cyklu.                                  |
| billingProvider          | řetězec                                                         | Získá poskytovatele fakturace.                                            |
| chargeEndDate            | řetězec ve formátu data a času UTC                                 | Získá nebo nastaví koncové datum poplatku.                             |
| chargeStartDate          | řetězec ve formátu data a času UTC                                 | Získá nebo nastaví počáteční datum poplatku.                           |
| chargeType               | řetězec                                                         | Získá nebo nastaví typ poplatku.                                      |
| currency                 | řetězec                                                         | Získá nebo nastaví měnu použitou pro tuto položku řádku.                    |
| customerId               | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor zákazníka na fakturační platformě Microsoftu.  |
| customerName             | řetězec ve formátu data a času UTC                                 | Získá nebo nastaví jméno zákazníka.                                       |
| Název_domény               | řetězec                                                         | Získá nebo nastaví název domény.                                             |
| durableOfferId           | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor trvalé nabídky.                     |
| invoiceLineItemType      | řetězec                                                         | Získá typ řádkové položky faktury.                                   |
| ID mpn                    | číslo                                                         | Získá nebo nastaví ID MPN přidružené k této položce řádku. U přímých prodejců se jedná o ID MPN prodejce. U nepřímých prodejců se jedná o ID MPN prodejce value added reseller (VAR).                                   |
| ID nabídky                  | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor nabídky.                             |
| název_nabídky                | řetězec                                                         | Získá nebo nastaví název nabídky.                                          |
| Kódobjednávky                  | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor objednávky.                             |
| ID partnera                | řetězec                                                         | Získá nebo nastaví ID tenanta Azure Active Directory partnera.            |
| quantity                 | číslo                                                         | Získá nebo nastaví počet jednotek přidružených k této položce řádku.      |
| Popis předplatného  | řetězec                                                         | Získá nebo nastaví popis předplatného.                            |
| subscriptionEndDate      | řetězec ve formátu data a času UTC                                 | Získá nebo nastaví datum vypršení platnosti předplatného.                      |
| subscriptionId           | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor předplatného.                      |
| subscriptionName         | řetězec                                                         | Získá nebo nastaví název předplatného.                                   |
| subscriptionStartDate    | řetězec ve formátu data a času UTC                                 | Získá nebo nastaví datum zahájení odběru.                   |
| Dílčí součet                 | číslo                                                         | Získá nebo nastaví částku po slevě.                               |
| syndicationPartnerSubscriptionNumber | řetězec                                             | Získá nebo nastaví číslo předplatného partnera syndikace.             |
| Daňové                      | číslo                                                         | Získá nebo nastaví účtované daně.                                       |
| tier2MpnId               | číslo                                                         | Získá nebo nastaví ID MPN partnera vrstvy 2 přidruženého k této řádkové položce. |
| totalForCustomer         | číslo                                                         | Získá nebo nastaví celkovou částku po slevě a dani.                 |
| totalOtherDiscount       | číslo                                                         | Získá nebo nastaví slevu přidruženou k tomuto nákupu.              |
| unitPrice                | číslo                                                         | Získá nebo nastaví jednotkovou cenu.                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

Představuje položku řádku fakturace faktury pro předplatná založená na využití.

| Vlastnost                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| atributy               | řetězec                                                         | Získá atributy.                                                  |
| billingCycleType         | řetězec                                                         | Získá nebo nastaví typ fakturačního cyklu.                                  |
| billingProvider          | řetězec                                                         | Získá poskytovatele fakturace.                                            |
| chargeEndDate            | řetězec ve formátu data a času UTC                                 | Získá nebo nastaví koncové datum poplatku.                             |
| chargeStartDate          | řetězec ve formátu data a času UTC                                 | Získá nebo nastaví počáteční datum poplatku.                           |
| chargeType               | řetězec                                                         | Získá nebo nastaví typ poplatku.                                      |
| consumedQuantity         | číslo                                                         | Získá nebo nastaví celkový počet spotřebovaných jednotek.                                |
| consumptionDiscount      | řetězec                                                         | Získá nebo nastaví slevu na spotřebu.                             |
| consumptionPrice         | řetězec                                                         | Získá nebo nastaví cenu spotřebovaného množství.                          |
| currency                 | řetězec                                                         | Získá nebo nastaví měnu přidruženou k cenám.                 |
| customerName             | řetězec                                                         | Získá nebo nastaví jméno zákazníka.                                       |
| customerId               | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor zákazníka.                          |
| detailLineItemId         | číslo                                                         | Získá nebo nastaví ID položky řádku podrobností. Jednoznačně identifikuje řádkové položky pro případy, kdy se výpočet pro spotřebované jednotky liší. Příklad: Celkové spotřebované = 1338, 1024 se účtuje jednou sazbou, 314 se účtuje s jinou sazbou.        |
| Název_domény               | řetězec                                                         | Získá nebo nastaví název domény.                                             |
| includedQuantity         | číslo                                                         | Získá nebo nastaví jednotky zahrnuté v pořadí.                         |
| invoiceLineItemType      | řetězec                                                         | Získá typ řádkové položky faktury.                                   |
| invoiceNumber            | řetězec                                                         | Získá nebo nastaví číslo faktury.                                      |
| Listprice                | číslo                                                         | Získá nebo nastaví cenu každé jednotky.                                  |
| ID mpn                    | číslo                                                         | Získá nebo nastaví ID MPN přidružené k této položce řádku. U přímých prodejců se jedná o ID MPN prodejce. U nepřímých prodejců se jedná o ID MPN prodejce value added reseller (VAR).                                   |
| Kódobjednávky                  | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor objednávky.                             |
| overageQuantity          | číslo                                                         | Získá nebo nastaví množství spotřebované nad povoleným využitím.               |
| partnerBillableAccountId | řetězec                                                         | Získá nebo nastaví ID fakturovatelného účtu partnera.                         |
| ID partnera                | řetězec                                                         | Získá nebo nastaví ID tenanta Azure Active Directory partnera.            |
| název partnera              | řetězec                                                         | Získá nebo nastaví název partnera.                                      |
| postTaxEffectiveRate     | číslo                                                         | Získá nebo nastaví efektivní cenu po daních.                         |
| postTaxTotal             | číslo                                                         | Získá nebo nastaví celkové poplatky po dani. Poplatky před zdaněním a částka daně |
| preTaxCharges            | číslo                                                         | Získá nebo nastaví cenu účtované před daněmi.                          |
| preTaxEffectiveRate      | číslo                                                         | Získá nebo nastaví efektivní cenu před daněmi.                        |
| oblast                   | řetězec                                                         | Získá nebo nastaví oblast přidruženou k instanci prostředku.        |
| resourceGuid (identifikátor GUID prostředku)             | řetězec                                                         | Získá nebo nastaví identifikátor prostředku.                                 |
| resourceName             | řetězec                                                         | Získá nebo nastaví název prostředku. Příklad: Databáze (GB/měsíc).         |
| Název_služby              | řetězec                                                         | Získá nebo nastaví název služby. Příklad: Azure Data Service.           |
| Servicetype              | řetězec                                                         | Získá nebo nastaví typ služby. Příklad: Azure SQL Azure DB.           |
| Sku                      | řetězec                                                         | Získá nebo nastaví SKU služby.                                         |
| Popis předplatného  | řetězec                                                         | Získá nebo nastaví popis předplatného.                            |
| subscriptionId           | řetězec                                                         | Získá nebo nastaví jedinečný identifikátor předplatného.                      |
| subscriptionName         | řetězec                                                         | Získá nebo nastaví název předplatného.                                   |
| taxAmount                | číslo                                                         | Získá nebo nastaví výši účtované daně.                               |
| tier2MpnId               | číslo                                                         | Získá nebo nastaví ID MPN partnera vrstvy 2 přidruženého k této řádkové položce. |
| unit                     | řetězec                                                         | Získá nebo nastaví měrnou jednotku pro využití Azure.                     |

## <a name="invoicestatement"></a>InvoiceStatement

Představuje operace dostupné na výpisu faktury v souboru application/pdf.

| Vlastnost                 | Typ                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | ByteArrayContent s contentType = application/pdf.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

Představuje řádkovou položku fakturace faktury pro licencovaná předplatná.

| Vlastnost | Typ | Description |
| --- | --- | --- |
| ID partnera | řetězec | Získá nebo nastaví ID partnerského tenanta. |
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
| CreditReasonCode | řetězec | Získá nebo nastaví kód důvodu kreditu. |
| DiscountDetails | řetězec |  **Zastaralé**. Získá nebo nastaví podrobnosti slevy spojené s tímto nákupem. |
| PricingCurrency | řetězec | Získá nebo nastaví kód cenové měny. |
| PCToBCExchangeRate | decimal | Získá nebo nastaví ceníkovou měnu na směnný kurz fakturační měny. |
| PCToBCExchangeRateDate | DateTime | Získá nebo nastaví datum směnného kurzu, ve kterém byla určená měna ceníku pro směnný kurz fakturační měny. |
| BillableQuantity | decimal | Získá nebo nastaví zakoupené jednotky. Pro každý sloupec návrhu s názvem **BillableQuantity**. |
| Popis měřiče | řetězec | Získá nebo nastaví popis měřiče pro položku řádku Consumption. |
| ReservationOrderId | řetězec | Získá nebo nastaví identifikátor objednávky rezervace pro nákup azure RI. |
| FakturaceFrequency | řetězec | Získá nebo nastaví četnost fakturace. |
| InvoiceLineItemType | InvoiceLineItemType | Vrátí typ řádkové položky faktury. |
| BillingProvider | BillingProvider | Vrátí poskytovatele fakturace. |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

Představuje nefaktované fakturované řádkové položky odsouhlasení pro využití podle denního hodnocení.

| Vlastnost | Typ | Description |
| --- | --- | --- |
| ID partnera | řetězec | Získá nebo nastaví ID tenanta partnera. |
| PartnerName | řetězec | Získá nebo nastaví název partnera. |
| CustomerId | řetězec | Získá nebo nastaví ID tenanta zákazníka, ke které využití patří. |
| CustomerName | řetězec | Získá nebo nastaví název zákaznické společnosti, do které patří využití. |
| CustomerDomainName | řetězec | Získá nebo nastaví název domény zákazníka, ke které patří využití. |
| InvoiceNumber | řetězec | Získá nebo nastaví ID faktury, ke které patří využití. |
| ProductId | řetězec | Získá nebo nastaví jedinečný identifikátor produktu. |
| ID SKU | řetězec | Získá nebo nastaví jedinečný identifikátor SKU. |
| ID dostupnosti | řetězec | Získá nebo nastaví jedinečný identifikátor dostupnosti. |
| SkuName | řetězec | Získá nebo nastaví název SKU pro službu. |
| ProductName | řetězec | Získá nebo nastaví název produktu. |
| Název vydavatele | řetězec | Získá nebo nastaví název vydavatele. |
| PublisherId | řetězec | Získá nebo nastaví ID vydavatele. |
| SubscriptionId | řetězec | Získá nebo nastaví ID předplatného. |
| Popis předplatného | řetězec | Získá nebo nastaví popis předplatného. |
| ChargeStartDate | DateTime | Získá nebo nastaví počáteční datum poplatku. |
| ChargeEndDate | DateTime | Získá nebo nastaví koncové datum poplatku. |
| UsageDate | DateTime | Získá nebo nastaví datum použití. |
| MeterType (Typ měřiče) | řetězec | Získá nebo nastaví typ měřiče. |
| MeterCategory | řetězec | Získá nebo nastaví kategorii měřiče. |
| MeterId | řetězec | Získá nebo nastaví ID měřiče (GUID). |
| MeterSubCategory | řetězec | Získá nebo nastaví dílčí kategorii měřiče. |
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
| HasPartnerEarnedCredit | bool | Get nebo set je aplikován kredit získaný partnerem. |
| RateOfCredit | decimal | Získá nebo nastaví sazbu kreditu pro daný typ kreditu. |
| CreditType | řetězec | Získá nebo nastaví typ kreditu. |
| InvoiceLineItemType | InvoiceLineItemType | Vrátí typ položky řádku faktury. |
| BillingProvider | BillingProvider | Vrátí zprostředkovatele fakturace. |
