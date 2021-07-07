---
title: Prostředky metadat smlouvy
description: Kolekce prostředků AgreementMetadata popisuje typy smlouvy, které mohou partneři použít k potvrzení přijetí zákazníkem.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: b930e3691b9d269ddb8d76ae18b6b26a217123c0
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025621"
---
# <a name="agreement-metadata-resources"></a>Prostředky metadat smlouvy

**Platí pro:** Partnerské centrum

**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Prostředek **AgreementMetaData** je aktuálně podporován Partnerské centrum ve veřejném cloudu Microsoftu. 

Kolekce **AgreementMetaData** poskytuje metadata o všech typech smlouvy. Partneři mohou tuto kolekci použít k potvrzení přijetí smluv zákazníkem. Kolekce **AgreementMetaData** vrací metadata pro oba typy smlouvy (**Smlouva o službách Microsoft Cloud** i **Smlouva se zákazníkem Microsoftu**).

## <a name="agreementmetadata"></a>AgreementMetaData

Vrácená metadata smlouvy zahrnují následující vlastnosti:

| Vlastnost      | Typ               | Description                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| ID šablony    | řetězec             | Jedinečný identifikátor šablony smlouvy                                       |
| typ          | řetězec             | Typ smlouvy. V současné době podporované hodnoty zahrnují **MicrosoftCloudAgreement** a **MicrosoftCustomerAgreement** (Preview). |
| odkaz na smlouvu | řetězec             | Adresa URL šablony smlouvy.                                                    |
