---
title: Získání kolekce nároků
description: Jak získat kolekci nároků.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d2cc485429941dd2080bd285553333a01fc0ffd1
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766848"
---
# <a name="get-a-collection-of-entitlements"></a>Získání kolekce nároků

**Platí pro**

- Partnerské centrum

Jak získat kolekci nároků.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Chcete-li získat kolekci nároků pro zákazníka, Získejte rozhraní pro udělení [**operací**](entitlement-resources.md#entitlement) voláním metody  [**IAggregatePartner. Customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka pro identifikaci zákazníka. Pak načtěte rozhraní z vlastnosti **oprávnění** a zavolejte metodu **Get ()** nebo **GetAsync ()** pro načtení kolekce nároků.

``` csharp
IAggregatePartner partnerOperations;
string customerId;

// Get the collection of entitlements.
var entitlements = partnerOperations.Customers.ById(customerId).Entitlements.Get();
```

Chcete-li naplnit data vypršení platnosti pro získání nároků, zavolejte stejné metody výše a nastavte volitelný logický parametr **showExpiry** na hodnotu true **Get (true)** nebo **GetAsync (true)**. To znamená, že se vyžadují data vypršení platnosti nároku (Pokud je to možné).

> [!IMPORTANT]
> Pro místní typy nároků neexistují data vypršení platnosti.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda | Identifikátor URI žádosti |
|--------|-------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customerId}/Entitlements HTTP/1.1                            |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

Při vytváření žádosti použijte následující cestu a parametry dotazu.

| Název | Typ | Vyžadováno | Popis |
|------|------|----------|-------------|
| customerId | řetězec | Yes | Identifikátor ID zákazníka ve formátu GUID, který identifikuje zákazníka. |
| entitlementType | řetězec | No | Dá se použít k určení typu nároků, které se mají načíst (**software** nebo **reservedInstance** ). Pokud není nastavené, načtou se všechny typy. |
| showExpiry | boolean | No | Volitelný příznak, který označuje, jestli se vyžadují data vypršení platnosti nároků. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/entitlements HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [nároků](entitlement-resources.md#entitlement) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 103778
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: EjFdw8fCpkKyMyza.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:42:51 GMT

{
  "totalCount": 2,
  "items": [
    {
      "includedEntitlements": [],
      "referenceOrder": {
        "id": "KaJ8XvkKc_GoNZOUyjVaRJalTBN5MWdV1",
        "lineItemId": "0"
      },
      "productId": "DZH318Z0BQ3W",
      "quantity": 1,
      "entitledArtifacts": [
        {
          "link": {
            "uri": "/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336",
            "method": "GET",
            "headers": []
          },
          "resourceId": "ebf2e74b-630e-4a09-857d-a1f6c6351336",
          "artifactType": "reservedinstance"
        }
      ],
      "skuId": "007J",
      "entitlementType": "reservedinstance"
      "dynamicAttributes": {
               "reservationType": "virtualmachines"
        }
    },
    {
      "includedEntitlements": [
        {
          "includedEntitlements": [],
          "referenceOrder": {
              "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
              "lineItemId": "0"
          },
          "productId": "DG7GMGF0DWTJ",
          "quantity": 1,
          "entitledArtifacts": [],
          "skuId": "0001",
          "entitlementType": "software"
        },
        {
          "includedEntitlements": [],
          "referenceOrder": {
            "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
            "lineItemId": "0"
          },
            "productId": "DG7GMGF0DWLG",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
          }
        ],
        "referenceOrder": {
          "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
          "lineItemId": "0"
        },
        "productId": "DG7GMGF0DWTK",
        "quantity": 1,
        "entitledArtifacts": [],
        "skuId": "0002",
        "entitlementType": "software"
    }
  ],
  "attributes": {
    "objectType": "Collection"
  }
}
```

## <a name="additional-examples"></a>Další příklady

Následující příklad ukazuje, jak načíst konkrétní typ nároků spolu s daty vypršení platnosti (je-li k dispozici).

### <a name="c-example"></a>\#Příklad C

Chcete-li načíst konkrétní typ oprávnění, Získejte rozhraní **ByEntitlementType** z rozhraní **nároků** a použijte metody **Get ()** nebo **GetAsync ()** .

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("software").Get(true);
```

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/de3dcef9-9991-459c-ac71-2903d1127414/entitlements?entitlementtype=software&showExpiry=true
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 1791
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
X-Locale: en-US
MS-CV: yD+4LBKePUSp/vqJ.0
MS-ServerId: 000002
Date: Mon, 28 Jan 2019 18:31:43 GMT

{
    "totalCount": 2,
    "items": [
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWM2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWMK",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "0",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWM3",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
        },
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV1",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "1",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWBQ",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0003",
            "entitlementType": "software",
            "expiryDate": "2022-01-28T00:00:00Z"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

Následující příklady vám ukážou, jak načíst informace o produktech a rezervacích od nároku.

### <a name="retrieve-virtual-machine-reservation-details-from-an-entitlement-by-using-sdk-v18"></a>Načíst podrobnosti rezervace virtuálních počítačů z nároku pomocí sady SDK V 1.8

### <a name="c-example"></a>\#Příklad C

Pokud chcete získat další podrobnosti týkající se rezervací virtuálních počítačů od nároku, vyvolejte identifikátor URI vystavený v rámci entitledArtifacts. Propojte s artifactType = virtual_machine_reserved_instance.

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("VirtualMachineReservedInstance").Get();

((VirtualMachineReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.VirtualMachineReservedInstance)).Link.InvokeAsync<VirtualMachineReservedInstanceArtifactDetails>(partnerOperations)
```

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/virtualmachinereservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "virtual_machine_reserved_instance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="retrieve-reservation-details-from-an-entitlement-by-using-sdk-v19"></a>Načtení podrobností o rezervacích z nároku pomocí sady SDK V 1.9

### <a name="c-example"></a>\#Příklad C

Chcete-li získat další podrobnosti týkající se rezervací z rezervované instance, vyvolejte identifikátor URI vystavený v ```entitledArtifacts.link``` rámci ```artifactType = reservedinstance``` .

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("ReservedInstance").Get();

((ReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.ReservedInstance)).Link.InvokeAsync<ReservedInstanceArtifactDetails>(partnerOperations);
```

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "reservedinstance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="api-consumers"></a>Příjemci rozhraní API

Partneři, kteří používají rozhraní API k dotazování na nároky na rezervované instance virtuálního počítače – aktualizujte identifikátor URI požadavku z **/Customers/{customerId}/Entitlements na/Customers/{customerId}/Entitlements? entitlementType = virtualmachinereservedinstance** , aby se zachovala zpětná kompatibilita. Aby bylo možné využívat virtuální počítač nebo Azure SQL s pokročilou smlouvou, aktualizujte identifikátor URI žádosti na **/Customers/{customerId}/Entitlements? entitlementType = reservedinstance**.
