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
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>Z prosince 2020 změny rozhraní REST API pro partnerský Center

Tady najdete změny rozhraní REST API pro partnerské Centrum.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Vylepšení rozhraní API pro nárok na ceny pro vzdělávání



### <a name="what-has-changed"></a>Co se změnilo?

V současné době má rozhraní API partnerského centra získat a dát kvalifikaci k ověření nároku na vzdělávání zákazníků. Rozhraní API pro získání kvalifikace nebude nijak nijak měnit. Přidali jsme ale návratový případ do rozhraní API kvalifikace PUT.

- ZÍSKAT změny. [Aktuální článek o rozhraní API](get-a-customer-s-qualification.md)
- Přidá se případ vrácení vložení. [Aktuální článek o rozhraní API](update-a-customer-s-qualification.md)

Tato rozhraní API budou vyřazena na konci února 2021, která budou nahrazena novými rozhraními API, jak je popsáno níže.

### <a name="scenarios-impacted"></a>Ovlivněné scénáře:

Nárok zákazníků na ceny pro vzdělávání na vybraných SKU

### <a name="detail-descriptions"></a>Popisy podrobností

Budou zavedena dvě nová rozhraní API GET a POST. Nová rozhraní API budou používat **kvalifikaci**, nikoli **kvalifikaci**. Rozhraní API budou k dispozici pro testování v FY21 Q2.

#### <a name="get-qualifications"></a>ZÍSKAT kvalifikaci

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

- Hodnoty VettingStatus: schváleno, zamítnuto, inrevize atd.

- VettingReason hodnoty:
   - Nejedná se o zákazníka vzdělávání.
   - Už není zákazník pro vzdělávání.
   - Nejedná se o zákazníka vzdělávání – po kontrole
   - Omezené na zákazníka vzdělávání
   - Nejedná se o akademickou doménu.
   - Neoprávněná knihovna
   - Nejedná se o opravňující Museum
 
#### <a name="post-qualifications"></a>Vystavení kvalifikace

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
