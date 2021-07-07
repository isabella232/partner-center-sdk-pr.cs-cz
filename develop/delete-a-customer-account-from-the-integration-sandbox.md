---
title: Odstranění zákaznického účet ze sandboxu pro integraci
description: Jak odstranit účet zákazníka z karantény integrace v produkčním prostředí (Tip)
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9d9e44ac9c40bd4e3c7e1a9e04253f853dfd96c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973124"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a><span data-ttu-id="b970d-103">Odstranění zákaznického účet ze sandboxu pro integraci</span><span class="sxs-lookup"><span data-stu-id="b970d-103">Delete a customer account from the integration sandbox</span></span>

<span data-ttu-id="b970d-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b970d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b970d-105">Tento článek vysvětluje, jak přerušit vztah mezi partnerem a účtem zákazníka a znovu získáte kvótu pro testování v izolovaném prostoru integrace (Tip) Integration.</span><span class="sxs-lookup"><span data-stu-id="b970d-105">This article explains, how to break the relationship between the partner and the customer account and regain the quota for Testing in Production (Tip) integration sandbox.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b970d-106">Když odstraníte účet zákazníka, vyprázdní se všechny prostředky přidružené k tomuto tenantovi zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b970d-106">When you delete a customer account, all resources associated with that customer tenant will be purged.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b970d-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b970d-107">Prerequisites</span></span>

- <span data-ttu-id="b970d-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b970d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b970d-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="b970d-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b970d-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b970d-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b970d-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b970d-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b970d-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="b970d-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b970d-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="b970d-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b970d-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="b970d-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b970d-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b970d-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b970d-116">Před odstraněním zákazníka z karantény integrace s tipem se musí zrušit všechny nákupní objednávky Azure Reserved Virtual Machine Instances a softwaru.</span><span class="sxs-lookup"><span data-stu-id="b970d-116">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="c"></a><span data-ttu-id="b970d-117">C\#</span><span class="sxs-lookup"><span data-stu-id="b970d-117">C\#</span></span>

<span data-ttu-id="b970d-118">Odstranění zákazníka z izolovaného prostoru integrace s tipem:</span><span class="sxs-lookup"><span data-stu-id="b970d-118">To delete a customer from the Tip integration sandbox:</span></span>

1. <span data-ttu-id="b970d-119">Předání přihlašovacích údajů k účtu Tip metodě [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) k získání rozhraní [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) pro partnerské operace.</span><span class="sxs-lookup"><span data-stu-id="b970d-119">Pass your Tip account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to partner operations.</span></span>

2. <span data-ttu-id="b970d-120">Pro načtení kolekce oprávnění použijte rozhraní partnerských operací:</span><span class="sxs-lookup"><span data-stu-id="b970d-120">Use the partner operations interface to retrieve the collection of entitlements:</span></span>

    1. <span data-ttu-id="b970d-121">Pro určení zákazníka zavolejte metodu [**Customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b970d-121">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer.</span></span>

    2. <span data-ttu-id="b970d-122">Zavolejte vlastnost **oprávnění** .</span><span class="sxs-lookup"><span data-stu-id="b970d-122">Call the **Entitlements** property.</span></span>

    3. <span data-ttu-id="b970d-123">Pro načtení kolekce [**nároků**](entitlement-resources.md) zavolejte metodu **Get** nebo **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="b970d-123">Call the **Get** or **GetAsync** method to retrieve the [**Entitlement**](entitlement-resources.md) collection.</span></span>

3. <span data-ttu-id="b970d-124">Ujistěte se, že všechny nákupní objednávky Azure Reserved Virtual Machine Instances a softwaru pro tohoto zákazníka se zrušily.</span><span class="sxs-lookup"><span data-stu-id="b970d-124">Make sure that all Azure Reserved Virtual Machine Instances and software purchase orders for that customer are canceled.</span></span> <span data-ttu-id="b970d-125">Pro každé [**oprávnění**](entitlement-resources.md) v kolekci:</span><span class="sxs-lookup"><span data-stu-id="b970d-125">For each [**Entitlement**](entitlement-resources.md) in the collection:</span></span>

    1. <span data-ttu-id="b970d-126">Použijte [**oprávnění. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) získat místní kopii odpovídajícího [pořadí](order-resources.md#order) z kolekce objednávek zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b970d-126">Use the [**entitlement.ReferenceOrder.Id**](entitlement-resources.md#referenceorder) to get a local copy of the corresponding [Order](order-resources.md#order) from the customer's collection of orders.</span></span>

    2. <span data-ttu-id="b970d-127">Nastavte vlastnost [**Order. status**](order-resources.md#order) na "zrušeno".</span><span class="sxs-lookup"><span data-stu-id="b970d-127">Set the [**Order.Status**](order-resources.md#order) property to "Cancelled".</span></span>

    3. <span data-ttu-id="b970d-128">K aktualizaci objednávky použijte metodu **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="b970d-128">Use the **Patch()** method to update the order.</span></span>

4. <span data-ttu-id="b970d-129">Zruší všechny objednávky.</span><span class="sxs-lookup"><span data-stu-id="b970d-129">Cancel all orders.</span></span> <span data-ttu-id="b970d-130">Například následující příklad kódu používá smyčku k cyklickému dotazování každého pořadí, dokud jeho stav není "zrušeno".</span><span class="sxs-lookup"><span data-stu-id="b970d-130">For example, the following code sample uses a loop to poll each order until its status is "Cancelled".</span></span>

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be canceled.
    ResourceCollection<Entitlement> entitlements = tipAccountPartnerOperations.Customers.ById(customerTenantId).Entitlements.Get();

    // Cancel all orders
    foreach (var entitlement in entitlements)
    {
        var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
        order.Status = "Cancelled";
        order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(order.Id).Patch(order);
    }

    // Keep polling until the status of all orders is "Cancelled".
    bool proceed = true;
    do
    {
        // Check if all the orders were canceled.
        foreach (var entitlement in entitlements)
        {
            var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
            if (!order.Status.Equals("Cancelled", StringComparison.OrdinalIgnoreCase))
            {
                proceed = false;
            }
        }

        // Wait for a few seconds.
        Thread.Sleep(5000);
    }
    while (proceed == false);

    tipAccountPartnerOperations.Customers.ById(customerTenantId).Delete();
    ```

5. <span data-ttu-id="b970d-131">Zajistěte, aby byly všechny objednávky zrušené voláním metody **Delete** pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b970d-131">Make sure all orders are canceled by calling the **Delete** method for the customer.</span></span>

<span data-ttu-id="b970d-132">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b970d-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b970d-133">**Project**: partnerská **třída** PartnerCenterSDK. FeaturesSamples: DeleteCustomerFromTipAccount. cs</span><span class="sxs-lookup"><span data-stu-id="b970d-133">**Project**: Partner Center PartnerCenterSDK.FeaturesSamples **Class**: DeleteCustomerFromTipAccount.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b970d-134">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b970d-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b970d-135">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b970d-135">Request syntax</span></span>

| <span data-ttu-id="b970d-136">Metoda</span><span class="sxs-lookup"><span data-stu-id="b970d-136">Method</span></span>     | <span data-ttu-id="b970d-137">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b970d-137">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="b970d-138">DELETE</span><span class="sxs-lookup"><span data-stu-id="b970d-138">DELETE</span></span>     | <span data-ttu-id="b970d-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b970d-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="b970d-140">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b970d-140">URI parameter</span></span>

<span data-ttu-id="b970d-141">K odstranění zákazníka použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="b970d-141">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="b970d-142">Název</span><span class="sxs-lookup"><span data-stu-id="b970d-142">Name</span></span>                   | <span data-ttu-id="b970d-143">Typ</span><span class="sxs-lookup"><span data-stu-id="b970d-143">Type</span></span>     | <span data-ttu-id="b970d-144">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b970d-144">Required</span></span> | <span data-ttu-id="b970d-145">Popis</span><span class="sxs-lookup"><span data-stu-id="b970d-145">Description</span></span>                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="b970d-146">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="b970d-146">customer-tenant-id</span></span>     | <span data-ttu-id="b970d-147">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="b970d-147">GUID</span></span>     | <span data-ttu-id="b970d-148">Y</span><span class="sxs-lookup"><span data-stu-id="b970d-148">Y</span></span>        | <span data-ttu-id="b970d-149">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="b970d-149">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b970d-150">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b970d-150">Request headers</span></span>

<span data-ttu-id="b970d-151">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b970d-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b970d-152">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b970d-152">Request body</span></span>

<span data-ttu-id="b970d-153">Žádné</span><span class="sxs-lookup"><span data-stu-id="b970d-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b970d-154">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b970d-154">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="b970d-155">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b970d-155">REST response</span></span>

<span data-ttu-id="b970d-156">V případě úspěchu vrátí tato metoda prázdnou odpověď.</span><span class="sxs-lookup"><span data-stu-id="b970d-156">If successful, this method returns an empty response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b970d-157">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b970d-157">Response success and error codes</span></span>

<span data-ttu-id="b970d-158">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b970d-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b970d-159">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b970d-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b970d-160">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b970d-160">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b970d-161">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b970d-161">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
