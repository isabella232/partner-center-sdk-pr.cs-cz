---
title: Získání kolekce nároků
description: Jak získat kolekci nároků.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7bb8d3aefb11fae0af4bce790b41598d935de57c
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906427"
---
# <a name="get-a-collection-of-entitlements"></a><span data-ttu-id="ac63c-103">Získání kolekce nároků</span><span class="sxs-lookup"><span data-stu-id="ac63c-103">Get a collection of entitlements</span></span>

<span data-ttu-id="ac63c-104">Jak získat kolekci nároků.</span><span class="sxs-lookup"><span data-stu-id="ac63c-104">How to get a collection of entitlements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac63c-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ac63c-105">Prerequisites</span></span>

- <span data-ttu-id="ac63c-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ac63c-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ac63c-107">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="ac63c-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="ac63c-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ac63c-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ac63c-109">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="ac63c-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ac63c-110">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="ac63c-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ac63c-111">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="ac63c-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ac63c-112">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="ac63c-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ac63c-113">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ac63c-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="ac63c-114">C\#</span><span class="sxs-lookup"><span data-stu-id="ac63c-114">C\#</span></span>

<span data-ttu-id="ac63c-115">Chcete-li získat kolekci nároků pro zákazníka, Získejte rozhraní pro udělení [**operací**](entitlement-resources.md#entitlement) voláním metody  [**IAggregatePartner. Customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka pro identifikaci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ac63c-115">To get an entitlements collection for a customer, obtain an interface to [**Entitlement**](entitlement-resources.md#entitlement) operations by calling the  [**IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="ac63c-116">Pak načtěte rozhraní z vlastnosti **oprávnění** a zavolejte metodu **Get ()** nebo **GetAsync ()** pro načtení kolekce nároků.</span><span class="sxs-lookup"><span data-stu-id="ac63c-116">Then, retrieve the interface from the **Entitlements** property and call the **Get()** or **GetAsync()** method to retrieve the collection of entitlements.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;

// Get the collection of entitlements.
var entitlements = partnerOperations.Customers.ById(customerId).Entitlements.Get();
```

<span data-ttu-id="ac63c-117">Chcete-li naplnit data vypršení platnosti pro získání nároků, zavolejte stejné metody výše a nastavte volitelný logický parametr **showExpiry** na hodnotu true **Get (true)** nebo **GetAsync (true)**.</span><span class="sxs-lookup"><span data-stu-id="ac63c-117">To populate expiry dates for the entitlements to be retrieved, call the same methods above and set the optional boolean parameter **showExpiry** to true **Get(true)** or **GetAsync(true)**.</span></span> <span data-ttu-id="ac63c-118">To znamená, že se vyžadují data vypršení platnosti nároku (Pokud je to možné).</span><span class="sxs-lookup"><span data-stu-id="ac63c-118">This indicates that entitlement expiry dates are required (when applicable).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac63c-119">Pro místní typy nároků neexistují data vypršení platnosti.</span><span class="sxs-lookup"><span data-stu-id="ac63c-119">On-premise entitlement types do not have expiry dates.</span></span>

## <a name="rest-request"></a><span data-ttu-id="ac63c-120">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="ac63c-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ac63c-121">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="ac63c-121">Request syntax</span></span>

| <span data-ttu-id="ac63c-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="ac63c-122">Method</span></span> | <span data-ttu-id="ac63c-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ac63c-123">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="ac63c-124">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="ac63c-124">**GET**</span></span> | <span data-ttu-id="ac63c-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customerId}/Entitlements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ac63c-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/entitlements HTTP/1.1</span></span>                            |

### <a name="uri-parameters"></a><span data-ttu-id="ac63c-126">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="ac63c-126">URI parameters</span></span>

<span data-ttu-id="ac63c-127">Při vytváření žádosti použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="ac63c-127">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="ac63c-128">Název</span><span class="sxs-lookup"><span data-stu-id="ac63c-128">Name</span></span> | <span data-ttu-id="ac63c-129">Typ</span><span class="sxs-lookup"><span data-stu-id="ac63c-129">Type</span></span> | <span data-ttu-id="ac63c-130">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ac63c-130">Required</span></span> | <span data-ttu-id="ac63c-131">Popis</span><span class="sxs-lookup"><span data-stu-id="ac63c-131">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="ac63c-132">customerId</span><span class="sxs-lookup"><span data-stu-id="ac63c-132">customerId</span></span> | <span data-ttu-id="ac63c-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="ac63c-133">string</span></span> | <span data-ttu-id="ac63c-134">Yes</span><span class="sxs-lookup"><span data-stu-id="ac63c-134">Yes</span></span> | <span data-ttu-id="ac63c-135">Identifikátor ID zákazníka ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ac63c-135">A GUID formatted customerId that identifies the customer.</span></span> |
| <span data-ttu-id="ac63c-136">entitlementType</span><span class="sxs-lookup"><span data-stu-id="ac63c-136">entitlementType</span></span> | <span data-ttu-id="ac63c-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="ac63c-137">string</span></span> | <span data-ttu-id="ac63c-138">No</span><span class="sxs-lookup"><span data-stu-id="ac63c-138">No</span></span> | <span data-ttu-id="ac63c-139">Dá se použít k určení typu nároků, které se mají načíst (**software** nebo **reservedInstance** ).</span><span class="sxs-lookup"><span data-stu-id="ac63c-139">Can be used to specify the type of entitlements to be retrieved (**software** or **reservedInstance** ).</span></span> <span data-ttu-id="ac63c-140">Pokud není nastavené, načtou se všechny typy.</span><span class="sxs-lookup"><span data-stu-id="ac63c-140">If not set, all types will be retrieved</span></span> |
| <span data-ttu-id="ac63c-141">showExpiry</span><span class="sxs-lookup"><span data-stu-id="ac63c-141">showExpiry</span></span> | <span data-ttu-id="ac63c-142">boolean</span><span class="sxs-lookup"><span data-stu-id="ac63c-142">boolean</span></span> | <span data-ttu-id="ac63c-143">No</span><span class="sxs-lookup"><span data-stu-id="ac63c-143">No</span></span> | <span data-ttu-id="ac63c-144">Volitelný příznak, který označuje, jestli se vyžadují data vypršení platnosti nároků.</span><span class="sxs-lookup"><span data-stu-id="ac63c-144">Optional flag that indicates if entitlements expiry dates are required.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ac63c-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ac63c-145">Request headers</span></span>

<span data-ttu-id="ac63c-146">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ac63c-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ac63c-147">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ac63c-147">Request body</span></span>

<span data-ttu-id="ac63c-148">Žádné</span><span class="sxs-lookup"><span data-stu-id="ac63c-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ac63c-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ac63c-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/entitlements HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ac63c-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ac63c-150">REST response</span></span>

<span data-ttu-id="ac63c-151">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [nároků](entitlement-resources.md#entitlement) .</span><span class="sxs-lookup"><span data-stu-id="ac63c-151">If successful, the response body contains a collection of [Entitlement](entitlement-resources.md#entitlement) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ac63c-152">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="ac63c-152">Response success and error codes</span></span>

<span data-ttu-id="ac63c-153">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ac63c-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ac63c-154">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="ac63c-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ac63c-155">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ac63c-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ac63c-156">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ac63c-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 103778
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: EjFdw8fCpkKyMyza.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:42:51 GMT

{
  "totalCount": 2,
  "items": [
    {
      "includedEntitlements": [],
      "referenceOrder": {
        "id": "KaJ8XvkKc_GoNZOUyjVaRJalTBN5MWdV1",
        "lineItemId": "0"
      },
      "productId": "DZH318Z0BQ3W",
      "quantity": 1,
      "entitledArtifacts": [
        {
          "link": {
            "uri": "/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336",
            "method": "GET",
            "headers": []
          },
          "resourceId": "ebf2e74b-630e-4a09-857d-a1f6c6351336",
          "artifactType": "reservedinstance"
        }
      ],
      "skuId": "007J",
      "entitlementType": "reservedinstance"
      "dynamicAttributes": {
               "reservationType": "virtualmachines"
        }
    },
    {
      "includedEntitlements": [
        {
          "includedEntitlements": [],
          "referenceOrder": {
              "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
              "lineItemId": "0"
          },
          "productId": "DG7GMGF0DWTJ",
          "quantity": 1,
          "entitledArtifacts": [],
          "skuId": "0001",
          "entitlementType": "software"
        },
        {
          "includedEntitlements": [],
          "referenceOrder": {
            "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
            "lineItemId": "0"
          },
            "productId": "DG7GMGF0DWLG",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
          }
        ],
        "referenceOrder": {
          "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
          "lineItemId": "0"
        },
        "productId": "DG7GMGF0DWTK",
        "quantity": 1,
        "entitledArtifacts": [],
        "skuId": "0002",
        "entitlementType": "software"
    }
  ],
  "attributes": {
    "objectType": "Collection"
  }
}
```

## <a name="additional-examples"></a><span data-ttu-id="ac63c-157">Další příklady</span><span class="sxs-lookup"><span data-stu-id="ac63c-157">Additional Examples</span></span>

<span data-ttu-id="ac63c-158">Následující příklad ukazuje, jak načíst konkrétní typ nároků spolu s daty vypršení platnosti (je-li k dispozici).</span><span class="sxs-lookup"><span data-stu-id="ac63c-158">The following example shows you how to retrieve a specific type of entitlements along with expiry dates (when applicable)</span></span>

### <a name="c-example"></a><span data-ttu-id="ac63c-159">\#Příklad C</span><span class="sxs-lookup"><span data-stu-id="ac63c-159">C\# example</span></span>

<span data-ttu-id="ac63c-160">Chcete-li načíst konkrétní typ oprávnění, Získejte rozhraní **ByEntitlementType** z rozhraní **nároků** a použijte metody **Get ()** nebo **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="ac63c-160">To retrieve a specific type of entitlements, obtain the **ByEntitlementType** interface from the **Entitlements** interface and use the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("software").Get(true);
```

### <a name="request-example"></a><span data-ttu-id="ac63c-161">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ac63c-161">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/de3dcef9-9991-459c-ac71-2903d1127414/entitlements?entitlementtype=software&showExpiry=true
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="ac63c-162">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ac63c-162">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1791
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
X-Locale: en-US
MS-CV: yD+4LBKePUSp/vqJ.0
MS-ServerId: 000002
Date: Mon, 28 Jan 2019 18:31:43 GMT

{
    "totalCount": 2,
    "items": [
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWM2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWMK",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "0",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWM3",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
        },
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV1",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "1",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWBQ",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0003",
            "entitlementType": "software",
            "expiryDate": "2022-01-28T00:00:00Z"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

<span data-ttu-id="ac63c-163">Následující příklady vám ukážou, jak načíst informace o produktech a rezervacích od nároku.</span><span class="sxs-lookup"><span data-stu-id="ac63c-163">The following examples show you how to retrieve information about products and reservations from an entitlement.</span></span>

### <a name="retrieve-virtual-machine-reservation-details-from-an-entitlement-by-using-sdk-v18"></a><span data-ttu-id="ac63c-164">Načíst podrobnosti rezervace virtuálních počítačů z nároku pomocí sady SDK V 1.8</span><span class="sxs-lookup"><span data-stu-id="ac63c-164">Retrieve virtual machine reservation details from an entitlement by using SDK V1.8</span></span>

### <a name="c-example"></a><span data-ttu-id="ac63c-165">\#Příklad C</span><span class="sxs-lookup"><span data-stu-id="ac63c-165">C\# example</span></span>

<span data-ttu-id="ac63c-166">Chcete-li získat další podrobnosti týkající se rezervací virtuálních počítačů od nároku, vyvolejte identifikátor URI vystavený v rámci entitledArtifacts.link s artifactType = virtual_machine_reserved_instance.</span><span class="sxs-lookup"><span data-stu-id="ac63c-166">To retrieve more details related to the virtual machine reservations from an entitlement, invoke the URI exposed under entitledArtifacts.link with artifactType = virtual_machine_reserved_instance.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("VirtualMachineReservedInstance").Get();

((VirtualMachineReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.VirtualMachineReservedInstance)).Link.InvokeAsync<VirtualMachineReservedInstanceArtifactDetails>(partnerOperations)
```

### <a name="request-example"></a><span data-ttu-id="ac63c-167">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ac63c-167">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/virtualmachinereservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="ac63c-168">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ac63c-168">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "virtual_machine_reserved_instance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="retrieve-reservation-details-from-an-entitlement-by-using-sdk-v19"></a><span data-ttu-id="ac63c-169">Načtení podrobností o rezervacích z nároku pomocí sady SDK V 1.9</span><span class="sxs-lookup"><span data-stu-id="ac63c-169">Retrieve reservation details from an entitlement by using SDK V1.9</span></span>

### <a name="c-example"></a><span data-ttu-id="ac63c-170">\#Příklad C</span><span class="sxs-lookup"><span data-stu-id="ac63c-170">C\# example</span></span>

<span data-ttu-id="ac63c-171">Chcete-li získat další podrobnosti týkající se rezervací z rezervované instance, vyvolejte identifikátor URI vystavený v ```entitledArtifacts.link``` rámci ```artifactType = reservedinstance``` .</span><span class="sxs-lookup"><span data-stu-id="ac63c-171">To retrieve more details related to the reservations from a reserved instance entitlement, invoke the URI exposed under ```entitledArtifacts.link``` with ```artifactType = reservedinstance```.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("ReservedInstance").Get();

((ReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.ReservedInstance)).Link.InvokeAsync<ReservedInstanceArtifactDetails>(partnerOperations);
```

### <a name="request-example"></a><span data-ttu-id="ac63c-172">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ac63c-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="ac63c-173">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ac63c-173">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "reservedinstance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="api-consumers"></a><span data-ttu-id="ac63c-174">Příjemci rozhraní API</span><span class="sxs-lookup"><span data-stu-id="ac63c-174">API Consumers</span></span>

<span data-ttu-id="ac63c-175">Partneři, kteří používají rozhraní API k dotazování na nároky na rezervované instance virtuálního počítače – aktualizujte identifikátor URI požadavku z **/Customers/{customerId}/Entitlements na/Customers/{customerId}/Entitlements? entitlementType = virtualmachinereservedinstance** , aby se zachovala zpětná kompatibilita.</span><span class="sxs-lookup"><span data-stu-id="ac63c-175">Partners who are using the API to query virtual machine reserved instance entitlements - Update the request URI from **/customers/{customerId}/entitlements to /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance** to maintain backward compatibility.</span></span> <span data-ttu-id="ac63c-176">pokud chcete využívat virtuální počítač nebo Azure SQL se zdokonalenou smlouvou, aktualizujte identifikátor URI žádosti na **/customers/{customerId}/entitlements? entitlementType = reservedinstance**.</span><span class="sxs-lookup"><span data-stu-id="ac63c-176">To consume virtual machine or Azure SQL with enhanced contract, update the request URI to **/customers/{customerId}/entitlements?entitlementType=reservedinstance**.</span></span>
