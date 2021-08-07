---
title: Prostředky uživatele
description: Popisuje jednotlivé uživatele partnerského centra, jejich osobní údaje a informace o účtech a oprávnění, která mají v partnerském centru.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c91e3509d86c8817da30c8ad0d96a2b1b6eec7697e43b47d3dfb96055cac632
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989215"
---
# <a name="user-resources"></a>Prostředky uživatele

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Popisuje jednotlivé uživatele partnerského centra, jejich osobní údaje a informace o účtech a oprávnění, která mají v partnerském centru.

## <a name="user"></a>Uživatel

Popisuje jednotlivé uživatele.

| Vlastnost              | Typ                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | řetězec                                                         | Identifikátor uživatele.                                                                                                                                                                                                       |
| userPrincipalName (Hlavní název uživatele)     | řetězec                                                         | Identifikátor zabezpečení uživatele                                                                                                                                                                                             |
| firstName             | řetězec                                                         | Křestní jméno uživatele                                                                                                                                                                                                |
| lastName              | řetězec                                                         | Příjmení uživatele                                                                                                                                                                                                 |
| displayName           | řetězec                                                         | Zobrazované jméno uživatele                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Profil hesla uživatele.                                                                                                                                                                                               |
| phoneNumber           | řetězec                                                         | Telefonní číslo uživatele                                                                                                                                                                                                   |
| lastDirectorySyncTime | řetězec ve formátu data a času UTC                                 | čas, kdy se informace pro tohoto uživatele synchronizovaly mezi Azure Active Directory a místní službou Active Directory. hodnota data A času se zobrazí pouze v případě, že je povolena Azure AD Connect synchronizace. V opačném případě je hodnota null. |
| userDomainType        | řetězec                                                         | Typ domény uživatele: "none", "Managed" nebo "federované".                                                                                                                                                                   |
| state                 | řetězec                                                         | Stav uživatele: "aktivní", "neaktivní" (pro odstraněného uživatele).                                                                                                                                                          |
| softDeletionTime      | řetězec ve formátu data a času UTC                                 | Představuje začátek 30denní období, po kterém se trvale odstraní data přidružená k odstraněnému uživateli, a proto se neobnoví.                                                                          |
| odkazy                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky.                                                                                                                                                                                                        |
| atributy            | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                                                                                                                                                                                                   |

## <a name="customeruser"></a>CustomerUser

Popisuje uživatele zákazníka.

| Vlastnost              | Typ                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | řetězec                                                         | Místo, kde uživatel zamýšlí používat licenci.                                                                                                                                                                    |
| id                    | řetězec                                                         | Identifikátor uživatele.                                                                                                                                                                                                       |
| userPrincipalName (Hlavní název uživatele)     | řetězec                                                         | Identifikátor zabezpečení uživatele                                                                                                                                                                                             |
| firstName             | řetězec                                                         | Křestní jméno uživatele                                                                                                                                                                                                |
| lastName              | řetězec                                                         | Příjmení uživatele                                                                                                                                                                                                 |
| displayName           | řetězec                                                         | Zobrazované jméno uživatele                                                                                                                                                                                            |
| immutableId           | řetězec                                                         | Neměnné ID uživatele                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Profil hesla uživatele.                                                                                                                                                                                               |
| phoneNumber           | řetězec                                                         | Telefonní číslo uživatele                                                                                                                                                                                                   |
| lastDirectorySyncTime | řetězec ve formátu data a času UTC                                 | čas, kdy se informace pro tohoto uživatele synchronizovaly mezi Azure Active Directory a místní službou Active Directory. hodnota data A času se zobrazí pouze v případě, že je povolena Azure AD Connect synchronizace. V opačném případě je hodnota null. |
| userDomainType        | řetězec                                                         | Typ domény uživatele: "none", "Managed" nebo "federované".                                                                                                                                                                   |
| state                 | řetězec                                                         | Stav uživatele: "aktivní", "neaktivní" (pro odstraněného uživatele).                                                                                                                                                          |
| softDeletionTime      | řetězec ve formátu data a času UTC                                 | Představuje začátek 30denní období, po kterém se trvale odstraní data přidružená k odstraněnému uživateli, a proto se neobnoví.                                                                          |
| odkazy                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky.                                                                                                                                                                                                        |
| atributy            | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                                                                                                                                                                                                   |

## <a name="usercredentials"></a>UserCredentials

Popisuje přihlašovací údaje uživatele.

| Vlastnost | Typ                                               | Description                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | řetězec                                             | Jméno uživatele                |
| heslo | [SecureString](utility-resources.md#securestring) | Heslo uživatele bezpečně uložilo. |

## <a name="usermember"></a>UserMember

Popisuje informace o členovi uživatele.

| Vlastnost          | Typ                                                           | Description                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | řetězec                                                         | Zobrazované jméno uživatele   |
| userPrincipalName (Hlavní název uživatele) | řetězec                                                         | Název objektu zabezpečení uživatele.    |
| roleId            | řetězec                                                         | Identifikátor role uživatele |
| id                | řetězec                                                         | Identifikátor člena.      |
| atributy        | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.           |

