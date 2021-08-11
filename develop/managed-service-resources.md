---
title: Prostředky spravované služby
description: Spravované služby jsou služby, ke kterým má partner delegovaná oprávnění správce. Partneři můžou poskytovat podporu pro žádosti a souborové služby jménem svých spravovaných služeb.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 066c9f2a0d5ca8d03553508c2b471ca49735406a5a0566bf48b0773385c129f7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994383"
---
# <a name="managed-service-resources"></a>Prostředky spravované služby

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

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
| Self          | Odkaz | Identifikátor URI pro sebe.               |
| Další          | Odkaz | Další stránka položek     |
| Předchozí      | Odkaz | Předchozí stránka položek |

