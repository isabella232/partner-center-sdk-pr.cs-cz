---
title: Získejte stav přímého podepisování zákazníka pro zákaznickou smlouvu Microsoftu.
description: Pomocí prostředku DirectSignedCustomerAgreementStatus můžete získat stav přímého podepisování zákazníka (přímé přijetí) smlouvy o zákaznících Microsoftu.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 3f1deb20a18bc6e7133cac91db528f2d1ad694e2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766664"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="0bf9f-103">Získání stavu přímého podepisování zákazníka (přímé přijetí) smlouvy o zákaznících Microsoftu</span><span class="sxs-lookup"><span data-stu-id="0bf9f-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="0bf9f-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="0bf9f-104">**Applies to:**</span></span>

- <span data-ttu-id="0bf9f-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="0bf9f-105">Partner Center</span></span>

<span data-ttu-id="0bf9f-106">Partner Center v současné době podporuje prostředek **DirectSignedCustomerAgreementStatus** jenom ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="0bf9f-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="0bf9f-107">Tento prostředek *nelze použít* pro:</span><span class="sxs-lookup"><span data-stu-id="0bf9f-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="0bf9f-108">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="0bf9f-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="0bf9f-109">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="0bf9f-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0bf9f-110">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0bf9f-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0bf9f-111">Tento článek vysvětluje, jak můžete načíst stav přímého přijetí smlouvy o zákaznících Microsoftu v rámci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0bf9f-111">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="rest-request"></a><span data-ttu-id="0bf9f-112">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="0bf9f-112">REST request</span></span>

<span data-ttu-id="0bf9f-113">Pokud chcete načíst stav přímého souhlasu zákazníka s zákaznickou smlouvou Microsoftu, vytvořte žádost REST, která načte [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0bf9f-113">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0bf9f-114">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="0bf9f-114">Request syntax</span></span>

<span data-ttu-id="0bf9f-115">Použijte následující syntaxi žádosti:</span><span class="sxs-lookup"><span data-stu-id="0bf9f-115">Use the following request syntax:</span></span>

| <span data-ttu-id="0bf9f-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="0bf9f-116">Method</span></span> | <span data-ttu-id="0bf9f-117">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0bf9f-117">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0bf9f-118">GET</span><span class="sxs-lookup"><span data-stu-id="0bf9f-118">GET</span></span>    | <span data-ttu-id="0bf9f-119">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0bf9f-119">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="0bf9f-120">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="0bf9f-120">URI parameters</span></span>

<span data-ttu-id="0bf9f-121">S vaším požadavkem můžete použít následující parametry identifikátoru URI:</span><span class="sxs-lookup"><span data-stu-id="0bf9f-121">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="0bf9f-122">Název</span><span class="sxs-lookup"><span data-stu-id="0bf9f-122">Name</span></span>             | <span data-ttu-id="0bf9f-123">Typ</span><span class="sxs-lookup"><span data-stu-id="0bf9f-123">Type</span></span> | <span data-ttu-id="0bf9f-124">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="0bf9f-124">Required</span></span> | <span data-ttu-id="0bf9f-125">Popis</span><span class="sxs-lookup"><span data-stu-id="0bf9f-125">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="0bf9f-126">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="0bf9f-126">customer-tenant-id</span></span> | <span data-ttu-id="0bf9f-127">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="0bf9f-127">GUID</span></span> | <span data-ttu-id="0bf9f-128">Yes</span><span class="sxs-lookup"><span data-stu-id="0bf9f-128">Yes</span></span> | <span data-ttu-id="0bf9f-129">Hodnota je **CustomerTenantId** ve formátu GUID, který umožňuje určit ID tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0bf9f-129">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0bf9f-130">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0bf9f-130">Request headers</span></span>

<span data-ttu-id="0bf9f-131">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0bf9f-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0bf9f-132">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0bf9f-132">Request body</span></span>

<span data-ttu-id="0bf9f-133">Žádné</span><span class="sxs-lookup"><span data-stu-id="0bf9f-133">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0bf9f-134">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="0bf9f-134">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="0bf9f-135">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0bf9f-135">REST response</span></span>

<span data-ttu-id="0bf9f-136">V případě úspěchu tato metoda vrátí prostředek [ **DirectSignedCustomerAgreementStatus**](./customer-agreement-direct-sign-status-resource.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="0bf9f-136">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="0bf9f-137">Prostředek má vlastnost **podepsatelných** , která označuje stav přímého podepisování (přímého přijetí) zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0bf9f-137">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="0bf9f-138">Hodnota **true** označuje, že smlouva byla podepsána (přijata) přímo zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="0bf9f-138">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="0bf9f-139">Hodnota **false** znamená, že *smlouva nebyla* podepsána (přijata) přímo zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="0bf9f-139">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0bf9f-140">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="0bf9f-140">Response success and error codes</span></span>

<span data-ttu-id="0bf9f-141">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0bf9f-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="0bf9f-142">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="0bf9f-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0bf9f-143">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0bf9f-143">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0bf9f-144">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="0bf9f-144">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
