---
title: Získání potvrzení přijetí Smlouvy o službách Microsoft Cloud ze strany zákazníka
description: Tento článek vysvětluje, jak získat potvrzení souhlasu zákazníka s Smlouva o službách Microsoft Cloud.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: 1b1a8cbacb667e579bcd218a29c3f553afce26c2
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549259"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a><span data-ttu-id="427d5-103">Získání potvrzení přijetí Smlouvy o službách Microsoft Cloud ze strany zákazníka</span><span class="sxs-lookup"><span data-stu-id="427d5-103">Get confirmation of customer acceptance of Microsoft Cloud Agreement</span></span>

<span data-ttu-id="427d5-104">**Platí pro:** Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="427d5-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="427d5-105">**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="427d5-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="427d5-106">Prostředek **smlouvy** je aktuálně podporován Partnerské centrum ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="427d5-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="427d5-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="427d5-107">Prerequisites</span></span>

- <span data-ttu-id="427d5-108">Pokud používáte sadu .NET SDK Partnerské centrum, vyžaduje se verze 1.9 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="427d5-108">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="427d5-109">Pokud používáte sadu Java SDK Partnerské centrum, vyžaduje se verze 1.8 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="427d5-109">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="427d5-110">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="427d5-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="427d5-111">Tento scénář podporuje pouze ověřování aplikací a uživatelů.</span><span class="sxs-lookup"><span data-stu-id="427d5-111">This scenario only supports app + user authentication.</span></span>

- <span data-ttu-id="427d5-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="427d5-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="427d5-113">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="427d5-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="427d5-114">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="427d5-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="427d5-115">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="427d5-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="427d5-116">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="427d5-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="427d5-117">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="427d5-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net-version-14-or-newer"></a><span data-ttu-id="427d5-118">.NET (verze 1.4 nebo novější)</span><span class="sxs-lookup"><span data-stu-id="427d5-118">.NET (version 1.4 or newer)</span></span>

<span data-ttu-id="427d5-119">Získání potvrzení přijetí zákazníkem, která byla dříve poskytnuta:</span><span class="sxs-lookup"><span data-stu-id="427d5-119">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="427d5-120">Použijte kolekci **IAggregatePartner.Customers** a zavolejte **metodu ById** se zadaným identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="427d5-120">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="427d5-121">**Načítá** vlastnost Agreements a filtruje výsledky, Smlouva o službách Microsoft Cloud voláním **metody ByAgreementType.**</span><span class="sxs-lookup"><span data-stu-id="427d5-121">Fetch the **Agreements** property and filter the results to Microsoft Cloud Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="427d5-122">Volejte **metodu Get** **nebo GetAsync.**</span><span class="sxs-lookup"><span data-stu-id="427d5-122">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="427d5-123">Úplnou ukázku najdete ve třídě [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) z projektu [konzolové testovací](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) aplikace.</span><span class="sxs-lookup"><span data-stu-id="427d5-123">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="427d5-124">.NET (verze 1.9 – 1.13)</span><span class="sxs-lookup"><span data-stu-id="427d5-124">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="427d5-125">Pokud chcete načíst potvrzení o přijetí zákazníkem, které jste uvedli dříve:</span><span class="sxs-lookup"><span data-stu-id="427d5-125">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="427d5-126">Použijte kolekci **IAggregatePartner.Customers** a zavolejte metodu **ById** s identifikátorem zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="427d5-126">Use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's identifier.</span></span> <span data-ttu-id="427d5-127">Pak získejte vlastnost **Agreements** a potom voláním **metod Get** nebo **GetAsync.**</span><span class="sxs-lookup"><span data-stu-id="427d5-127">Then, get the **Agreements** property, followed by calling the **Get** or **GetAsync** methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a><span data-ttu-id="427d5-128">Java</span><span class="sxs-lookup"><span data-stu-id="427d5-128">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="427d5-129">Pokud chcete načíst potvrzení o přijetí zákazníkem, které jste uvedli dříve:</span><span class="sxs-lookup"><span data-stu-id="427d5-129">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="427d5-130">Použijte funkci **IAggregatePartner.getCustomers** a zavolejte funkci **byId** s identifikátorem zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="427d5-130">Use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier.</span></span> <span data-ttu-id="427d5-131">Pak získejte **funkci getAgreements** a potom zavoláte **funkci get.**</span><span class="sxs-lookup"><span data-stu-id="427d5-131">Then, get the **getAgreements** function, followed by calling the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

<span data-ttu-id="427d5-132">Úplnou ukázku najdete ve třídě [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) z projektu [konzolové testovací](https://github.com/Microsoft/Partner-Center-Java-Samples) aplikace.</span><span class="sxs-lookup"><span data-stu-id="427d5-132">A complete sample can be found in the [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="427d5-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="427d5-133">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="427d5-134">Pokud chcete načíst potvrzení o přijetí zákazníkem, které jste uvedli dříve:</span><span class="sxs-lookup"><span data-stu-id="427d5-134">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="427d5-135">Použijte příkaz [**Get-PartnerCustomerAgreement.**](/powershell/module/partnercenter/get-partnercustomeragreement)</span><span class="sxs-lookup"><span data-stu-id="427d5-135">Use the [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) command.</span></span>

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a><span data-ttu-id="427d5-136">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="427d5-136">REST request</span></span>

<span data-ttu-id="427d5-137">Pokud chcete získat potvrzení o přijetí zákazníkem, které jste uvedli dříve, přečtěte si následující pokyny.</span><span class="sxs-lookup"><span data-stu-id="427d5-137">To retrieve confirmation of customer acceptance provided previously, see the following instructions.</span></span>

<span data-ttu-id="427d5-138">Vytvořte nový prostředek **smlouvy** s příslušnými certifikačními informacemi.</span><span class="sxs-lookup"><span data-stu-id="427d5-138">Create a new **Agreement** resource with the relevant certification information.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="427d5-139">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="427d5-139">Request syntax</span></span>

| <span data-ttu-id="427d5-140">Metoda</span><span class="sxs-lookup"><span data-stu-id="427d5-140">Method</span></span> | <span data-ttu-id="427d5-141">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="427d5-141">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="427d5-142">GET</span><span class="sxs-lookup"><span data-stu-id="427d5-142">GET</span></span>    | <span data-ttu-id="427d5-143">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/smlouvy HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="427d5-143">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="427d5-144">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="427d5-144">URI parameter</span></span>

<span data-ttu-id="427d5-145">Pomocí následujícího parametru dotazu zadejte zákazníka, který potvrzujete.</span><span class="sxs-lookup"><span data-stu-id="427d5-145">Use the following query parameter to specify the customer you are confirming.</span></span>

| <span data-ttu-id="427d5-146">Název</span><span class="sxs-lookup"><span data-stu-id="427d5-146">Name</span></span>             | <span data-ttu-id="427d5-147">Typ</span><span class="sxs-lookup"><span data-stu-id="427d5-147">Type</span></span> | <span data-ttu-id="427d5-148">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="427d5-148">Required</span></span> | <span data-ttu-id="427d5-149">Popis</span><span class="sxs-lookup"><span data-stu-id="427d5-149">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="427d5-150">CustomerTenantId</span><span class="sxs-lookup"><span data-stu-id="427d5-150">CustomerTenantId</span></span> | <span data-ttu-id="427d5-151">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="427d5-151">GUID</span></span> | <span data-ttu-id="427d5-152">Y</span><span class="sxs-lookup"><span data-stu-id="427d5-152">Y</span></span>        | <span data-ttu-id="427d5-153">Hodnota je identifikátor GUID naformátovaný **jako CustomerTenantId,** který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="427d5-153">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="427d5-154">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="427d5-154">Request headers</span></span>

<span data-ttu-id="427d5-155">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="427d5-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="427d5-156">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="427d5-156">Request body</span></span>

<span data-ttu-id="427d5-157">Žádné</span><span class="sxs-lookup"><span data-stu-id="427d5-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="427d5-158">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="427d5-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="427d5-159">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="427d5-159">REST response</span></span>

<span data-ttu-id="427d5-160">V případě úspěchu vrátí tato  metoda v textu odpovědi kolekci prostředků smlouvy.</span><span class="sxs-lookup"><span data-stu-id="427d5-160">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="427d5-161">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="427d5-161">Response success and error codes</span></span>

<span data-ttu-id="427d5-162">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="427d5-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="427d5-163">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="427d5-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="427d5-164">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="427d5-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="427d5-165">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="427d5-165">Response example</span></span>

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
