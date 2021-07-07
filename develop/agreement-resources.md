---
title: Zdroje informací o smlouvě
description: Prostředek smlouvy představuje smlouvu se zákazníkem Microsoftu pro cloud s podrobnostmi o certifikaci poskytovanou partnerem.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 5fa196e711d9ff899b61ba20e75edd92749165e5
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025612"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a>Prostředky smlouvy představující smlouvu se zákazníkem Microsoftu pro cloud

**Platí pro:** Partnerské centrum

**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Prostředek **smlouvy** je aktuálně podporován Partnerské centrum ve veřejném cloudu Microsoftu.

Prostředek **smlouvy** představuje smlouvu se zákazníkem Microsoftu pro cloud.

## <a name="agreement"></a>Smlouva

Prostředek **smlouvy** představuje podrobnosti o certifikaci poskytované partnerem.

| Vlastnost       | Typ   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | řetězec                         | Identifikátor objektu přihlášeného uživatele v partnerském tenantovi, který poskytuje potvrzení jménem partnerské organizace. Při použití ověřování aplikací a uživatelů k vytvoření prostředku smlouvy Partnerské centrum automaticky odvodí hodnotu **atributu userId** z tokenu App+User.                                                                             |
| primaryContact | [Kontakt](./utility-resources.md#contact) | Informace o uživateli z organizace zákazníka, který smlouvu přijal, včetně:  **firstName**, **lastName**, **email** a **phoneNumber** (volitelné). |
| datum odgreed     | řetězec ve formátu data a času UTC | Datum, kdy zákazník smlouvu přijal.                                 |
| ID šablony     |řetězec                          | Jedinečný identifikátor smlouvy, kterou zákazník přijal |
| typ           |řetězec                          | Typ smlouvy. V současné době podporované hodnoty zahrnují **MicrosoftCloudAgreement** a **MicrosoftCustomerAgreement**.|
| odkaz na smlouvu  | řetězec                         | Adresa URL šablony smlouvy.                                                    |
