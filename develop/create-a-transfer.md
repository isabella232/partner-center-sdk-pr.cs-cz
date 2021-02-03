---
title: Vytvořit přenos
description: Jak vytvořit přenos předplatných pro zákazníka.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5e70cc5b7ce4fcfa715f581a2151f0b8d1922b0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766694"
---
# <a name="create-a-transfer"></a>Vytvořit přenos

**Platí pro:**

- Partnerské centrum

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Transfers HTTP/1.1                    |

### <a name="uri-parameter"></a>Parametr URI

K identifikaci zákazníka použijte následující parametr cesty.

| Název            | Typ     | Vyžadováno | Popis                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ID zákazníka** | řetězec   | Yes      | Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.             |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje vlastnosti [TransferEntity](transfer-entity-resources.md) v textu požadavku.

| Vlastnost              | Typ          | Vyžadováno  | Popis                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| id                    | řetězec        | No    | TransferEntity identifikátor, který je poskytnut po úspěšném vytvoření transferEntity.                               |
| createdTime           | DateTime      | No    | Datum, kdy byl transferEntity vytvořen, ve formátu data a času. Použito po úspěšném vytvoření transferEntity.      |
| Časposledníúpravy      | DateTime      | No    | Datum poslední aktualizace transferEntity ve formátu data a času. Použito po úspěšném vytvoření transferEntity. |
| lastModifiedUser      | řetězec        | No    | Uživatel, který transferEntity naposledy aktualizoval. Použito po úspěšném vytvoření transferEntity.                          |
| customerName          | řetězec        | No    | Nepovinný parametr. Jméno zákazníka, jehož odběry se přenáší.                                              |
| customerTenantId      | řetězec        | No    | Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka. Použito po úspěšném vytvoření transferEntity.         |
| partnertenantid       | řetězec        | No    | ID partnera naformátovaného identifikátorem GUID, který identifikuje partnera.                                                                   |
| sourcePartnerName     | řetězec        | No    | Nepovinný parametr. Název organizace partnera, který iniciuje přenos.                                           |
| sourcePartnerTenantId | řetězec        | Yes   | ID partnera naformátovaného identifikátorem GUID, který identifikuje partnera iniciující přenos.                                           |
| targetPartnerName     | řetězec        | No    | Nepovinný parametr. Název organizace partnera, na kterou je přenos zaměřen.                                         |
| targetPartnerTenantId | řetězec        | Yes   | ID partnera formátovaného identifikátorem GUID, který identifikuje partnera, kterému je směrován cíl přenosu.                                  |
| Položky řádku             | Pole objektů | Yes| Pole prostředků [TransferLineItem](transfer-entity-resources.md#transferlineitem)                                   |
| status                | řetězec        | No    | Stav transferEntity. Možné hodnoty jsou "aktivní" (lze je odstranit/odeslat) a "dokončeno" (již bylo dokončeno). Použito po úspěšném vytvoření transferEntity.|

Tato tabulka popisuje vlastnosti [TransferLineItem](transfer-entity-resources.md#transferlineitem) v textu požadavku.

|      Vlastnost       |            Typ             | Vyžadováno | Popis                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| id                   | řetězec                     | No       | Jedinečný identifikátor pro položku na lince přenosu. Použito po úspěšném vytvoření transferEntity.|
| subscriptionId       | řetězec                     | Yes      | Identifikátor předplatného.                                                                         |
| quantity             | int                        | No       | Počet licencí nebo instancí.                                                                 |
| billingCycle         | Objekt                     | No       | Typ fakturačního cyklu nastaveného pro aktuální období.                                                |
| friendlyName         | řetězec                     | No       | Nepovinný parametr. Popisný název položky definované partnerem, který vám umožní určit nejednoznačnost.                |
| partnerIdOnRecord    | řetězec                     | No       | PartnerId na záznamu (MPNID) při nákupu, který se stane při přijetí přenosu.              |
| Hodnotami OfferId              | řetězec                     | No       | Identifikátor nabídky                                                                                |
| addonItems           | Seznam objektů **TransferLineItem** | No | Kolekce položek řádku transferEntity pro doplňky, které se přenesou spolu se základním předplatným, které se přenáší. Použito po úspěšném vytvoření transferEntity.|
| transferError        | řetězec                     | No       | Používá se po přijetí transferEntity v případě chyby.                                        |
| status               | řetězec                     | No       | Stav LineItem v transferEntity.                                                    |

### <a name="request-example"></a>Příklad požadavku

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí naplněný prostředek [TransferEnity](transfer-entity-resources.md) v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```
