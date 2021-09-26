---
title: Povýšení prostředků
description: Popisuje prostředky pro propagační akce, které se vztahují na transakce pro nová předplatná obchodu.
ms.date: 09/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 6a0b38576f5756a127fe6ba787f970db9ac59be3
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2021
ms.locfileid: "128715977"
---
# <a name="promotions-resources"></a>Prostředky propagace

**Platí pro**

- Partnerské centrum

**Příslušné role**

- Globální správce
- Agent správce

> [!Note] 
> nové obchodní změny jsou aktuálně k dispozici pouze partnerům, kteří jsou součástí Microsoft 365 a Dynamics 365 new Commerce experience technical preview.

Popisuje prostředky pro propagační akce, které se vztahují na transakce pro nová předplatná obchodu.

## <a name="promotion"></a>Promotion

Použití slevy při nákupu skladové položky produktu, pokud jsou splněna kritéria způsobilosti.

| Vlastnost          | Typ                    | Popis                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| id | řetězec                  | Identifikátor povýšení |
| name | řetězec                  | Popisný název povýšení |
| description | řetězec                  | Popis povýšení. |
| startDate | řetězec | Počáteční datum, kdy se bude povýšení uplatňovat. |
| endDate | řetězec  | Koncové datum, kdy se bude povýšení uplatňovat. |
| requiredProducts | seznam requiredProducts | Podrobnosti o produktech, SKU a cenách, ke kterým se povýšení vztahuje. | 
| properties | seznam vlastností | Vlastnosti pro povýšení, včetně toho, zda je propagace automaticky platná. | 

## <a name="requiredproducts"></a>RequiredProducts

Podrobnosti o produktech, SKU a cenách, ke kterým se povýšení vztahuje.

| Vlastnost          | Typ                    | Popis                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| productId| řetězec | Identifikátor produktu, pro který je povýšení k dispozici. |
| skuId | řetězec | Identifikátor SKU, pro který je povýšení k dispozici. |
| doby | Pojem | Termín včetně doby trvání a fakturačního cyklu, pro který je povýšení k dispozici. |
| pricingPolicies| Seznam pricingPolicies | Seznam zásad, které definují typy a hodnoty propagační slevy. |

## <a name="term"></a>Pojem

Představuje termín, pro který lze povýšení zakoupit.

| Vlastnost          | Typ                    | Popis                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| doba trvání          | řetězec                  | ISO 8601 reprezentace doby trvání období. Aktuální podporované hodnoty jsou P1M (jeden měsíc), P1Y (jeden rok) a P3Y (tři roky). 
| billingCycle      | řetězec | Popisuje, jak často se bude povýšení použít pro fakturaci. Hodnoty můžou zahrnovat každý měsíc, roční, jednorázová nebo neznámý. | 

## <a name="pricingpolicies"></a>PricingPolicies

Popište typy a hodnoty propagačních slev.

| Vlastnost          | Typ               | Popis                                                                  |          
|-------------------|--------------------|------------------------------------------------------------------------------|
| typ | řetězec | Popište, jestli je sleva založená na procentech nebo paušálních slevách. |
| hodnota | řetězec  | Definuje množství využité slevy. |

## <a name="properties"></a>Vlastnosti

Vlastnosti pro povýšení

| Vlastnost          | Typ               | Popis                                        |
|-------------------|--------------------|----------------------------------------------------|
| isAutoApplicable  | bool  | Označuje, zda je propagační akce použita automaticky nebo zda musí být předána partnerem. |


## <a name="promotioneligibilitiesrequestitem"></a>PromotionEligibilitiesRequestItem

Vlastnosti reprezentující transakci a nárok na propagaci.

| Vlastnost          | Typ               | Popis                                        |
|-------------------|--------------------|----------------------------------------------------|
| id | int| Identifikátor položky eligibilities propagace. |
| catalogItemId | řetězec | Identifikátor položky katalogu, na kterou se bude povýšení použít Zahrnuje ID produktu, ID SKU a ID dostupnosti. |
| quantity | int | Počet licencí nebo instancí. |
| termDuration | řetězec | Reprezentace doby trvání období podle STANDARDu ISO 8601. Aktuální podporované hodnoty jsou P1M (jeden měsíc), P1Y (jeden rok) a P3Y (tři roky). |
| billingCycle | řetězec | Popisuje, jak často se povýšení použije na fakturaci. Mezi hodnoty patří Měsíční, Roční, OneTime nebo Neznámé. | 
| promotionID (ID povýšení) | řetězec | Identifikátor povýšení. |

## <a name="promotioneligibilities"></a>PromotionEligibilities

Seznam produktů, skladových položek a jejich způsobilosti pro povýšení.

| Vlastnost          | Typ               | Popis                                        |
|-------------------|--------------------|----------------------------------------------------|
| id | int| Identifikátor položky způsobilosti pro propagační akce. |
| catalogItemId | řetězec | Identifikátor položky katalogu, na který se povýšení použije. Zahrnuje ID produktu, ID SKU a ID dostupnosti. |
| quantity | int | Počet licencí nebo instancí |
| termDuration | řetězec | Reprezentace doby trvání období podle STANDARDu ISO 8601. Aktuální podporované hodnoty jsou P1M (jeden měsíc), P1Y (jeden rok) a P3Y (tři roky). |
| billingCycle | řetězec | Popisuje, jak často se povýšení použije na fakturaci. Hodnoty mohou zahrnovat měsíční, roční, onetime nebo neznámé. | 
| způsobilost | Seznam funkcí povýšení | Představuje seznam výsledků způsobilosti pro propagační akci. |

## <a name="promotioneligibility"></a>PromotionEligibility

Seznam produktů, skladových položek a jejich způsobilosti pro povýšení.

| Vlastnost          | Typ               | Popis                                        |
|-------------------|--------------------|----------------------------------------------------|
| ID povýšení | řetězec | Identifikátor povýšení. |
| isEligible | bool | Popisuje, jestli má povýšení nárok na danou položku žádosti o nárok. |
| chyby | Seznam chyb PromotionEligibilityErrors | Chyby popisující, proč položka žádosti o nárok na propagační akci nebyla způsobilá. | 

## <a name="promotioneligibilityerror"></a>PromotionEligibilityError

Vysvětluje, proč položka žádosti o nárok na propagační akci nebyla oprávněná. 

| Vlastnost          | Typ               | Popis                                        |
|-------------------|--------------------|----------------------------------------------------|
| typ | řetězec | Mezi typy chyb způsobilosti pro povýšení patří InvalidCatalogItemId, InvalidPromotion, PrerequisiteProductOwnership, RedemptionLimit, SeatCount, OfferPurchasedPreviously nebo Term. |
| description | řetězec | Popisuje, jestli má povýšení nárok na danou položku žádosti o nárok. |

## <a name="redemptionlimitpromotioneligibilityerror"></a>RedemptionLimitPromotionEligibilityError

Obsahuje podrobnosti o tom, proč byl překročen limit pro uplatnění.

| Vlastnost          | Typ               | Popis                                        |
|-------------------|--------------------|----------------------------------------------------|
| maxPromotionRedemptionCount | int | Maximální počet, kolikrát je možné povýšení získat. |
| remainingPromotionRedemptionCount| int | Zbývající počet, kolikrát je možné získat povýšení. |

## <a name="seatcountpromotioneligibilityerror"></a>SeatCountPromotionEligibilityError

Obsahuje podrobnosti o tom, proč byl překročen limit počtu míst. Obě hodnoty mohou mít hodnotu null.

| Vlastnost          | Typ               | Popis                                        |
|-------------------|--------------------|----------------------------------------------------|
| minimumRequiredSeats | Int? | Minimální licence, které bude povýšení podporovat. |
| maximumRequiredSeats | Int? | Maximální počet licencí, které bude povýšení podporovat. |

## <a name="termpromotioneligibilityerror"></a>TermPromotionEligibilityError

Obsahuje podrobnosti o tom, proč se období povýšení nepřijalo.

| Vlastnost          | Typ               | Popis                                        |
|-------------------|--------------------|----------------------------------------------------|
| eligibleTerms | PromotionTerm | Podmínky, na které se nárok nárok mají, bude propagační akce podporovat. |

## <a name="promotionterm"></a>PromotionTerm

Obsahuje podrobnosti o tom, proč byl překročen limit počtu míst.

| Vlastnost          | Typ               | Popis                                        |
|-------------------|--------------------|----------------------------------------------------|
| billingCycle | řetězec | Popisuje, jak často se povýšení použije na fakturaci. Hodnoty mohou zahrnovat měsíční, roční, onetime nebo neznámé. |
| doba trvání | řetězec | Doba trvání zakoupeného období. |




