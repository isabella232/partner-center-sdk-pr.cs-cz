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
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a><span data-ttu-id="d32eb-103">Převod zkušebního předplatného na placené pomocí Partnerské centrum API</span><span class="sxs-lookup"><span data-stu-id="d32eb-103">Convert a trial subscription to paid using Partner Center APIs</span></span>

<span data-ttu-id="d32eb-104">Zkušební předplatné můžete převést na placené.</span><span class="sxs-lookup"><span data-stu-id="d32eb-104">You can convert a trial subscription to paid.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d32eb-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d32eb-105">Prerequisites</span></span>

- <span data-ttu-id="d32eb-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d32eb-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d32eb-107">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="d32eb-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d32eb-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d32eb-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d32eb-109">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d32eb-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d32eb-110">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="d32eb-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d32eb-111">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="d32eb-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d32eb-112">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d32eb-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d32eb-113">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d32eb-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d32eb-114">ID předplatného pro aktivní zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="d32eb-114">A subscription ID for an active trial subscription.</span></span>

- <span data-ttu-id="d32eb-115">Dostupná nabídka převodu.</span><span class="sxs-lookup"><span data-stu-id="d32eb-115">An available conversion offer.</span></span>

## <a name="convert-a-trial-subscription-to-a-paid-subscription-through-code"></a><span data-ttu-id="d32eb-116">Převod zkušebního předplatného na placené předplatné prostřednictvím kódu</span><span class="sxs-lookup"><span data-stu-id="d32eb-116">Convert a trial subscription to a paid subscription through code</span></span>

<span data-ttu-id="d32eb-117">Pokud chcete zkušební předplatné převést na placené, musíte nejprve získat kolekci dostupných převodů zkušební verze.</span><span class="sxs-lookup"><span data-stu-id="d32eb-117">To convert a trial subscription to a paid one, you must first obtain a collection of the trial conversions available.</span></span> <span data-ttu-id="d32eb-118">Pak musíte zvolit nabídku převodu, kterou chcete koupit.</span><span class="sxs-lookup"><span data-stu-id="d32eb-118">Then, you must choose the conversion offer that you want to purchase.</span></span>

<span data-ttu-id="d32eb-119">Nabídky převodu budou zadat množství, které ve výchozím nastavení určuje stejný počet licencí jako zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="d32eb-119">The conversion offers will specify a quantity that defaults to the same number of licenses as the trial subscription.</span></span> <span data-ttu-id="d32eb-120">Toto množství můžete změnit nastavením vlastnosti [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) na počet licencí, které chcete zakoupit.</span><span class="sxs-lookup"><span data-stu-id="d32eb-120">You can change this quantity by setting the [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) property to the number of licenses that you want to purchase.</span></span>

> [!NOTE]
> <span data-ttu-id="d32eb-121">Bez ohledu na počet zakoupených licencí se ID předplatného zkušební verze znovu použije pro zakoupené licence.</span><span class="sxs-lookup"><span data-stu-id="d32eb-121">Regardless of the number of licenses purchased, the subscription ID of the trial is reused for the purchased licenses.</span></span> <span data-ttu-id="d32eb-122">Výsledkem je, že platnost zkušební verze zmizí a nákup se nahradí.</span><span class="sxs-lookup"><span data-stu-id="d32eb-122">As a result, the trial in effect disappears and is replaced by the purchase.</span></span>

<span data-ttu-id="d32eb-123">K převodu zkušebního předplatného prostřednictvím kódu použijte následující postup:</span><span class="sxs-lookup"><span data-stu-id="d32eb-123">Use the following steps to convert a trial subscription through code:</span></span>

1. <span data-ttu-id="d32eb-124">Získejte rozhraní pro dostupné operace předplatného.</span><span class="sxs-lookup"><span data-stu-id="d32eb-124">Get an interface to the subscription operations available.</span></span> <span data-ttu-id="d32eb-125">Musíte identifikovat zákazníka a zadat identifikátor předplatného zkušebního předplatného.</span><span class="sxs-lookup"><span data-stu-id="d32eb-125">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. <span data-ttu-id="d32eb-126">Získejte kolekci dostupných nabídek převodu.</span><span class="sxs-lookup"><span data-stu-id="d32eb-126">Get a collection of the available conversion offers.</span></span> <span data-ttu-id="d32eb-127">Další informace a podrobnosti o požadavku a odpovědi pro tuto metodu najdete v tématu Získání seznamu nabídek [převodu zkušební verze.](get-a-list-of-trial-conversion-offers.md)</span><span class="sxs-lookup"><span data-stu-id="d32eb-127">For more information and details on the request/response for this method, see [Get a list of trial conversion offers](get-a-list-of-trial-conversion-offers.md).</span></span>

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. <span data-ttu-id="d32eb-128">Zvolte nabídku převodu.</span><span class="sxs-lookup"><span data-stu-id="d32eb-128">Choose a conversion offer.</span></span> <span data-ttu-id="d32eb-129">Následující kód zvolí první nabídku převodu v kolekci.</span><span class="sxs-lookup"><span data-stu-id="d32eb-129">The following code chooses the first conversion offer in the collection.</span></span>

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. <span data-ttu-id="d32eb-130">Volitelně můžete zadat počet licencí k nákupu.</span><span class="sxs-lookup"><span data-stu-id="d32eb-130">Optionally, specify the number of licenses to purchase.</span></span> <span data-ttu-id="d32eb-131">Výchozí hodnota je počet licencí ve zkušebním předplatném.</span><span class="sxs-lookup"><span data-stu-id="d32eb-131">The default is the number of licenses in the trial subscription.</span></span>

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. <span data-ttu-id="d32eb-132">Pokud chcete [**převést**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) zkušební předplatné na placené, zavolejte metodu Create nebo [**CreateAsync.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync)</span><span class="sxs-lookup"><span data-stu-id="d32eb-132">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to convert the trial subscription to paid.</span></span>

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a><span data-ttu-id="d32eb-133">C\#</span><span class="sxs-lookup"><span data-stu-id="d32eb-133">C\#</span></span>

<span data-ttu-id="d32eb-134">Převod zkušebního předplatného na placené předplatné:</span><span class="sxs-lookup"><span data-stu-id="d32eb-134">To convert a trial subscription to a paid one:</span></span>

1. <span data-ttu-id="d32eb-135">K identifikaci zákazníka použijte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d32eb-135">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="d32eb-136">Získejte rozhraní pro operace předplatného voláním metody [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID zkušebního předplatného.</span><span class="sxs-lookup"><span data-stu-id="d32eb-136">Get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="d32eb-137">Uložte odkaz na rozhraní operací předplatného do místní proměnné.</span><span class="sxs-lookup"><span data-stu-id="d32eb-137">Save a reference to the subscription operations interface in a local variable.</span></span>

3. <span data-ttu-id="d32eb-138">Pomocí vlastnosti [**Převody**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) získejte rozhraní pro dostupné operace převodů a potom zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) nebo [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) která načte kolekci dostupných [**nabídek převodu.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion)</span><span class="sxs-lookup"><span data-stu-id="d32eb-138">Use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span> <span data-ttu-id="d32eb-139">Musíte vybrat jednu možnost.</span><span class="sxs-lookup"><span data-stu-id="d32eb-139">You must choose one.</span></span> <span data-ttu-id="d32eb-140">Následující příklad ve výchozím nastavení používá první dostupný převod.</span><span class="sxs-lookup"><span data-stu-id="d32eb-140">The following example defaults to the first conversion available.</span></span>

4. <span data-ttu-id="d32eb-141">Použijte odkaz na rozhraní operací předplatného, které jste uložili do místní proměnné, a vlastnost [**Převody**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) k získání rozhraní pro dostupné operace převodů.</span><span class="sxs-lookup"><span data-stu-id="d32eb-141">Use the reference to the subscription operations interface that you saved in a local variable and the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions.</span></span>

5. <span data-ttu-id="d32eb-142">Předejte vybraný objekt nabídky převodu [**metodě Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) a pokuste se o převod zkušební verze.</span><span class="sxs-lookup"><span data-stu-id="d32eb-142">Pass the selected conversion offer object to the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to attempt the trial conversion.</span></span>

### <a name="c-example"></a><span data-ttu-id="d32eb-143">Příklad \# jazyka C</span><span class="sxs-lookup"><span data-stu-id="d32eb-143">C\# example</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="d32eb-144">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="d32eb-144">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d32eb-145">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="d32eb-145">Request syntax</span></span>

| <span data-ttu-id="d32eb-146">Metoda</span><span class="sxs-lookup"><span data-stu-id="d32eb-146">Method</span></span>   | <span data-ttu-id="d32eb-147">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d32eb-147">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d32eb-148">**Příspěvek**</span><span class="sxs-lookup"><span data-stu-id="d32eb-148">**POST**</span></span> | <span data-ttu-id="d32eb-149">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/subscriptions/{ID_předplatného}/převody HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d32eb-149">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d32eb-150">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="d32eb-150">URI parameter</span></span>

<span data-ttu-id="d32eb-151">K identifikaci zákazníka a zkušebního předplatného použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="d32eb-151">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="d32eb-152">Název</span><span class="sxs-lookup"><span data-stu-id="d32eb-152">Name</span></span>            | <span data-ttu-id="d32eb-153">Typ</span><span class="sxs-lookup"><span data-stu-id="d32eb-153">Type</span></span>   | <span data-ttu-id="d32eb-154">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d32eb-154">Required</span></span> | <span data-ttu-id="d32eb-155">Popis</span><span class="sxs-lookup"><span data-stu-id="d32eb-155">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="d32eb-156">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="d32eb-156">customer-id</span></span>     | <span data-ttu-id="d32eb-157">řetězec</span><span class="sxs-lookup"><span data-stu-id="d32eb-157">string</span></span> | <span data-ttu-id="d32eb-158">Yes</span><span class="sxs-lookup"><span data-stu-id="d32eb-158">Yes</span></span>      | <span data-ttu-id="d32eb-159">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d32eb-159">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="d32eb-160">id předplatného</span><span class="sxs-lookup"><span data-stu-id="d32eb-160">subscription-id</span></span> | <span data-ttu-id="d32eb-161">řetězec</span><span class="sxs-lookup"><span data-stu-id="d32eb-161">string</span></span> | <span data-ttu-id="d32eb-162">Yes</span><span class="sxs-lookup"><span data-stu-id="d32eb-162">Yes</span></span>      | <span data-ttu-id="d32eb-163">Řetězec formátovaný identifikátorem GUID, který identifikuje zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="d32eb-163">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d32eb-164">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d32eb-164">Request headers</span></span>

<span data-ttu-id="d32eb-165">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d32eb-165">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d32eb-166">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d32eb-166">Request body</span></span>

<span data-ttu-id="d32eb-167">Vyplněný [prostředek Převod](conversions-resources.md#conversion) musí být součástí textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="d32eb-167">A populated [Conversion](conversions-resources.md#conversion) resource must be included in the request body.</span></span>

### <a name="request-example"></a><span data-ttu-id="d32eb-168">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d32eb-168">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="d32eb-169">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d32eb-169">REST response</span></span>

<span data-ttu-id="d32eb-170">V případě úspěchu bude tělo odpovědi obsahovat [prostředek ConversionResult.](conversions-resources.md#conversionresult)</span><span class="sxs-lookup"><span data-stu-id="d32eb-170">If successful, the response body contains a [ConversionResult](conversions-resources.md#conversionresult) resource.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="d32eb-171">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="d32eb-171">Response success and error codes</span></span>

<span data-ttu-id="d32eb-172">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d32eb-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d32eb-173">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="d32eb-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d32eb-174">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d32eb-174">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="d32eb-175">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="d32eb-175">Response example</span></span>

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
