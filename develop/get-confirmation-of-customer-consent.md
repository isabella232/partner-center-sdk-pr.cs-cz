---
title: Získání potvrzení přijetí Smlouvy o službách Microsoft Cloud ze strany zákazníka
description: Tento článek vysvětluje, jak získat potvrzení přijetí smlouvy Microsoft Cloud zákazníkům.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: d91f70cbd8bc9b8622b8d41ab9e601e2aee2cfab
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767037"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a><span data-ttu-id="24b45-103">Získání potvrzení přijetí Smlouvy o službách Microsoft Cloud ze strany zákazníka</span><span class="sxs-lookup"><span data-stu-id="24b45-103">Get confirmation of customer acceptance of Microsoft Cloud Agreement</span></span>

<span data-ttu-id="24b45-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="24b45-104">**Applies To**</span></span>

- <span data-ttu-id="24b45-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="24b45-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="24b45-106">Prostředek **smlouvy** je aktuálně podporovaný partnerským centrem jenom ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="24b45-106">The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="24b45-107">Neplatí pro:</span><span class="sxs-lookup"><span data-stu-id="24b45-107">It isn't applicable to:</span></span>
>
> - <span data-ttu-id="24b45-108">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="24b45-108">Partner Center operated by 21Vianet</span></span>
> - <span data-ttu-id="24b45-109">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="24b45-109">Partner Center for Microsoft Cloud Germany</span></span>
> - <span data-ttu-id="24b45-110">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="24b45-110">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24b45-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="24b45-111">Prerequisites</span></span>

- <span data-ttu-id="24b45-112">Pokud používáte sadu SDK partnerského centra .NET, verze 1,9 nebo novější je povinná.</span><span class="sxs-lookup"><span data-stu-id="24b45-112">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="24b45-113">Pokud používáte sadu SDK pro partnerský Center Java, verze 1,8 nebo novější je povinná.</span><span class="sxs-lookup"><span data-stu-id="24b45-113">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="24b45-114">Přihlašovací údaje popsané v [partnerském centru ověřování](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="24b45-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="24b45-115">Tento scénář podporuje jenom ověřování aplikací a uživatelů.</span><span class="sxs-lookup"><span data-stu-id="24b45-115">This scenario supports only supports app + user authentication.</span></span>

- <span data-ttu-id="24b45-116">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="24b45-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="24b45-117">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="24b45-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="24b45-118">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="24b45-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="24b45-119">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="24b45-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="24b45-120">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="24b45-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="24b45-121">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="24b45-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net-version-14-or-newer"></a><span data-ttu-id="24b45-122">.NET (verze 1,4 nebo novější)</span><span class="sxs-lookup"><span data-stu-id="24b45-122">.NET (version 1.4 or newer)</span></span>

<span data-ttu-id="24b45-123">Chcete-li získat potvrzení o přijetí od zákazníka, které bylo dříve poskytnuto:</span><span class="sxs-lookup"><span data-stu-id="24b45-123">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="24b45-124">Použijte kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById** se zadaným identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="24b45-124">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="24b45-125">Načtěte vlastnost **smluvs** a vyfiltrujte výsledky na Microsoft Cloud smlouvu voláním metody **ByAgreementType** .</span><span class="sxs-lookup"><span data-stu-id="24b45-125">Fetch the **Agreements** property and filter the results to Microsoft Cloud Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="24b45-126">Volejte metodu **Get** nebo **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="24b45-126">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="24b45-127">Kompletní ukázku najdete ve třídě [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) z projektu [testovací aplikace konzoly](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .</span><span class="sxs-lookup"><span data-stu-id="24b45-127">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="24b45-128">.NET (verze 1,9 – 1,13)</span><span class="sxs-lookup"><span data-stu-id="24b45-128">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="24b45-129">Postup načtení potvrzení o přijetí od zákazníka, které jste zadali dříve:</span><span class="sxs-lookup"><span data-stu-id="24b45-129">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="24b45-130">Použijte kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById** se zadaným identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="24b45-130">Use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's identifier.</span></span> <span data-ttu-id="24b45-131">Poté Získejte vlastnost **smluv** následovaným voláním metod **Get** nebo **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="24b45-131">Then, get the **Agreements** property, followed by calling the **Get** or **GetAsync** methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a><span data-ttu-id="24b45-132">Java</span><span class="sxs-lookup"><span data-stu-id="24b45-132">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="24b45-133">Postup načtení potvrzení o přijetí od zákazníka, které jste zadali dříve:</span><span class="sxs-lookup"><span data-stu-id="24b45-133">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="24b45-134">Použijte funkci **IAggregatePartner. GetCustomers** a zavolejte funkci **byId** se zadaným identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="24b45-134">Use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier.</span></span> <span data-ttu-id="24b45-135">Potom Získejte funkci **Getagreements** následovanou voláním funkce **Get** .</span><span class="sxs-lookup"><span data-stu-id="24b45-135">Then, get the **getAgreements** function, followed by calling the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

<span data-ttu-id="24b45-136">Kompletní ukázku najdete ve třídě [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) z projektu [testovací aplikace konzoly](https://github.com/Microsoft/Partner-Center-Java-Samples) .</span><span class="sxs-lookup"><span data-stu-id="24b45-136">A complete sample can be found in the [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="24b45-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24b45-137">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="24b45-138">Postup načtení potvrzení o přijetí od zákazníka, které jste zadali dříve:</span><span class="sxs-lookup"><span data-stu-id="24b45-138">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="24b45-139">Použijte příkaz [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) .</span><span class="sxs-lookup"><span data-stu-id="24b45-139">Use the [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) command.</span></span>

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a><span data-ttu-id="24b45-140">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="24b45-140">REST request</span></span>

<span data-ttu-id="24b45-141">Pokud chcete načíst potvrzení o přijetí od zákazníka, které jste zadali dřív, přečtěte si následující pokyny.</span><span class="sxs-lookup"><span data-stu-id="24b45-141">To retrieve confirmation of customer acceptance provided previously, see the following instructions.</span></span>

<span data-ttu-id="24b45-142">Vytvořte nový prostředek **smlouvy** s příslušnými informacemi o certifikaci.</span><span class="sxs-lookup"><span data-stu-id="24b45-142">Create a new **Agreement** resource with the relevant certification information.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="24b45-143">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="24b45-143">Request syntax</span></span>

| <span data-ttu-id="24b45-144">Metoda</span><span class="sxs-lookup"><span data-stu-id="24b45-144">Method</span></span> | <span data-ttu-id="24b45-145">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="24b45-145">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="24b45-146">GET</span><span class="sxs-lookup"><span data-stu-id="24b45-146">GET</span></span>    | <span data-ttu-id="24b45-147">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="24b45-147">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="24b45-148">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="24b45-148">URI parameter</span></span>

<span data-ttu-id="24b45-149">K určení zákazníka, kterého potvrzujete, použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="24b45-149">Use the following query parameter to specify the customer you are confirming.</span></span>

| <span data-ttu-id="24b45-150">Název</span><span class="sxs-lookup"><span data-stu-id="24b45-150">Name</span></span>             | <span data-ttu-id="24b45-151">Typ</span><span class="sxs-lookup"><span data-stu-id="24b45-151">Type</span></span> | <span data-ttu-id="24b45-152">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="24b45-152">Required</span></span> | <span data-ttu-id="24b45-153">Popis</span><span class="sxs-lookup"><span data-stu-id="24b45-153">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="24b45-154">CustomerTenantId</span><span class="sxs-lookup"><span data-stu-id="24b45-154">CustomerTenantId</span></span> | <span data-ttu-id="24b45-155">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="24b45-155">GUID</span></span> | <span data-ttu-id="24b45-156">Y</span><span class="sxs-lookup"><span data-stu-id="24b45-156">Y</span></span>        | <span data-ttu-id="24b45-157">Hodnota je **CustomerTenantId** ve formátu GUID, který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="24b45-157">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="24b45-158">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="24b45-158">Request headers</span></span>

<span data-ttu-id="24b45-159">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="24b45-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="24b45-160">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="24b45-160">Request body</span></span>

<span data-ttu-id="24b45-161">Žádné</span><span class="sxs-lookup"><span data-stu-id="24b45-161">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="24b45-162">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="24b45-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="24b45-163">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="24b45-163">REST response</span></span>

<span data-ttu-id="24b45-164">V případě úspěchu tato metoda vrátí kolekci prostředků **smlouvy** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="24b45-164">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="24b45-165">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="24b45-165">Response success and error codes</span></span>

<span data-ttu-id="24b45-166">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="24b45-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="24b45-167">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="24b45-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="24b45-168">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="24b45-168">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="24b45-169">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="24b45-169">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```
