---
title: Získejte stav přímého podepisování zákazníka pro zákaznickou smlouvu Microsoftu.
description: Pomocí prostředku DirectSignedCustomerAgreementStatus můžete získat stav přímého podepisování zákazníka (přímé přijetí) smlouvy o zákaznících Microsoftu.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: a17775614b4eb328514b2b32b4cac1e513019cff
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549174"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="d0495-103">Získání stavu přímého podepisování zákazníka (přímé přijetí) smlouvy o zákaznících Microsoftu</span><span class="sxs-lookup"><span data-stu-id="d0495-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="d0495-104">**Platí pro**: partnerské Centrum</span><span class="sxs-lookup"><span data-stu-id="d0495-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="d0495-105">Nevztahuje **se na**: partnerské Centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d0495-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d0495-106">Partner Center v současné době podporuje prostředek **DirectSignedCustomerAgreementStatus** jenom ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="d0495-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="d0495-107">Tento článek vysvětluje, jak můžete načíst stav přímého přijetí smlouvy o zákaznících Microsoftu v rámci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d0495-107">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0495-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d0495-108">Prerequisites</span></span>

- <span data-ttu-id="d0495-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d0495-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d0495-110">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="d0495-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d0495-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d0495-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d0495-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="d0495-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d0495-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="d0495-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d0495-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="d0495-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d0495-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="d0495-115">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d0495-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d0495-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="d0495-117">C\#</span><span class="sxs-lookup"><span data-stu-id="d0495-117">C\#</span></span>

<span data-ttu-id="d0495-118">Pokud chcete načíst stav přímého souhlasu zákazníka s zákaznickou smlouvou Microsoftu, zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d0495-118">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="d0495-119">Pak použijte vlastnost [**smlouvy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) pro načtení rozhraní [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) .</span><span class="sxs-lookup"><span data-stu-id="d0495-119">Then use the [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) property to retrieve a [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) interface.</span></span> <span data-ttu-id="d0495-120">Nakonec zavolejte `GetDirectSignedCustomerAgreementStatus()` nebo `GetDirectSignedCustomerAgreementStatusAsync()` pro načtení stavu.</span><span class="sxs-lookup"><span data-stu-id="d0495-120">Finally, call `GetDirectSignedCustomerAgreementStatus()` or `GetDirectSignedCustomerAgreementStatusAsync()` to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

<span data-ttu-id="d0495-121">**Ukázka**: [ukázková aplikace konzoly](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="d0495-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="d0495-122">**Project**: **třída** SdkSamples: GetDirectSignedCustomerAgreementStatus. cs</span><span class="sxs-lookup"><span data-stu-id="d0495-122">**Project**: SdkSamples **Class**: GetDirectSignedCustomerAgreementStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d0495-123">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="d0495-123">REST request</span></span>

<span data-ttu-id="d0495-124">Pokud chcete načíst stav přímého souhlasu zákazníka s zákaznickou smlouvou Microsoftu, vytvořte žádost REST, která načte [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d0495-124">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d0495-125">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="d0495-125">Request syntax</span></span>

<span data-ttu-id="d0495-126">Použijte následující syntaxi žádosti:</span><span class="sxs-lookup"><span data-stu-id="d0495-126">Use the following request syntax:</span></span>

| <span data-ttu-id="d0495-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="d0495-127">Method</span></span> | <span data-ttu-id="d0495-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d0495-128">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d0495-129">GET</span><span class="sxs-lookup"><span data-stu-id="d0495-129">GET</span></span>    | <span data-ttu-id="d0495-130">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d0495-130">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="d0495-131">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="d0495-131">URI parameters</span></span>

<span data-ttu-id="d0495-132">S vaším požadavkem můžete použít následující parametry identifikátoru URI:</span><span class="sxs-lookup"><span data-stu-id="d0495-132">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="d0495-133">Název</span><span class="sxs-lookup"><span data-stu-id="d0495-133">Name</span></span>             | <span data-ttu-id="d0495-134">Typ</span><span class="sxs-lookup"><span data-stu-id="d0495-134">Type</span></span> | <span data-ttu-id="d0495-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d0495-135">Required</span></span> | <span data-ttu-id="d0495-136">Popis</span><span class="sxs-lookup"><span data-stu-id="d0495-136">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="d0495-137">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="d0495-137">customer-tenant-id</span></span> | <span data-ttu-id="d0495-138">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="d0495-138">GUID</span></span> | <span data-ttu-id="d0495-139">Yes</span><span class="sxs-lookup"><span data-stu-id="d0495-139">Yes</span></span> | <span data-ttu-id="d0495-140">Hodnota je **CustomerTenantId** ve formátu GUID, který umožňuje určit ID tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d0495-140">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d0495-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d0495-141">Request headers</span></span>

<span data-ttu-id="d0495-142">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d0495-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d0495-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d0495-143">Request body</span></span>

<span data-ttu-id="d0495-144">Žádné</span><span class="sxs-lookup"><span data-stu-id="d0495-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d0495-145">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d0495-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="d0495-146">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d0495-146">REST response</span></span>

<span data-ttu-id="d0495-147">V případě úspěchu tato metoda vrátí prostředek [ **DirectSignedCustomerAgreementStatus**](./customer-agreement-direct-sign-status-resource.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="d0495-147">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="d0495-148">Prostředek má vlastnost **podepsatelných** , která označuje stav přímého podepisování (přímého přijetí) zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d0495-148">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="d0495-149">Hodnota **true** označuje, že smlouva byla podepsána (přijata) přímo zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="d0495-149">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="d0495-150">Hodnota **false** znamená, že *smlouva nebyla* podepsána (přijata) přímo zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="d0495-150">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d0495-151">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="d0495-151">Response success and error codes</span></span>

<span data-ttu-id="d0495-152">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d0495-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="d0495-153">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="d0495-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d0495-154">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d0495-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d0495-155">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="d0495-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
