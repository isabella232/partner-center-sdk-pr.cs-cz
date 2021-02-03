---
title: Stav přímého podepisování (přímé přijetí) zákaznické smlouvy.
description: Prostředek DirectSignedCustomerAgreementStatus představuje stav přímého podepisování (přímé přijetí) zákaznické smlouvy.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9c4fd12ac3319057f3c4034aa0c8d93dcda726c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766683"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a>Stav přímého podepisování (přímé přijetí) pro zákaznickou smlouvu

**Platí pro:**

- Partnerské centrum

Partner Center v současné době podporuje prostředek **DirectSignedCustomerAgreementStatus** jenom ve veřejném cloudu Microsoftu.

Tento prostředek *nelze použít* pro:

- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Prostředek **DirectSignedCustomerAgreementStatus** představuje stav přímého přijetí smlouvy se zákazníkem.

## <a name="directsignedcustomeragreementstatus"></a>DirectSignedCustomerAgreementStatus

Prostředek **DirectSignedCustomerAgreementStatus** obsahuje následující vlastnosti:

| Vlastnost       | Typ   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| Podepsaný | boolean | Určuje, jestli je zákazníkská smlouva od zákazníka přímo podepsaná (přijatá). |
