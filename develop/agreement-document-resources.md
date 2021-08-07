---
title: Prostředky dokumentu smlouvy
description: Prostředek AgreementDocument je dokument s smlouvou Microsoftu pro náhled a stažení. Podporuje ho Partnerská centra ve veřejném cloudu Microsoftu.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: eddde1e8072c6aeeee814b52f46c7648d870b6ba63c09b20e4270b17f8386383
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991102"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a>Prostředky dokumentů smlouvy podporované partnerským centrem ve veřejném cloudu Microsoftu

**Platí pro**: partnerské Centrum

Nevztahuje **se na**: partnerské Centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Partner Center v současné době podporuje prostředek **AgreementDocument** jenom ve veřejném cloudu Microsoftu.

Prostředek **AgreementDocument** představuje dokument smlouvy Microsoft, který je k dispozici pro náhled a stažení.

## <a name="agreementdocument"></a>AgreementDocument

Prostředek **AgreementDocument** obsahuje následující vlastnosti:

| Vlastnost       | Typ   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| country | řetězec | Země nebo trh, na který se vztahuje tento dokument. |
| language | řetězec | Jazyk, ve kterém je tento dokument lokalizován. |
| displayUri | řetězec | Odkaz na náhled dokumentu smlouvy v prohlížeči  |
| downloadUri |řetězec | odkaz ke stažení dokumentu smlouvy (ve formátu Microsoft Word). |
