---
title: Prostředky uživatelů
description: Popisuje jednotlivého Partnerské centrum uživatele, jeho osobní údaje a informace o účtu a oprávnění, která má v Partnerské centrum.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 26bb202db3eefd9be8fe57ed2cc4dc220c8807d4
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529677"
---
# <a name="user-resources"></a>Prostředky uživatelů

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Popisuje jednotlivého Partnerské centrum uživatele, jeho osobní údaje a informace o účtu a oprávnění, která má v Partnerské centrum.

## <a name="user"></a>Uživatel

Popisuje jednotlivé uživatele.

| Vlastnost              | Typ                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | řetězec                                                         | Identifikátor uživatele.                                                                                                                                                                                                       |
| userPrincipalName (Hlavní název uživatele)     | řetězec                                                         | Identifikátor objektu zabezpečení uživatele.                                                                                                                                                                                             |
| firstName             | řetězec                                                         | Jméno uživatele                                                                                                                                                                                                |
| lastName              | řetězec                                                         | Příjmení uživatele                                                                                                                                                                                                 |
| displayName           | řetězec                                                         | Zobrazené jméno uživatele                                                                                                                                                                                            |
| PasswordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Profil hesla uživatele.                                                                                                                                                                                               |
| Phonenumber           | řetězec                                                         | Telefonní číslo uživatele.                                                                                                                                                                                                   |
| lastDirectorySyncTime | řetězec ve formátu data a času UTC                                 | Čas poslední synchronizace těchto informací pro tohoto uživatele mezi Azure Active Directory a místní Active Directory. Hodnota data a času se zobrazí pouze v případě, Připojení je povolená synchronizace služby Azure AD. V opačném případě je hodnota null. |
| userDomainType        | řetězec                                                         | Typ domény uživatele: "none", "managed" nebo "federated".                                                                                                                                                                   |
| state                 | řetězec                                                         | Stav uživatele: "aktivní", "neaktivní" (pro odstraněné uživatele).                                                                                                                                                          |
| softDeletionTime      | řetězec ve formátu data a času UTC                                 | Představuje začátek 30denního období, po kterém se trvale odstraní data přidružená k odstraněným uživatelům, a proto je nelze napravit.                                                                          |
| Odkazy                 | [Odkazy na prostředky](utility-resources.md#resourcelinks)           | Odkazy na prostředky.                                                                                                                                                                                                        |
| atributy            | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat.                                                                                                                                                                                                   |

## <a name="customeruser"></a>Uživatel zákazníka

Popisuje uživatele zákazníka.

| Vlastnost              | Typ                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | řetězec                                                         | Umístění, ve kterém chce uživatel licenci používat.                                                                                                                                                                    |
| id                    | řetězec                                                         | Identifikátor uživatele.                                                                                                                                                                                                       |
| userPrincipalName (Hlavní název uživatele)     | řetězec                                                         | Identifikátor objektu zabezpečení uživatele.                                                                                                                                                                                             |
| firstName             | řetězec                                                         | Jméno uživatele                                                                                                                                                                                                |
| lastName              | řetězec                                                         | Příjmení uživatele                                                                                                                                                                                                 |
| displayName           | řetězec                                                         | Zobrazené jméno uživatele                                                                                                                                                                                            |
| immutableId           | řetězec                                                         | Neměnné ID uživatele.                                                                                                                                                                                              |
| PasswordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Profil hesla uživatele.                                                                                                                                                                                               |
| Phonenumber           | řetězec                                                         | Telefonní číslo uživatele.                                                                                                                                                                                                   |
| lastDirectorySyncTime | řetězec ve formátu data a času UTC                                 | Čas poslední synchronizace těchto informací pro tohoto uživatele mezi Azure Active Directory a místní Active Directory. Hodnota data a času se zobrazí pouze v případě, Připojení je povolená synchronizace služby Azure AD. V opačném případě je hodnota null. |
| userDomainType        | řetězec                                                         | Typ domény uživatele: "none", "managed" nebo "federated".                                                                                                                                                                   |
| state                 | řetězec                                                         | Stav uživatele: "aktivní", "neaktivní" (pro odstraněné uživatele).                                                                                                                                                          |
| softDeletionTime      | řetězec ve formátu data a času UTC                                 | Představuje začátek 30denního období, po kterém se trvale odstraní data přidružená k odstraněným uživatelům, a proto je nelze napravit.                                                                          |
| Odkazy                 | [Odkazy na prostředky](utility-resources.md#resourcelinks)           | Odkazy na prostředky.                                                                                                                                                                                                        |
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

