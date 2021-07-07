---
title: Stav přímého podepisování (přímé přijetí) zákaznické smlouvy.
description: Prostředek DirectSignedCustomerAgreementStatus představuje stav přímého podepisování (přímé přijetí) zákaznické smlouvy.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: d4d97667b5fd6b92c85889f1288dd770c2d1c035
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973107"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a>Stav přímého podepisování (přímé přijetí) pro zákaznickou smlouvu

**Platí pro**: partnerské Centrum

Nevztahuje **se na**: partnerské Centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Partner Center v současné době podporuje prostředek **DirectSignedCustomerAgreementStatus** jenom ve veřejném cloudu Microsoftu.

Prostředek **DirectSignedCustomerAgreementStatus** představuje stav přímého přijetí smlouvy se zákazníkem.

## <a name="directsignedcustomeragreementstatus"></a>DirectSignedCustomerAgreementStatus

Prostředek **DirectSignedCustomerAgreementStatus** obsahuje následující vlastnosti:

| Vlastnost       | Typ   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| Podepsaný | boolean | Určuje, jestli je zákazníkská smlouva od zákazníka přímo podepsaná (přijatá). |
