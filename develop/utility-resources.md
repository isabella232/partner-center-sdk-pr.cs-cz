---
title: Pomocné prostředky
description: Tento Partnerské centrum REST API obsahuje mnoho prostředků, které popisují datové modely pro obecné účely používané v celé sadě SDK.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 095cf36d47b147eb6df28d8747889e218c270659
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529660"
---
# <a name="utility-resources"></a>Pomocné prostředky

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Tento Partnerské centrum REST API obsahuje mnoho prostředků, které popisují datové modely pro obecné účely používané v celé sadě SDK.

## <a name="address"></a>Adresa

Adresa, která se má použít pro profily zákazníků nebo partnerů. Další informace o podporovaných formátech a vlastnostech v různých zemích a oblastech najdete v tématu [Získání pravidel formátování adres podle trhu.](get-market-specific-validation-data.md)

| Vlastnost     | Typ   | Délka (min., max.) | Description                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | řetězec | (1, 200)          | První řádek adresy.                                                                   |
| AddressLine2 | řetězec | (0, 200)          | Druhý řádek adresy. Tato vlastnost je nepovinná.                                       |
| City (Město)         | řetězec | Není k dispozici               | Město.                                                                                        |
| Stav        | řetězec | (0, 2)            | Stav                                                                                       |
| PostalCode   | řetězec | Není k dispozici               | PSČ.                                                                     |
| Země      | řetězec | (2, 2)            | Země/oblast ve formátu ISO s kódem země.                                                   |
| Oblast       | řetězec | Není k dispozici               | Oblast.                                                                                      |
| FirstName    | řetězec | (1, 50)           | Jméno kontaktu ve společnosti nebo organizaci zákazníka.                              |
| Middlename   | řetězec | (1, 50)           | Prostřední jméno kontaktu ve společnosti nebo organizaci zákazníka. Tato vlastnost je nepovinná.  |
| LastName     | řetězec | (1, 50)           | Příjmení kontaktu ve společnosti nebo organizaci zákazníka.                               |
| PhoneNumber  | řetězec | Není k dispozici               | Telefonní číslo kontaktu ve společnosti nebo organizaci zákazníka. Tato vlastnost je nepovinná.|
|PhoneNumber|řetězec|Není k dispozici|Telefonní číslo kontaktu ve společnosti nebo organizaci zákazníka. V profilu zákazníka je tato vlastnost povinná pro společnost nebo organizaci zákazníka, která se nachází v následujících zemích: Arménie (AM), Kaskády (AZ), Pohotová (BY), Zamyšlená (HU), Zamícená (KZ), Sidean (KG), Svižnost (MD), Korea (RU), Tingtán(TJ), Zamísť (UZ), Indy (UA),Indie, Brazílie, Jižní Afrika, Saúdská Arábie, Saúdská Arábie, Zamísťování, Zamísťování, Vietnam, Zamís, Zamísťování a Jižní Afrika. V opačném případě je to volitelné.|


## <a name="contact"></a>Kontakt

Popisuje kontaktní informace pro konkrétního jednotlivce.

| Vlastnost    | Typ   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | řetězec | Jméno kontaktu.    |
| LastName    | řetězec | Příjmení kontaktu.     |
| E-mail       | řetězec | E-mailová adresa kontaktu |
| PhoneNumber | řetězec | Telefonní číslo kontaktu.  |

## <a name="fieldfilter"></a>Filtr pole

Popisuje filtr, který lze použít u výsledků hledání.

| Vlastnost | Typ   | Description                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Operátor | řetězec | Operátor filtru: "equals", "not \_ equals", "greater \_ than", "greater \_ than or \_ \_ equals", "less \_ than", "less \_ than or \_ \_ equals", "substring", "and", "or", "starts \_ with", "not \_ starts \_ with". |

## <a name="fileinfo"></a>Fileinfo

Představuje externí soubor nahraný do Partnerské centrum.

| Vlastnost                 | Typ   | Description                                   |
|--------------------------|--------|-----------------------------------------------|
| Komentář                  | řetězec | Komentář přidružený k nahrání souboru    |
| Fileextension            | řetězec | Přípona souboru.                           |
| FileNameWithoutExtension | řetězec | Název souboru, přípona není zahrnutý. |
| Velikost                 | long   | Velikost souboru.                         |
| Id                       | řetězec | Jedinečné ID pro nahrání souboru.            |

## <a name="link"></a>Odkaz

Obsahuje odkaz uri a přidružené informace.

| Vlastnost | Typ                   | Description                        |
|----------|------------------------|------------------------------------|
| Identifikátor URI      | řetězec                 | Identifikátor URI.                           |
| Metoda   | řetězec                 | Metoda reprezentována identifikátorem URI. |
| Hlavičky  | Pole KeyValuePairs | Hlavičky odkazu.          |

## <a name="passwordprofile"></a>PasswordProfile

Popisuje konkrétní heslo a to, jestli je potřeba toto heslo změnit.

>[!NOTE]
>Nepodporované Partnerské centrum provozované společností 21Vianet.

| Vlastnost            | Typ                          | Description                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Heslo            | [Securestring](#securestring) | Heslo.                                                          |
| ForceChangePassword | boolean                       | Určuje, jestli se při příštím přihlášení musí heslo vynuctě změnit. |

## <a name="resourcelinks"></a>Odkazy na prostředky

Obsahuje seznam odkazů pro prostředek.

| Vlastnost   | Typ                                      | Description                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self       | [Odkaz](#link)                             | Identifikátor URI sebe sama.                                      |
| Další       | [Odkaz](#link)                             | Další stránka položek                            |
| Předchozí   | [Odkaz](#link)                             | Předchozí stránka položek                        |
| Atributy | [Atributy prostředků](#resourceattributes) | Atributy metadat odpovídající uživateli. |

## <a name="resourceattributes"></a>Atributy prostředků

Obsahuje metadata atributu pro prostředek.

| Vlastnost   | Typ   | Description                                 |
|------------|--------|---------------------------------------------|
| Etag       | řetězec | ETag, označované také jako verze objektu. |
| ObjectType | řetězec | Typ objektu základního prostředku.    |

## <a name="securestring"></a>Securestring

Ukládá zabezpečené informace, například heslo.

| Vlastnost | Typ | Description                       |
|----------|------|-----------------------------------|
| Délka   | int  | Délka zabezpečeného řetězce. |

## <a name="validationcode"></a>Kód ověření

Představuje ověřovací kód Government Community Cloud partnera.

| Vlastnost         | Typ         | Description                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| ID partnera        | Identifikátor GUID         | Identifikátor partnera                                                       |
| OrganizationName | řetězec       | Název organizace poskytnutý během procesu ověřování             |
| ID ověření     | int          | Jedinečný identifikátor pro ověřování                                       |
| MaxCreates (Maximální počet vytvoření)       | nullable int | Maximální počet zákazníků, které je možné vytvořit s tímto ověřovacím kódem    |
| RemainingCreates (Zbývajícívytvoření) | nullable int | Zbývající zákazník vytvoří v rámci tohoto ID ověření.                      |
| Etag             | řetězec       | Konkrétní verze tohoto prostředku. Změní se při změně prostředku. |
