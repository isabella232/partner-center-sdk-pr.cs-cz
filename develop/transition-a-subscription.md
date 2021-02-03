---
title: Převod předplatného
description: Upgraduje předplatné zákazníka na zadané cílové předplatné.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b757eee8bc65c16b5c65221a4c14b6c0fd6369e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766730"
---
# <a name="transition-a-subscription"></a><span data-ttu-id="f7483-103">Převod předplatného</span><span class="sxs-lookup"><span data-stu-id="f7483-103">Transition a subscription</span></span>

<span data-ttu-id="f7483-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="f7483-104">**Applies To**</span></span>

- <span data-ttu-id="f7483-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="f7483-105">Partner Center</span></span>
- <span data-ttu-id="f7483-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="f7483-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f7483-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="f7483-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f7483-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f7483-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f7483-109">Upgraduje předplatné zákazníka na zadané cílové předplatné.</span><span class="sxs-lookup"><span data-stu-id="f7483-109">Upgrades a customer's subscription to a specified target subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7483-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f7483-110">Prerequisites</span></span>

- <span data-ttu-id="f7483-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f7483-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f7483-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="f7483-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f7483-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f7483-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f7483-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="f7483-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f7483-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="f7483-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f7483-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="f7483-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f7483-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="f7483-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f7483-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f7483-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f7483-119">Dvě ID předplatného, jeden pro počáteční předplatné a jeden pro cílové předplatné.</span><span class="sxs-lookup"><span data-stu-id="f7483-119">Two subscription IDs, one for the initial subscription and one for the target subscription.</span></span>

## <a name="c"></a><span data-ttu-id="f7483-120">C\#</span><span class="sxs-lookup"><span data-stu-id="f7483-120">C\#</span></span>

<span data-ttu-id="f7483-121">Pokud chcete upgradovat předplatné zákazníka, nejdřív [získejte předplatné customer's](get-a-subscription-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="f7483-121">To upgrade a customer's subscription, first [get that's customer's subscription](get-a-subscription-by-id.md).</span></span> <span data-ttu-id="f7483-122">Pak Získejte seznam upgradů pro toto předplatné voláním vlastnosti **upgrade** následovaný metodami **Get ()** nebo **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="f7483-122">Then, obtain a list of upgrades for that subscription by calling the **Upgrades** property followed by the **Get()** or **GetAsync()** methods.</span></span> <span data-ttu-id="f7483-123">Zvolte cíl upgradu z tohoto seznamu upgradů a potom zavolejte vlastnost **upgrady** počátečního předplatného, za kterou následuje metoda **Create ()** .</span><span class="sxs-lookup"><span data-stu-id="f7483-123">Choose a target upgrade from that list of upgrades, and then call the **Upgrades** property of the initial subscription, followed by the **Create()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionIdForUpgrade;
// Upgrade targetOffer;

UpgradeResult upgradeResult = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionIdForUpgrade).Upgrades.Create(targetOffer);
```

<span data-ttu-id="f7483-124">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f7483-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f7483-125">**Projekt**: PartnerSDK. FeatureSamples **Třída**: UpgradeSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="f7483-125">**Project**: PartnerSDK.FeatureSamples **Class**: UpgradeSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f7483-126">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="f7483-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f7483-127">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="f7483-127">Request syntax</span></span>

| <span data-ttu-id="f7483-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="f7483-128">Method</span></span>   | <span data-ttu-id="f7483-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="f7483-129">Request URI</span></span>                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f7483-130">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="f7483-130">**GET**</span></span>  | <span data-ttu-id="f7483-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription}/Upgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f7483-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1</span></span> |
| <span data-ttu-id="f7483-132">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="f7483-132">**POST**</span></span> | <span data-ttu-id="f7483-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Target}/Upgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f7483-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1</span></span>       |

### <a name="uri-parameter"></a><span data-ttu-id="f7483-134">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="f7483-134">URI parameter</span></span>

<span data-ttu-id="f7483-135">K převodu předplatného použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="f7483-135">Use the following query parameter to transition the subscription.</span></span>

| <span data-ttu-id="f7483-136">Název</span><span class="sxs-lookup"><span data-stu-id="f7483-136">Name</span></span>                    | <span data-ttu-id="f7483-137">Typ</span><span class="sxs-lookup"><span data-stu-id="f7483-137">Type</span></span>     | <span data-ttu-id="f7483-138">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="f7483-138">Required</span></span> | <span data-ttu-id="f7483-139">Popis</span><span class="sxs-lookup"><span data-stu-id="f7483-139">Description</span></span>                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| <span data-ttu-id="f7483-140">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="f7483-140">**customer-tenant-id**</span></span>  | <span data-ttu-id="f7483-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="f7483-141">**guid**</span></span> | <span data-ttu-id="f7483-142">Y</span><span class="sxs-lookup"><span data-stu-id="f7483-142">Y</span></span>        | <span data-ttu-id="f7483-143">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="f7483-143">A GUID corresponding to the customer.</span></span>             |
| <span data-ttu-id="f7483-144">**ID pro předplatné**</span><span class="sxs-lookup"><span data-stu-id="f7483-144">**id-for-subscription**</span></span> | <span data-ttu-id="f7483-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="f7483-145">**guid**</span></span> | <span data-ttu-id="f7483-146">Y</span><span class="sxs-lookup"><span data-stu-id="f7483-146">Y</span></span>        | <span data-ttu-id="f7483-147">Identifikátor GUID, který odpovídá počátečnímu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="f7483-147">A GUID corresponding to the initial subscription.</span></span> |
| <span data-ttu-id="f7483-148">**ID pro cíl**</span><span class="sxs-lookup"><span data-stu-id="f7483-148">**id-for-target**</span></span>       | <span data-ttu-id="f7483-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="f7483-149">**guid**</span></span> | <span data-ttu-id="f7483-150">Y</span><span class="sxs-lookup"><span data-stu-id="f7483-150">Y</span></span>        | <span data-ttu-id="f7483-151">Identifikátor GUID, který odpovídá cílovému předplatnému.</span><span class="sxs-lookup"><span data-stu-id="f7483-151">A GUID corresponding to the target subscription.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="f7483-152">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="f7483-152">Request headers</span></span>

<span data-ttu-id="f7483-153">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f7483-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f7483-154">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="f7483-154">Request body</span></span>

<span data-ttu-id="f7483-155">Žádné</span><span class="sxs-lookup"><span data-stu-id="f7483-155">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f7483-156">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="f7483-156">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

POST https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 750fd5ea-904b-4c3e-b476-60d0feacab0d
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
Content-Type: application/json
Content-Length: 1098
Expect: 100-continue

{
    "TargetOffer":{
        "Id":"796B6B5F-613C-4E24-A17C-EBA730D49C02",
        "Name":"Office 365 Enterprise E3",
        "Description":"The best plan for businesses that need full productivity, communication and collaboration tools with the familiar Office suite, including Office Online.",
        "MinimumQuantity":1,
        "MaximumQuantity":10000000,
        "Rank":61,
        "Uri":"/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/796B6B5F-613C-4E24-A17C-EBA730D49C02",
        "Locale":"en-us",
        "Country":"US",
        "Category":{
            "Id":"Enterprise_Key",
            "Name":"Enterprise",
            "Rank":20,
            "Locale":"en-us",
            "Country":"US",
            "Attributes":{
                "ObjectType":"OfferCategory"
            }
        },
        "PrerequisiteOffers":[],
        "IsAddOn":false,
        "IsAvailableForPurchase":true,
        "Billing":"license",
        "IsAutoRenewable":true,
        "Product":{
            "Id":"6fd2c87f-b296-42f0-b197-1e91e994b900",
            "Name":"Office 365 Enterprise E3",
            "Unit":"Licenses"
        },
        "UnitType":"Licenses",
        "Links":{
            "LearnMore":{
                "Uri":"http://g.microsoftonline.com/0BXPS00en/1015",
                "Method":"GET",
                "Headers":[]
            }
        }
        "Attributes":{
            "ObjectType":"Offer"
        }
    },
    "UpgradeType":1,
    "IsEligible":true,
    "Quantity":1,
    "UpgradeErrors":[],
    "Attributes":{
        "ObjectType":"Upgrade"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="f7483-157">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="f7483-157">REST response</span></span>

<span data-ttu-id="f7483-158">V případě úspěchu tato metoda vrátí prostředek výsledků **upgradu** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="f7483-158">If successful, this method returns an **Upgrade** result resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f7483-159">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="f7483-159">Response success and error codes</span></span>

<span data-ttu-id="f7483-160">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="f7483-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f7483-161">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="f7483-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f7483-162">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f7483-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f7483-163">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="f7483-163">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 29 Jan 2016 20:42:26 GMT

{
    "totalCount": 1,
    "items": [{
        "targetOffer": {
            "id": "91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "name": "Office 365 Enterprise E1",
            "description": "For businesses that need communication and collaboration tools and the ability to read and do lightweight editing of documents with Office Online.",
            "minimumQuantity": 1,
            "maximumQuantity": 10000000,
            "rank": 48,
            "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "locale": "en-us",
            "country": "US",
            "category": {
                "id": "Enterprise_Key",
                "name": "Enterprise",
                "rank": 20,
                "locale": "en-us",
                "country": "US",
                "attributes": {
                    "objectType": "OfferCategory"
                }
            },
            "prerequisiteOffers": [],
            "isAddOn": false,
            "isAvailableForPurchase": true,
            "billing": "license",
            "isAutoRenewable": true,
            "isInternal": false,
            "conversionTargetOffers": [],
            "partnerQualifications": ["none"],
            "product": {
                "id": "18181a46-0d4e-45cd-891e-60aabd171b4e",
                "name": "Office 365 Enterprise E1",
                "unit": "Licenses"
            },
            "unitType": "Licenses",
            "links": {
                "learnMore": {
                    "uri": "http://g.microsoftonline.com/0BXPS00en/1013",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/offers/91FD106F-4B2C-4938-95AC-F54F74E9A239?country=US",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Offer"
            }
        },
        "upgradeType": "upgrade_only",
        "isEligible": false,
        "quantity": 1,
        "upgradeErrors": [{
            "code": 2,
            "description": "Subscription cannot be upgraded because the source subscription state is not active.  Additional Details contains the current source subscription state.",
            "attributes": {
                "objectType": "UpgradeError"
            }
        }],
        "attributes": {
            "objectType": "Upgrade"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}

HTTP/1.1 200 OK
Content-Length: 448
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 750fd5ea-904b-4c3e-b476-60d0feacab0d
MS-CV: RnK86LBbDkWP/w2R.0
MS-ServerId: 102031201
Date: Fri, 29 Jan 2016 20:44:21 GMT

{
    "sourceSubscriptionId":"896a2862-67e2-4f3d-bb3f-c50c42b5fad8",
    "targetSubscriptionId":"2add8a55-454a-4ae5-a4c9-5107dc6e9768",
    "upgradeType":1,
    "upgradeErrors":[],
    "licenseErrors":[],
    "attributes":{
        "objectType":"UpgradeResult"
    }
}
```
