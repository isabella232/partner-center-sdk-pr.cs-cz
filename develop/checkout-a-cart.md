---
title: Odbavení košíku
description: Naučte se rezervovat objednávku pro zákazníka na vozíku pomocí rozhraní API partnerského centra. Můžete to udělat tak, abyste objednávku zákazníka mohli dokončit.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 094817a34cd29bc96788fcfb6a16610a8192d784
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2020
ms.locfileid: "97767111"
---
# <a name="checkout-an-order-for-a-customer-in-a-cart"></a><span data-ttu-id="a745d-104">Rezervace objednávky zákazníka na vozíku</span><span class="sxs-lookup"><span data-stu-id="a745d-104">Checkout an order for a customer in a cart</span></span>

<span data-ttu-id="a745d-105">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="a745d-105">**Applies to:**</span></span>

- <span data-ttu-id="a745d-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="a745d-106">Partner Center</span></span>
- <span data-ttu-id="a745d-107">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="a745d-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="a745d-108">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="a745d-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a745d-109">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a745d-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a745d-110">Jak rezervovat objednávku pro zákazníka na vozíku.</span><span class="sxs-lookup"><span data-stu-id="a745d-110">How to checkout an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a745d-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a745d-111">Prerequisites</span></span>

- <span data-ttu-id="a745d-112">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a745d-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a745d-113">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="a745d-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a745d-114">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a745d-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a745d-115">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="a745d-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a745d-116">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="a745d-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a745d-117">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="a745d-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a745d-118">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="a745d-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a745d-119">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a745d-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a745d-120">ID košíku pro existující košík.</span><span class="sxs-lookup"><span data-stu-id="a745d-120">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="a745d-121">C\#</span><span class="sxs-lookup"><span data-stu-id="a745d-121">C\#</span></span>

<span data-ttu-id="a745d-122">Pokud chcete rezervovat objednávku pro zákazníka, získejte odkaz na košík pomocí košíku a identifikátoru zákazníka.</span><span class="sxs-lookup"><span data-stu-id="a745d-122">To checkout an order for a customer, get a reference to the cart using the cart and customer identifier.</span></span> <span data-ttu-id="a745d-123">Nakonec zavolejte funkci **Create** nebo **CreateAsync** k dokončení objednávky.</span><span class="sxs-lookup"><span data-stu-id="a745d-123">Finally, call the **Create** or **CreateAsync** functions to complete the order.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Checkout();
```

## <a name="java"></a><span data-ttu-id="a745d-124">Java</span><span class="sxs-lookup"><span data-stu-id="a745d-124">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="a745d-125">Pokud chcete rezervovat objednávku pro zákazníka, získejte odkaz na košík pomocí košíku a identifikátoru zákazníka.</span><span class="sxs-lookup"><span data-stu-id="a745d-125">To checkout an order for a customer, get a reference to the cart using the cart and customer identifier.</span></span> <span data-ttu-id="a745d-126">Nakonec voláním funkce **Create** Dokončete objednávku.</span><span class="sxs-lookup"><span data-stu-id="a745d-126">Finally, call the **create** function to complete the order.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String cartId;

Cart cart = partnerOperations.getCustomers().byId(customerId).getCart().byId(cartId).checkout();
```

## <a name="powershell"></a><span data-ttu-id="a745d-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a745d-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="a745d-128">Chcete-li rezervovat objednávku pro zákazníka, spusťte příkaz [**Submit-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Submit-PartnerCustomerCart.md) , který objednávku dokončí.</span><span class="sxs-lookup"><span data-stu-id="a745d-128">To checkout an order for a customer, execute the [**Submit-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Submit-PartnerCustomerCart.md) to complete the order.</span></span>

```powershell
# $customerId
# $cartId

Submit-PartnerCustomerCart -CartId $cartId -CustomerId $customerId
```

## <a name="rest-request"></a><span data-ttu-id="a745d-129">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="a745d-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a745d-130">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="a745d-130">Request syntax</span></span>

| <span data-ttu-id="a745d-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="a745d-131">Method</span></span>   | <span data-ttu-id="a745d-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="a745d-132">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a745d-133">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="a745d-133">**POST**</span></span> | <span data-ttu-id="a745d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts/{Cart-ID}/checkout http/1.1</span><span class="sxs-lookup"><span data-stu-id="a745d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id}/checkout HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="a745d-135">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="a745d-135">URI parameters</span></span>

<span data-ttu-id="a745d-136">Použijte následující parametry cesty k identifikaci zákazníka a určení košíku, který má být rezervován.</span><span class="sxs-lookup"><span data-stu-id="a745d-136">Use the following path parameters to identify the customer and specify the cart to be checked out.</span></span>

| <span data-ttu-id="a745d-137">Název</span><span class="sxs-lookup"><span data-stu-id="a745d-137">Name</span></span>            | <span data-ttu-id="a745d-138">Typ</span><span class="sxs-lookup"><span data-stu-id="a745d-138">Type</span></span>     | <span data-ttu-id="a745d-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="a745d-139">Required</span></span> | <span data-ttu-id="a745d-140">Popis</span><span class="sxs-lookup"><span data-stu-id="a745d-140">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="a745d-141">**ID zákazníka**</span><span class="sxs-lookup"><span data-stu-id="a745d-141">**customer-id**</span></span> | <span data-ttu-id="a745d-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="a745d-142">string</span></span>   | <span data-ttu-id="a745d-143">Yes</span><span class="sxs-lookup"><span data-stu-id="a745d-143">Yes</span></span>      | <span data-ttu-id="a745d-144">Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="a745d-144">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="a745d-145">**košík – ID**</span><span class="sxs-lookup"><span data-stu-id="a745d-145">**cart-id**</span></span>     | <span data-ttu-id="a745d-146">řetězec</span><span class="sxs-lookup"><span data-stu-id="a745d-146">string</span></span>   | <span data-ttu-id="a745d-147">Yes</span><span class="sxs-lookup"><span data-stu-id="a745d-147">Yes</span></span>      | <span data-ttu-id="a745d-148">Identifikátor košíku formátovaného identifikátorem GUID, který identifikuje vozík.</span><span class="sxs-lookup"><span data-stu-id="a745d-148">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="a745d-149">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="a745d-149">Request headers</span></span>

<span data-ttu-id="a745d-150">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a745d-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a745d-151">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="a745d-151">Request body</span></span>

<span data-ttu-id="a745d-152">Žádné</span><span class="sxs-lookup"><span data-stu-id="a745d-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a745d-153">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="a745d-153">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/checkout HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0
Expect: 100-continue

No-Content-Body
```

## <a name="rest-response"></a><span data-ttu-id="a745d-154">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="a745d-154">REST response</span></span>

<span data-ttu-id="a745d-155">V případě úspěchu obsahuje tělo odpovědi naplněný prostředek [CartCheckoutResult](cart-resources.md#cartcheckoutresult) .</span><span class="sxs-lookup"><span data-stu-id="a745d-155">If successful, the response body contains the populated [CartCheckoutResult](cart-resources.md#cartcheckoutresult) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a745d-156">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="a745d-156">Response success and error codes</span></span>

<span data-ttu-id="a745d-157">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="a745d-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a745d-158">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="a745d-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a745d-159">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a745d-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a745d-160">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="a745d-160">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
?{
  "orders": [
    {
      "id": "3c6f2530-1e31-4088-8230-dd1c31a18bce",
      "alternateId": "3c6f2530-1e31-4088-8230-dd1c31a18bce",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "monthly",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "MS-AZR-0145P",
          "subscriptionId": "EF2E1307-86E6-40E3-A794-872403FBD31C",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Microsoft Azure",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:44.76+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    },
    {
      "id": "311qiN8iFwkv-XARWMvXRYAwYKMACVqv1",
      "alternateId": "0a3624c6e47d",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "one_time",
      "currencyCode": "USD",
      "currencySymbol": "$",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Reserved VM Instance, Standard_NV12, US East 2, 1 Year",
          "quantity": 1,
          "links": {...}
        },
        {
          "lineItemNumber": 1,
          "offerId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
          "termDuration": "P3Y",
          "transactionType": "New",
          "friendlyName": "Reserved VM Instance, Standard_NV12, US East 2, 3 Years",
          "quantity": 1,
          "links": {...}
        },
        {
          "lineItemNumber": 2,
          "offerId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
          "transactionType": "New",
          "friendlyName": "BizTalk Server 2016 Branch",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:51.6578126Z",
      "status": "pending",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    },
    {
      "id": "HVu_cO8Ea7fNRQP4ia1QTpZap-kg_7P71",
      "alternateId": "55a4e6854d54",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "monthly",
      "currencyCode": "USD",
      "currencySymbol": "$",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
          "termDuration": "P1M",
          "transactionType": "New",
          "friendlyName": "Barracuda WaaS - Medium Plan",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:44.4514129Z",
      "status": "pending",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    }
  ],
  ...
}
```
