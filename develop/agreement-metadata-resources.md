---
title: Prostředky metadat smlouvy
description: Kolekce prostředků AgreementMetadata popisuje typy smluv, které mohou partneři použít k potvrzení přijetí zákazníka.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 7c09dc2a8dd88e3d3a6a7925f6f61737cbbd410eabda6ecb4c3ead13d889de04
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991255"
---
# <a name="agreement-metadata-resources"></a>Prostředky metadat smlouvy

**Platí pro**: partnerské Centrum

Nevztahuje **se na**: partnerské Centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Partner Center v současné době podporuje prostředek **AgreementMetaData** jenom ve veřejném cloudu Microsoftu. 

Kolekce **AgreementMetaData** poskytuje metadata o všech typech smluv. Partneři mohou tuto kolekci použít k potvrzení přijetí smlouvy od zákazníků. Kolekce **AgreementMetaData** vrací metadata pro oba typy smluv (**Microsoft Cloud smlouva** a **smlouvy o zákaznících Microsoftu**).

## <a name="agreementmetadata"></a>AgreementMetaData

Vrácená metadata smlouvy obsahují následující vlastnosti:

| Vlastnost      | Typ               | Description                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | řetězec             | Jedinečný identifikátor šablony smlouvy                                       |
| typ          | řetězec             | Typ smlouvy V současné době podporované hodnoty zahrnují **MicrosoftCloudAgreement** a **MicrosoftCustomerAgreement** (Preview). |
| agreementLink | řetězec             | Adresa URL šablony smlouvy                                                    |
