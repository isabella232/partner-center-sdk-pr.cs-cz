---
title: Referenční informace k rozhraní REST API pro Partnerské centrum
description: Přečtěte si, jak můžou partneři CSP používat rozhraní REST API služby partner Center k integraci svého softwaru CRM a fakturace se systémy Microsoftu pro lepší správu zákaznických účtů.
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 3f83b2b73c3480f76646cae4fcbbcbacd31d4b3f
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/11/2020
ms.locfileid: "97767065"
---
# <a name="partner-center-rest-api-reference-to-rest-urls-rest-headers-rest-resources-and-rest-events"></a><span data-ttu-id="922c4-103">Partnerské centrum REST API odkaz na adresy URL REST, záhlaví REST, prostředky REST a události REST.</span><span class="sxs-lookup"><span data-stu-id="922c4-103">Partner Center REST API reference to REST URLs, REST headers, REST resources, and REST events</span></span>

<span data-ttu-id="922c4-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="922c4-104">**Applies to:**</span></span>

- <span data-ttu-id="922c4-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="922c4-105">Partner Center</span></span>
- <span data-ttu-id="922c4-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="922c4-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="922c4-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="922c4-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="922c4-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="922c4-108">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="partner-center-rest-api"></a><span data-ttu-id="922c4-109">REST API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="922c4-109">Partner Center REST API</span></span>

<span data-ttu-id="922c4-110">Partnerská centra REST API pomáhají partnerům poskytovatele Cloud Solution Provider integrovat svůj stávající Software CRM nebo fakturace se systémy Microsoftu, které spravují účty zákazníků, umísťují objednávky, spravují předplatná a zpracovávají žádosti o podporu.</span><span class="sxs-lookup"><span data-stu-id="922c4-110">The Partner Center REST API helps Cloud Solution Provider (CSP) partners integrate their existing CRM or billing software with the Microsoft systems that manage customer accounts, place orders, manage subscriptions, and handle support requests.</span></span>

<span data-ttu-id="922c4-111">Další informace o tom, co může rozhraní API provádět, včetně ukázkového kódu, najdete v tématu [scénáře](scenarios.md) , včetně přehledu na pozadí.</span><span class="sxs-lookup"><span data-stu-id="922c4-111">For more information about what the API can do, including sample code, see the [Scenarios](scenarios.md) topic, including the background overview.</span></span>

<span data-ttu-id="922c4-112">Než začnete s kódováním, přečtěte [si téma Začínáme](get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="922c4-112">Before you begin coding, read the [Get started](get-started.md) topic.</span></span> <span data-ttu-id="922c4-113">Tento článek obsahuje informace o nastavení testovacích a provozních účtů, získávání ověřování a hledání ukázkového kódu.</span><span class="sxs-lookup"><span data-stu-id="922c4-113">This article contains information about setting up your test and production accounts, getting authentication working, and finding the sample code.</span></span>

## <a name="topics"></a><span data-ttu-id="922c4-114">Témata</span><span class="sxs-lookup"><span data-stu-id="922c4-114">Topics</span></span>

| <span data-ttu-id="922c4-115">Téma</span><span class="sxs-lookup"><span data-stu-id="922c4-115">Topic</span></span> | <span data-ttu-id="922c4-116">Description</span><span class="sxs-lookup"><span data-stu-id="922c4-116">Description</span></span> |
| ----- | ----------- |
| [<span data-ttu-id="922c4-117">Adresy URL rozhraní REST pro Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="922c4-117">Partner Center REST URLs</span></span>](partner-center-rest-urls.md) | <span data-ttu-id="922c4-118">Definuje koncové body REST API pro různé verze partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="922c4-118">Defines the REST API endpoints for different versions of Partner Center.</span></span> |
| [<span data-ttu-id="922c4-119">Hlavičky rozhraní REST pro Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="922c4-119">Partner Center REST headers</span></span>](headers.md) | <span data-ttu-id="922c4-120">Definuje hlavičky žádosti a odpovědi, které používá REST API.</span><span class="sxs-lookup"><span data-stu-id="922c4-120">Defines the request and response headers used by the REST API.</span></span> |
| [<span data-ttu-id="922c4-121">Prostředky rozhraní REST pro Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="922c4-121">Partner Center REST resources</span></span>](partner-center-rest-resources.md) | <span data-ttu-id="922c4-122">Definuje konstrukce JSON, které reprezentují objekty potřebné k použití REST API.</span><span class="sxs-lookup"><span data-stu-id="922c4-122">Defines the JSON constructs that represent the objects needed to use the REST API.</span></span> |
| [<span data-ttu-id="922c4-123">Události rozhraní REST pro Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="922c4-123">Partner Center REST events</span></span>](partner-center-webhook-events.md) | <span data-ttu-id="922c4-124">Definuje události změny prostředku REST podporované Webhooky partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="922c4-124">Defines the REST resource change events that are supported by Partner Center webhooks.</span></span> |
| [<span data-ttu-id="922c4-125">Podporované jazyka a lokality pro Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="922c4-125">Partner Center supported languages and locales</span></span>](partner-center-supported-languages-and-locales.md) | <span data-ttu-id="922c4-126">Zobrazuje seznam národních prostředí, jazyků a kódů zemí a oblastí, které jsou podporované v rozhraních API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="922c4-126">Lists the locales, languages, and country/region codes that are supported in the Partner Center APIs.</span></span> |
| [<span data-ttu-id="922c4-127">Webhooky Partnerského centra</span><span class="sxs-lookup"><span data-stu-id="922c4-127">Partner Center webhooks</span></span>](partner-center-webhooks.md) | <span data-ttu-id="922c4-128">Jak přijímat události, ověřovat zpětné volání a používat rozhraní API Webhooku partnerského centra k vytvoření, zobrazení a aktualizaci registrace události.</span><span class="sxs-lookup"><span data-stu-id="922c4-128">How to receive events, authenticate a callback, and use the Partner Center webhook APIs to create, view, and update an event registration.</span></span> |