---
title: Profilové prostředky
description: Popisuje chování Cloud Solution Provider profilu uživatele.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 945cfa141d1e6bde1709da882a177daaa32fba1f
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547780"
---
# <a name="profile-resources"></a>Profilové prostředky

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Popisuje chování Cloud Solution Provider profilu uživatele.

## <a name="billingprofile"></a>Profil fakturace

Popisuje fakturační profil partnera.

| Vlastnost            | Typ                                                           | Description                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| Companyname         | řetězec                                                         | Název fakturační společnosti.                                   |
| adresa             | [Adresa](utility-resources.md#address)                       | Fakturační adresa společnosti nebo organizace. |
| primaryContact      | [Kontakt](utility-resources.md#contact)                       | Primární kontakt pro společnost nebo organizaci.        |
| purchaseOrderNumber | řetězec                                                         | Číslo nákupní objednávky společnosti nebo organizace.        |
| taxId (ID daně)               | řetězec                                                         | TID společnosti nebo organizace                       |
| billingCurrency     | řetězec                                                         | Měna používaná společností nebo organizací.           |
| typ profilu         | řetězec                                                         | Typ profilu partnera.                                   |
| Odkazy               | [Odkazy na prostředky](utility-resources.md#resourcelinks)           | Propojení prostředků odpovídající profilu.            |
| atributy          | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu.       |

## <a name="legalbusinessprofile"></a>LegalBusinessProfile

Popisuje právní obchodní profil partnera.

| Vlastnost               | Typ                                                           | Description                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Companyname            | řetězec                                                         | Oficiální název společnosti.                                                                                                                                              |
| adresa                | [Adresa](utility-resources.md#address)                       | Adresa společnosti nebo organizace.                                                                                                                          |
| primaryContact         | [Kontakt](utility-resources.md#contact)                       | Primární kontakt pro společnost nebo organizaci.                                                                                                                 |
| companyApproverAddress | [Adresa](utility-resources.md#address)                       | Adresa schvalovatel společnosti.                                                                                                                                        |
| companyApproverEmail   | řetězec                                                         | E-mail schvalovatel společnosti.                                                                                                                                          |
| stav prověřování          | řetězec                                                         | Stav prověřování. Tato hodnota je řetězcová reprezentace jednoho z názvů členů nalezených ve [**VettingStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus).           |
| vettingSubStatus       | řetězec                                                         | Dílčí stav prověřování. Tato hodnota je řetězcová reprezentace jednoho z názvů členů nalezených ve [**VettingSubStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus). |
| typ profilu            | řetězec                                                         | Typ profilu partnera.                                                                                                                                            |
| Odkazy                  | [Odkazy na prostředky](utility-resources.md#resourcelinks)           | Propojení prostředků odpovídající profilu.                                                                                                                     |
| atributy             | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu.                                                                                                                |

## <a name="mpnprofile"></a>Profil Mpn

Popisuje profil Microsoft Partner Network partnera.

| Vlastnost    | Typ                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| název partnera | řetězec                                                         | Název společnosti nebo organizace.                     |
| ID mpn       | řetězec                                                         | ID Microsoft Partner Network (MPN).                     |
| typ profilu | řetězec                                                         | Typ profilu partnera.                             |
| Odkazy       | [Odkazy na prostředky](utility-resources.md#resourcelinks)           | Propojení prostředků odpovídající profilu.      |
| atributy  | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu. |

## <a name="organizationprofile"></a>Profil organizace

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

