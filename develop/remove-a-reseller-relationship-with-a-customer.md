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
# <a name="remove-a-reseller-relationship-with-a-customer"></a>Odebrání vztahu prodejce se zákazníkem

Odeberte vztah prodejce se zákazníkem, se kterou už nemáte transakce.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Před odebráním vztahu prodejce je nutné zrušit všechny objednávky rezervovaných instancí virtuálních počítače Azure. Pokud podpora Azure všechny otevřené objednávky rezervovaných instancí virtuálních počítače Azure, zavolejte na e-účet.

## <a name="c"></a>C\#

Pokud chcete odebrat vztah prodejce pro zákazníka, nejprve se ujistěte, že jsou Azure Reserved VM Instances všechny aktivní položky pro tohoto zákazníka zrušené. Dále se ujistěte, že jsou všechna aktivní předplatná pro tohoto zákazníka pozastavená. Pokud to chcete udělat, určete ID zákazníka, pro kterého chcete odstranit vztah prodejce. V následujícím příkladu kódu se uživateli zobrazí výzva k zadání identifikátoru zákazníka.

Pokud chcete zjistit, jestli je nutné zrušit jakoukoli Azure Reserved VM Instances pro zákazníka, načtěte kolekci nároků voláním metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s použitím identifikátoru zákazníka k určení zákazníka a vlastnosti [**Entitlements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) pro načtení rozhraní pro operace kolekce nároků. Voláním [**metody Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) načtěte kolekci nároků. Vyfiltrujte kolekci pro jakákoli oprávnění s hodnotou [**EntitlementType.VirtualMachineReservedInstance,**](entitlement-resources.md#entitlementtype) a pokud existují, zrušte je voláním podpory před pokračováním. [](entitlement-resources.md#entitlementtype)

Potom načtěte kolekci předplatných zákazníka voláním metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s použitím identifikátoru zákazníka k určení zákazníka a vlastnosti [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) pro načtení rozhraní pro operace shromažďování předplatných. Nakonec zavolejte [**metodu Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) a načtěte kolekci předplatných zákazníka. Prohlédněte kolekci předplatného a ujistěte se, že žádné z předplatných nemají hodnotu vlastnosti [**Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) [**vlastnosti SubscriptionStatus.Active.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus) Pokud je předplatné stále aktivní, informace o [tom,](suspend-a-subscription.md) jak předplatné pozastavit, najdete v tématu Pozastavení předplatného.

Po potvrzení, že jsou Azure Reserved VM Instances všechny aktivní předplatné pro tohoto zákazníka zrušené a všechna aktivní předplatná jsou pozastavená, můžete pro zákazníka odebrat vztah prodejce. Nejprve vytvořte nový objekt [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) s vlastností [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) nastavenou na [**Hodnotu CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship). Potom zavolejte [**metodu IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) pomocí identifikátoru zákazníka a určete zákazníka a zavolejte metodu **Patch,** která předá nový objekt zákazníka.

Pokud chcete vztah znovu vytvořit, opakujte postup [vyžádání vztahu prodejce/ partnerského centra / vývoje / vztahu žádost-prodejce).

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

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** PartnerSDK.FeatureSample **– třída:** DeletePartnerCustomerRelationship.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda     | Identifikátor URI žádosti                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **Oprava**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/ HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro odebrání vztahu prodejce.

| Název                   | Typ     | Vyžadováno | Popis                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Hodnota je IDENTIFIKÁTOR GUID **naformátovaný jako customer-tenant-id,** který identifikuje zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

V **textu** požadavku se vyžaduje prostředek zákazníka. Ujistěte **se, že vlastnost RelationshipToPartner** je nastavená na hodnotu none.

### <a name="request-example"></a>Příklad požadavku

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

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda odebere vztah prodejce pro zadaného zákazníka.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

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
