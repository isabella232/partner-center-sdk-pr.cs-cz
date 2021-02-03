---
title: Prostředky smlouvy
description: Prostředek smlouvy představuje smlouvu zákazníka v cloudu Microsoftu s podrobnostmi o certifikaci poskytované partnerem.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: d964b1c7c6d70814ef68e48f05611ecbb113c8fe
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/13/2020
ms.locfileid: "97767091"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a>Prostředky smlouvy, které představují zákaznickou smlouvu o cloudu Microsoftu

**Platí pro:**

- Partnerské centrum

Prostředek **smlouvy** je aktuálně podporovaný partnerským centrem jenom ve veřejném cloudu Microsoftu. Neplatí pro:

- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Prostředek **smlouvy** představuje zákaznickou smlouvu Microsoftu pro Cloud.

## <a name="agreement"></a>Smlouva

Prostředek **smlouvy** představuje podrobnosti o certifikaci poskytované partnerem.

| Vlastnost       | Typ   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | řetězec                         | Identifikátor objektu přihlášeného uživatele v partnerském tenantovi, který poskytuje potvrzení jménem partnerské organizace. Při použití ověřování aplikací a uživatelů k vytvoření prostředku smlouvy partnerské Centrum automaticky odvozuje hodnotu atributu **userId** z tokenu App + User.                                                                             |
| primaryContact | [Kontakt](./utility-resources.md#contact) | Informace o uživateli od organizace zákazníka, která smlouvu přijala, včetně:  **FirstName**, **LastName**, **email** a **phoneNumber** (volitelné). |
| dateAgreed     | řetězec ve formátu data a času UTC | Datum, kdy zákazník smlouvu přijal.                                 |
| templateId     |řetězec                          | Jedinečný identifikátor smlouvy, kterou zákazník přijal |
| typ           |řetězec                          | Typ smlouvy V současné době podporované hodnoty zahrnují **MicrosoftCloudAgreement** a **MicrosoftCustomerAgreement**.|
| agreementLink  | řetězec                         | Adresa URL šablony smlouvy                                                    |
