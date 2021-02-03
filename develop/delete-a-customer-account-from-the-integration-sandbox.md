---
title: Odstranění zákaznického účet ze sandboxu pro integraci
description: Jak odstranit účet zákazníka z karantény integrace v produkčním prostředí (Tip)
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e3a1642c0202c174ddd4f65a6aeda2752def9176
ms.sourcegitcommit: b1ff781b67b1d322820bbcac2c583229201a8c07
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2020
ms.locfileid: "97766892"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a><span data-ttu-id="44366-103">Odstranění zákaznického účet ze sandboxu pro integraci</span><span class="sxs-lookup"><span data-stu-id="44366-103">Delete a customer account from the integration sandbox</span></span>

<span data-ttu-id="44366-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="44366-104">**Applies to:**</span></span>

- <span data-ttu-id="44366-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="44366-105">Partner Center</span></span>
- <span data-ttu-id="44366-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="44366-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="44366-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="44366-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="44366-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="44366-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="44366-109">Tento článek vysvětluje, jak přerušit vztah mezi partnerem a účtem zákazníka a znovu získáte kvótu pro testování v izolovaném prostoru integrace (Tip) Integration.</span><span class="sxs-lookup"><span data-stu-id="44366-109">This article explains, how to break the relationship between the partner and the customer account and regain the quota for Testing in Production (Tip) integration sandbox.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44366-110">Když odstraníte účet zákazníka, vyprázdní se všechny prostředky přidružené k tomuto tenantovi zákazníka.</span><span class="sxs-lookup"><span data-stu-id="44366-110">When you delete a customer account, all resources associated with that customer tenant will be purged.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44366-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="44366-111">Prerequisites</span></span>

- <span data-ttu-id="44366-112">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="44366-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="44366-113">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="44366-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="44366-114">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="44366-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="44366-115">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="44366-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="44366-116">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="44366-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="44366-117">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="44366-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="44366-118">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="44366-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="44366-119">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="44366-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="44366-120">Před odstraněním zákazníka z karantény integrace s tipem se musí zrušit všechny nákupní objednávky Azure Reserved Virtual Machine Instances a softwaru.</span><span class="sxs-lookup"><span data-stu-id="44366-120">All Azure Reserved Virtual Machine Instances and software purchase orders must be cancelled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="c"></a><span data-ttu-id="44366-121">C\#</span><span class="sxs-lookup"><span data-stu-id="44366-121">C\#</span></span>

<span data-ttu-id="44366-122">Odstranění zákazníka z izolovaného prostoru integrace s tipem:</span><span class="sxs-lookup"><span data-stu-id="44366-122">To delete a customer from the Tip integration sandbox:</span></span>

1. <span data-ttu-id="44366-123">Předání přihlašovacích údajů k účtu Tip metodě [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) k získání rozhraní [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) pro partnerské operace.</span><span class="sxs-lookup"><span data-stu-id="44366-123">Pass your Tip account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to partner operations.</span></span>

2. <span data-ttu-id="44366-124">Pro načtení kolekce oprávnění použijte rozhraní partnerských operací:</span><span class="sxs-lookup"><span data-stu-id="44366-124">Use the partner operations interface to retrieve the collection of entitlements:</span></span>

    1. <span data-ttu-id="44366-125">Pro určení zákazníka zavolejte metodu [**Customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="44366-125">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer.</span></span>

    2. <span data-ttu-id="44366-126">Zavolejte vlastnost **oprávnění** .</span><span class="sxs-lookup"><span data-stu-id="44366-126">Call the **Entitlements** property.</span></span>

    3. <span data-ttu-id="44366-127">Pro načtení kolekce [**nároků**](entitlement-resources.md) zavolejte metodu **Get** nebo **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="44366-127">Call the **Get** or **GetAsync** method to retrieve the [**Entitlement**](entitlement-resources.md) collection.</span></span>

3. <span data-ttu-id="44366-128">Ujistěte se, že všechny nákupní objednávky Azure Reserved Virtual Machine Instances a softwaru pro tohoto zákazníka se zrušily.</span><span class="sxs-lookup"><span data-stu-id="44366-128">Make sure that all Azure Reserved Virtual Machine Instances and software purchase orders for that customer are cancelled.</span></span> <span data-ttu-id="44366-129">Pro každé [**oprávnění**](entitlement-resources.md) v kolekci:</span><span class="sxs-lookup"><span data-stu-id="44366-129">For each [**Entitlement**](entitlement-resources.md) in the collection:</span></span>

    1. <span data-ttu-id="44366-130">Použijte [**oprávnění. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) získat místní kopii odpovídajícího [pořadí](order-resources.md#order) z kolekce objednávek zákazníka.</span><span class="sxs-lookup"><span data-stu-id="44366-130">Use the [**entitlement.ReferenceOrder.Id**](entitlement-resources.md#referenceorder) to get a local copy of the corresponding [Order](order-resources.md#order) from the customer's collection of orders.</span></span>

    2. <span data-ttu-id="44366-131">Nastavte vlastnost [**Order. status**](order-resources.md#order) na "zrušeno".</span><span class="sxs-lookup"><span data-stu-id="44366-131">Set the [**Order.Status**](order-resources.md#order) property to "Cancelled".</span></span>

    3. <span data-ttu-id="44366-132">K aktualizaci objednávky použijte metodu **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="44366-132">Use the **Patch()** method to update the order.</span></span>

4. <span data-ttu-id="44366-133">Zruší všechny objednávky.</span><span class="sxs-lookup"><span data-stu-id="44366-133">Cancel all orders.</span></span> <span data-ttu-id="44366-134">Například následující příklad kódu používá smyčku k cyklickému dotazování každého pořadí, dokud jeho stav není "zrušeno".</span><span class="sxs-lookup"><span data-stu-id="44366-134">For example, the following code sample uses a loop to poll each order until its status is "Cancelled".</span></span>

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be cancelled.
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
        // Check if all the orders were cancelled.
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

5. <span data-ttu-id="44366-135">Zajistěte, aby byly všechny objednávky zrušené voláním metody **Delete** pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="44366-135">Make sure all orders are cancelled by calling the **Delete** method for the customer.</span></span>

<span data-ttu-id="44366-136">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="44366-136">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="44366-137">**Projekt**: Partnerská **Třída** PartnerCenterSDK. FeaturesSamples: DeleteCustomerFromTipAccount.cs</span><span class="sxs-lookup"><span data-stu-id="44366-137">**Project**: Partner Center PartnerCenterSDK.FeaturesSamples **Class**: DeleteCustomerFromTipAccount.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="44366-138">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="44366-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="44366-139">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="44366-139">Request syntax</span></span>

| <span data-ttu-id="44366-140">Metoda</span><span class="sxs-lookup"><span data-stu-id="44366-140">Method</span></span>     | <span data-ttu-id="44366-141">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="44366-141">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="44366-142">DELETE</span><span class="sxs-lookup"><span data-stu-id="44366-142">DELETE</span></span>     | <span data-ttu-id="44366-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="44366-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="44366-144">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="44366-144">URI parameter</span></span>

<span data-ttu-id="44366-145">K odstranění zákazníka použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="44366-145">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="44366-146">Název</span><span class="sxs-lookup"><span data-stu-id="44366-146">Name</span></span>                   | <span data-ttu-id="44366-147">Typ</span><span class="sxs-lookup"><span data-stu-id="44366-147">Type</span></span>     | <span data-ttu-id="44366-148">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="44366-148">Required</span></span> | <span data-ttu-id="44366-149">Popis</span><span class="sxs-lookup"><span data-stu-id="44366-149">Description</span></span>                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="44366-150">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="44366-150">customer-tenant-id</span></span>     | <span data-ttu-id="44366-151">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="44366-151">GUID</span></span>     | <span data-ttu-id="44366-152">Y</span><span class="sxs-lookup"><span data-stu-id="44366-152">Y</span></span>        | <span data-ttu-id="44366-153">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="44366-153">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="44366-154">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="44366-154">Request headers</span></span>

<span data-ttu-id="44366-155">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="44366-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="44366-156">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="44366-156">Request body</span></span>

<span data-ttu-id="44366-157">Žádné</span><span class="sxs-lookup"><span data-stu-id="44366-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="44366-158">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="44366-158">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="44366-159">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="44366-159">REST response</span></span>

<span data-ttu-id="44366-160">V případě úspěchu vrátí tato metoda prázdnou odpověď.</span><span class="sxs-lookup"><span data-stu-id="44366-160">If successful, this method returns an empty response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="44366-161">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="44366-161">Response success and error codes</span></span>

<span data-ttu-id="44366-162">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="44366-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="44366-163">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="44366-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="44366-164">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="44366-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="44366-165">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="44366-165">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
