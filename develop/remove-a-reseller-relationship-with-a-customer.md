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
# <a name="remove-a-reseller-relationship-with-a-customer"></a>Odebrání vztahu prodejce se zákazníkem

**Platí pro**

- Partnerské centrum

Odeberte vztah prodejce se zákazníkem, se kterým již nebudete mít transakce.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Před odebráním vztahu prodejce se musí zrušit všechny objednávky rezervovaných instancí virtuálních počítačů Azure. Zavolejte podporu Azure pro zrušení všech otevřených objednávek rezervované instance virtuálního počítače Azure.

## <a name="c"></a>C\#

Chcete-li odebrat vztah prodejce pro zákazníka, nejprve zajistěte, aby všechny aktivní Azure Reserved VM Instances pro tohoto zákazníka byly zrušeny. Dále zajistěte, aby všechny aktivní odběry pro tohoto zákazníka byly pozastaveny. Provedete to tak, že určíte ID zákazníka, pro kterého chcete odstranit vztah prodejce. V následujícím příkladu kódu se uživateli zobrazí výzva k zadání identifikátoru zákazníka.

Chcete-li určit, zda je nutné zrušit některý Azure Reserved VM Instances pro zákazníka, načtěte kolekci nároků voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) pomocí identifikátoru zákazníka a určete zákazníka a vlastnost [**oprávnění**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) k načtení rozhraní pro operace shromažďování nároků. Pro načtení kolekce nároků zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) . Vyfiltrujte kolekci pro všechna oprávnění s hodnotou [**EntitlementType**](entitlement-resources.md#entitlementtype) [**EntitlementType. VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) , a pokud existují, zrušte je voláním podpory, než budete pokračovat.

Pak načtěte kolekci předplatných zákazníka voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) pomocí identifikátoru zákazníka a zadejte zákazníka a vlastnost [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) pro načtení rozhraní pro operace shromažďování předplatných. Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) načtěte kolekci předplatných zákazníka. Prochází kolekci předplatných a zajistěte, aby žádné odběry neměly [**předplatné.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) hodnota vlastnosti status [**SubscriptionStatus. Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus). Pokud je předplatné pořád aktivní, přečtěte si téma [pozastavení předplatného](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) , kde najdete informace o tom, jak ho pozastavit.

Po potvrzení, že se všechny aktivní Azure Reserved VM Instances pro tohoto zákazníka zruší a že se všechna aktivní předplatná pozastaví, můžete pro zákazníka odebrat vztah prodejce. Nejprve vytvořte nový objekt [Customer/dotnet/API/Microsoft. Store. partnercenter. Models. Customers. Customer. Customer. Customer. Customers. Customer. [](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship) Potom zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) pomocí identifikátoru zákazníka pro určení zákazníka a zavolejte metodu **patch** a předejte ji do nového objektu Customer.

Chcete-li znovu vytvořit relaci, opakujte postup [vyžadování vztahu prodejce/partner-Center/vývoj/vývoj/požadavek-prodejce – vztah).

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

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: PartnerSDK. FeatureSample **Třída**: DeletePartnerCustomerRelationship.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda     | Identifikátor URI žádosti                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **POUŽITA**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro odebrání vztahu prodejce.

| Název                   | Typ     | Vyžadováno | Popis                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **Customer-tenant-ID** | **guid** | Y        | Hodnota je identifikátor **zákazníka (zákazníka** ), který identifikuje zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

V textu žádosti se vyžaduje prostředek **zákazníka** . Ujistěte se, že vlastnost **RelationshipToPartner** byla nastavena na hodnotu None.

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

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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
