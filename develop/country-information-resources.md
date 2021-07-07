---
title: Zdroje informací o zemích
description: Přečtěte si o Partnerské centrum API s informacemi o zemích a popisnými metadaty souvisejícími s konkrétní zemí nebo oblastí.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: caf56282d21df35ae9e179a98a37317f864117a3
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973821"
---
# <a name="country-information-resources-available-from-partner-center-apis"></a>Zdroje informací o zemích dostupné z Partnerské centrum API

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Následující zdroje informací jsou popisná metadata pro zemi nebo oblast.

## <a name="countryinformation"></a>CountryInformation (Informace o zemi)

| Vlastnost                      | Typ               | Description                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | řetězec             | Data rozšíření.                                                                                |
| Iso2Code                      | řetězec             | Kód ISO-2.                                                                                     |
| Iso3Code                      | řetězec             | Kód ISO-3.                                                                                     |
| DefaultCulture                | řetězec             | Výchozí jazyková verze.                                                                               |
| IsStateRequired               | boolean            | Určuje, jestli je stát nebo kraj povinné.                                             |
| SupportedStatesList           | pole řetězců   | Pokud se vyžaduje stát nebo kraj, vrátí úplný seznam pro zemi nebo oblast.                    |
| Seznam podporovaných jazyků        | pole řetězců   | Seznam podporovaných jazyků                                                                     |
| SupportedCulturesList         | pole řetězců   | Seznam podporovaných jazykových verzí.                                                                      |
| IsPostalCodeRequired          | boolean            | Určuje, jestli se vyžaduje PSČ nebo PSČ.                                    |
| PostalCodeRegex               | řetězec             | Regulární výraz, který definuje PSČ.                                          |
| IsCityRequired                | boolean            | Určuje, jestli je město povinné.                                                       |
| IsVatIdSupported              | boolean            | Určuje, jestli je DIČ povinné.                                                     |
| TaxIdFormat                   | řetězec             | Formát TID                                                                                 |
| TaxIdSample                   | řetězec             | Ukázka TID                                                                                 |
| VatIdRegex                    | řetězec             | Regulární výraz TID                                                                     |
| PhoneNumberRegex              | řetězec             | Regulární výraz telefonního čísla                                                               |
| IsRegistrationNumberSupported | boolean            | Určuje, jestli je číslo registrace podporované nebo ne.                                       |
| IsTaxIdSupported              | boolean            | Určuje, jestli je nebo není podporované TID. To se liší od IsVatIdSupported. |
| ResellerAgreementRegion       | řetězec             | Oblast smlouvy s prodejcem.                                                                     |
| Geografická oblast              | řetězec             | Geografická oblast.                                                                             |
| CountryCallingCodesList       | pole řetězců   | Podporované volající kódy v zemi nebo oblasti.                                                 |
| Atributy                    | Atributy prostředků | Atributy metadat odpovídající prostředku CountryInformation.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Popisuje pravidla formátování adres pro zemi nebo oblast.

| Vlastnost                | Typ               | Description                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | řetězec             | Kód ISO-2.                                                                                     |
| DefaultCulture          | řetězec             | Výchozí jazyková verze.                                                                               |
| IsStateRequired         | boolean            | Určuje, jestli je stát nebo kraj povinné.                                             |
| SupportedStatesList     | pole řetězců   | Pokud se vyžaduje stát nebo kraj, vrátí úplný seznam pro zemi nebo oblast.                    |
| Seznam podporovaných jazyků  | pole řetězců   | Seznam podporovaných jazyků                                                                     |
| SupportedCulturesList   | pole řetězců   | Seznam podporovaných jazykových verzí.                                                                      |
| IsPostalCodeRequired    | boolean            | Určuje, jestli se vyžaduje PSČ nebo PSČ.                                    |
| PostalCodeRegex         | řetězec             | Regulární výraz, který definuje PSČ.                                          |
| IsCityRequired          | boolean            | Určuje, jestli je město povinné.                                                       |
| IsVatIdSupported        | boolean            | Určuje, jestli je DIČ povinné.                                                     |
| TaxIdFormat             | řetězec             | Formát TID                                                                                 |
| TaxIdSample             | řetězec             | Ukázka TID                                                                                 |
| VatIdRegex              | řetězec             | Regulární výraz TID                                                                     |
| PhoneNumberRegex        | řetězec             | Regulární výraz telefonního čísla                                                               |
| IsTaxIdSupported        | boolean            | Určuje, jestli je nebo není podporované TID. Tato vlastnost se liší od IsVatIdSupported. |
| IsTaxIdOptional         | boolean            | Určuje, jestli je DIČ volitelné nebo ne.                                                     |
| CountryCallingCodesList | pole řetězců   | Podporované volající kódy v zemi nebo oblasti.                                                 |
| Atributy              | Atributy prostředků | Atributy metadat odpovídající prostředku CountryInformation.                          |
