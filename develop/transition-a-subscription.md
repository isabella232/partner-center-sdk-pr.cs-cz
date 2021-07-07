---
title: Převod předplatného
description: Upgraduje předplatné zákazníka na zadané cílové předplatné.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 01455315825cad026830268b6bbd55509e964bb5
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530225"
---
# <a name="transition-a-subscription"></a><span data-ttu-id="a5edb-103">Převod předplatného</span><span class="sxs-lookup"><span data-stu-id="a5edb-103">Transition a subscription</span></span>

<span data-ttu-id="a5edb-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a5edb-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a5edb-105">Upgraduje předplatné zákazníka na zadané cílové předplatné.</span><span class="sxs-lookup"><span data-stu-id="a5edb-105">Upgrades a customer's subscription to a specified target subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5edb-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a5edb-106">Prerequisites</span></span>

- <span data-ttu-id="a5edb-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a5edb-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a5edb-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="a5edb-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a5edb-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a5edb-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a5edb-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="a5edb-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a5edb-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="a5edb-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a5edb-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="a5edb-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a5edb-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="a5edb-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a5edb-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a5edb-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a5edb-115">Dvě ID předplatného, jeden pro počáteční předplatné a jeden pro cílové předplatné.</span><span class="sxs-lookup"><span data-stu-id="a5edb-115">Two subscription IDs, one for the initial subscription and one for the target subscription.</span></span>

## <a name="c"></a><span data-ttu-id="a5edb-116">C\#</span><span class="sxs-lookup"><span data-stu-id="a5edb-116">C\#</span></span>

<span data-ttu-id="a5edb-117">Pokud chcete upgradovat předplatné zákazníka, nejdřív [získejte předplatné customer's](get-a-subscription-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="a5edb-117">To upgrade a customer's subscription, first [get that's customer's subscription](get-a-subscription-by-id.md).</span></span> <span data-ttu-id="a5edb-118">Pak Získejte seznam upgradů pro toto předplatné voláním vlastnosti **upgrade** následovaný metodami **Get ()** nebo **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="a5edb-118">Then, obtain a list of upgrades for that subscription by calling the **Upgrades** property followed by the **Get()** or **GetAsync()** methods.</span></span> <span data-ttu-id="a5edb-119">Zvolte cíl upgradu z tohoto seznamu upgradů a potom zavolejte vlastnost **upgrady** počátečního předplatného, za kterou následuje metoda **Create ()** .</span><span class="sxs-lookup"><span data-stu-id="a5edb-119">Choose a target upgrade from that list of upgrades, and then call the **Upgrades** property of the initial subscription, followed by the **Create()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionIdForUpgrade;
// Upgrade targetOffer;

UpgradeResult upgradeResult = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionIdForUpgrade).Upgrades.Create(targetOffer);
```

<span data-ttu-id="a5edb-120">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a5edb-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a5edb-121">**Project**: PartnerSDK. FeatureSamples **třída**: UpgradeSubscription. cs</span><span class="sxs-lookup"><span data-stu-id="a5edb-121">**Project**: PartnerSDK.FeatureSamples **Class**: UpgradeSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a5edb-122">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="a5edb-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a5edb-123">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="a5edb-123">Request syntax</span></span>

| <span data-ttu-id="a5edb-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="a5edb-124">Method</span></span>   | <span data-ttu-id="a5edb-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="a5edb-125">Request URI</span></span>                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a5edb-126">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="a5edb-126">**GET**</span></span>  | <span data-ttu-id="a5edb-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription}/Upgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a5edb-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1</span></span> |
| <span data-ttu-id="a5edb-128">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="a5edb-128">**POST**</span></span> | <span data-ttu-id="a5edb-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Target}/Upgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a5edb-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1</span></span>       |

### <a name="uri-parameter"></a><span data-ttu-id="a5edb-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="a5edb-130">URI parameter</span></span>

<span data-ttu-id="a5edb-131">K převodu předplatného použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="a5edb-131">Use the following query parameter to transition the subscription.</span></span>

| <span data-ttu-id="a5edb-132">Název</span><span class="sxs-lookup"><span data-stu-id="a5edb-132">Name</span></span>                    | <span data-ttu-id="a5edb-133">Typ</span><span class="sxs-lookup"><span data-stu-id="a5edb-133">Type</span></span>     | <span data-ttu-id="a5edb-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="a5edb-134">Required</span></span> | <span data-ttu-id="a5edb-135">Popis</span><span class="sxs-lookup"><span data-stu-id="a5edb-135">Description</span></span>                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| <span data-ttu-id="a5edb-136">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="a5edb-136">**customer-tenant-id**</span></span>  | <span data-ttu-id="a5edb-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="a5edb-137">**guid**</span></span> | <span data-ttu-id="a5edb-138">Y</span><span class="sxs-lookup"><span data-stu-id="a5edb-138">Y</span></span>        | <span data-ttu-id="a5edb-139">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="a5edb-139">A GUID corresponding to the customer.</span></span>             |
| <span data-ttu-id="a5edb-140">**ID pro předplatné**</span><span class="sxs-lookup"><span data-stu-id="a5edb-140">**id-for-subscription**</span></span> | <span data-ttu-id="a5edb-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="a5edb-141">**guid**</span></span> | <span data-ttu-id="a5edb-142">Y</span><span class="sxs-lookup"><span data-stu-id="a5edb-142">Y</span></span>        | <span data-ttu-id="a5edb-143">Identifikátor GUID, který odpovídá počátečnímu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="a5edb-143">A GUID corresponding to the initial subscription.</span></span> |
| <span data-ttu-id="a5edb-144">**ID pro cíl**</span><span class="sxs-lookup"><span data-stu-id="a5edb-144">**id-for-target**</span></span>       | <span data-ttu-id="a5edb-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="a5edb-145">**guid**</span></span> | <span data-ttu-id="a5edb-146">Y</span><span class="sxs-lookup"><span data-stu-id="a5edb-146">Y</span></span>        | <span data-ttu-id="a5edb-147">Identifikátor GUID, který odpovídá cílovému předplatnému.</span><span class="sxs-lookup"><span data-stu-id="a5edb-147">A GUID corresponding to the target subscription.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="a5edb-148">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="a5edb-148">Request headers</span></span>

<span data-ttu-id="a5edb-149">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a5edb-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a5edb-150">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="a5edb-150">Request body</span></span>

<span data-ttu-id="a5edb-151">Žádná</span><span class="sxs-lookup"><span data-stu-id="a5edb-151">None</span></span>

### <a name="request-example"></a><span data-ttu-id="a5edb-152">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="a5edb-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="a5edb-153">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="a5edb-153">REST response</span></span>

<span data-ttu-id="a5edb-154">V případě úspěchu tato metoda vrátí prostředek výsledků **upgradu** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="a5edb-154">If successful, this method returns an **Upgrade** result resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a5edb-155">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="a5edb-155">Response success and error codes</span></span>

<span data-ttu-id="a5edb-156">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="a5edb-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a5edb-157">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="a5edb-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a5edb-158">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a5edb-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a5edb-159">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="a5edb-159">Response example</span></span>

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
