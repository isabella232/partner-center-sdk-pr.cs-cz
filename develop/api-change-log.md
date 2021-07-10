---
title: Protokol změn rozhraní REST API pro Partnerské centrum
description: Tato stránka obsahuje seznam změn v rozhraních PARTNERSKÉ CENTRUM REST API.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: d4f7f034a36a26b6219086ca952b189f7a313ef7
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/09/2021
ms.locfileid: "113571991"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a><span data-ttu-id="63b0b-103">Změny rozhraní REST API z prosince 2020 Partnerské centrum 2020</span><span class="sxs-lookup"><span data-stu-id="63b0b-103">December 2020 changes to Partner Center REST APIs</span></span>

<span data-ttu-id="63b0b-104">Změny v rozhraních REST API Partnerské centrum tady.</span><span class="sxs-lookup"><span data-stu-id="63b0b-104">Check here for changes to Partner Center REST APIs.</span></span>

## <a name="enhancements-to-education-pricing-eligibility-apis"></a><span data-ttu-id="63b0b-105">Vylepšení cen pro nárok na rozhraní API pro vzdělávací instituce</span><span class="sxs-lookup"><span data-stu-id="63b0b-105">Enhancements to education pricing Eligibility APIs</span></span>



### <a name="what-has-changed"></a><span data-ttu-id="63b0b-106">Co se změnilo?</span><span class="sxs-lookup"><span data-stu-id="63b0b-106">What has changed?</span></span>

<span data-ttu-id="63b0b-107">V současné době Partnerské centrum API získalo kvalifikaci GET a PUT pro ověření způsobilosti zákazníků v oblasti vzdělávání.</span><span class="sxs-lookup"><span data-stu-id="63b0b-107">Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility.</span></span> <span data-ttu-id="63b0b-108">Rozhraní GET Qualification API se nezmění.</span><span class="sxs-lookup"><span data-stu-id="63b0b-108">There will be no changes to the GET Qualification API.</span></span> <span data-ttu-id="63b0b-109">Do rozhraní PUT Qualification API jsme ale přidali případ vrácení.</span><span class="sxs-lookup"><span data-stu-id="63b0b-109">However, we’ve added a return case to the PUT Qualification API.</span></span>

- <span data-ttu-id="63b0b-110">GET – nezmění se.</span><span class="sxs-lookup"><span data-stu-id="63b0b-110">GET - doesn't change.</span></span>
- <span data-ttu-id="63b0b-111">PUT – přidá se případ vrácení.</span><span class="sxs-lookup"><span data-stu-id="63b0b-111">PUT - return case will be added.</span></span>

<span data-ttu-id="63b0b-112">Tato rozhraní API se na konci února 2021 vyřazena, aby byla nahrazena novými rozhraními API, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="63b0b-112">These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.</span></span>

### <a name="scenarios-impacted"></a><span data-ttu-id="63b0b-113">Ovlivněné scénáře:</span><span class="sxs-lookup"><span data-stu-id="63b0b-113">Scenarios impacted:</span></span>

<span data-ttu-id="63b0b-114">Nárok zákazníka na ceny za vzdělávání pro vybrané skladové položky</span><span class="sxs-lookup"><span data-stu-id="63b0b-114">Customer eligibility for education pricing on select SKUs</span></span>

### <a name="detail-descriptions"></a><span data-ttu-id="63b0b-115">Podrobné popisy</span><span class="sxs-lookup"><span data-stu-id="63b0b-115">Detail descriptions</span></span>

<span data-ttu-id="63b0b-116">Budou zavedena dvě nová rozhraní API pro kvalifikace GET a POST.</span><span class="sxs-lookup"><span data-stu-id="63b0b-116">Two new GET and POST Qualifications APIs will be introduced.</span></span> <span data-ttu-id="63b0b-117">Nová rozhraní API budou používat **kvalifikace,** nikoli **kvalifikace**.</span><span class="sxs-lookup"><span data-stu-id="63b0b-117">The new APIs will be using **Qualifications**, not **Qualification**.</span></span> <span data-ttu-id="63b0b-118">Rozhraní API budou k dispozici pro testování ve FY21 Q2.</span><span class="sxs-lookup"><span data-stu-id="63b0b-118">The APIs will be available for testing in FY21 Q2.</span></span>

#### <a name="get-qualifications"></a><span data-ttu-id="63b0b-119">GET – kvalifikace</span><span class="sxs-lookup"><span data-stu-id="63b0b-119">GET Qualifications</span></span>

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a><span data-ttu-id="63b0b-120">Příklad odpovědi:</span><span class="sxs-lookup"><span data-stu-id="63b0b-120">Response example:</span></span>

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a><span data-ttu-id="63b0b-121">Pole odpovědi:</span><span class="sxs-lookup"><span data-stu-id="63b0b-121">Response fields:</span></span> 

- <span data-ttu-id="63b0b-122">Hodnoty VettingStatus: Approved, Denied, InReview atd.</span><span class="sxs-lookup"><span data-stu-id="63b0b-122">VettingStatus values: Approved, Denied, InReview, etc.</span></span>

- <span data-ttu-id="63b0b-123">Hodnoty VettingReason:</span><span class="sxs-lookup"><span data-stu-id="63b0b-123">VettingReason values:</span></span>
   - <span data-ttu-id="63b0b-124">Není zákazníkem v oblasti vzdělávání</span><span class="sxs-lookup"><span data-stu-id="63b0b-124">Not an Education Customer</span></span>
   - <span data-ttu-id="63b0b-125">Už není zákazníkem v oblasti vzdělávání</span><span class="sxs-lookup"><span data-stu-id="63b0b-125">No longer an Education Customer</span></span>
   - <span data-ttu-id="63b0b-126">Není zákazníkem v oblasti vzdělávání – po dokončení revize</span><span class="sxs-lookup"><span data-stu-id="63b0b-126">Not an Education Customer - After Review</span></span>
   - <span data-ttu-id="63b0b-127">Omezená možnost být zákazníkem v oblasti vzdělávání</span><span class="sxs-lookup"><span data-stu-id="63b0b-127">Restricted being an Education Customer</span></span>
   - <span data-ttu-id="63b0b-128">Není to academic domain</span><span class="sxs-lookup"><span data-stu-id="63b0b-128">Not an Academic Domain</span></span>
   - <span data-ttu-id="63b0b-129">Není oprávněná knihovna</span><span class="sxs-lookup"><span data-stu-id="63b0b-129">Not an eligible Library</span></span>
   - <span data-ttu-id="63b0b-130">Není oprávněným kachlem</span><span class="sxs-lookup"><span data-stu-id="63b0b-130">Not an eligible Museum</span></span>
 
#### <a name="post-qualifications"></a><span data-ttu-id="63b0b-131">Kvalifikace POST</span><span class="sxs-lookup"><span data-stu-id="63b0b-131">POST Qualifications</span></span>

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a><span data-ttu-id="63b0b-132">Příklad odpovědi:</span><span class="sxs-lookup"><span data-stu-id="63b0b-132">Response example:</span></span>

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a><span data-ttu-id="63b0b-133">Další kroky</span><span class="sxs-lookup"><span data-stu-id="63b0b-133">Next steps</span></span>

[<span data-ttu-id="63b0b-134">Referenční informace k rozhraní REST API pro Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="63b0b-134">Partner Center REST API reference</span></span>](partner-center-rest-api-reference.md)
