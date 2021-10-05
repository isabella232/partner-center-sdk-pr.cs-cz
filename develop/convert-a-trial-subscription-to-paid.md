---
title: Převod zkušební verze předplatného na placenou
description: Naučte se používat rozhraní API partnerského centra k převedení zkušebního předplatného na placené předplatné.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7cee9b9afddb12137bb66b57250a9487bd4902f5
ms.sourcegitcommit: f112efee7344d739bdbf385adba0c554ea2a63e3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2021
ms.locfileid: "129439323"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a>Převod zkušebního předplatného na placené pomocí rozhraní API partnerského centra

> [!NOTE]
> Tyto kroky se nevztahují na nové produkty pro obchod. Přečtěte si, jak přejít na novou dokumentaci k **předplatnému pro obchod** pro převod nových zkušebních verzí na placené předplatné

Zkušební předplatné můžete převést na placené.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného pro aktivní zkušební předplatné.

- Dostupná nabídka pro převod.

## <a name="convert-a-trial-subscription-to-a-paid-subscription-through-code"></a>Převod zkušebního předplatného na placené předplatné prostřednictvím kódu

K převedení zkušebního předplatného na placené předplatné musíte nejdřív získat kolekci zkušebních verzí, které jsou k dispozici. Pak je nutné zvolit nabídku pro převod, kterou chcete koupit.

Nabídka převodů určí množství, které se ve výchozím nastavení shoduje se stejným počtem licencí jako zkušební předplatné. Toto množství můžete změnit nastavením vlastnosti [**množství**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) na počet licencí, které chcete koupit.

> [!NOTE]
> Bez ohledu na počet zakoupených licencí se ID předplatného zkušební verze znovu použije pro zakoupené licence. V důsledku toho se zkušební verze v tomto případě zmizí a její nákup se nahradí.

K převedení zkušebního předplatného prostřednictvím kódu použijte následující postup:

1. Získat rozhraní k dispozici pro operace odběru. Musíte identifikovat zákazníka a zadat identifikátor předplatného zkušebního předplatného.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. Získá kolekci dostupných nabídek převodu. Další informace a podrobnosti o žádosti a odpovědi pro tuto metodu najdete v tématu [získání seznamu nabídek pro převod zkušební verze](get-a-list-of-trial-conversion-offers.md).

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. Vyberte nabídku pro převod. Následující kód zvolí první nabídku převodu v kolekci.

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. Volitelně zadejte počet licencí, které se mají koupit. Výchozí hodnota je počet licencí ve zkušebním předplatném.

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. Voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) převeďte zkušební předplatné na placené.

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a>C\#

Převod zkušebního předplatného na placené předplatné:

1. K identifikaci zákazníka použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.

2. Přičtěte si rozhraní k operacím předplatného voláním metody [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID zkušebního předplatného. Uložte odkaz na rozhraní operace odběru v místní proměnné.

3. Použijte vlastnost [**převody**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) k získání rozhraní k dostupným operacím pro převody a potom zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) pro načtení kolekce dostupných nabídek [**převodu**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) . Musíte zvolit jednu z nich. Následující příklad je výchozím nastavením prvního dostupného převodu.

4. Použijte odkaz na rozhraní operace předplatného, které jste uložili v místní proměnné a vlastnost [**převody**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) , abyste získali rozhraní k dostupným operacím pro převody.

5. Předejte vybraný objekt nabídky pro převod do metody [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) k pokusu o převod zkušební verze.

### <a name="c-example"></a>\#Příklad C

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get subscription operations for the trial subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the available conversions.
var conversions = subscriptionOperations.Conversions.Get();

// If there are no conversions available, we&#39;re done.
// Otherwise, convert the trial to the first available conversion offer.
if (conversions.TotalCount <= 0)
{
    System.Console.WriteLine("This subscription has no conversions");
}
else
{
    // Default to the first conversion.
    var selectedConversion = conversions.Items.ToList()[0];

    // Convert the trial and return the result.
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
}
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/Conversions HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K identifikaci zákazníka a zkušebního předplatného použijte následující parametry cesty.

| Název            | Typ   | Vyžadováno | Popis                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| ID zákazníka     | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.           |
| ID předplatného | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zkušební předplatné. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

V textu žádosti musí být zahrnutý prostředek pro [Převod](conversions-resources.md#conversion) .

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 234
Expect: 100-continue

{
    "OfferId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "TargetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "OrderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
    "Quantity": 25,
    "BillingCycle": "monthly",
    "Attributes": {
        "ObjectType": "Conversion"
    }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi prostředek [ConversionResult](conversions-resources.md#conversionresult) .

#### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

#### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 211
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CV: kW4GzmhvHEqCq1ls.0
MS-ServerId: 030020643
Date: Thu, 15 Jun 2017 23:10:40 GMT

 {
    "subscriptionId": "488745B5-2086-4912-802C-6ABB9F7C3638",
    "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "attributes": {
        "objectType": "ConversionResult"
    }
}
```
