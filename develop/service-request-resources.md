---
title: Prostředky žádosti o služby
description: Partneři můžou podávat žádosti o služby prostřednictvím spisu jménem svých partnerů, aby nahlásily služby, které společnost Microsoft poskytuje, nebo aby požádaly o jinou technickou podporu, že nepodporují poskytování.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 072f9eddaf9d854f1dcc8cc65f7928b6c95700fa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766726"
---
# <a name="service-request-resources"></a>Prostředky žádosti o služby

**Platí pro**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Partneři můžou podávat žádosti o služby prostřednictvím spisu jménem svých partnerů, aby nahlásily služby, které společnost Microsoft poskytuje, nebo aby požádaly o jinou technickou podporu, že nepodporují poskytování.

## <a name="servicerequest"></a>ServiceRequest

Popisuje žádost o službu podanou partnerem, včetně toho, jak probíhá požadavek.

| Vlastnost         | Typ                                                          | Description                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Nadpis            | řetězec                                                        | Název žádosti o službu.                                                           |
| Description      | řetězec                                                        | Popis.                                                                     |
| Závažnost         | řetězec                                                        | Závažnost: "neznámá", "kritická", "střední" nebo "Minimal".                       |
| SupportTopicId   | řetězec                                                        | ID tématu podpory                                                         |
| SupportTopicName | řetězec                                                        | Název tématu podpory                                                       |
| Id               | řetězec                                                        | ID žádosti o službu.                                                       |
| Status           | řetězec                                                        | Stav žádosti o službu: "žádné", "otevřeno", "uzavřeno" nebo " \_ nutná pozornost". |
| Organizace     | [ServiceRequestOrganization](#servicerequestorganization)     | Organizace, pro kterou je vytvořen požadavek služby.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Primární kontakt na žádost o službu                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | "Poslední aktualizace": kontaktuje změny žádosti o službu.                        |
| ProductName      | řetězec                                                        | Název produktu, který odpovídá žádosti o služby.                     |
| ProductId        | řetězec                                                        | ID produktu                                                               |
| CreatedDate      | date                                                          | Datum vytvoření žádosti o službu.                                          |
| LastModifiedDate. | date                                                          | Datum poslední změny žádosti o službu.                                 |
| LastClosedDate   | date                                                          | Datum poslední uzavření žádosti o službu.                                   |
| Odkazy na připojení        | pole prostředků [FileInfo](utility-resources.md#fileinfo) | Kolekce odkazů na soubory, které se vztahují k žádosti o službu.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | Do existující žádosti o službu je možné přidat poznámku.                                  |
| Poznámky            | pole [ServiceRequestNotes](#servicerequestnote)           | Kolekce poznámek přidaných do žádosti o službu.                                  |
| CountryCode      | řetězec                                                        | Země odpovídající žádosti o službu.                                    |
| Atributy       | ResourceAttributes                                            | Atributy metadat odpovídající žádosti o službu.                        |

## <a name="servicerequestcontact"></a>ServiceRequestContact

Popisuje kontakt, který vytvoří nebo upraví žádost o služby.

| Vlastnost     | Typ                                                      | Description                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Organizace | [ServiceRequestOrganization](#servicerequestorganization) | Organizace, pro kterou je vytvořen požadavek služby. |
| ContactId    | řetězec                                                    | Jedinečné ID kontaktu                               |
| LastName     | řetězec                                                    | Příjmení kontaktu                          |
| FirstName    | řetězec                                                    | Křestní jméno kontaktu                         |
| E-mail        | řetězec                                                    | E-mail kontaktu                              |
| PhoneNumber  | řetězec                                                    | Telefonní číslo kontaktu                       |

## <a name="servicerequestnote"></a>ServiceRequestNote

Popisuje poznámku připojenou k žádosti o služby.

| Vlastnost      | Typ   | Description                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | řetězec | Jméno autora poznámky         |
| CreatedDate   | date   | Datum a čas vytvoření poznámky |
| Text          | řetězec | Text poznámky                        |

## <a name="servicerequestorganization"></a>ServiceRequestOrganization

Popisuje organizaci, pro kterou je vytvořen požadavek služby.

| Vlastnost    | Typ   | Description                           |
|-------------|--------|---------------------------------------|
| Id          | řetězec | Jedinečné ID organizace    |
| Name        | řetězec | Název organizace         |
| PhoneNumber | řetězec | Telefonní číslo organizace |

## <a name="supporttopic"></a>SupportTopic

Popisuje téma podpory. Žádosti o služby určují téma podpory, které zajistí, že budou zpracovávány rychle a efektivně.

| Vlastnost    | Typ               | Popis                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Název        | řetězec             | Název tématu podpory                                |
| Description | řetězec             | Popis tématu podpory                         |
| Id          | řetězec             | Jedinečné ID tématu podpory                           |
| Atributy  | ResourceAttributes | Atributy metadat odpovídající žádosti o službu. |

