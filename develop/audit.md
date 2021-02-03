---
title: Operace auditu aktivity partnerského centra
description: Přečtěte si o typu operací auditu partnerského centra rozhraní API, které můžete použít k získání záznamu o aktivitě partnerského centra.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 019bebe40c43f6ee1c2ac7da381a86ca190702d4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/13/2020
ms.locfileid: "97767082"
---
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a><span data-ttu-id="4333e-103">Operace auditu dostupné prostřednictvím rozhraní API partnerského centra, které zobrazuje záznam aktivity partnerského centra</span><span class="sxs-lookup"><span data-stu-id="4333e-103">Audit operations available via Partner Center API that show a record of Partner Center activity</span></span>

<span data-ttu-id="4333e-104">Rozhraní API partnerského centra poskytují funkce auditování, abyste mohli získat záznam o aktivitě partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="4333e-104">The Partner Center APIs provide auditing features so you can get a record of Partner Center activity.</span></span>

<span data-ttu-id="4333e-105">Můžete načíst záznamy o auditu za posledních 30 dní od aktuálního data nebo pro rozsah dat zadaný zahrnutím počátečního data a/nebo koncového data.</span><span class="sxs-lookup"><span data-stu-id="4333e-105">You can retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="4333e-106">Upozorňujeme ale, že z důvodů výkonu je dostupnost dat protokolu aktivit omezená na předchozí 90 dní.</span><span class="sxs-lookup"><span data-stu-id="4333e-106">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="4333e-107">Žádosti s počátečním datem větším než 90 dní před aktuálním datem obdrží výjimku špatné žádosti (kód chyby: 400) a příslušnou zprávu.</span><span class="sxs-lookup"><span data-stu-id="4333e-107">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="retrieve-audit-records"></a><span data-ttu-id="4333e-108">Načtení záznamů auditu</span><span class="sxs-lookup"><span data-stu-id="4333e-108">Retrieve audit records</span></span>

<span data-ttu-id="4333e-109">Získat podrobné záznamy o provedených auditech operací provedených partnerským uživatelem nebo aplikací:</span><span class="sxs-lookup"><span data-stu-id="4333e-109">Get detailed historical audit records of operations performed by a partner user or application:</span></span>

- [<span data-ttu-id="4333e-110">Získání záznamu o aktivitě Partnerského centra</span><span class="sxs-lookup"><span data-stu-id="4333e-110">Get a record of Partner Center activity</span></span>](get-a-record-of-partner-center-activity-by-user.md)
- [<span data-ttu-id="4333e-111">Auditování prostředků</span><span class="sxs-lookup"><span data-stu-id="4333e-111">Auditing resources</span></span>](auditing-resources.md)