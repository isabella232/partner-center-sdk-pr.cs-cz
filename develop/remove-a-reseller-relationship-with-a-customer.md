---
title: Odebrání vztahu prodejce se zákazníkem
description: Jak odebrat vztah prodejce se zákazníkem, se kterou už nemáte transakce.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 45eca3564c3b9078e04d1f8155d08849a589d52f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446594"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a><span data-ttu-id="2d54e-103">Odebrání vztahu prodejce se zákazníkem</span><span class="sxs-lookup"><span data-stu-id="2d54e-103">Remove a reseller relationship with a customer</span></span>

<span data-ttu-id="2d54e-104">Odeberte vztah prodejce se zákazníkem, se kterou už nemáte transakce.</span><span class="sxs-lookup"><span data-stu-id="2d54e-104">Remove a reseller relationship with a customer that you no longer have transactions with.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d54e-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="2d54e-105">Prerequisites</span></span>

- <span data-ttu-id="2d54e-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2d54e-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2d54e-107">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="2d54e-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2d54e-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2d54e-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2d54e-109">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="2d54e-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2d54e-110">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="2d54e-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2d54e-111">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="2d54e-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2d54e-112">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="2d54e-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2d54e-113">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2d54e-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2d54e-114">Před odebráním vztahu prodejce je nutné zrušit všechny objednávky rezervovaných instancí virtuálních počítače Azure.</span><span class="sxs-lookup"><span data-stu-id="2d54e-114">All Azure Reserved VM Instance orders must be canceled before a reseller relationship is removed.</span></span> <span data-ttu-id="2d54e-115">Pokud podpora Azure všechny otevřené objednávky rezervovaných instancí virtuálních počítače Azure, zavolejte na e-účet.</span><span class="sxs-lookup"><span data-stu-id="2d54e-115">Call Azure support for canceling any open Azure Reserved VM Instance orders.</span></span>

## <a name="c"></a><span data-ttu-id="2d54e-116">C\#</span><span class="sxs-lookup"><span data-stu-id="2d54e-116">C\#</span></span>

<span data-ttu-id="2d54e-117">Pokud chcete odebrat vztah prodejce pro zákazníka, nejprve se ujistěte, že jsou Azure Reserved VM Instances všechny aktivní položky pro tohoto zákazníka zrušené.</span><span class="sxs-lookup"><span data-stu-id="2d54e-117">To remove the reseller relationship for a customer, first ensure that any active Azure Reserved VM Instances for that customer are canceled.</span></span> <span data-ttu-id="2d54e-118">Dále se ujistěte, že jsou všechna aktivní předplatná pro tohoto zákazníka pozastavená.</span><span class="sxs-lookup"><span data-stu-id="2d54e-118">Next, ensure that all active subscriptions for that customer are suspended.</span></span> <span data-ttu-id="2d54e-119">Pokud to chcete udělat, určete ID zákazníka, pro kterého chcete odstranit vztah prodejce.</span><span class="sxs-lookup"><span data-stu-id="2d54e-119">To do so, determine the ID of the customer for whom you want to delete the reseller relationship.</span></span> <span data-ttu-id="2d54e-120">V následujícím příkladu kódu se uživateli zobrazí výzva k zadání identifikátoru zákazníka.</span><span class="sxs-lookup"><span data-stu-id="2d54e-120">In the following code example, the user is prompted to provide the customer identifier.</span></span>

<span data-ttu-id="2d54e-121">Pokud chcete zjistit, jestli je nutné zrušit jakoukoli Azure Reserved VM Instances pro zákazníka, načtěte kolekci nároků voláním metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s použitím identifikátoru zákazníka k určení zákazníka a vlastnosti [**Entitlements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) pro načtení rozhraní pro operace kolekce nároků.</span><span class="sxs-lookup"><span data-stu-id="2d54e-121">To determine if any Azure Reserved VM Instances for the customer must be canceled, retrieve the collection of entitlements by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Entitlements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to entitlement collection operations.</span></span> <span data-ttu-id="2d54e-122">Voláním [**metody Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) načtěte kolekci nároků.</span><span class="sxs-lookup"><span data-stu-id="2d54e-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the entitlement collection.</span></span> <span data-ttu-id="2d54e-123">Vyfiltrujte kolekci pro jakákoli oprávnění s hodnotou [**EntitlementType.VirtualMachineReservedInstance,**](entitlement-resources.md#entitlementtype) a pokud existují, zrušte je voláním podpory před pokračováním. [](entitlement-resources.md#entitlementtype)</span><span class="sxs-lookup"><span data-stu-id="2d54e-123">Filter the collection for any entitlements with an [**EntitlementType**](entitlement-resources.md#entitlementtype) value of [**EntitlementType.VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) and if there are any, cancel them by calling support before proceeding.</span></span>

<span data-ttu-id="2d54e-124">Potom načtěte kolekci předplatných zákazníka voláním metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s použitím identifikátoru zákazníka k určení zákazníka a vlastnosti [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) pro načtení rozhraní pro operace shromažďování předplatných.</span><span class="sxs-lookup"><span data-stu-id="2d54e-124">Then, retrieve a collection of the customer's subscriptions by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="2d54e-125">Nakonec zavolejte [**metodu Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) a načtěte kolekci předplatných zákazníka.</span><span class="sxs-lookup"><span data-stu-id="2d54e-125">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the customer's subscriptions collection.</span></span> <span data-ttu-id="2d54e-126">Prohlédněte kolekci předplatného a ujistěte se, že žádné z předplatných nemají hodnotu vlastnosti [**Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) [**vlastnosti SubscriptionStatus.Active.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)</span><span class="sxs-lookup"><span data-stu-id="2d54e-126">Traverse the subscription collection and ensure that none of the subscriptions have a [**Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property value of [**SubscriptionStatus.Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="2d54e-127">Pokud je předplatné stále aktivní, informace o [tom,](suspend-a-subscription.md) jak předplatné pozastavit, najdete v tématu Pozastavení předplatného.</span><span class="sxs-lookup"><span data-stu-id="2d54e-127">If a subscription is still active, see [Suspend a subscription](suspend-a-subscription.md) for information on how to suspend it.</span></span>

<span data-ttu-id="2d54e-128">Po potvrzení, že jsou Azure Reserved VM Instances všechny aktivní předplatné pro tohoto zákazníka zrušené a všechna aktivní předplatná jsou pozastavená, můžete pro zákazníka odebrat vztah prodejce.</span><span class="sxs-lookup"><span data-stu-id="2d54e-128">After confirming that all active Azure Reserved VM Instances for that customer are canceled and all active subscriptions are suspended, you can remove the reseller relationship for the customer.</span></span> <span data-ttu-id="2d54e-129">Nejprve vytvořte nový objekt [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) s vlastností [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) nastavenou na [**Hodnotu CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span><span class="sxs-lookup"><span data-stu-id="2d54e-129">First, create a new [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object with the [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) property set to [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span></span> <span data-ttu-id="2d54e-130">Potom zavolejte [**metodu IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) pomocí identifikátoru zákazníka a určete zákazníka a zavolejte metodu **Patch,** která předá nový objekt zákazníka.</span><span class="sxs-lookup"><span data-stu-id="2d54e-130">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and call the **Patch** method, passing in the new customer object.</span></span>

<span data-ttu-id="2d54e-131">Pokud chcete vztah znovu vytvořit, opakujte postup [vyžádání vztahu prodejce/ partnerského centra / vývoje / vztahu žádost-prodejce).</span><span class="sxs-lookup"><span data-stu-id="2d54e-131">To re-establish the relationship, repeat the process of [requesting a reseller relationship/partner-center/develop/request-reseller-relationship).</span></span>

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

<span data-ttu-id="2d54e-132">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2d54e-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2d54e-133">**Project:** PartnerSDK.FeatureSample **– třída:** DeletePartnerCustomerRelationship.cs</span><span class="sxs-lookup"><span data-stu-id="2d54e-133">**Project**: PartnerSDK.FeatureSample **Class**: DeletePartnerCustomerRelationship.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2d54e-134">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="2d54e-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2d54e-135">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="2d54e-135">Request syntax</span></span>

| <span data-ttu-id="2d54e-136">Metoda</span><span class="sxs-lookup"><span data-stu-id="2d54e-136">Method</span></span>     | <span data-ttu-id="2d54e-137">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="2d54e-137">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2d54e-138">**Oprava**</span><span class="sxs-lookup"><span data-stu-id="2d54e-138">**PATCH**</span></span>  | <span data-ttu-id="2d54e-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/ HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2d54e-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2d54e-140">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="2d54e-140">URI parameter</span></span>

<span data-ttu-id="2d54e-141">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro odebrání vztahu prodejce.</span><span class="sxs-lookup"><span data-stu-id="2d54e-141">This table lists the required query parameters to remove a reseller relationship.</span></span>

| <span data-ttu-id="2d54e-142">Název</span><span class="sxs-lookup"><span data-stu-id="2d54e-142">Name</span></span>                   | <span data-ttu-id="2d54e-143">Typ</span><span class="sxs-lookup"><span data-stu-id="2d54e-143">Type</span></span>     | <span data-ttu-id="2d54e-144">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="2d54e-144">Required</span></span> | <span data-ttu-id="2d54e-145">Popis</span><span class="sxs-lookup"><span data-stu-id="2d54e-145">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="2d54e-146">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="2d54e-146">**customer-tenant-id**</span></span> | <span data-ttu-id="2d54e-147">**guid**</span><span class="sxs-lookup"><span data-stu-id="2d54e-147">**guid**</span></span> | <span data-ttu-id="2d54e-148">Y</span><span class="sxs-lookup"><span data-stu-id="2d54e-148">Y</span></span>        | <span data-ttu-id="2d54e-149">Hodnota je IDENTIFIKÁTOR GUID **naformátovaný jako customer-tenant-id,** který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="2d54e-149">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2d54e-150">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="2d54e-150">Request headers</span></span>

<span data-ttu-id="2d54e-151">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2d54e-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2d54e-152">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="2d54e-152">Request body</span></span>

<span data-ttu-id="2d54e-153">V **textu** požadavku se vyžaduje prostředek zákazníka.</span><span class="sxs-lookup"><span data-stu-id="2d54e-153">A **Customer** resource is required in the request body.</span></span> <span data-ttu-id="2d54e-154">Ujistěte **se, že vlastnost RelationshipToPartner** je nastavená na hodnotu none.</span><span class="sxs-lookup"><span data-stu-id="2d54e-154">Ensure the **RelationshipToPartner** property has been set to none.</span></span>

### <a name="request-example"></a><span data-ttu-id="2d54e-155">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="2d54e-155">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2d54e-156">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="2d54e-156">REST response</span></span>

<span data-ttu-id="2d54e-157">V případě úspěchu tato metoda odebere vztah prodejce pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="2d54e-157">If successful, this method removes a reseller relationship for the specified customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2d54e-158">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="2d54e-158">Response success and error codes</span></span>

<span data-ttu-id="2d54e-159">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="2d54e-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2d54e-160">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="2d54e-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2d54e-161">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2d54e-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2d54e-162">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="2d54e-162">Response example</span></span>

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
