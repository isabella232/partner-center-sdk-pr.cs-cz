---
title: Převod zkušební verze předplatného na placenou
description: Naučte se používat rozhraní API partnerského centra k převedení zkušebního předplatného na placené předplatné.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 59dcf6caf21d407b2fba4cc8438bc435fda9dc77
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2020
ms.locfileid: "97767106"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a><span data-ttu-id="fcb9e-103">Převod zkušebního předplatného na placené pomocí rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="fcb9e-103">Convert a trial subscription to paid using Partner Center APIs</span></span>

<span data-ttu-id="fcb9e-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="fcb9e-104">**Applies to:**</span></span>

- <span data-ttu-id="fcb9e-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="fcb9e-105">Partner Center</span></span>

<span data-ttu-id="fcb9e-106">Zkušební předplatné můžete převést na placené.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-106">You can convert a trial subscription to paid.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcb9e-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="fcb9e-107">Prerequisites</span></span>

- <span data-ttu-id="fcb9e-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fcb9e-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fcb9e-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="fcb9e-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fcb9e-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fcb9e-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fcb9e-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fcb9e-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fcb9e-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="fcb9e-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fcb9e-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fcb9e-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fcb9e-116">ID předplatného pro aktivní zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-116">A subscription ID for an active trial subscription.</span></span>

- <span data-ttu-id="fcb9e-117">Dostupná nabídka pro převod.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-117">An available conversion offer.</span></span>

## <a name="convert-a-trial-subscription-to-paid-through-code"></a><span data-ttu-id="fcb9e-118">Převod zkušebního předplatného na placený kód</span><span class="sxs-lookup"><span data-stu-id="fcb9e-118">Convert a trial subscription to paid through code</span></span>

<span data-ttu-id="fcb9e-119">K převedení zkušebního předplatného na placené předplatné musíte nejdřív získat kolekci zkušebních verzí, které jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-119">To convert a trial subscription to a paid one, you must first obtain a collection of the trial conversions available.</span></span> <span data-ttu-id="fcb9e-120">Pak je nutné zvolit nabídku pro převod, kterou chcete koupit.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-120">Then, you must choose the conversion offer that you want to purchase.</span></span>

<span data-ttu-id="fcb9e-121">Nabídka převodů určí množství, které se ve výchozím nastavení shoduje se stejným počtem licencí jako zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-121">The conversion offers will specify a quantity that defaults to the same number of licenses as the trial subscription.</span></span> <span data-ttu-id="fcb9e-122">Toto množství můžete změnit nastavením vlastnosti [**množství**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) na počet licencí, které chcete koupit.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-122">You can change this quantity by setting the [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) property to the number of licenses that you want to purchase.</span></span>

> [!NOTE]
> <span data-ttu-id="fcb9e-123">Bez ohledu na počet zakoupených licencí se ID předplatného zkušební verze znovu použije pro zakoupené licence.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-123">Regardless of the number of licenses purchased, the subscription ID of the trial is reused for the purchased licenses.</span></span> <span data-ttu-id="fcb9e-124">V důsledku toho se zkušební verze v tomto případě zmizí a její nákup se nahradí.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-124">As a result, the trial in effect disappears and is replaced by the purchase.</span></span>

<span data-ttu-id="fcb9e-125">K převedení zkušebního předplatného prostřednictvím kódu použijte následující postup:</span><span class="sxs-lookup"><span data-stu-id="fcb9e-125">Use the following steps to convert a trial subscription through code:</span></span>

1. <span data-ttu-id="fcb9e-126">Získat rozhraní k dispozici pro operace odběru.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-126">Get an interface to the subscription operations available.</span></span> <span data-ttu-id="fcb9e-127">Musíte identifikovat zákazníka a zadat identifikátor předplatného zkušebního předplatného.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-127">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. <span data-ttu-id="fcb9e-128">Získá kolekci dostupných nabídek převodu.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-128">Get a collection of the available conversion offers.</span></span> <span data-ttu-id="fcb9e-129">Další informace a podrobnosti o žádosti a odpovědi pro tuto metodu najdete v tématu [získání seznamu nabídek pro převod zkušební verze](get-a-list-of-trial-conversion-offers.md).</span><span class="sxs-lookup"><span data-stu-id="fcb9e-129">For more information and details on the request/response for this method, see [Get a list of trial conversion offers](get-a-list-of-trial-conversion-offers.md).</span></span>

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. <span data-ttu-id="fcb9e-130">Vyberte nabídku pro převod.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-130">Choose a conversion offer.</span></span> <span data-ttu-id="fcb9e-131">Následující kód zvolí první nabídku převodu v kolekci.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-131">The following code chooses the first conversion offer in the collection.</span></span>

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. <span data-ttu-id="fcb9e-132">Volitelně zadejte počet licencí, které se mají koupit.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-132">Optionally, specify the number of licenses to purchase.</span></span> <span data-ttu-id="fcb9e-133">Výchozí hodnota je počet licencí ve zkušebním předplatném.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-133">The default is the number of licenses in the trial subscription.</span></span>

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. <span data-ttu-id="fcb9e-134">Voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) převeďte zkušební předplatné na placené.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-134">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to convert the trial subscription to paid.</span></span>

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a><span data-ttu-id="fcb9e-135">C\#</span><span class="sxs-lookup"><span data-stu-id="fcb9e-135">C\#</span></span>

<span data-ttu-id="fcb9e-136">Převod zkušebního předplatného na placené předplatné:</span><span class="sxs-lookup"><span data-stu-id="fcb9e-136">To convert a trial subscription to a paid one:</span></span>

1. <span data-ttu-id="fcb9e-137">K identifikaci zákazníka použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-137">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="fcb9e-138">Přičtěte si rozhraní k operacím předplatného voláním metody [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID zkušebního předplatného.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-138">Get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="fcb9e-139">Uložte odkaz na rozhraní operace odběru v místní proměnné.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-139">Save a reference to the subscription operations interface in a local variable.</span></span>

3. <span data-ttu-id="fcb9e-140">Použijte vlastnost [**převody**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) k získání rozhraní k dostupným operacím pro převody a potom zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) pro načtení kolekce dostupných nabídek [**převodu**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) .</span><span class="sxs-lookup"><span data-stu-id="fcb9e-140">Use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span> <span data-ttu-id="fcb9e-141">Musíte zvolit jednu z nich.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-141">You must choose one.</span></span> <span data-ttu-id="fcb9e-142">Následující příklad je výchozím nastavením prvního dostupného převodu.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-142">The following example defaults to the first conversion available.</span></span>

4. <span data-ttu-id="fcb9e-143">Použijte odkaz na rozhraní operace předplatného, které jste uložili v místní proměnné a vlastnost [**převody**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) , abyste získali rozhraní k dostupným operacím pro převody.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-143">Use the reference to the subscription operations interface that you saved in a local variable and the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions.</span></span>

5. <span data-ttu-id="fcb9e-144">Předejte vybraný objekt nabídky pro převod do metody [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) k pokusu o převod zkušební verze.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-144">Pass the selected conversion offer object to the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to attempt the trial conversion.</span></span>

### <a name="c-example"></a><span data-ttu-id="fcb9e-145">\#Příklad C</span><span class="sxs-lookup"><span data-stu-id="fcb9e-145">C\# example</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="fcb9e-146">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="fcb9e-146">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fcb9e-147">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="fcb9e-147">Request syntax</span></span>

| <span data-ttu-id="fcb9e-148">Metoda</span><span class="sxs-lookup"><span data-stu-id="fcb9e-148">Method</span></span>   | <span data-ttu-id="fcb9e-149">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="fcb9e-149">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fcb9e-150">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="fcb9e-150">**POST**</span></span> | <span data-ttu-id="fcb9e-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/Conversions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fcb9e-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fcb9e-152">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fcb9e-152">URI parameter</span></span>

<span data-ttu-id="fcb9e-153">K identifikaci zákazníka a zkušebního předplatného použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-153">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="fcb9e-154">Název</span><span class="sxs-lookup"><span data-stu-id="fcb9e-154">Name</span></span>            | <span data-ttu-id="fcb9e-155">Typ</span><span class="sxs-lookup"><span data-stu-id="fcb9e-155">Type</span></span>   | <span data-ttu-id="fcb9e-156">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fcb9e-156">Required</span></span> | <span data-ttu-id="fcb9e-157">Popis</span><span class="sxs-lookup"><span data-stu-id="fcb9e-157">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="fcb9e-158">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="fcb9e-158">customer-id</span></span>     | <span data-ttu-id="fcb9e-159">řetězec</span><span class="sxs-lookup"><span data-stu-id="fcb9e-159">string</span></span> | <span data-ttu-id="fcb9e-160">Yes</span><span class="sxs-lookup"><span data-stu-id="fcb9e-160">Yes</span></span>      | <span data-ttu-id="fcb9e-161">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-161">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="fcb9e-162">ID předplatného</span><span class="sxs-lookup"><span data-stu-id="fcb9e-162">subscription-id</span></span> | <span data-ttu-id="fcb9e-163">řetězec</span><span class="sxs-lookup"><span data-stu-id="fcb9e-163">string</span></span> | <span data-ttu-id="fcb9e-164">Yes</span><span class="sxs-lookup"><span data-stu-id="fcb9e-164">Yes</span></span>      | <span data-ttu-id="fcb9e-165">Řetězec ve formátu GUID, který identifikuje zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-165">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fcb9e-166">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="fcb9e-166">Request headers</span></span>

<span data-ttu-id="fcb9e-167">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fcb9e-167">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fcb9e-168">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="fcb9e-168">Request body</span></span>

<span data-ttu-id="fcb9e-169">V textu žádosti musí být zahrnutý prostředek pro [Převod](conversions-resources.md#conversion) .</span><span class="sxs-lookup"><span data-stu-id="fcb9e-169">A populated [Conversion](conversions-resources.md#conversion) resource must be included in the request body.</span></span>

### <a name="request-example"></a><span data-ttu-id="fcb9e-170">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="fcb9e-170">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="fcb9e-171">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="fcb9e-171">REST response</span></span>

<span data-ttu-id="fcb9e-172">V případě úspěchu obsahuje tělo odpovědi prostředek [ConversionResult](conversions-resources.md#conversionresult) .</span><span class="sxs-lookup"><span data-stu-id="fcb9e-172">If successful, the response body contains a [ConversionResult](conversions-resources.md#conversionresult) resource.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="fcb9e-173">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="fcb9e-173">Response success and error codes</span></span>

<span data-ttu-id="fcb9e-174">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-174">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fcb9e-175">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="fcb9e-175">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fcb9e-176">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fcb9e-176">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="fcb9e-177">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="fcb9e-177">Response example</span></span>

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
