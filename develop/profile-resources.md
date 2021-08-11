---
title: Prostředky profilu
description: popisuje chování profilů Cloud Solution Provider.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8d4c091e186b7a3ad13aee7202b3d992af95db8db50acd40a5ade496d7087359
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997307"
---
# <a name="profile-resources"></a>Prostředky profilu

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

popisuje chování profilů Cloud Solution Provider.

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
| mpnId       | řetězec                                                         | ID Microsoft Partner Network (MPN).                     |
| Typ souboru | řetězec                                                         | Typ partnerského profilu.                             |
| odkazy       | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky odpovídající profilu.      |
| atributy  | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu. |

## <a name="organizationprofile"></a>OrganizationProfile

Popisuje profil organizace partnera.

| Vlastnost       | Typ                                                           | Description                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | řetězec                                                         | ID organizace.                                                 |
| Companyname    | řetězec                                                         | Název společnosti nebo organizace.                               |
| výchozí_adresa | [Adresa](utility-resources.md#address)                       | Výchozí adresa společnosti nebo organizace.                    |
| ID tenanta       | řetězec                                                         | Identifikátor tenanta.                                                 |
| doména         | řetězec                                                         | Doména společnosti nebo organizace.                                  |
| e-mail          | řetězec                                                         | Získá nebo nastaví nadřazené předplatné.                                  |
| language       | řetězec                                                         | Preferovaný jazyk pro komunikaci.                              |
| jazyková verze        | řetězec                                                         | Upřednostňovaná jazyková verze komunikace a měny, například en-us. |
| typ profilu    | řetězec                                                         | Typ profilu partnera.                                              |
| Odkazy          | [Odkazy na prostředky](utility-resources.md#resourcelinks)           | Propojení prostředků odpovídající profilu.                       |
| atributy     | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu.                  |

## <a name="supportprofile"></a>Profil podpory

Popisuje profil podpory partnera.

| Vlastnost    | Typ                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| e-mail       | řetězec                                                         | E-mailová adresa přidružená k profilu.        |
| Telefonní   | řetězec                                                         | Telefonní číslo přidružené k profilu.         |
| Webové stránky     | řetězec                                                         | Web podpory.                                  |
| typ profilu | řetězec                                                         | Typ profilu partnera.                             |
| Odkazy       | [Odkazy na prostředky](utility-resources.md#resourcelinks)           | Propojení prostředků odpovídající profilu.      |
| atributy  | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu. |

