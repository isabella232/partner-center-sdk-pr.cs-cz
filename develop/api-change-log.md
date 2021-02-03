---
title: Protokol změn rozhraní REST API pro Partnerské centrum
description: Tato stránka obsahuje seznam změn v rozhraních REST API partnerského centra.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: 79359414276a1259117a8f506bbfae4441cdcbed
ms.sourcegitcommit: f8ca3a14a763013fefafd3262d0a740881d1d7b1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/17/2020
ms.locfileid: "97767666"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a><span data-ttu-id="1e9b3-103">Z prosince 2020 změny rozhraní REST API pro partnerský Center</span><span class="sxs-lookup"><span data-stu-id="1e9b3-103">December 2020 changes to Partner Center REST APIs</span></span>

<span data-ttu-id="1e9b3-104">Tady najdete změny rozhraní REST API pro partnerské Centrum.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-104">Check here for changes to Partner Center REST APIs.</span></span>

## <a name="enhancements-to-education-pricing-eligibility-apis"></a><span data-ttu-id="1e9b3-105">Vylepšení rozhraní API pro nárok na ceny pro vzdělávání</span><span class="sxs-lookup"><span data-stu-id="1e9b3-105">Enhancements to education pricing Eligibility APIs</span></span>



### <a name="what-has-changed"></a><span data-ttu-id="1e9b3-106">Co se změnilo?</span><span class="sxs-lookup"><span data-stu-id="1e9b3-106">What has changed?</span></span>

<span data-ttu-id="1e9b3-107">V současné době má rozhraní API partnerského centra získat a dát kvalifikaci k ověření nároku na vzdělávání zákazníků.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-107">Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility.</span></span> <span data-ttu-id="1e9b3-108">Rozhraní API pro získání kvalifikace nebude nijak nijak měnit.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-108">There will be no changes to the GET Qualification API.</span></span> <span data-ttu-id="1e9b3-109">Přidali jsme ale návratový případ do rozhraní API kvalifikace PUT.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-109">However, we’ve added a return case to the PUT Qualification API.</span></span>

- <span data-ttu-id="1e9b3-110">ZÍSKAT změny.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-110">GET - doesn't change.</span></span> [<span data-ttu-id="1e9b3-111">Aktuální článek o rozhraní API</span><span class="sxs-lookup"><span data-stu-id="1e9b3-111">Current API article</span></span>](get-a-customer-s-qualification.md)
- <span data-ttu-id="1e9b3-112">Přidá se případ vrácení vložení.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-112">PUT - return case will be added.</span></span> [<span data-ttu-id="1e9b3-113">Aktuální článek o rozhraní API</span><span class="sxs-lookup"><span data-stu-id="1e9b3-113">Current API article</span></span>](update-a-customer-s-qualification.md)

<span data-ttu-id="1e9b3-114">Tato rozhraní API budou vyřazena na konci února 2021, která budou nahrazena novými rozhraními API, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-114">These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.</span></span>

### <a name="scenarios-impacted"></a><span data-ttu-id="1e9b3-115">Ovlivněné scénáře:</span><span class="sxs-lookup"><span data-stu-id="1e9b3-115">Scenarios impacted:</span></span>

<span data-ttu-id="1e9b3-116">Nárok zákazníků na ceny pro vzdělávání na vybraných SKU</span><span class="sxs-lookup"><span data-stu-id="1e9b3-116">Customer eligibility for education pricing on select SKUs</span></span>

### <a name="detail-descriptions"></a><span data-ttu-id="1e9b3-117">Popisy podrobností</span><span class="sxs-lookup"><span data-stu-id="1e9b3-117">Detail descriptions</span></span>

<span data-ttu-id="1e9b3-118">Budou zavedena dvě nová rozhraní API GET a POST.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-118">Two new GET and POST Qualifications APIs will be introduced.</span></span> <span data-ttu-id="1e9b3-119">Nová rozhraní API budou používat **kvalifikaci**, nikoli **kvalifikaci**.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-119">The new APIs will be using **Qualifications**, not **Qualification**.</span></span> <span data-ttu-id="1e9b3-120">Rozhraní API budou k dispozici pro testování v FY21 Q2.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-120">The APIs will be available for testing in FY21 Q2.</span></span>

#### <a name="get-qualifications"></a><span data-ttu-id="1e9b3-121">ZÍSKAT kvalifikaci</span><span class="sxs-lookup"><span data-stu-id="1e9b3-121">GET Qualifications</span></span>

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a><span data-ttu-id="1e9b3-122">Příklad odpovědi:</span><span class="sxs-lookup"><span data-stu-id="1e9b3-122">Response example:</span></span>

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a><span data-ttu-id="1e9b3-123">Pole odpovědi:</span><span class="sxs-lookup"><span data-stu-id="1e9b3-123">Response fields:</span></span> 

- <span data-ttu-id="1e9b3-124">Hodnoty VettingStatus: schváleno, zamítnuto, inrevize atd.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-124">VettingStatus values: Approved, Denied, InReview, etc.</span></span>

- <span data-ttu-id="1e9b3-125">VettingReason hodnoty:</span><span class="sxs-lookup"><span data-stu-id="1e9b3-125">VettingReason values:</span></span>
   - <span data-ttu-id="1e9b3-126">Nejedná se o zákazníka vzdělávání.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-126">Not an Education Customer</span></span>
   - <span data-ttu-id="1e9b3-127">Už není zákazník pro vzdělávání.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-127">No longer an Education Customer</span></span>
   - <span data-ttu-id="1e9b3-128">Nejedná se o zákazníka vzdělávání – po kontrole</span><span class="sxs-lookup"><span data-stu-id="1e9b3-128">Not an Education Customer - After Review</span></span>
   - <span data-ttu-id="1e9b3-129">Omezené na zákazníka vzdělávání</span><span class="sxs-lookup"><span data-stu-id="1e9b3-129">Restricted being an Education Customer</span></span>
   - <span data-ttu-id="1e9b3-130">Nejedná se o akademickou doménu.</span><span class="sxs-lookup"><span data-stu-id="1e9b3-130">Not an Academic Domain</span></span>
   - <span data-ttu-id="1e9b3-131">Neoprávněná knihovna</span><span class="sxs-lookup"><span data-stu-id="1e9b3-131">Not an eligible Library</span></span>
   - <span data-ttu-id="1e9b3-132">Nejedná se o opravňující Museum</span><span class="sxs-lookup"><span data-stu-id="1e9b3-132">Not an eligible Museum</span></span>
 
#### <a name="post-qualifications"></a><span data-ttu-id="1e9b3-133">Vystavení kvalifikace</span><span class="sxs-lookup"><span data-stu-id="1e9b3-133">POST Qualifications</span></span>

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a><span data-ttu-id="1e9b3-134">Příklad odpovědi:</span><span class="sxs-lookup"><span data-stu-id="1e9b3-134">Response example:</span></span>

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a><span data-ttu-id="1e9b3-135">Další kroky</span><span class="sxs-lookup"><span data-stu-id="1e9b3-135">Next steps</span></span>

[<span data-ttu-id="1e9b3-136">Referenční informace k rozhraní REST API pro Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="1e9b3-136">Partner Center REST API reference</span></span>](partner-center-rest-api-reference.md)
