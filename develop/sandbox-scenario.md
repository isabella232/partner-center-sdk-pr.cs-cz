---
title: Možnosti partnerského sandboxu, které podporují vztah s prodejci
description: Partner izolovaného prostoru (sandbox) má schopnost podporovat vztahy mezi partnerem a zákazníkem.
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: af46811b3615e1f904a9619de85b0aca7622490b
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711861"
---
# <a name="partner-sandbox-capabilities-that-support-reseller-relationship"></a>Možnosti partnerského sandboxu, které podporují vztah s prodejci

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozované společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Tento článek vysvětluje, co je podporováno v izolovaném prostoru (sandbox) pro vztahy prodejců mezi partnerem a zákazníkem. 

## <a name="prerequisites"></a>Předpoklady

- Přihlašovací údaje účtu partnerského centra Scénář izolovaného prostoru (sandbox) podporuje ověřování jak pro samostatnou aplikaci, tak i pro přihlašovací údaje uživatele a aplikace.
- ID zákazníka (Customer-tenant-ID). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard/home)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka (Customer-tenant-ID).
- Před odstraněním zákazníka z karantény integrace s tipem se musí zrušit všechny nákupní objednávky Azure Reserved Virtual Machine Instances a softwaru.

## <a name="scenarios-supporting-reseller-relationship"></a>Scénáře podporující vztah prodejce

1.  Partneři izolovaného prostoru (sandboxu) a nepřímá poskytovatelé můžou vytvářet relace s zákazníkem izolovaného prostoru. 
2.  Partneři izolovaného prostoru (sandboxu) a nepřímá poskytovatelé můžou pozvat zákazníky izolovaného prostoru



### <a name="in-the-sandbox"></a>V izolovaném prostoru

**Partneři s přímým účtováním**:

• Může přidat existující zákazníky.

• Nemůžou vyžádat relace s novými zákazníky.

**Nepřímí zprostředkovatelé**:

• Může přidat existující zákazníky.

• Nemůžou vyžádat relace s novými zákazníky.

• Nemůže mít relaci s nepřímým prodejcem

**Nepřímý prodejce**: (už brzy)

• Může mít relace s existujícími zákazníky.

• Nemůžete požádat o nové relace ani přidat nové zákazníky.

### <a name="in-partner-center"></a>V partnerském centru

**Partneři s přímým účtováním**:

• Může přidat nové zákazníky.

• Může vyžádat relace s novými zákazníky

**Nepřímí zprostředkovatelé**:

• Může přidat nové zákazníky.

• Může vyžádat relace s novými zákazníky

• Může mít relace s nepřímými prodejci.

**Nepřímí prodejci**:

• Nemůžete přidávat nové zákazníky.

• Může vyžádat relace s novými zákazníky

3. Partner s přímým přístupem k izolovanému prostoru a nepřímá poskytovatelé můžou odebrat vztah prodejce z uživatelského rozhraní a rozhraní API partnerského centra.

4. V izolovaném prostoru odeberte vztah prodejce, který bude volat odstranění přístupového bodu zákazníka. Tato akce odebere vztah a odstraní tenanta zákazníka. {baseURL}/v1/Customers/{customer-Tenant-id}

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