---
title: Referenční informace k rozhraní REST API pro Partnerské centrum
description: Přečtěte si, jak můžou partneři CSP používat rozhraní REST API služby partner Center k integraci svého softwaru CRM a fakturace se systémy Microsoftu pro lepší správu zákaznických účtů.
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 18621fdb94f91f066b69a11f7d557410d653787e
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548035"
---
# <a name="partner-center-rest-api-reference-to-rest-urls-rest-headers-rest-resources-and-rest-events"></a><span data-ttu-id="44519-103">Partnerské centrum REST API odkaz na adresy URL REST, záhlaví REST, prostředky REST a události REST.</span><span class="sxs-lookup"><span data-stu-id="44519-103">Partner Center REST API reference to REST URLs, REST headers, REST resources, and REST events</span></span>

<span data-ttu-id="44519-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="44519-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="partner-center-rest-api"></a><span data-ttu-id="44519-105">REST API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="44519-105">Partner Center REST API</span></span>

<span data-ttu-id="44519-106">partnerská REST API pomáhá partnerům Cloud Solution Provider (CSP) integrovat svůj stávající software CRM nebo fakturační software se systémy microsoftu, které spravují účty zákazníků, umísťují objednávky, spravují předplatná a zpracovávají žádosti o podporu.</span><span class="sxs-lookup"><span data-stu-id="44519-106">The Partner Center REST API helps Cloud Solution Provider (CSP) partners integrate their existing CRM or billing software with the Microsoft systems that manage customer accounts, place orders, manage subscriptions, and handle support requests.</span></span>

<span data-ttu-id="44519-107">Další informace o tom, co může rozhraní API provádět, včetně ukázkového kódu, najdete v tématu [scénáře](scenarios.md) , včetně přehledu na pozadí.</span><span class="sxs-lookup"><span data-stu-id="44519-107">For more information about what the API can do, including sample code, see the [Scenarios](scenarios.md) topic, including the background overview.</span></span>

<span data-ttu-id="44519-108">Než začnete s kódováním, přečtěte [si téma Začínáme](get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="44519-108">Before you begin coding, read the [Get started](get-started.md) topic.</span></span> <span data-ttu-id="44519-109">Tento článek obsahuje informace o nastavení testovacích a provozních účtů, získávání ověřování a hledání ukázkového kódu.</span><span class="sxs-lookup"><span data-stu-id="44519-109">This article contains information about setting up your test and production accounts, getting authentication working, and finding the sample code.</span></span>

<span data-ttu-id="44519-110">Referenční příručka, která vysvětluje každé rozhraní API, najdete v tématu [partner Center REST API](/rest/api/partner-center-rest/).</span><span class="sxs-lookup"><span data-stu-id="44519-110">For a reference guide explaining each API, see [Partner Center REST API](/rest/api/partner-center-rest/).</span></span>

## <a name="topics"></a><span data-ttu-id="44519-111">Témata</span><span class="sxs-lookup"><span data-stu-id="44519-111">Topics</span></span>

| <span data-ttu-id="44519-112">Téma</span><span class="sxs-lookup"><span data-stu-id="44519-112">Topic</span></span> | <span data-ttu-id="44519-113">Description</span><span class="sxs-lookup"><span data-stu-id="44519-113">Description</span></span> |
| ----- | ----------- |
| [<span data-ttu-id="44519-114">REST API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="44519-114">Partner Center REST API</span></span>](/rest/api/partner-center-rest/) | <span data-ttu-id="44519-115">Referenční informace o jednotlivých REST APIch dostupných pro partnerské Centrum.</span><span class="sxs-lookup"><span data-stu-id="44519-115">Reference of each REST API available for Partner Center.</span></span> |
| [<span data-ttu-id="44519-116">Adresy URL rozhraní REST pro Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="44519-116">Partner Center REST URLs</span></span>](partner-center-rest-urls.md) | <span data-ttu-id="44519-117">Definuje koncové body REST API pro různé verze partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="44519-117">Defines the REST API endpoints for different versions of Partner Center.</span></span> |
| [<span data-ttu-id="44519-118">Hlavičky rozhraní REST pro Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="44519-118">Partner Center REST headers</span></span>](headers.md) | <span data-ttu-id="44519-119">Definuje hlavičky žádosti a odpovědi, které používá REST API.</span><span class="sxs-lookup"><span data-stu-id="44519-119">Defines the request and response headers used by the REST API.</span></span> |
| [<span data-ttu-id="44519-120">Prostředky rozhraní REST pro Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="44519-120">Partner Center REST resources</span></span>](partner-center-rest-resources.md) | <span data-ttu-id="44519-121">Definuje konstrukce JSON, které reprezentují objekty potřebné k použití REST API.</span><span class="sxs-lookup"><span data-stu-id="44519-121">Defines the JSON constructs that represent the objects needed to use the REST API.</span></span> |
| [<span data-ttu-id="44519-122">Události rozhraní REST pro Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="44519-122">Partner Center REST events</span></span>](partner-center-webhook-events.md) | <span data-ttu-id="44519-123">Definuje události změny prostředku REST podporované Webhooky partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="44519-123">Defines the REST resource change events that are supported by Partner Center webhooks.</span></span> |
| [<span data-ttu-id="44519-124">Podporované jazyka a lokality pro Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="44519-124">Partner Center supported languages and locales</span></span>](partner-center-supported-languages-and-locales.md) | <span data-ttu-id="44519-125">Zobrazuje seznam národních prostředí, jazyků a kódů zemí a oblastí, které jsou podporované v rozhraních API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="44519-125">Lists the locales, languages, and country/region codes that are supported in the Partner Center APIs.</span></span> |
| [<span data-ttu-id="44519-126">Webhooky Partnerského centra</span><span class="sxs-lookup"><span data-stu-id="44519-126">Partner Center webhooks</span></span>](partner-center-webhooks.md) | <span data-ttu-id="44519-127">Jak přijímat události, ověřovat zpětné volání a používat rozhraní API Webhooku partnerského centra k vytvoření, zobrazení a aktualizaci registrace události.</span><span class="sxs-lookup"><span data-stu-id="44519-127">How to receive events, authenticate a callback, and use the Partner Center webhook APIs to create, view, and update an event registration.</span></span> |
