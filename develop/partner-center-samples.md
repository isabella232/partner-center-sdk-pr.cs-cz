---
title: Ukázky pro Partnerské centrum
description: Abychom vám pomohli rychle začít pracovat s rozhraními API partnerského centra, poskytujeme vzorový program, C \ spravované fragmenty kódu a požadavky na ukázky a odpovědi na ně.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 2098544e8607eabc4d25d90dcd7cad41510778a9
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2020
ms.locfileid: "97766916"
---
# <a name="partner-center-samples"></a>Ukázky pro Partnerské centrum

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Abychom vám pomohli rychle začít pracovat s rozhraními API partnerského centra, poskytujeme vzorový program, fragmenty spravovaného kódu v jazyce C# a požadavky na ukázky a odpovědi na ně.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

| Ukázka                                                        | Podrobnosti                                             |
|---------------------------------------------------------------|-----------------------------------------------------|
| Fragmenty kódu                                                 | Pro ukazatele a fragmenty kódu .NET, Java a PowerShellu, které ukazují, jak používat spravované rozhraní API partnerského centra pro správu zákaznických účtů, získání analýz, umístění objednávek, správa fakturace a předplatných, poskytování podpory a správy účtů a profilů, najdete v tématu [scénáře](scenarios.md).                                                                          |
| Ukázky REST                                                  | Ukázkové požadavky a odpovědi, které ukazují, jak používat REST API partnerského centra ke správě účtů zákazníků, získání analýz, umístění objednávek, správě fakturace a předplatných, poskytování podpory a správě účtů a profilů, najdete v tématu věnovaném [scénářům](scenarios.md).                                                                                                       |
| [Aplikace pro testování konzoly](console-test-app.md)                       | Tato aplikace je k dispozici v jazycích C# a Java a poskytuje kód a některé zpracování chyb pro všechny scénáře uvedené v části scénáře.                                                                        |
| [Webová výkladní skříň pro zákazníky CSP](csp-customer-web-storefront.md) | Tato lokalita ukazuje pracovní online obchod, který můžou vaši zákazníci použít k nákupu předplatných produktů Microsoftu. Web pro vaši společnost můžete snadno vytvořit pomocí [příručky pro rychlý Start tvůrce prezentace pro zákazníka CSP](csp-customer-storefront-builder-quick-start-guide-.md).                                                              |
| Uložit web                                                | Tato aplikace ukazuje, jak vytvořit webové úložiště založené na katalogu nabídek dostupných pro partnery Cloud Solution Provider. Zákazníci můžou vytvořit účet Store a objednat si předplatné softwaru prostřednictvím vašeho webu.<br/><br/>                  **Získat kód:**<br/> [Stažení ukázkového kódu](https://go.microsoft.com/fwlink/p/?LinkId=746683)<br/><br/>                                            **Co nakonfigurovat před vydáním:**<br/><br/> -Authentication: ID aplikace & tajný klíč.<br/> -Branding: logo a název společnosti<br/> – Uvítací zpráva<br/> – Nabídky, včetně popisů a cen. Aplikace předpokládá, že ceník obsahuje všechny platné daně. Alternativně můžete přidat další logiku pro výpočet daně během rezervace.<br/> -Platební údaje: zadejte vlastní možnosti platební karty, PayPal nebo jiné typy plateb. Před konfigurací této části si přečtěte příručku [bez platby, podvodů nebo zneužití](/partner-center/non-payment-fraud-misuse). |