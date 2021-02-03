---
title: Prostředky metadat smlouvy
description: Kolekce prostředků AgreementMetadata popisuje typy smluv, které mohou partneři použít k potvrzení přijetí zákazníka.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36ba2aa2f78552dc9a835168b5bbd5b6a3ce47f3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766697"
---
# <a name="agreement-metadata-resources"></a>Prostředky metadat smlouvy

**Platí pro:**

- Partnerské centrum

Partner Center v současné době podporuje prostředek **AgreementMetaData** jenom ve *veřejném cloudu Microsoftu*. Tento prostředek se nedá použít pro:

- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Kolekce **AgreementMetaData** poskytuje metadata o všech typech smluv. Partneři mohou tuto kolekci použít k potvrzení přijetí smlouvy od zákazníků. Kolekce **AgreementMetaData** vrací metadata pro oba typy smluv (**Microsoft Cloud smlouva** a **smlouvy o zákaznících Microsoftu**).

## <a name="agreementmetadata"></a>AgreementMetaData

Vrácená metadata smlouvy obsahují následující vlastnosti:

| Vlastnost      | Typ               | Description                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | řetězec             | Jedinečný identifikátor šablony smlouvy                                       |
| typ          | řetězec             | Typ smlouvy V současné době podporované hodnoty zahrnují **MicrosoftCloudAgreement** a **MicrosoftCustomerAgreement** (Preview). |
| agreementLink | řetězec             | Adresa URL šablony smlouvy                                                    |
