---
title: Vytvoření nepřímého prodejce v izolovaném prostoru
description: Poskytuje informace o nepřímých poskytovatelích izolovaného prostoru na povolení koncových testování pomocí rozhraní API.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 970b7ba49f6bb4b842f0f7d96e689856b0362c03949e14c9cf5a0e205573277b
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991442"
---
# <a name="create-indirect-reseller-in-sandbox"></a>Vytvoření nepřímého prodejce v izolovaném prostoru

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo

Tento dokument ukazuje, jak vytvořit nepřímé zprostředkovatele izolovaného prostoru (sandbox) a jak povolit komplexní testování pomocí rozhraní API.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.

## <a name="csp-indirect-provider"></a>CSP Indirect Provider

| Provozní možnosti             | Možnosti izolovaného prostoru                            |
|-------------------------------------|-------------------------------------------------|
| Prodává se prostřednictvím nepřímého prodejce k koncovému zákazníkovi | Podporováno |
| Vlastní prodej, fakturace, zřizování a Správa/podpora | Podporováno |
| Požádat o partnerství se prodejci | Podporováno |
| Zobrazit zákazníky podle prodejce | Podporováno |
| Přidat nové zákazníky podle prodejců | Podporováno |
| Pozvat zákazníky | Požadavek vztahu zákazníka není v izolovaném prostoru (sandbox) podporován. |
| Nepřímý poskytovatel izolovaného prostoru může jako POR při umísťování transakce vybrat Sandbox IR (MPN ID). | Podporováno |
| Nepodporováno v produkčním prostředí | Nepřímý poskytovatel izolovaného prostoru může vytvořit nepřímý prodejce izolovaného prostoru (sandbox) |
| ID MPN izolovaného prostoru (sandbox) by mělo být zadané, ID MPN produktu nebude fungovat. | Nepodporováno v produkčním prostředí |
| Nepodporováno v produkčním prostředí | Přímý poskytovatel izolovaného prostoru může odstranit nepřímý prodejce izolovaného prostoru (sandbox). |

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller"></a>Nepřímý poskytovatel izolovaného prostoru – vytvoření nepřímý prodejce izolovaného prostoru

Tato funkce je k dispozici pouze v izolovaném prostoru (sandbox) a poskytuje nepřímým poskytovatelům izolovaného prostoru možnost vytvářet nepřímé prodejce izolovaného prostoru.

1. Limit pěti nepřímých prodejců v izolovaném prostoru (sandbox) povolených pro jednotlivé nepřímých dodavatele
2. Nepřímé zprostředkovatele izolovaného prostoru můžou vytvářet zákazníky s `associatedPartnerId` nepřímým prodejcem izolovaného prostoru (sandbox)
3. Zadejte ID [MPN](/partner-center/mpn-create-a-partner-center-account) konkrétní oblasti při vytváření nepřímého prodejce izolovaného prostoru (sandbox). Víc nepřímých prodejců izolovaného prostoru (sandbox) je možné vytvořit se stejným ID MPN izolovaného prostoru.
4. Pro nepřímý poskytovatel izolovaného prostoru (sandboxu) jsou povoleni jenom 75

## <a name="sandbox-indirect-resellers--view-customers"></a>Nepřímý prodej v izolovaném prostoru – zobrazit zákazníky

1. Nepřímý prodejci izolovaného prostoru můžou zobrazit seznam zákazníků v izolovaném prostoru (sandbox) podle nepřímých poskytovatelů izolovaného prostoru
2. Nepřímý prodejci v izolovaném prostoru můžou spravovat účet zákazníka pomocí oprávnění delegovaného správce.

## <a name="create-sandbox-indirect-reseller-through-api"></a>Vytvoření nepřímého prodejce izolovaného prostoru prostřednictvím rozhraní API

### <a name="rest-request"></a>Žádost REST

#### <a name="request-syntax"></a>Syntaxe žádosti

| **Metoda** | **Identifikátor URI žádosti**                                                        |
|------------|------------------------------------------------------------------------|
| **SPUŠTĚNÍ**   | [*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller |

#### <a name="request-headers"></a>Hlavičky požadavku

- Toto rozhraní API se idempotentní (nepřinese se mu jiný výsledek, pokud ho zavoláte víckrát).
- Vyžaduje se ID žádosti a ID korelace.
- Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

#### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje požadované vlastnosti v textu žádosti.

| Vlastnost             | Typ           | Description                                      |
|----------------------|----------------|--------------------------------------------------|
| mpnId                | řetězec         | ID MPN pro IR v konkrétní oblasti         |
| tenant               | &lt;Řetězec slovníku, řetězec&gt; | Kolekce základních informací definující účet, který se má vytvořit |
| legalBusinessProfile | &lt;Řetězec slovníku, řetězec&gt; | Kolekce informací, které představují právní obchodní entitu, jako je kontakt, adresa a jméno |
| organizationProfileLanguage | &lt;Řetězec slovníku, řetězec&gt; | Identifikátor jazyka organizace |

Tato tabulka popisuje požadované vlastnosti v atributu **tenanta** .

| Vlastnost           | Typ           | Description                         |
|--------------------|----------------|-------------------------------------|
| domainPrefix       | Řetezce tabulka | Doména pro účet tenanta       |
| name               | řetězec         | Popisný název tenanta         |
| displayName        | řetězec         | Zobrazovaný název účtu        |
| adminUserName      | řetězec         | Uživatelské jméno pro účet pro přihlášení |
| adminfirstname     | řetězec         | Křestní jméno pro uživatele s oprávněními správce       |
| adminlastname      | řetězec         | Příjmení pro uživatele s oprávněními správce        |
| adminAlernateEmail | řetězec         | e-mail pro uživatele s oprávněními správce            |
| country            | řetězec         | Země účtu              |
| jazyková verze            | řetězec         | Jazykové předvolby pro účet     |

Tato tabulka popisuje požadované vlastnosti v **atributu legalBusinessProfile.**

| Vlastnost       | Typ                             | Description                          |
|----------------|----------------------------------|--------------------------------------|
| Companyname    | řetězec                           | Název společnosti pro právnickou osobu        |
| adresa        | Řetězec &lt; slovníku, řetězec&gt; | Adresa umístění právní osoby |
| primaryContact | Řetězec &lt; slovníku, řetězec&gt; | Kontaktní údaje společnosti       |
| jazyková verze        | řetězec                           | Jazyk upřednostňovaný společností    |

### <a name="request-example"></a>Příklad požadavku

```http
{
    "mpnId": "6363276",
    "tenant": {
        "domainPrefix": "TipIRIntTest705",
        "name": "TipIRIntTest705",
        "displayName": "TipIRIntTest705",
        "adminUserName": "admin",
        "adminFirstName": "TipIRIntTest705",
        "adminLastName": "TipIRIntTest705",
        "adminAlternateEmail": "TipIRIntTest705@test.com",
        "country": "US",
        "culture": "en-us"
    },
    "legalBusinessProfile": {
        "companyName": "TipIRIntTest705",
        "address": {
            "country": "FR",
            "city": "Issy-les-Moulineaux",
            "state": "",
            "addressLine1": "39-41 quai du Président Roosevelt",
            "addressLine2": "",
            "postalCode": "92130"
        },
        "primaryContact": {
            "firstName": "Sandbox",
            "lastName": "Scenario",
            "email": "Sandbox.Scenario@test.com",
            "phoneNumber": "1234567890"
        },
        "culture": "en-US"
    },
    "organizationProfileLanguage": "en"
}
```

### <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí vyplněný prostředek sandboxového prostředí IR v textu odpovědi.

```http
{

    "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
    "mpnId": "6363276",
    "tenant": {
        "id": "6f94b119-793c-44c7-862b-c327c9057eab",
        "adminUserAccount": "admin@TipIRIntTest705.onmicrosoft.com",
        "password": "\*\*\*\*\*\*”
    },
    "agreementSignature": {
        "id": "30ac23e7-e200-42cf-a5bc-dd9148cdc632",
        "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
        "agreementId": "1e18c5b2-e42a-4b84-82c8-d0155aa94c6e",
        "agreementType": "ValueAddedReseller",
        "dateSigned": "2021-02-23T18:10:14.8461137Z",
        "signedByFirstName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserPrincipalName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserObjectId": "e6e0c29d-acda-4ef2-b370-d37a4e06fb98",
        "signedByUserTenantId": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "attributes": {
            "objectType": "AgreementSignatureResponse"
        }
    },
    "partnerRelationship": {
        "id": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "name": "PLAMUATT2NetNew",
        "relationshipType": "is\_indirect\_reseller\_of",
        "state": "Active",
        "mpnId": "6363276",
        "attributes": {
            "objectType": "PartnerRelationshipResponse"
        }
    }
}
```
