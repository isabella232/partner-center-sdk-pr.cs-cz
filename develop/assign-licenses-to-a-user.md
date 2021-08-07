---
title: Přiřazení licencí uživateli
description: Naučte se, jak přiřadit licence uživateli zákazníka prostřednictvím rozhraní API partnerského centra, jako je například použití \# rozhraní API jazyka C nebo REST.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8263f7f274e453603305324cc7ac6e8b25820561ade3136b873c65ffa21e94fc
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989062"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a>Přiřazení licencí uživateli prostřednictvím partnerských rozhraní API partnerského centra

Jak přiřadit licence uživateli zákazníka.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor uživatele zákazníka Toto ID identifikuje uživatele, kterému chcete přiřadit licenci.

- Identifikátor SKU produktu, který identifikuje produkt pro licenci.

## <a name="assigning-licenses-through-code"></a>Přiřazování licencí prostřednictvím kódu

Když přiřadíte licence uživateli, musíte si vybrat z kolekce předplatitelů předplatných SKU zákazníka. Po identifikaci produktů, které chcete přiřadit, musíte získat ID SKU produktu pro každý produkt, aby bylo možné provést přiřazení. Každá instance [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) obsahuje vlastnost [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) , ze které můžete odkazovat na objekt [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) a získat [**ID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).

Požadavek na přiřazení licence musí obsahovat licence z jedné skupiny licencí. Nemůžete například přiřadit licence z [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) a **skupina2** ve stejné žádosti. Pokus o přiřazení licencí z více než jedné skupiny v rámci jedné žádosti se nezdaří s příslušnou chybou. Pokud chcete zjistit, jaké licence jsou k dispozici v rámci skupiny licencí, přečtěte si téma [získání seznamu dostupných licencí podle skupiny licencí](get-a-list-of-available-licenses-by-license-group.md).

Tady je postup, jak přiřadit licence prostřednictvím kódu:

1. Vytvořte instanci objektu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) . Pomocí tohoto objektu určíte SKU produktu a plány služeb, které chcete přiřadit.

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. Naplňte vlastnosti objektu, jak je znázorněno níže. Tento kód předpokládá, že již máte ID SKU produktu a že budou přiřazeny všechny dostupné plány služeb (to znamená, že žádné nebudou vyloučeny).

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. Pokud nemáte ID SKU produktu, bude nutné načíst kolekci předplaceného SKU a získat ID SKU produktu z jednoho z nich. Tady je příklad, pokud znáte název SKU produktu.

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. Dále vytvořte instanci nového seznamu typu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)a přidejte do něj objekt License. Můžete přiřadit více než jednu licenci tím, že je přidáte do seznamu jednotlivě. Licence zahrnuté v tomto seznamu musí být ze stejné skupiny licencí.

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. Vytvořte instanci [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) a přiřaďte seznam přiřazení licencí k vlastnosti [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. Zavolejte metodu [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) a předejte objekt aktualizace licence, jak je znázorněno níže, aby bylo možné přiřadit licence.

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>C\#

Chcete-li přiřadit licenci uživateli zákazníka, nejprve vytvořte instanci objektu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) a naplňte vlastnosti [**skuId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) a [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) . Pomocí tohoto objektu určíte skladovou jednotku produktu, kterou chcete přiřadit, a plány služby, které se mají vyloučit. Dále vytvořte instanci nového seznamu typu **LicenseAssignment** a přidejte do seznamu objekt licence. Pak vytvořte instanci [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) a přiřaďte seznam přiřazení licencí k vlastnosti [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .

Dále použijte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka k identifikaci zákazníka a metodu [**Users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID uživatele k identifikaci uživatele. Pak z vlastnosti [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) Získejte rozhraní pro zákaznické operace aktualizace uživatelských licencí.

Nakonec voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) a předáním objektu aktualizace licence přiřaďte licenci.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerUserId;
// string selectedCustomerId;
// string selectedProductSkuId;

// Instantiate and populate a LicenseAssignment object.
LicenseAssignment license = new LicenseAssignment();
license.SkuId = selectedProductSkuId;
license.ExcludedPlans = null;

// Instantiate a list of licenses to assign and add the license to it.
List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
licenseList.Add(license);

// Instantiate a LicenseUpdate object and add the list of licenses to assign.
LicenseUpdate updateLicense = new LicenseUpdate();
updateLicense.LicensesToAssign = licenseList;

// Update the user licenses.
var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Project**: **třída** microsoft Partner SDK samples: CustomerUserAssignLicenses. cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenseupdates HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci zákazníka a uživatele použijte následující parametry cesty.

| Název        | Typ   | Vyžadováno | Popis                                       |
|-------------|--------|----------|---------------------------------------------------|
| ID zákazníka | řetězec | Yes      | ID formátovaného identifikátoru GUID identifikující zákazníka. |
| user-id     | řetězec | Yes      | ID formátované identifikátorem GUID, které uživatele identifikuje.     |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Do textu žádosti zadejte prostředek [LicenseUpdate](license-resources.md#licenseupdate) , který určuje, jaké licence se mají přiřadit.

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/554526aa-cf5e-46fa-95df-98dbc55d8a1e/licenseupdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 183
Expect: 100-continue

{
    "LicensesToAssign": [{
            "ExcludedPlans": null,
            "SkuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "LicensesToRemove": null,
    "LicenseWarnings": null,
    "Attributes": {
        "ObjectType": "LicenseUpdate"
    }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu se vrátí stavový kód odpovědi HTTP 201 a tělo odpovědi obsahuje prostředek [LicenseUpdate](license-resources.md#licenseupdate) s informacemi o licenci.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example-success"></a>Příklad odpovědi (úspěch)

```http
HTTP/1.1 201 Created
Content-Length: 139
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CV: 5AnzcZQrvUqCq3kd.0
MS-ServerId: 030020525
Date: Thu, 20 Apr 2017 21:50:39 GMT

{
    "licensesToAssign": [{
            "skuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "licenseWarnings": [],
    "attributes": {
        "objectType": "LicenseUpdate"
    }
}
```

### <a name="response-example-license-isnt-available"></a>Příklad odpovědi (licence není k dispozici)

```http
HTTP/1.1 400 Bad Request
Content-Length: 341
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: f4f3b748-8b22-4d07-a5a1-dceb32824192
MS-CV: 5npA0K22CUmWPOzB.0
MS-ServerId: 102030524
Date: Thu, 20 Apr 2017 22:12:36 GMT

{
    "code": 60012,
    "description": "We&#39;re sorry, it looks like you've run out of licenses. Buy more licenses, and then try again.",
    "data": ["LicenseQuotaExceededException : Subscription with Account 0c39d6d5-c70d-4c55-bc02-f620844f3fd1 and SKU f8a1db68-be16-40ed-86d5-cb42ce701560 does not have any available licenses left."],
    "source": "PartnerFD"
}
```
