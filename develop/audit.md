---
title: Operace auditu aktivity partnerského centra
description: Přečtěte si o typu operací auditu partnerského centra rozhraní API, které můžete použít k získání záznamu o aktivitě partnerského centra.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0e8010bde75bee4c4954034d8f61f19b076d96349e4a05807e272ca88efbc2fa
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994264"
---
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a>Operace auditu dostupné prostřednictvím rozhraní API partnerského centra, které zobrazuje záznam aktivity partnerského centra

Rozhraní API partnerského centra poskytují funkce auditování, abyste mohli získat záznam o aktivitě partnerského centra.

Můžete načíst záznamy o auditu za posledních 30 dní od aktuálního data nebo pro rozsah dat zadaný zahrnutím počátečního data a/nebo koncového data. Upozorňujeme ale, že z důvodů výkonu je dostupnost dat protokolu aktivit omezená na předchozí 90 dní. Žádosti s počátečním datem větším než 90 dní před aktuálním datem obdrží výjimku špatné žádosti (kód chyby: 400) a příslušnou zprávu.

## <a name="retrieve-audit-records"></a>Načtení záznamů auditu

Získat podrobné záznamy o provedených auditech operací provedených partnerským uživatelem nebo aplikací:

- [Získání záznamu o aktivitě Partnerského centra](get-a-record-of-partner-center-activity-by-user.md)
- [Auditování prostředků](auditing-resources.md)