---
title: Zdroje informací o zákaznících
description: Zdroje informací o zákaznících, které reprezentují zákazníka nebo prodejce.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 7d76de33c9a0d28e9d3fb0b0821cbd37ad67e7af
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973141"
---
# <a name="customer-resources"></a>Zdroje informací o zákaznících

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

## <a name="customer"></a>Zákazník

Prostředek **zákazníka** představuje zákazníka nebo prodejce. Obecně platí, že zákazníkovým zdrojem může být jakákoli osoba, zaměstnanec nebo organizace, které chtějí dělat firmy s prodejci Microsoftu a prodejci Microsoftu. Zákazníci mají také profil společnosti a fakturační profil.

>[!NOTE]
>Prostředek **zákazníka** má omezení četnosti 500 požadavků za minutu na identifikátor tenanta.

| Vlastnost              | Typ                                                             | Description                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | řetězec                                                           | ID zákazníka.                                                                                                                             |
| commerceId            | řetězec                                                           | ID obchodu.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | Další informace o společnosti nebo organizaci                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | Další informace, které se používají k fakturaci.                                                                                                     |
| relationshipToPartner | řetězec                                                           | Definuje licenční program, který partner používá pro tohoto zákazníka: "none", "prodejce", "Advisor", "syndikace" nebo " \_ Podpora Microsoftu". |
| allowDelegatedAccess  | boolean                                                          | Určuje, jestli má partner udělena oprávnění delegovaného správce tohoto zákazníka. Tato vlastnost je k dispozici pouze při získávání zákazníka podle ID, nikoli podle seznamu.                                                         |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | Přihlašovací údaje uživatele                                                                                                                        |
| customDomains         | pole řetězců                                                 | Seznam vlastních domén zákazníka.                                                                                                        |
| associatedPartnerId   | řetězec                                                           | Nepřímý prodejce přidružený k tomuto účtu zákazníka. Tuto hodnotu můžou nastavit jenom nepřímí partneři CSP.                              |
| odkazy                 | [ResourceLinks](utility-resources.md#resourcelinks)             | Odkazy na prostředky obsažené v profilu.                                                                                             |
| atributy            | [ResourceAttributes](utility-resources.md#resourceattributes)   | Atributy metadat odpovídající profilu.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

Prostředek **CustomerCompanyProfile** je další informace o společnosti nebo organizaci.

| Vlastnost    | Typ                                                           | Description                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | řetězec                                                         | Identifikátor tenanta zákazníka pro Azure AD. Tento název se také označuje jako MicrosoftID. |
| doména      | řetězec                                                         | Název zákazníka, například contoso.onmicrosoft.com.                             |
| Společnosti | řetězec                                                         | Název společnosti nebo organizace.                                          |
| odkazy       | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky obsažené v profilu.                                  |
| atributy  | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu.                             |
|organizationRegistrationNumber|Řetězec|Registrační číslo organizace zákazníka (také označované jako DIČ v určitých zemích). Požadované jenom pro společnost nebo organizaci zákazníka, která se nachází v následujících zemích: Arménská (AM), Ázerbájdžán (AZ), Bělorusko (BY), Maďarsko (HU), Kazachstán (KZ), Kyrgyzstán (KG), Moldavsko (MD), Rusko (RU), Tádžikistán (TJ), Uzbekistán (UZ), Ukrajina (UA), Indie, Brazílie, Jižní Afrika, Polsko, Spojené arabské emiráty, Saúdská Arábie, Turecko, Thajsko, Vietnam, Maďarsko, Jižní Súdán a Venezuela. Pro společnost nebo organizaci zákazníka nacházející se v jiných zemích by to nemělo být určeno.|


## <a name="customerbillingprofile"></a>CustomerBillingProfile

Prostředek **CustomerBillingProfile** jsou další informace, které se používají k fakturaci zákazníka.

| Vlastnost       | Typ                                                           | Description                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | řetězec                                                         | Identifikátor profilu.                                                                                                                                |
| firstName      | řetězec                                                         | Křestní jméno kontaktní osoby na společnosti zákazníka. To je osoba, na kterou faktury a další fakturační komunikace budou směrovány. |
| lastName       | řetězec                                                         | Příjmení kontaktní osoby pro fakturaci                                                                                                                  |
| e-mail          | řetězec                                                         | E-mailová adresa fakturačního kontaktu                                                                                                                    |
| jazyková verze        | řetězec                                                         | Upřednostňovaná jazyková verze pro komunikaci a měnu, jako je "en-US".                                                                               |
| language       | řetězec                                                         | Upřednostňovaný jazyk pro komunikaci.                                                                                                            |
| Společnosti    | řetězec                                                         | Název společnosti nebo organizace.                                                                                                               |
| defaultAddress | [Adresa](utility-resources.md#address)                       | Adresa, na kterou se účtují faktury, kde kontaktní e-mail funguje.                                                                                   |
| odkazy          | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky obsažené v profilu.                                                                                                       |
| atributy     | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající profilu.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

Prostředek **CustomerRelationshipRequest** obsahuje adresu URL, kterou zákazník používá k navázání vztahu prodejce k partnerovi.

| Vlastnost   | Typ                                                           | Description                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | řetězec                                                         | Adresa URL, kterou zákazník používá k navázání vztahu s partnerem. |
| atributy | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající požadavku vztahu       |