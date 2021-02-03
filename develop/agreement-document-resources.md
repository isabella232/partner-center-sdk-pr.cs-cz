---
title: Prostředky dokumentu smlouvy
description: Prostředek AgreementDocument je dokument s smlouvou Microsoftu pro náhled a stažení. Podporuje ho Partnerská centra ve veřejném cloudu Microsoftu.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 4805d25b0838bf922b81bebd998810c3f6a809c3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/13/2020
ms.locfileid: "97767094"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a>Prostředky dokumentů smlouvy podporované partnerským centrem ve veřejném cloudu Microsoftu

**Platí pro:**

- Partnerské centrum

Partner Center v současné době podporuje prostředek **AgreementDocument** jenom ve *veřejném cloudu Microsoftu*. Tento prostředek se nedá použít pro:

- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Prostředek **AgreementDocument** představuje dokument smlouvy Microsoft, který je k dispozici pro náhled a stažení.

## <a name="agreementdocument"></a>AgreementDocument

Prostředek **AgreementDocument** obsahuje následující vlastnosti:

| Vlastnost       | Typ   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| country | řetězec | Země nebo trh, na který se vztahuje tento dokument. |
| language | řetězec | Jazyk, ve kterém je tento dokument lokalizován. |
| displayUri | řetězec | Odkaz na náhled dokumentu smlouvy v prohlížeči  |
| downloadUri |řetězec | Odkaz ke stažení dokumentu smlouvy (ve formátu aplikace Microsoft Word). |
