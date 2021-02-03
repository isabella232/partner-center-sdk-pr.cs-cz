---
title: Odebrání vztahu prodejce se zákazníkem
description: Postup odebrání vztahu prodejce k zákazníkovi, se kterým již transakce nemáte.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 084797997e57c63b5c447379bb08ecb88ebd0cc4
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766952"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a><span data-ttu-id="bdc62-103">Odebrání vztahu prodejce se zákazníkem</span><span class="sxs-lookup"><span data-stu-id="bdc62-103">Remove a reseller relationship with a customer</span></span>

<span data-ttu-id="bdc62-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="bdc62-104">**Applies To**</span></span>

- <span data-ttu-id="bdc62-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="bdc62-105">Partner Center</span></span>

<span data-ttu-id="bdc62-106">Odeberte vztah prodejce se zákazníkem, se kterým již nebudete mít transakce.</span><span class="sxs-lookup"><span data-stu-id="bdc62-106">Remove a reseller relationship with a customer that you no longer have transactions with.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdc62-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="bdc62-107">Prerequisites</span></span>

- <span data-ttu-id="bdc62-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bdc62-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bdc62-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="bdc62-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="bdc62-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bdc62-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="bdc62-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="bdc62-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="bdc62-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="bdc62-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="bdc62-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="bdc62-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="bdc62-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="bdc62-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="bdc62-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bdc62-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="bdc62-116">Před odebráním vztahu prodejce se musí zrušit všechny objednávky rezervovaných instancí virtuálních počítačů Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc62-116">All Azure Reserved VM Instance orders must be canceled before a reseller relationship is removed.</span></span> <span data-ttu-id="bdc62-117">Zavolejte podporu Azure pro zrušení všech otevřených objednávek rezervované instance virtuálního počítače Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc62-117">Call Azure support for canceling any open Azure Reserved VM Instance orders.</span></span>

## <a name="c"></a><span data-ttu-id="bdc62-118">C\#</span><span class="sxs-lookup"><span data-stu-id="bdc62-118">C\#</span></span>

<span data-ttu-id="bdc62-119">Chcete-li odebrat vztah prodejce pro zákazníka, nejprve zajistěte, aby všechny aktivní Azure Reserved VM Instances pro tohoto zákazníka byly zrušeny.</span><span class="sxs-lookup"><span data-stu-id="bdc62-119">To remove the reseller relationship for a customer, first ensure that any active Azure Reserved VM Instances for that customer are canceled.</span></span> <span data-ttu-id="bdc62-120">Dále zajistěte, aby všechny aktivní odběry pro tohoto zákazníka byly pozastaveny.</span><span class="sxs-lookup"><span data-stu-id="bdc62-120">Next, ensure that all active subscriptions for that customer are suspended.</span></span> <span data-ttu-id="bdc62-121">Provedete to tak, že určíte ID zákazníka, pro kterého chcete odstranit vztah prodejce.</span><span class="sxs-lookup"><span data-stu-id="bdc62-121">To do so, determine the ID of the customer for whom you want to delete the reseller relationship.</span></span> <span data-ttu-id="bdc62-122">V následujícím příkladu kódu se uživateli zobrazí výzva k zadání identifikátoru zákazníka.</span><span class="sxs-lookup"><span data-stu-id="bdc62-122">In the following code example, the user is prompted to provide the customer identifier.</span></span>

<span data-ttu-id="bdc62-123">Chcete-li určit, zda je nutné zrušit některý Azure Reserved VM Instances pro zákazníka, načtěte kolekci nároků voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) pomocí identifikátoru zákazníka a určete zákazníka a vlastnost [**oprávnění**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) k načtení rozhraní pro operace shromažďování nároků.</span><span class="sxs-lookup"><span data-stu-id="bdc62-123">To determine if any Azure Reserved VM Instances for the customer must be canceled, retrieve the collection of entitlements by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Entitlements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to entitlement collection operations.</span></span> <span data-ttu-id="bdc62-124">Pro načtení kolekce nároků zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="bdc62-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the entitlement collection.</span></span> <span data-ttu-id="bdc62-125">Vyfiltrujte kolekci pro všechna oprávnění s hodnotou [**EntitlementType**](entitlement-resources.md#entitlementtype) [**EntitlementType. VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) , a pokud existují, zrušte je voláním podpory, než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="bdc62-125">Filter the collection for any entitlements with an [**EntitlementType**](entitlement-resources.md#entitlementtype) value of [**EntitlementType.VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) and if there are any, cancel them by calling support before proceeding.</span></span>

<span data-ttu-id="bdc62-126">Pak načtěte kolekci předplatných zákazníka voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) pomocí identifikátoru zákazníka a zadejte zákazníka a vlastnost [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) pro načtení rozhraní pro operace shromažďování předplatných.</span><span class="sxs-lookup"><span data-stu-id="bdc62-126">Then, retrieve a collection of the customer's subscriptions by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="bdc62-127">Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) načtěte kolekci předplatných zákazníka.</span><span class="sxs-lookup"><span data-stu-id="bdc62-127">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the customer's subscriptions collection.</span></span> <span data-ttu-id="bdc62-128">Prochází kolekci předplatných a zajistěte, aby žádné odběry neměly [**předplatné.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) hodnota vlastnosti status [**SubscriptionStatus. Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="bdc62-128">Traverse the subscription collection and ensure that none of the subscriptions have a [**Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property value of [**SubscriptionStatus.Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="bdc62-129">Pokud je předplatné pořád aktivní, přečtěte si téma [pozastavení předplatného](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) , kde najdete informace o tom, jak ho pozastavit.</span><span class="sxs-lookup"><span data-stu-id="bdc62-129">If a subscription is still active, see [Suspend a subscription](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) for information on how to suspend it.</span></span>

<span data-ttu-id="bdc62-130">Po potvrzení, že se všechny aktivní Azure Reserved VM Instances pro tohoto zákazníka zruší a že se všechna aktivní předplatná pozastaví, můžete pro zákazníka odebrat vztah prodejce.</span><span class="sxs-lookup"><span data-stu-id="bdc62-130">After confirming that all active Azure Reserved VM Instances for that customer are canceled and all active subscriptions are suspended, you can remove the reseller relationship for the customer.</span></span> <span data-ttu-id="bdc62-131">Nejprve vytvořte nový objekt [Customer/dotnet/API/Microsoft. Store. partnercenter. Models. Customers. Customer. Customer. Customer. Customers. Customer. [](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship)</span><span class="sxs-lookup"><span data-stu-id="bdc62-131">First, create a new [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object with the [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) property set to [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span></span> <span data-ttu-id="bdc62-132">Potom zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) pomocí identifikátoru zákazníka pro určení zákazníka a zavolejte metodu **patch** a předejte ji do nového objektu Customer.</span><span class="sxs-lookup"><span data-stu-id="bdc62-132">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and call the **Patch** method, passing in the new customer object.</span></span>

<span data-ttu-id="bdc62-133">Chcete-li znovu vytvořit relaci, opakujte postup [vyžadování vztahu prodejce/partner-Center/vývoj/vývoj/požadavek-prodejce – vztah).</span><span class="sxs-lookup"><span data-stu-id="bdc62-133">To re-establish the relationship, repeat the process of [requesting a reseller relationship/partner-center/develop/request-reseller-relationship).</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// Prompt the user the enter the customer ID.
var customerIdToDeleteRelationshipOf = this.Context.ConsoleHelper.ReadNonEmptyString("Please enter the ID of the customer you want to delete the relationship with", "The customer ID can't be empty");

// Determine if there are any active Azure Reserved VM Instances for this customer.
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Entitlements.Get();

If (entitlements.Items.Where(x => x.EntitlementType == EntitlementType.VirtualMachineReservedInstance).Any())
{
    this.Context.ConsoleHelper.Warning("Please cancel Azure Reserved Virtual Machine Instance orders through support and try again. Aborting the delete customer relationship operation");
               return;
}

// Verify that there are no active subscriptions.
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Subscriptions.Get();
IList<Subscription> subscriptions = new List<Subscription>(customerSubscriptions.Items);

foreach (Subscription customerSubscription in subscriptions)
{
    if (customerSubscription.Status == SubscriptionStatus.Active)
    {
        this.Context.ConsoleHelper.Warning(String.Format("Subscription with ID :{0}  OfferName: {1} cannot be in active state, ", customerSubscription.Id, customerSubscription.OfferName));
        this.Context.ConsoleHelper.Warning("Please Suspend all the Subscriptions and try again. Aborting the delete customer relationship operation");
               return;
    }
}

// Delete the customer's relationship to the partner.
Customer customer = new Customer();
customer.RelationshipToPartner = CustomerPartnerRelationship.None;
customer = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Patch(customer);

if (customer.RelationshipToPartner == CustomerPartnerRelationship.None)
{
    this.Context.ConsoleHelper.Success("Customer Partner Relationship successfully deleted");
}
```

<span data-ttu-id="bdc62-134">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="bdc62-134">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="bdc62-135">**Projekt**: PartnerSDK. FeatureSample **Třída**: DeletePartnerCustomerRelationship.cs</span><span class="sxs-lookup"><span data-stu-id="bdc62-135">**Project**: PartnerSDK.FeatureSample **Class**: DeletePartnerCustomerRelationship.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="bdc62-136">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="bdc62-136">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bdc62-137">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="bdc62-137">Request syntax</span></span>

| <span data-ttu-id="bdc62-138">Metoda</span><span class="sxs-lookup"><span data-stu-id="bdc62-138">Method</span></span>     | <span data-ttu-id="bdc62-139">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="bdc62-139">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bdc62-140">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="bdc62-140">**PATCH**</span></span>  | <span data-ttu-id="bdc62-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="bdc62-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="bdc62-142">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="bdc62-142">URI parameter</span></span>

<span data-ttu-id="bdc62-143">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro odebrání vztahu prodejce.</span><span class="sxs-lookup"><span data-stu-id="bdc62-143">This table lists the required query parameters to remove a reseller relationship.</span></span>

| <span data-ttu-id="bdc62-144">Název</span><span class="sxs-lookup"><span data-stu-id="bdc62-144">Name</span></span>                   | <span data-ttu-id="bdc62-145">Typ</span><span class="sxs-lookup"><span data-stu-id="bdc62-145">Type</span></span>     | <span data-ttu-id="bdc62-146">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="bdc62-146">Required</span></span> | <span data-ttu-id="bdc62-147">Popis</span><span class="sxs-lookup"><span data-stu-id="bdc62-147">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="bdc62-148">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="bdc62-148">**customer-tenant-id**</span></span> | <span data-ttu-id="bdc62-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="bdc62-149">**guid**</span></span> | <span data-ttu-id="bdc62-150">Y</span><span class="sxs-lookup"><span data-stu-id="bdc62-150">Y</span></span>        | <span data-ttu-id="bdc62-151">Hodnota je identifikátor **zákazníka (zákazníka** ), který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="bdc62-151">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="bdc62-152">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="bdc62-152">Request headers</span></span>

<span data-ttu-id="bdc62-153">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="bdc62-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bdc62-154">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="bdc62-154">Request body</span></span>

<span data-ttu-id="bdc62-155">V textu žádosti se vyžaduje prostředek **zákazníka** .</span><span class="sxs-lookup"><span data-stu-id="bdc62-155">A **Customer** resource is required in the request body.</span></span> <span data-ttu-id="bdc62-156">Ujistěte se, že vlastnost **RelationshipToPartner** byla nastavena na hodnotu None.</span><span class="sxs-lookup"><span data-stu-id="bdc62-156">Ensure the **RelationshipToPartner** property has been set to none.</span></span>

### <a name="request-example"></a><span data-ttu-id="bdc62-157">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="bdc62-157">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Content-Length: 74
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
MS-RequestId: 9fef8b23-6e3e-45d2-8678-e9fe89c35af5
Date: Fri, 12 Jan 2018 00:31:55 GMT

{
    "relationshipToPartner":"none",
    "attributes":{
        "objectType":"Customer"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="bdc62-158">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="bdc62-158">REST response</span></span>

<span data-ttu-id="bdc62-159">V případě úspěchu tato metoda odebere vztah prodejce pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="bdc62-159">If successful, this method removes a reseller relationship for the specified customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bdc62-160">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="bdc62-160">Response success and error codes</span></span>

<span data-ttu-id="bdc62-161">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="bdc62-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bdc62-162">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="bdc62-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bdc62-163">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bdc62-163">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bdc62-164">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="bdc62-164">Response example</span></span>

```http
HTTP/1.1 200 OK
MS-RequestId: 7988dde4-b516-472c-b226-6d53fb18f04e
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
X-Locale: en-US
Content-Type: application/json
Content-Length: 242
Expect: 100-continue

{
    "Id":null,
    "CommerceId":null,
    "CompanyProfile":null,
    "BillingProfile":null,
    "RelationshipToPartner":"none",
    "AllowDelegatedAccess":null,
    "UserCredentials":null,
    "CustomDomains":null,
    "AssociatedPartnerId":null,
    "Attributes":{
        "ObjectType":"Customer"
    }
}
```
