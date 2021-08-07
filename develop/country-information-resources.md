---
title: Zdroje informací o zemi
description: Přečtěte si o používání rozhraní API partnerského centra s informačními prostředky země a popisnými metadaty, které se vztahují k určité zemi nebo oblasti.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 35b570b27466699d8d85819f7603794888f8dd943038ee28a0a734b7ef9aa0d1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991816"
---
# <a name="country-information-resources-available-from-partner-center-apis"></a>Prostředky informací o zemi dostupné z rozhraní API partnerského centra

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Následující zdroje jsou popisné metadata pro zemi nebo oblast.

## <a name="countryinformation"></a>CountryInformation

| Vlastnost                      | Typ               | Description                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData –                 | řetězec             | Data rozšíření.                                                                                |
| Iso2Code                      | řetězec             | Kód ISO-2.                                                                                     |
| Iso3Code                      | řetězec             | Kód ISO-3.                                                                                     |
| DefaultCulture                | řetězec             | Výchozí jazyková verze.                                                                               |
| IsStateRequired               | boolean            | Označuje, zda je kraj nebo kraj povinný.                                             |
| SupportedStatesList           | pole řetězců   | Pokud je vyžadována země nebo provincie, vrátí úplný seznam pro danou zemi nebo oblast.                    |
| SupportedLanguagesList        | pole řetězců   | Seznam podporovaných jazyků                                                                     |
| SupportedCulturesList         | pole řetězců   | Seznam podporovaných jazykových verzí.                                                                      |
| IsPostalCodeRequired          | boolean            | Označuje, zda je požadováno PSČ nebo PSČ.                                    |
| PostalCodeRegex               | řetězec             | Regulární výraz definující poštovní směrovací číslo.                                          |
| IsCityRequired                | boolean            | Označuje, zda je město povinné nebo ne.                                                       |
| IsVatIdSupported              | boolean            | Označuje, zda je vyžadováno ID DPH.                                                     |
| TaxIdFormat                   | řetězec             | Formát daňového ID.                                                                                 |
| TaxIdSample                   | řetězec             | Ukázka daňového ID.                                                                                 |
| VatIdRegex                    | řetězec             | Regulární výraz daňového ID.                                                                     |
| PhoneNumberRegex              | řetězec             | Regulární výraz telefonního čísla.                                                               |
| IsRegistrationNumberSupported | boolean            | Označuje, zda je registrační číslo podporováno nebo nikoli.                                       |
| IsTaxIdSupported              | boolean            | Označuje, zda je daňové ID podporováno nebo nikoli. To se liší od IsVatIdSupported. |
| ResellerAgreementRegion       | řetězec             | Oblast smlouvy pro prodejce.                                                                     |
| GeographicRegion              | řetězec             | Zeměpisná oblast.                                                                             |
| CountryCallingCodesList       | pole řetězců   | Kódy volání podporované v zemi nebo oblasti.                                                 |
| Atributy                    | ResourceAttributes | Atributy metadat odpovídající prostředku CountryInformation                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Popisuje pravidla formátování adres pro zemi nebo oblast.

| Vlastnost                | Typ               | Description                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | řetězec             | Kód ISO-2.                                                                                     |
| DefaultCulture          | řetězec             | Výchozí jazyková verze.                                                                               |
| IsStateRequired         | boolean            | Označuje, zda je kraj nebo kraj povinný.                                             |
| SupportedStatesList     | pole řetězců   | Pokud je vyžadována země nebo provincie, vrátí úplný seznam pro danou zemi nebo oblast.                    |
| SupportedLanguagesList  | pole řetězců   | Seznam podporovaných jazyků                                                                     |
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
