---
title: Prostředky profilu
description: Popisuje chování profilů poskytovatele cloudových řešení.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e0561278995f4f9747320866b51de57efea8f712
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766972"
---
# <a name="profile-resources"></a>Prostředky profilu

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Popisuje chování profilů poskytovatele cloudových řešení.

## <a name="billingprofile"></a>BillingProfile

Popisuje Fakturační profil partnera.

| Vlastnost            | Typ                                                           | Description                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| Společnosti         | řetězec                                                         | Název fakturační společnosti                                   |
| adresa             | [Adresa](utility-resources.md#address)                       | Fakturační adresa společnosti nebo organizace. |
| primaryContact      | [Kontakt](utility-resources.md#contact)                       | Primární kontakt společnosti nebo organizace.        |
| purchaseOrderNumber | řetězec                                                         | Číslo nákupní objednávky společnosti nebo organizace.        |
| taxId               | řetězec                                                         | Daňové ID společnosti nebo organizace.                       |
| billingCurrency     | řetězec                                                         | Měna, kterou používá společnost nebo organizace.           |
| Typ souboru         | řetězec                                                         | Typ partnerského profilu.                                   |
| odkazy               | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky odpovídající profilu.            |
| atributy          | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu.       |

## <a name="legalbusinessprofile"></a>LegalBusinessProfile

Popisuje oficiální obchodní profil partnera.

| Vlastnost               | Typ                                                           | Description                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Společnosti            | řetězec                                                         | Platný název společnosti.                                                                                                                                              |
| adresa                | [Adresa](utility-resources.md#address)                       | Adresa společnosti nebo organizace.                                                                                                                          |
| primaryContact         | [Kontakt](utility-resources.md#contact)                       | Primární kontakt společnosti nebo organizace.                                                                                                                 |
| companyApproverAddress | [Adresa](utility-resources.md#address)                       | Adresa schvalovatele společnosti                                                                                                                                        |
| companyApproverEmail   | řetězec                                                         | E-mail schvalovatele společnosti                                                                                                                                          |
| vettingStatus          | řetězec                                                         | Stav dozvíte ČSFD Tato hodnota představuje řetězcovou reprezentaci jednoho z názvů členů nalezených v [**VettingStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus).           |
| vettingSubStatus       | řetězec                                                         | Dílčí stav dozvíte ČSFD Tato hodnota představuje řetězcovou reprezentaci jednoho z názvů členů nalezených v [**VettingSubStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus). |
| Typ souboru            | řetězec                                                         | Typ partnerského profilu.                                                                                                                                            |
| odkazy                  | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky odpovídající profilu.                                                                                                                     |
| atributy             | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu.                                                                                                                |

## <a name="mpnprofile"></a>MpnProfile

Popisuje profil Microsoft Partner Network partnera.

| Vlastnost    | Typ                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | řetězec                                                         | Název společnosti nebo organizace.                     |
| mpnId       | řetězec                                                         | ID Microsoft Partner Network.                     |
| Typ souboru | řetězec                                                         | Typ partnerského profilu.                             |
| odkazy       | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky odpovídající profilu.      |
| atributy  | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu. |

## <a name="organizationprofile"></a>OrganizationProfile

Popisuje profil organizace partnera.

| Vlastnost       | Typ                                                           | Description                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | řetězec                                                         | ID organizace.                                                 |
| Společnosti    | řetězec                                                         | Název společnosti nebo organizace.                               |
| defaultAddress | [Adresa](utility-resources.md#address)                       | Výchozí adresa společnosti nebo organizace.                    |
| tenantId       | řetězec                                                         | Identifikátor tenanta                                                 |
| doména         | řetězec                                                         | Doména společnosti nebo organizace.                                  |
| e-mail          | řetězec                                                         | Získá nebo nastaví nadřazený odběr.                                  |
| language       | řetězec                                                         | Preferovaný jazyk pro komunikaci.                              |
| jazyková verze        | řetězec                                                         | Upřednostňovaná jazyková verze pro komunikaci a měnu, jako je "en-US". |
| Typ souboru    | řetězec                                                         | Typ partnerského profilu.                                              |
| odkazy          | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky odpovídající profilu.                       |
| atributy     | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu.                  |

## <a name="supportprofile"></a>SupportProfile

Popisuje profil podpory partnera.

| Vlastnost    | Typ                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| e-mail       | řetězec                                                         | E-mailová adresa přidružená k profilu        |
| Link   | řetězec                                                         | Telefonní číslo přidružené k profilu         |
| webu     | řetězec                                                         | Web podpory.                                  |
| Typ souboru | řetězec                                                         | Typ partnerského profilu.                             |
| odkazy       | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky odpovídající profilu.      |
| atributy  | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu. |

