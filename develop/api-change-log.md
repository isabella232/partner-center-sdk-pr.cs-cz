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
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>Změny rozhraní REST API z prosince 2020 Partnerské centrum 2020

Změny v rozhraních REST API Partnerské centrum tady.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Vylepšení cen pro nárok na rozhraní API pro vzdělávací instituce



### <a name="what-has-changed"></a>Co se změnilo?

V současné době Partnerské centrum API získalo kvalifikaci GET a PUT pro ověření způsobilosti zákazníků v oblasti vzdělávání. Rozhraní GET Qualification API se nezmění. Do rozhraní PUT Qualification API jsme ale přidali případ vrácení.

- GET – nezmění se.
- PUT – přidá se případ vrácení.

Tato rozhraní API se na konci února 2021 vyřazena, aby byla nahrazena novými rozhraními API, jak je popsáno níže.

### <a name="scenarios-impacted"></a>Ovlivněné scénáře:

Nárok zákazníka na ceny za vzdělávání pro vybrané skladové položky

### <a name="detail-descriptions"></a>Podrobné popisy

Budou zavedena dvě nová rozhraní API pro kvalifikace GET a POST. Nová rozhraní API budou používat **kvalifikace,** nikoli **kvalifikace**. Rozhraní API budou k dispozici pro testování ve FY21 Q2.

#### <a name="get-qualifications"></a>GET – kvalifikace

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a>Příklad odpovědi:

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a>Pole odpovědi: 

- Hodnoty VettingStatus: Approved, Denied, InReview atd.

- Hodnoty VettingReason:
   - Není zákazníkem v oblasti vzdělávání
   - Už není zákazníkem v oblasti vzdělávání
   - Není zákazníkem v oblasti vzdělávání – po dokončení revize
   - Omezená možnost být zákazníkem v oblasti vzdělávání
   - Není to academic domain
   - Není oprávněná knihovna
   - Není oprávněným kachlem
 
#### <a name="post-qualifications"></a>Kvalifikace POST

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a>Příklad odpovědi:

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a>Další kroky

[Referenční informace k rozhraní REST API pro Partnerské centrum](partner-center-rest-api-reference.md)
