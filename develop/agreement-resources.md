---
title: Zdroje informací o smlouvě
description: Prostředek smlouvy představuje smlouvu se zákazníkem Microsoftu pro cloud s podrobnostmi o certifikaci poskytovanou partnerem.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: dc67d93a40cdced977412ff8151a661f6655c0fa1d079c8f1bc468f0f8b1eea2
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992466"
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
