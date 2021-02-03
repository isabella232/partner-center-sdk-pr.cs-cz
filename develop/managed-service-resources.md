---
title: Prostředky spravované služby
description: Spravované služby jsou služby, ke kterým má partner delegovaná oprávnění správce. Partneři můžou poskytovat podporu pro žádosti a souborové služby jménem svých spravovaných služeb.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef644ac4d8ae9660cffc9558af33cc27832556c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766705"
---
# <a name="managed-service-resources"></a>Prostředky spravované služby

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Spravované služby jsou služby, ke kterým má partner delegovaná oprávnění správce. Partneři můžou poskytovat podporu pro žádosti a souborové služby jménem svých spravovaných služeb.

## <a name="managedservice"></a>ManagedService

Popisuje spravovanou službu.

| Vlastnost   | Typ                | Description                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | řetězec              | ID spravované služby                                  |
| Name       | řetězec              | Název spravované služby.                         |
| Parametr  | řetězec              | Název skupiny, do které patří služba.      |
| Odkazy      | ManagedServiceLinks | Odkazy na prostředky odpovídající spravované službě. |
| Atributy | ResourceAttributes  | Atributy metadat odpovídající smlouvě.  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

Obsahuje odkazy, které umožňují partnerovi s delegovaným oprávněním správce poskytovat podporu pro službu.

| Vlastnost      | Typ | Description                 |
|---------------|------|-----------------------------|
| AdminService  | Odkaz | Identifikátor URI služby pro správu      |
| ServiceHealth | Odkaz | Identifikátor URI stavu služby.     |
| ServiceTicket | Odkaz | Identifikátor URI lístku služby.     |
| Self          | Odkaz | Identifikátor URI samostatného.               |
| Další          | Odkaz | Další stránka položek     |
| Předchozí      | Odkaz | Předchozí stránka položek |

