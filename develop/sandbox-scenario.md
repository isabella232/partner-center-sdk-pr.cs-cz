---
title: Možnosti sandboxu pro vztah prodejce
description: Partnerský sandbox může podporovat vztahy mezi partnerem a zákazníkem.
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9bef4a15685ebbdc2212988f5ac5724b946cfd54
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2021
ms.locfileid: "110243380"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a>Možnosti sandboxu pro vztah prodejce

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozované společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Tento článek vysvětluje, co sandbox podporuje pro vztahy prodejce mezi partnerem a zákazníkem. 

## <a name="prerequisites"></a>Požadavky

- Partnerské centrum přihlašovací údaje účtu. Scénář sandboxu podporuje ověřování pomocí samostatné aplikace i přihlašovacích údajů aplikace a uživatele.
- ID zákazníka (customer-tenant-id) Pokud ID zákazníka neznáme, můžete ho hledat na řídicím panelu Partnerské centrum [.](https://partner.microsoft.com/dashboard/home) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte ID **Microsoftu** v části **Informace o účtu** zákazníka. ID Microsoftu je stejné jako ID zákazníka (customer-tenant-id).
- Všechny Azure Reserved Virtual Machine Instances a nákupní objednávky softwaru se musí před odstraněním zákazníka z sandboxu integrace tipů zrušit.

## <a name="scenarios-supporting-reseller-relationship"></a>Scénáře podporující vztah prodejce

1.  Partneři s přímým vyúčtováním sandboxu a nepřímí poskytovatelé mohou vytvářet vztahy se zákazníkem sandboxu. 
2.  Partneři sandboxu s přímým vyúčtováním a nepřímí poskytovatelé nemohou pozvat zákazníky sandboxu.

3. Partneři s přímým vyúčtováním sandboxu a nepřímí poskytovatelé zprostředkovatelé mohou odebrat vztah prodejce Partnerské centrum uživatelském rozhraní a rozhraní API.

4. Sandbox Remove Reseller Relationship zavolá příkaz Delete customer AP (Odstranit přístupový bod zákazníka). Tím odeberete relaci a odstraníte tenanta zákazníka. {baseURL}/v1/Customers/{customer-Tenant-id}


    ### <a name="in-the-sandbox"></a>V izolovaném prostoru

    **Partneři s přímým účtováním**:

    - Může přidat existující zákazníky.

    - Vztahy s novými zákazníky nejde vyžádat.

    **Nepřímí zprostředkovatelé**:

    - Může přidat existující zákazníky.

    - Vztahy s novými zákazníky nejde vyžádat.

    - Nemůže mít relaci s nepřímým prodejcem.

    **Nepřímý prodejce**: 

    -   Můžou mít relace s existujícími zákazníky.

    -   Nejde požádat o nové relace ani přidat nové zákazníky.

    ### <a name="in-partner-center"></a>V partnerském centru

    **Partneři s přímým účtováním**:

    -   Může přidat nové zákazníky.

    -   Může vyžádat vztahy s novými zákazníky.

    **Nepřímí zprostředkovatelé**:

    -   Může přidat nové zákazníky.

    -   Může vyžádat vztahy s novými zákazníky.

    -   Může mít relace s nepřímými prodejci

    **Nepřímí prodejci**:

    -   Nejde přidat nové zákazníky.

    -   Může vyžádat vztahy s novými zákazníky.


Podrobnější informace pro zákazníka získáte pomocí [vztahu odebrat prodejce](remove-a-reseller-relationship-with-a-customer.md) . Existují však určité rozdíly mezi funkcemi produktu a izolovaného prostoru (sandbox).

### <a name="request-syntax"></a>SYNTAXE ŽÁDOSTI

|**Metoda**|**Odstranit**|
|-------------|------------|
|Odstranit|{baseURL}/v1/Customers/{customer-Tenant-id} |

Tělo žádosti není žádné

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](./error-codes.md).

## <a name="next-steps"></a>Další kroky

- [Aktivovat předplatná izolovaného prostoru pro Azure Marketplace produkty](activate-sandbox-subscription-azure-marketplace-products.md)

- [Zrušení objednávky z izolovaného prostoru](cancel-an-order-from-the-integration-sandbox.md)

- [Testování a ladění](test-and-debug.md)