---
title: Pomocné prostředky
description: REST API partnerského centra obsahuje mnoho prostředků, které popisují modely dat pro obecné účely používané v celé sadě SDK.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: de97feed13a4d0bae9743939a03f8cb8470f5f960bec0507cd9c5adfad287120
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115998038"
---
# <a name="utility-resources"></a>Pomocné prostředky

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

REST API partnerského centra obsahuje mnoho prostředků, které popisují modely dat pro obecné účely používané v celé sadě SDK.

## <a name="address"></a>Adresa

Adresa, která se má použít pro profily zákazníků nebo partnerů. Další informace o podporovaných formátech a vlastnostech v různých zemích nebo oblastech najdete v tématu [získání pravidel formátování adres podle trhu](get-market-specific-validation-data.md).

| Vlastnost     | Typ   | Délka (min, max) | Description                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | řetězec | (1, 200)          | První řádek adresy                                                                   |
| AddressLine2 | řetězec | (0, 200)          | Druhý řádek adresy. Tato vlastnost je nepovinná.                                       |
| City (Město)         | řetězec | Není k dispozici               | Město.                                                                                        |
| Stav        | řetězec | (0, 2)            | Stav                                                                                       |
| PostalCode   | řetězec | Není k dispozici               | Poštovní směrovací číslo nebo PSČ.                                                                     |
| Země      | řetězec | (2, 2)            | Země nebo oblast ve formátu kódu země ISO                                                   |
| Oblast       | řetězec | Není k dispozici               | Oblast.                                                                                      |
| FirstName    | řetězec | (1, 50)           | Jméno kontaktu na firmu nebo organizaci zákazníka                              |
| MiddleName   | řetězec | (1, 50)           | Prostřední jméno kontaktu na společnosti nebo organizaci zákazníka Tato vlastnost je nepovinná.  |
| LastName     | řetězec | (1, 50)           | Příjmení kontaktu na firmu nebo organizaci zákazníka                               |
| PhoneNumber  | řetězec | Není k dispozici               | Telefonní číslo kontaktu na společnosti nebo organizaci zákazníka Tato vlastnost je nepovinná.|
|PhoneNumber|řetězec|Není k dispozici|Telefonní číslo kontaktu na společnosti nebo organizaci zákazníka V profilu zákazníka je tato vlastnost pro společnost nebo organizaci zákazníka, která se nachází v následujících zemích, povinná: Arménská (AM), Ázerbájdžán (AZ), Bělorusko (BY), Maďarsko (HU), Kazachstán (KZ), Kyrgyzstán (KG), Moldavsko (MD), Rusko (RU), Tádžikistán (TJ), Uzbekistán (UZ), Ukrajina (UA), Indie, Brazílie, Jižní Afrika, Polsko, Spojené arabské emiráty, Saúdská Arábie, Turecko, Thajsko, Vietnam, Myanmar, Irák, Jižní Súdán a Venezuela. V opačném případě je to volitelné.|


## <a name="contact"></a>Kontakt

Popisuje kontaktní informace pro konkrétního jednotlivce.

| Vlastnost    | Typ   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | řetězec | Křestní jméno kontaktu    |
| LastName    | řetězec | Příjmení kontaktu     |
| E-mail       | řetězec | E-mailová adresa kontaktu |
| PhoneNumber | řetězec | Telefonní číslo kontaktu  |

## <a name="fieldfilter"></a>FieldFilter

Popisuje filtr, který lze použít na výsledky hledání.

| Vlastnost | Typ   | Description                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Operátor | řetězec | Operátor filtru: "Equals", "není \_ rovno", "větší \_ než", "větší \_ než \_ nebo \_ rovno", "menší \_ než", "menší \_ než \_ nebo \_ rovno", "podřetězec", "," nebo "," začíná znakem " \_ ," \_ nezačíná \_ ". |

## <a name="fileinfo"></a>FileInfo

Představuje externí soubor nahraný do partnerského centra.

| Vlastnost                 | Typ   | Description                                   |
|--------------------------|--------|-----------------------------------------------|
| Komentář                  | řetězec | Komentář přidružený k nahrání souboru    |
| FileExtension            | řetězec | Přípona souboru.                           |
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
