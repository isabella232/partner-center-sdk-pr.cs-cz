---
title: Ukázky pro Partnerské centrum
description: S rychlým zpočinkem rozhraní API Partnerské centrum nabízíme ukázkový program, fragmenty kódu spravované jazykem C\ a ukázkové požadavky a odpovědi REST.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 36d1c74e12ae680facef1414ce35ac2d6fb5322c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547831"
---
# <a name="partner-center-samples"></a>Ukázky pro Partnerské centrum

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

K rychlému zdůchování a zběhu rozhraní API Partnerské centrum nabízíme ukázkový program, fragmenty kódu spravované jazykem C# a ukázkové požadavky a odpovědi REST.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

| Ukázka                                                        | Podrobnosti                                             |
|---------------------------------------------------------------|-----------------------------------------------------|
| Fragmenty kódu                                                 | Informace o ukazatelích a fragmentech kódu .NET, Javy a PowerShellu, které ukazují, jak používat rozhraní PARTNERSKÉ CENTRUM MANAGED API ke správě zákaznických účtů, získání analýz, objednávek, správě fakturace a předplatných, poskytování podpory a správě účtů a profilů, najdete v [tématu](scenarios.md)Scénáře.                                                                          |
| Ukázky REST                                                  | Ukázkové požadavky a odpovědi, které ukazují, jak používat Partnerské centrum REST API ke správě zákaznických účtů, získání analýz, objednávek, správě fakturace a předplatných, poskytování podpory a správy účtů a profilů, najdete v tématu [Scénáře.](scenarios.md)                                                                                                       |
| [Aplikace pro testování konzoly](console-test-app.md)                       | Tato aplikace je dostupná v jazyce C# a Java, poskytuje kód a zpracování některých chyb pro všechny scénáře uvedené v části scénáře.                                                                        |
| [Webová výkladní skříň pro zákazníky CSP](csp-customer-web-storefront.md) | Tento web ukazuje fungující online obchod, který by vaši zákazníci mohli použít k nákupu předplatných produktů Microsoftu. Web pro vaši společnost můžete snadno vytvořit pomocí průvodce rychlým zprovozněním [pro CSP customer Storefront Builder.](csp-customer-storefront-builder-quick-start-guide-.md)                                                              |
| Store web site                                                | Tato aplikace ukazuje, jak vytvořit webové úložiště na základě katalogu nabídek dostupných pro Cloud Solution Provider partnery. Zákazníci mohou vytvořit účet úložiště a objednat si předplatná softwaru prostřednictvím vašeho webu.<br/><br/>                  **Získejte kód:**<br/> [Stažení ukázkového kódu](https://go.microsoft.com/fwlink/p/?LinkId=746683)<br/><br/>                                            **Co nakonfigurovat před vydáním:**<br/><br/> - Ověřování: ID aplikace & tajný kód<br/> - Branding: logo a název společnosti<br/> – Uvítací zpráva<br/> – Nabídky, včetně popisů a cen. Aplikace předpokládá, že ceníkové ceny zahrnují příslušné daně. Případně můžete přidat další logiku pro výpočet daně během pokladny.<br/> - Platební údaje: Zadejte vlastní možnosti platby platební kartou, PayPal nebo jiné typy plateb. Před konfigurací této části si přečtěte průvodce [Nezaplacení, podvod nebo zneužití.](/partner-center/non-payment-fraud-misuse) |