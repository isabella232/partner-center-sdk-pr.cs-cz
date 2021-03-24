---
title: Získejte stav přímého podepisování zákazníka pro zákaznickou smlouvu Microsoftu.
description: Pomocí prostředku DirectSignedCustomerAgreementStatus můžete získat stav přímého podepisování zákazníka (přímé přijetí) smlouvy o zákaznících Microsoftu.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 267e3aa63a94c5045977ad566eb5061df3b59882
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030551"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="86430-103">Získání stavu přímého podepisování zákazníka (přímé přijetí) smlouvy o zákaznících Microsoftu</span><span class="sxs-lookup"><span data-stu-id="86430-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="86430-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="86430-104">**Applies to:**</span></span>

- <span data-ttu-id="86430-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="86430-105">Partner Center</span></span>

<span data-ttu-id="86430-106">Partner Center v současné době podporuje prostředek **DirectSignedCustomerAgreementStatus** jenom ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="86430-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="86430-107">Tento prostředek *nelze použít* pro:</span><span class="sxs-lookup"><span data-stu-id="86430-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="86430-108">Partnerské centrum provozované společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="86430-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="86430-109">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="86430-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="86430-110">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="86430-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="86430-111">Tento článek vysvětluje, jak můžete načíst stav přímého přijetí smlouvy o zákaznících Microsoftu v rámci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="86430-111">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86430-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="86430-112">Prerequisites</span></span>

- <span data-ttu-id="86430-113">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="86430-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="86430-114">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="86430-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="86430-115">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="86430-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="86430-116">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="86430-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="86430-117">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="86430-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="86430-118">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="86430-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="86430-119">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="86430-119">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="86430-120">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="86430-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="86430-121">C\#</span><span class="sxs-lookup"><span data-stu-id="86430-121">C\#</span></span>

<span data-ttu-id="86430-122">Pokud chcete načíst stav přímého souhlasu zákazníka s zákaznickou smlouvou Microsoftu, zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="86430-122">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="86430-123">Pak použijte vlastnost [**smlouvy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) pro načtení rozhraní [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) .</span><span class="sxs-lookup"><span data-stu-id="86430-123">Then use the [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) property to retrieve a [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) interface.</span></span> <span data-ttu-id="86430-124">Nakonec zavolejte `GetDirectSignedCustomerAgreementStatus()` nebo `GetDirectSignedCustomerAgreementStatusAsync()` pro načtení stavu.</span><span class="sxs-lookup"><span data-stu-id="86430-124">Finally, call `GetDirectSignedCustomerAgreementStatus()` or `GetDirectSignedCustomerAgreementStatusAsync()` to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

<span data-ttu-id="86430-125">**Ukázka**: [ukázková aplikace konzoly](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="86430-125">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="86430-126">**Projekt**: **Třída** SdkSamples: GetDirectSignedCustomerAgreementStatus. cs</span><span class="sxs-lookup"><span data-stu-id="86430-126">**Project**: SdkSamples **Class**: GetDirectSignedCustomerAgreementStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="86430-127">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="86430-127">REST request</span></span>

<span data-ttu-id="86430-128">Pokud chcete načíst stav přímého souhlasu zákazníka s zákaznickou smlouvou Microsoftu, vytvořte žádost REST, která načte [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="86430-128">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="86430-129">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="86430-129">Request syntax</span></span>

<span data-ttu-id="86430-130">Použijte následující syntaxi žádosti:</span><span class="sxs-lookup"><span data-stu-id="86430-130">Use the following request syntax:</span></span>

| <span data-ttu-id="86430-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="86430-131">Method</span></span> | <span data-ttu-id="86430-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="86430-132">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="86430-133">GET</span><span class="sxs-lookup"><span data-stu-id="86430-133">GET</span></span>    | <span data-ttu-id="86430-134">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="86430-134">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="86430-135">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="86430-135">URI parameters</span></span>

<span data-ttu-id="86430-136">S vaším požadavkem můžete použít následující parametry identifikátoru URI:</span><span class="sxs-lookup"><span data-stu-id="86430-136">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="86430-137">Název</span><span class="sxs-lookup"><span data-stu-id="86430-137">Name</span></span>             | <span data-ttu-id="86430-138">Typ</span><span class="sxs-lookup"><span data-stu-id="86430-138">Type</span></span> | <span data-ttu-id="86430-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="86430-139">Required</span></span> | <span data-ttu-id="86430-140">Popis</span><span class="sxs-lookup"><span data-stu-id="86430-140">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="86430-141">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="86430-141">customer-tenant-id</span></span> | <span data-ttu-id="86430-142">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="86430-142">GUID</span></span> | <span data-ttu-id="86430-143">Yes</span><span class="sxs-lookup"><span data-stu-id="86430-143">Yes</span></span> | <span data-ttu-id="86430-144">Hodnota je **CustomerTenantId** ve formátu GUID, který umožňuje určit ID tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="86430-144">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="86430-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="86430-145">Request headers</span></span>

<span data-ttu-id="86430-146">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="86430-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="86430-147">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="86430-147">Request body</span></span>

<span data-ttu-id="86430-148">Žádné</span><span class="sxs-lookup"><span data-stu-id="86430-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="86430-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="86430-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="86430-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="86430-150">REST response</span></span>

<span data-ttu-id="86430-151">V případě úspěchu tato metoda vrátí prostředek [ **DirectSignedCustomerAgreementStatus**](./customer-agreement-direct-sign-status-resource.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="86430-151">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="86430-152">Prostředek má vlastnost **podepsatelných** , která označuje stav přímého podepisování (přímého přijetí) zákazníka.</span><span class="sxs-lookup"><span data-stu-id="86430-152">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="86430-153">Hodnota **true** označuje, že smlouva byla podepsána (přijata) přímo zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="86430-153">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="86430-154">Hodnota **false** znamená, že *smlouva nebyla* podepsána (přijata) přímo zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="86430-154">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="86430-155">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="86430-155">Response success and error codes</span></span>

<span data-ttu-id="86430-156">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="86430-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="86430-157">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="86430-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="86430-158">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="86430-158">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="86430-159">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="86430-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
