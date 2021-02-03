---
title: Scénáře rozhraní API partnerského centra
description: Přečtěte si, jak partneři programu Cloud Solution Provider můžou používat rozhraní API partnerského centra k programové správě účtů, objednávek, podpory a fakturace zákazníků.
ms.date: 10/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14dbd501e3d075c3880fae6f362feef797cba133
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/11/2020
ms.locfileid: "97767070"
---
# <a name="partner-center-api-scenarios-that-let-you-programmatically-manage-customer-accounts"></a>Scénáře rozhraní API partnerského centra, které umožňují programově spravovat účty zákazníků

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Tento článek popisuje některé způsoby, jak partneři v programu Cloud Solution Provider můžou pomocí rozhraní API partnerského centra programově spravovat oblasti, jako je:

- Zákaznické účty
- Orders (Objednávky)
- Předplatná
- Podpora
- Fakturace

K dispozici jsou různé verze partnerského centra, které obsahují různé možnosti. Ne všechny scénáře jsou podporovány ve všech verzích partnerského centra. Další informace najdete v tématu [vývoj pro partnerského centra pro národní Cloud Microsoftu](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="scenarios-supported-by-the-partner-center-sdk"></a>Scénáře podporované sadou partner Center SDK

Všechny následující scénáře mohou být dokončeny třemi různými způsoby:

- Ručně na řídicím panelu [partnerského centra](https://partner.microsoft.com/dashboard) .

- Prostřednictvím programu spravovaného rozhraní API partnerského centra.

- Prostřednictvím kódu programu REST API partnerského centra.

| Další informace o těchto podporovaných scénářích:  | Zobrazit tento prostředek:     |
|----------------------------------|--------------------------|
| **Analýza:** Naučte se načítat analytické údaje o využití, předplatných, licencích a odkazech Azure.         | [Analýzy](usage-analytics.md)  |
| **Operace auditu:** Naučte se, jak načíst historické záznamy auditu aktivity a činnosti partnerského centra. | [Operace auditu](audit.md)                     |
| **Nasazení zařízení:** Přečtěte si o zásadách konfigurace zařízení, práci s listy zařízení a metadatech zařízení. Mezi tyto scénáře patří přidání, odstranění, aktualizace a načtení zásad konfigurace zařízení.    | [Nasazení zařízení](device-deployment.md)  |
| **Účty a profily:** Naučte se, jak získat nebo aktualizovat profily pro fakturaci partnerů, profily legálních, profil MPN, obchodní profily nebo profily podpory. Můžete také získat seznam zákazníků nebo nepřímých prodejců. | [Správa účtů a profilů](manage-profiles-and-information.md)                                                                        |
| **Fakturace:** Přečtěte si o oblastech, jako je změna fakturačního cyklu, získání tarifů Azure a záznamů o využití Azure, získání faktur, získání aktuálního zůstatku účtu partnera nebo získání nákladů na služby zákazníkům.  | [Správa vyúčtování](manage-billing.md)   |
| **Útrata Azure:** Získejte informace o útratě Azure a využití partnerů, využití zákaznických předplatných, měření využití a rozpočtu využívání zákazníků. Scénáře také obsahují informace o tom, jak aktualizovat rozpočet zákaznického využití. | [Útrata v Azure](azure-spending.md)  |
| **Správa zákaznických účtů:** Naučte se, jak provádět mnoho aspektů správy zákaznických účtů, jako je vytváření a odstraňování zákaznických účtů nebo uživatelských účtů zákazníka, Správa a ověřování podrobností o účtu zákazníka, Správa uživatelských účtů a přiřazování licencí.  | [Správa zákazníků](manage-customers.md)  |
| **Správa objednávek:** Seznamte se se všemi způsoby, kterými můžete programově spravovat Zákaznické objednávky a odběry. Tato oblast zahrnuje nákup rezervací Azure, vytváření objednávek, získávání nabídek z katalogu a správu nabídek zkušebního převodu.   | [Správa objednávek](manage-orders.md)  |
| **Poskytování podpory:** Naučte se spravovat služby pro zákazníka, jak získat nebo aktualizovat kontakty podpory pro předplatné a jak spravovat žádosti o služby.  | [Poskytování podpory](provide-support.md)   |
| **Referenční seznamy:** Naučte se vytvořit odkaz, získat seznam odkazů nebo aktualizovat odkaz.  | [Reference](/partner/develop/referrals)  |
| **Nástroje:** Naučte se, jak ověřit adresu, získat pravidla formátování adres podle trhu, ověřit dostupnost domény, odstranit účet zákazníka z karantény integrace nebo získat záznam aktivity partnerského centra. | [Nástroje](utilities.md)  |
| **Zabezpečení:** Přečtěte si o rozhraních REST API souvisejících se službou Multi-Factor Authentication (MFA) v partnerském centru. Tato rozhraní API vám pomůžou vymáhat MFA pro každý uživatelský účet v partnerském tenantovi.  | [Stav požadavků na zabezpečení partnerů](partner-security-requirements.md)  |

## <a name="next-steps"></a>Další kroky

- [Viz Ukázka partnerského centra.](partner-center-samples.md)
- [Informace o tom, jak začít](get-started.md)