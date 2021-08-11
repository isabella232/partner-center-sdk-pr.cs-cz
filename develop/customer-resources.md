---
title: Zdroje informací pro zákazníky
description: Prostředky zákazníků, které představují zákazníka nebo prodejce.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 10798ae0bfae8c1a4e38777096861427992b8aee3799ee2dd9154c6f0e0c0799
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995165"
---
# <a name="customer-resources"></a>Zdroje informací pro zákazníky

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

## <a name="customer"></a>Zákazník

Prostředek **Zákazník** představuje zákazníka nebo prodejce. V širokém podniku může být zákaznickým zdrojem jakákoli osoba, zaměstnanec nebo organizace, která chce podnikat s Microsoftem a prodejci Microsoftu. Zákazníci mají také profil společnosti a fakturační profil.

>[!NOTE]
>U **prostředku** Zákazníka platí omezení rychlosti 500 požadavků za minutu na identifikátor tenanta.

| Vlastnost              | Typ                                                             | Description                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | řetězec                                                           | ID zákazníka.                                                                                                                             |
| id obchodu            | řetězec                                                           | ID obchodu                                                                                                                             |
| profil společnosti        | [Profil společnosti CustomerCompany](#customercompanyprofile)                | Další informace o společnosti nebo organizaci.                                                                                    |
| profil fakturace        | [CustomerBillingProfile](#customerbillingprofile)                | Další informace použité pro fakturaci.                                                                                                     |
| relationshipToPartner | řetězec                                                           | Definuje licenční program, který partner používá pro tohoto zákazníka: none, reseller, advisor, syndication nebo microsoft \_ support. |
| allowDelegatedAccess  | boolean                                                          | Určuje, jestli mu tento zákazník udělil delegovaná oprávnění správce. Tato vlastnost je dostupná jenom při získávání zákazníka podle ID, ne podle seznamu.                                                         |
| userCredentials       | [Přihlašovací údaje uživatele](user-resources.md#usercredentials) | Přihlašovací údaje uživatele.                                                                                                                        |
| customDomains         | pole řetězců                                                 | Seznam vlastních domén zákazníka                                                                                                        |
| associatedPartnerId   | řetězec                                                           | Nepřímý prodejce přidružený k tomuto zákaznickému účtu. Tuto hodnotu mohou nastavit pouze nepřímí partneři CSP.                              |
| Odkazy                 | [Odkazy na prostředky](utility-resources.md#resourcelinks)             | Odkazy na prostředky obsažené v profilu.                                                                                             |
| atributy            | [Atributy prostředků](utility-resources.md#resourceattributes)   | Atributy metadat odpovídající profilu.                                                                                        |

## <a name="customercompanyprofile"></a>Profil společnosti CustomerCompany

Prostředek **CustomerCompanyProfile** obsahuje další informace o společnosti nebo organizaci.

| Vlastnost    | Typ                                                           | Description                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| ID tenanta    | řetězec                                                         | Identifikátor tenanta zákazníka pro Azure AD. Říká se tomu také MicrosoftID. |
| doména      | řetězec                                                         | Jméno zákazníka, například contoso.onmicrosoft.com.                             |
| Companyname | řetězec                                                         | Název společnosti nebo organizace.                                          |
| Odkazy       | [Odkazy na prostředky](utility-resources.md#resourcelinks)           | Odkazy na prostředky obsažené v profilu.                                  |
| atributy  | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu.                             |
|organizationRegistrationNumber|Řetězec|Registrační číslo organizace zákazníka (v určitých zemích se také označuje jako číslo INN). Vyžaduje se pouze pro společnost nebo organizaci zákazníka, která se nachází v následujících zemích: Arménie (AM), Narština (AM), Kaskádština (AZ), Kaskády (BY), Kaskády (HU), KZ (KZ), Sidean (KG), Nar (MD), Korea (RU), Tádžština (TJ), Zamíce (UZ), Indie, Brazílie, Jižní Afrika, Saúdská Arábie, Saúdská Arábie, Malajsie, Malajsie, Zamísťování, Zamísťování, Jižní Asie a Malajsie. U společnosti nebo organizace zákazníka, která se nachází v jiných zemích, by se to nemělo zazadat.|


## <a name="customerbillingprofile"></a>CustomerBillingProfile

Prostředek **CustomerBillingProfile** jsou další informace, které slouží k fakturování zákazníkovi.

| Vlastnost       | Typ                                                           | Description                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | řetězec                                                         | Identifikátor profilu.                                                                                                                                |
| firstName      | řetězec                                                         | Jméno fakturačního kontaktu ve společnosti zákazníka. Na tuto osobu se budou směrovat faktury a další fakturační komunikace. |
| lastName       | řetězec                                                         | Příjmení fakturačního kontaktu.                                                                                                                  |
| e-mail          | řetězec                                                         | E-mailová adresa fakturačního kontaktu                                                                                                                    |
| jazyková verze        | řetězec                                                         | Jejich preferovaná kultura komunikace a měny, například en-us.                                                                               |
| language       | řetězec                                                         | Jejich preferovaný jazyk pro komunikaci.                                                                                                            |
| Companyname    | řetězec                                                         | Název společnosti nebo organizace.                                                                                                               |
| defaultAddress | [Adresa](utility-resources.md#address)                       | Adresa, na kterou se účtují faktury, kde kontaktní e-mail funguje.                                                                                   |
| odkazy          | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky obsažené v profilu.                                                                                                       |
| atributy     | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

Prostředek **CustomerRelationshipRequest** obsahuje adresu URL, kterou zákazník používá k navázání vztahu prodejce k partnerovi.

| Vlastnost   | Typ                                                           | Description                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | řetězec                                                         | Adresa URL, kterou zákazník používá k navázání vztahu s partnerem. |
| atributy | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající požadavku vztahu       |