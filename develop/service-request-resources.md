---
title: Prostředky žádostí o služby
description: Partneři mohou za své partnery zažádat o služby, aby nahlásit přerušení služeb poskytovaných Microsoftem nebo požádat o jinou technickou podporu, kterou nejsou schopní poskytovat.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f919b3c34ff179a7a6cd0541f34c53737ec4148e44791419d2252fae64b0658d
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993227"
---
# <a name="service-request-resources"></a>Prostředky žádostí o služby

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Partneři mohou za své partnery zažádat o služby, aby nahlásit přerušení služeb poskytovaných Microsoftem nebo požádat o jinou technickou podporu, kterou nejsou schopní poskytovat.

## <a name="servicerequest"></a>Požadavek na službu

Popisuje žádost o službu, kterou podá partner, včetně toho, jak tato žádost postupuje.

| Vlastnost         | Typ                                                          | Description                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Nadpis            | řetězec                                                        | Název žádosti o službu.                                                           |
| Description      | řetězec                                                        | Popis                                                                     |
| Závažnost         | řetězec                                                        | Závažnost: "neznámý", "kritický", "střední" nebo "minimální".                       |
| SUPPORTTopicId   | řetězec                                                        | ID tématu podpory.                                                         |
| SupportTopicName | řetězec                                                        | Název tématu podpory.                                                       |
| Id               | řetězec                                                        | ID žádosti o službu.                                                       |
| Status           | řetězec                                                        | Stav žádosti o službu: none( žádný), open (otevřený), closed (uzavřeno) nebo "attention needed" (potřeba \_ pozornosti). |
| Organizace     | [ServiceRequestOrganization](#servicerequestorganization)     | Organizace, pro kterou je žádost o službu vytvořena.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Primární kontakt v žádosti o služby.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | Kontakt "Poslední aktualizace", který se týká změn v žádosti o služby.                        |
| ProductName      | řetězec                                                        | Název produktu, který odpovídá žádosti o služby.                     |
| ProductId        | řetězec                                                        | ID produktu.                                                               |
| CreatedDate      | date                                                          | Datum vytvoření žádosti o služby                                          |
| LastModifiedDate. | date                                                          | Datum poslední změny žádosti o služby                                 |
| LastClosedDate   | date                                                          | Datum, kdy byla žádost o služby naposledy uzavřena.                                   |
| Odkazy na soubor        | pole prostředků [FileInfo](utility-resources.md#fileinfo) | Kolekce odkazů na soubory, které se týkají žádosti o služby.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | Poznámku je možné přidat k existující žádosti o služby.                                  |
| Poznámky            | pole [ServiceRequestNotes](#servicerequestnote)           | Kolekce poznámek přidaných k žádosti o služby.                                  |
| CountryCode      | řetězec                                                        | Země, která odpovídá žádosti o služby.                                    |
| Atributy       | Atributy prostředků                                            | Atributy metadat odpovídající žádosti o službu.                        |

## <a name="servicerequestcontact"></a>ServiceRequestContact

Popisuje kontakt, který vytvoří nebo upraví žádost o služby.

| Vlastnost     | Typ                                                      | Description                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Organizace | [ServiceRequestOrganization](#servicerequestorganization) | Organizace, pro kterou je žádost o službu vytvořena. |
| Contactid    | řetězec                                                    | Jedinečné ID kontaktu.                               |
| LastName     | řetězec                                                    | Příjmení kontaktu.                          |
| FirstName    | řetězec                                                    | Jméno kontaktu                         |
| E-mail        | řetězec                                                    | E-mail kontaktu                              |
| PhoneNumber  | řetězec                                                    | Telefonní číslo kontaktu.                       |

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

