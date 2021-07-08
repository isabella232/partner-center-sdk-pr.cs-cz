---
title: Získání seznamu produktů (podle zákazníka)
description: Pomocí identifikátoru zákazníka můžete získat kolekci produktů od zákazníka.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: a7cb2430aa93beb89e4d1f9b8c89a016d66624ca
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874189"
---
# <a name="get-a-list-of-products-by-customer"></a><span data-ttu-id="3c21d-103">Získání seznamu produktů (podle zákazníka)</span><span class="sxs-lookup"><span data-stu-id="3c21d-103">Get a list of products (by customer)</span></span>

<span data-ttu-id="3c21d-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3c21d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3c21d-105">Pomocí následujících metod můžete získat kolekci produktů pro existujícího zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3c21d-105">You can use the following methods to get a collection of products for an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c21d-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="3c21d-106">Prerequisites</span></span>

- <span data-ttu-id="3c21d-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3c21d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3c21d-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="3c21d-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3c21d-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3c21d-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3c21d-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="3c21d-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3c21d-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="3c21d-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3c21d-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="3c21d-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3c21d-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="3c21d-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3c21d-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3c21d-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="3c21d-115">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="3c21d-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3c21d-116">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="3c21d-116">Request syntax</span></span>

| <span data-ttu-id="3c21d-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="3c21d-117">Method</span></span> | <span data-ttu-id="3c21d-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="3c21d-118">Request URI</span></span>                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3c21d-119">POST</span><span class="sxs-lookup"><span data-stu-id="3c21d-119">POST</span></span>   | <span data-ttu-id="3c21d-120">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Products? targetView = {targetView} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3c21d-120">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1</span></span> |

#### <a name="request-uri-parameters"></a><span data-ttu-id="3c21d-121">Parametry identifikátoru URI žádosti</span><span class="sxs-lookup"><span data-stu-id="3c21d-121">Request URI parameters</span></span>

| <span data-ttu-id="3c21d-122">Název</span><span class="sxs-lookup"><span data-stu-id="3c21d-122">Name</span></span>               | <span data-ttu-id="3c21d-123">Typ</span><span class="sxs-lookup"><span data-stu-id="3c21d-123">Type</span></span> | <span data-ttu-id="3c21d-124">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="3c21d-124">Required</span></span> | <span data-ttu-id="3c21d-125">Popis</span><span class="sxs-lookup"><span data-stu-id="3c21d-125">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="3c21d-126">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="3c21d-126">**customer-tenant-id**</span></span> | <span data-ttu-id="3c21d-127">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="3c21d-127">GUID</span></span> | <span data-ttu-id="3c21d-128">Yes</span><span class="sxs-lookup"><span data-stu-id="3c21d-128">Yes</span></span> | <span data-ttu-id="3c21d-129">Hodnota je **číslo zákazníka**, který je ve formátu GUID, což je identifikátor, který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3c21d-129">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="3c21d-130">**targetView**</span><span class="sxs-lookup"><span data-stu-id="3c21d-130">**targetView**</span></span> | <span data-ttu-id="3c21d-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="3c21d-131">string</span></span> | <span data-ttu-id="3c21d-132">Yes</span><span class="sxs-lookup"><span data-stu-id="3c21d-132">Yes</span></span> | <span data-ttu-id="3c21d-133">Určuje cílové zobrazení katalogu.</span><span class="sxs-lookup"><span data-stu-id="3c21d-133">Identifies the target view of the catalog.</span></span> <span data-ttu-id="3c21d-134">Podporované hodnoty jsou:</span><span class="sxs-lookup"><span data-stu-id="3c21d-134">The supported values are:</span></span> <br/><br/><span data-ttu-id="3c21d-135">**Azure**, který zahrnuje všechny položky Azure</span><span class="sxs-lookup"><span data-stu-id="3c21d-135">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="3c21d-136">**AzureReservations**, která zahrnuje všechny položky rezervace Azure</span><span class="sxs-lookup"><span data-stu-id="3c21d-136">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="3c21d-137">**AzureReservationsVM**, která zahrnuje všechny položky rezervace virtuálních počítačů (VM)</span><span class="sxs-lookup"><span data-stu-id="3c21d-137">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="3c21d-138">**AzureReservationsSQL**, která zahrnuje všechny položky rezervace SQL</span><span class="sxs-lookup"><span data-stu-id="3c21d-138">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="3c21d-139">**AzureReservationsCosmosDb**, která zahrnuje všechny položky rezervace Cosmos databáze</span><span class="sxs-lookup"><span data-stu-id="3c21d-139">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="3c21d-140">**MicrosoftAzure**, která zahrnuje položky pro předplatná Microsoft Azure (**MS-AZR-0145P**) a plány Azure</span><span class="sxs-lookup"><span data-stu-id="3c21d-140">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="3c21d-141">**OnlineServices**, která zahrnuje všechny online položky služeb, včetně produktů z komerčního tržiště</span><span class="sxs-lookup"><span data-stu-id="3c21d-141">**OnlineServices**, which includes all online service items, including commercial marketplace products</span></span><br/><br/><span data-ttu-id="3c21d-142">**Software**, který zahrnuje všechny softwarové položky</span><span class="sxs-lookup"><span data-stu-id="3c21d-142">**Software**, which  includes all software items</span></span><br/><br/><span data-ttu-id="3c21d-143">**SoftwareSUSELinux**, která zahrnuje všechny položky softwaru SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="3c21d-143">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="3c21d-144">**SoftwarePerpetual**, která zahrnuje všechny trvalé softwarové položky</span><span class="sxs-lookup"><span data-stu-id="3c21d-144">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="3c21d-145">**SoftwareSubscriptions**, která zahrnuje všechny položky předplatného softwaru</span><span class="sxs-lookup"><span data-stu-id="3c21d-145">**SoftwareSubscriptions**, which includes all software subscription items</span></span>  |

### <a name="request-header"></a><span data-ttu-id="3c21d-146">Hlavička požadavku</span><span class="sxs-lookup"><span data-stu-id="3c21d-146">Request header</span></span>

<span data-ttu-id="3c21d-147">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3c21d-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3c21d-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="3c21d-148">Request body</span></span>

<span data-ttu-id="3c21d-149">Žádné</span><span class="sxs-lookup"><span data-stu-id="3c21d-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3c21d-150">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="3c21d-150">Request example</span></span>

<span data-ttu-id="3c21d-151">Vyžádá seznam produktů založených na využití Azure dostupných pro daného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3c21d-151">Request for a list of Azure usage-based products available to a given customer.</span></span> <span data-ttu-id="3c21d-152">pro zákazníky ve veřejném cloudu se vrátí produkty pro Microsoft Azure (MS-AZR-0145P) a plány Azure:</span><span class="sxs-lookup"><span data-stu-id="3c21d-152">Products for both Microsoft Azure (MS-AZR-0145P) and Azure plans will be returned for customers in public cloud:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="3c21d-153">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="3c21d-153">Rest response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3c21d-154">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="3c21d-154">Response success and error codes</span></span>

<span data-ttu-id="3c21d-155">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="3c21d-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3c21d-156">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="3c21d-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3c21d-157">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3c21d-157">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="3c21d-158">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="3c21d-158">This method returns the following error codes:</span></span>

| <span data-ttu-id="3c21d-159">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="3c21d-159">HTTP Status Code</span></span> | <span data-ttu-id="3c21d-160">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="3c21d-160">Error code</span></span>   | <span data-ttu-id="3c21d-161">Description</span><span class="sxs-lookup"><span data-stu-id="3c21d-161">Description</span></span>                     |
|------------------|--------------|---------------------------------|
| <span data-ttu-id="3c21d-162">403</span><span class="sxs-lookup"><span data-stu-id="3c21d-162">403</span></span> | <span data-ttu-id="3c21d-163">400036</span><span class="sxs-lookup"><span data-stu-id="3c21d-163">400036</span></span> | <span data-ttu-id="3c21d-164">Přístup k požadovanému targetView není povolený.</span><span class="sxs-lookup"><span data-stu-id="3c21d-164">Access to the requested targetView is not allowed.</span></span> |

### <a name="response-example"></a><span data-ttu-id="3c21d-165">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="3c21d-165">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "totalCount": 2,
    "items": [
        {
            "id": "MS-AZR-0145P",
            "productId": "9DEA7946-EC2C-441E-9FFD-E3B275F7E838",
            "title": "Microsoft Azure",
            "description": "Azure Cloud Solution Provider offer for Partner and Resellers",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "monthly"
            ],
            "purchasePrerequisites": [
                "MicrosoftCloudAgreement"
            ],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "billingType": "usage",
                "category": "Enterprise",
                "isAddon": false,
                "prerequisiteSkus": [],
                "rank": 1413,
                "hasAddOns": false,
                "isAutoRenewable": false,
                "upgradeTargetOffers": null,
                "conversionTargetOffers": [],
                "unitType": "Usage-based",
                "limitUnitOfMeasure": "None",
                "limit": 0,
                "reselleeQualifications": [],
                "resellerQualifications": []
            },
            "links": {
                "availabilities": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0001",
            "productId": "DZH318Z0BPS6",
            "title": "Microsoft Azure plan",
            "description": "Microsoft Azure plan (MS-AZR-0017G)",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "MicrosoftCustomerAgreement"
            ],
            "inventoryVariables": [],
            "provisioningVariables": [],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "pilotProgram": "modernazurepilot"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/e2a0c0f3-0f74-4d1c-808c-dfa511481913/products/all/skus?targetView=MicrosoftAzure&targetSegment=Commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
