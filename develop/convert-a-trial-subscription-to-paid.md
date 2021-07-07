---
title: Převod zkušební verze předplatného na placenou
description: Naučte se používat Partnerské centrum API k převodu zkušebního předplatného na placené.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1876cfc796b683bfff00b7d137bcfe0b7162c78
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973855"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a>Převod zkušebního předplatného na placené pomocí Partnerské centrum API

Zkušební předplatné můžete převést na placené.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného pro aktivní zkušební předplatné.

- Dostupná nabídka převodu.

## <a name="convert-a-trial-subscription-to-a-paid-subscription-through-code"></a>Převod zkušebního předplatného na placené předplatné prostřednictvím kódu

Pokud chcete zkušební předplatné převést na placené, musíte nejprve získat kolekci dostupných převodů zkušební verze. Pak musíte zvolit nabídku převodu, kterou chcete koupit.

Nabídky převodu budou zadat množství, které ve výchozím nastavení určuje stejný počet licencí jako zkušební předplatné. Toto množství můžete změnit nastavením vlastnosti [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) na počet licencí, které chcete zakoupit.

> [!NOTE]
> Bez ohledu na počet zakoupených licencí se ID předplatného zkušební verze znovu použije pro zakoupené licence. Výsledkem je, že platnost zkušební verze zmizí a nákup se nahradí.

K převodu zkušebního předplatného prostřednictvím kódu použijte následující postup:

1. Získejte rozhraní pro dostupné operace předplatného. Musíte identifikovat zákazníka a zadat identifikátor předplatného zkušebního předplatného.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. Získejte kolekci dostupných nabídek převodu. Další informace a podrobnosti o požadavku a odpovědi pro tuto metodu najdete v tématu Získání seznamu nabídek [převodu zkušební verze.](get-a-list-of-trial-conversion-offers.md)

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. Zvolte nabídku převodu. Následující kód zvolí první nabídku převodu v kolekci.

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. Volitelně můžete zadat počet licencí k nákupu. Výchozí hodnota je počet licencí ve zkušebním předplatném.

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. Pokud chcete [**převést**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) zkušební předplatné na placené, zavolejte metodu Create nebo [**CreateAsync.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync)

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a>C\#

Převod zkušebního předplatného na placené předplatné:

1. K identifikaci zákazníka použijte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.

2. Získejte rozhraní pro operace předplatného voláním metody [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID zkušebního předplatného. Uložte odkaz na rozhraní operací předplatného do místní proměnné.

3. Pomocí vlastnosti [**Převody**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) získejte rozhraní pro dostupné operace převodů a potom zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) nebo [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) která načte kolekci dostupných [**nabídek převodu.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) Musíte vybrat jednu možnost. Následující příklad ve výchozím nastavení používá první dostupný převod.

4. Použijte odkaz na rozhraní operací předplatného, které jste uložili do místní proměnné, a vlastnost [**Převody**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) k získání rozhraní pro dostupné operace převodů.

5. Předejte vybraný objekt nabídky převodu [**metodě Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) a pokuste se o převod zkušební verze.

### <a name="c-example"></a>Příklad \# jazyka C

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

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **Příspěvek** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/subscriptions/{ID_předplatného}/převody HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K identifikaci zákazníka a zkušebního předplatného použijte následující parametry cesty.

| Název            | Typ   | Vyžadováno | Popis                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| id zákazníka     | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.           |
| id předplatného | řetězec | Yes      | Řetězec formátovaný identifikátorem GUID, který identifikuje zkušební předplatné. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Vyplněný [prostředek Převod](conversions-resources.md#conversion) musí být součástí textu požadavku.

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

V případě úspěchu bude tělo odpovědi obsahovat [prostředek ConversionResult.](conversions-resources.md#conversionresult)

#### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)

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
