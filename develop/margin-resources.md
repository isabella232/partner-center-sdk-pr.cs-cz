---
title: Prostředky marže
description: Prostředky, které představují okraje. Obsahuje prostředky pro popis okrajů.
ms.date: 09/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 83ea2f95c72f4e5074e3396ef226462b5b007878
ms.sourcegitcommit: deb3207935fb5a74df515ed0fd4ffec90e6a143c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/07/2021
ms.locfileid: "129646384"
---
# <a name="margin-resources"></a>Prostředky marže

Prostředky, které představují dostupná okraje. Zahrnuje prostředky pro popis okrajů.  

Nezávislý výrobce softwaru (ISV) může vytvářet slevy nebo marže pro konkrétní poskytovatele CLOUD Solution Providers (CSP). Níže jsou uvedené prostředky, které představují a popisují okraje.
                
## <a name="margin"></a>Margin                   
                        
Představuje neocenitelnou marži pro daného poskytovatele CSP.
                
| Název            | Typ            | Description                               |
|-----------------|-----------------|-------------------------------------------|
| id              | řetězec          | Jedinečný identifikátor okrajů         |
| marginPercentage | číslo         | Procentuální sleva uplatněná na maloobchodní cenu CSP.  |
| productId       | řetězec          | ID produktu, pro které je marže k dispozici.   |
| název produktu    | řetězec          | Název produktu, pro který je marže k dispozici. |
| productType     | řetězec          | Typ produktu, pro který je marže k dispozici.   |
| publisherName   | řetězec          | Název isv, který vytvořil okraj.  |
| ID SKU           | řetězec          | ID SKU, pro které je margin k dispozici.  |
| skuTitle        | řetězec          | Název SKU, pro který je okraj k dispozici. |
| Datum_spuštění       | řetězec          | Počáteční datum, kdy je okraj k dispozici. |
| Enddate         | řetězec          | Koncové datum, ve které je okraj k dispozici. |
| status          | řetězec          | Stav určuje, jestli je okraj k dispozici. |
| statusDate (datum stavu)      | řetězec          | Datum poslední aktualizace stavu |

## <a name="definitions"></a>Definice

Různé typy artefaktů popisující okraje.                    

| Název            | Description          |
|-----------------|----------------------|
| Margin |  Definuje jednotlivý okraj.  |    
| MarginSearchResponse |  Definuje data odezvy okrajů.  |  
        
## <a name="related-documentation"></a>Související dokumentace

- [Okraje v Partnerské centrum přehledu](/partner-center/csp-commercial-marketplace-margins)
- [Nákup nabídek na marketplace](/partner-center/csp-commercial-marketplace-purchase)
- [Správa nabídek na marketplace](/partner-center/csp-commercial-marketplace-manage)
- [Získání seznamu okrajů](get-margins.md)
- [Stažení seznamu okrajů](download-margins.md)
