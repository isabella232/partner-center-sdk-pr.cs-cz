---
title: Stav přímého podepisování (přímé přijetí) zákaznické smlouvy.
description: Prostředek DirectSignedCustomerAgreementStatus představuje stav přímého podepisování (přímé přijetí) zákaznické smlouvy.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 3ca272e81a91d0f27b8c01104f6b26230327b772517b76268dbfc5014830b915
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995182"
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
