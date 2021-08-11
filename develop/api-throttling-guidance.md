---
title: Pokyny k omezování rozhraní API
description: V případě partnerů, kteří Partnerské centrum rozhraní API, zjistěte, která rozhraní API ovlivňuje omezování rozhraní API Microsoftu, a osvědčené postupy, jak se vyhnout omezování nebo je lépe zvládat.
ms.date: 04/14/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: 4eead16c5bb2b01f0fba85e30ea35fbcdae9d5a6682872eecfeeb9e47f43d324
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993754"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a>Pokyny k omezování rozhraní API pro partnery, kteří Partnerské centrum rozhraní API 

Microsoft provádí implementaci omezování rozhraní API, aby partnerům volajícím rozhraní API Partnerské centrum konzistentnější výkon. Omezování omezuje počet požadavků na službu v časovém intervalu, aby se zabránilo přílišnému využívání prostředků. Přestože Partnerské centrum je navržená tak, aby zvládla velké množství požadavků, pokud dochází k obrovskému počtu požadavků několika partnerů, omezování pomáhá udržovat optimální výkon a spolehlivost pro všechny partnery.  

Limity omezování se liší v závislosti na scénáři. Pokud například provádíte velký objem zápisů, je možnost omezování vyšší než v případě, že provádíte pouze čtení.

## <a name="what-happens-when-throttling-occurs"></a>Co se stane, když dojde k omezování? 

Při překročení prahové hodnoty omezování Partnerské centrum všechny další požadavky od tohoto klienta na určitou dobu. Chování při omezování závisí na typu a počtu požadavků.   

### <a name="common-throttling-scenarios"></a>Běžné scénáře omezování 

Mezi nejběžnější příčiny omezování klientů patří: 

- Velký počet požadavků na rozhraní API na **ID partnerského tenanta:** U některých rozhraní API Partnerské centrum se omezování určuje podle ID tenanta partnera. Příliš mnoho volání těchto rozhraní API se stejným ID partnerského tenanta bude mít za následek překročení prahové hodnoty omezení.  

- Velký počet požadavků na rozhraní API na ID tenanta partnera na **ID tenanta** zákazníka: Pro jiná rozhraní API se omezování určuje podle kombinace ID tenanta partnera a ID tenanta zákazníka. V těchto případech bude příliš mnoho volání se stejným ID tenanta zákazníka mít za následek omezování , zatímco volání vůči jiným zákazníkům mohou být úspěšná.

## <a name="best-practices-to-avoid-throttling"></a>Osvědčené postupy pro zabránění omezování 
 
Programovací postupy, jako je průběžné dotazování prostředku, aby kontroloval aktualizace a pravidelně kontroloval kolekce prostředků a kontroloval nové nebo odstraněné prostředky, s větší pravděpodobností vedou k omezování a zhoršují celkový výkon. Souběžná volání rozhraní API mohou vést k vysokému počtu požadavků za jednotku času, což také způsobí omezování požadavků. Místo toho byste měli používat sledování změn a oznámení o změně. Kromě toho byste měli být schopni používat protokoly aktivit ke zjišťování změn. Další informace najdete v tématu [Partnerské centrum aktivit.](get-a-record-of-partner-center-activity-by-user.md)  Důrazně doporučujeme partnerům zvážit použití rozhraní API protokolu aktivit, abyste se vyhnuli omezování. Podívejte se také na příklad použití protokolů aktivit níže.

## <a name="best-practices-to-handle-throttling"></a>Osvědčené postupy pro zpracování omezování

Tady jsou osvědčené postupy pro zpracování omezování: 

- Snižte stupeň paralelismu. 
- Snižte frekvenci volání. 
- Vyhněte se okamžitému opakování, protože všechny požadavky narůstá do limitů využití. 

Při implementaci zpracování chyb k detekci omezování využijte kód chyby HTTP 429. Neúspěšná odpověď zahrnuje hlavičku Retry-After odpovědi. Obnovení požadavků pomocí zpoždění Opakování po je nejrychlejší způsob, jak se zotavit z omezování. 

Pokud chcete použít zpoždění Opakování po, proveďte následující: 

1. Počkejte počet sekund zadaný v záhlaví Retry-After souboru. 

2. Zkuste požadavek zopakovat.  

3. Pokud požadavek znovu selže s kódem chyby 429, stále dochází k omezování. Zkuste to znovu s exponenciálním zpomalováním, použijte doporučené Retry-After prodlevu a zkuste požadavek zopakovat, dokud nebude úspěšný.

4. Pokud používáte sadu SDK, při omezování požadavku se zobrazí výjimka se stavový kódem 429. Ve výjimce použijte vlastnost RetryAfter a po uplynutí doby zkuste požadavek zopakovat.


## <a name="apis-currently-impacted-by-throttling"></a>Omezení aktuálně ovlivňuje rozhraní API

Na konci bude omezení každého rozhraní API Partnerské centrum, které api.partnercenter.microsoft.com/ koncového bodu. V současné době se limity omezení vynucují pouze u níže uvedených rozhraní API. Partnerské centrum bude shromažďovat telemetrii jednotlivých rozhraní API a dynamicky upravovat limity omezování. Následující tabulka uvádí rozhraní API, u kterých se v současné době vynucuje omezování.  


|**Operace**| **Dokumentace k Partnerskému centru**|
|------------------------|----------------------------|
|{baseURL}/v1/customers/{customer_id}/orders|[vytvoření objednávky](create-an-order.md)|
|{baseURL}/v1/customers/{ID_tenanta_zákazníka}/subscriptions/{id-pro-předplatné}/upgrady|[převod předplatného](transition-a-subscription.md)|
|{baseURL}/v1/customers/{ID_tenanta_zákazníka}/orders/{ID_objednávky}|[nákup doplňku k předplatnému](purchase-an-add-on-to-a-subscription.md)|
|{baseURL}/v1/customers/{ID_zákazníka}/carts/{ID_košíku}|[vytvoření košíku](create-a-cart.md)|
|{baseURL}/v1/customers/{ID_zákazníka}/carts/{ID_košíku}/pokladna|[pokladna košíku](checkout-a-cart.md)|
|{baseURL}/v1/customers/{ID_zákazníka}/carts/{ID_košíku}|[aktualizace košíku](update-a-cart.md)|
|{baseURL}/v1/customers/{ID_zákazníka}/předplatná/{ID_předplatného}/registrace|[registrace předplatného](register-a-subscription.md)|
|{baseURL}/v1/productupgrades|[vytvoření entity upgradu produktu](create-product-upgrade-entity.md)|
|{baseURL}/v1/customers/{ID_zákazníka}/předplatná/{ID_předplatného}/převody |[Převod zkušebního předplatného na placené](convert-a-trial-subscription-to-paid.md)|
|{baseURL}/v1/customers/{ID_tenanta_zákazníka}|[získání zákazníka podle ID](get-a-customer-by-id.md)|
|{baseURL}/v1/productUpgrades/eligibility|[získání způsobilosti pro upgrade produktu](get-eligibility-for-product-upgrade.md)|
|{baseURL}/v1/customers/{ID_tenanta_zákazníka}/subscriptions/{id-pro-předplatné} |[správa předplatného](manage-orders.md#manage-a-subscription)|
|{baseURL}/v1/customers/{customer_id}/subscriptions |[získání všech předplatných zákazníka](get-all-of-a-customer-s-subscriptions.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}|[Získání předplatného podle ID](get-a-subscription-by-id.md)|
|{baseURL}/v1/customers/{customer_id}/orders|[Získání všech objednávek zákazníků](get-all-of-a-customer-s-orders.md)|
|{baseURL}/v1/customers/{customer_id}/orders/{order_id}|[Získání objednávky podle ID](get-an-order-by-id.md)|
|{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus|[Získání stavu zřizování předplatných](get-subscription-provisioning-status.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}|[Správa objednávek a správa předplatného](manage-orders.md#manage-a-subscription)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons|[Získání seznamu doplňků pro předplatné](get-a-list-of-add-ons-for-a-subscription.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntiments|[Získání seznamu oprávnění Azure pro předplatné](get-a-list-of-azure-entitlements-for-subscription.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus|[Získání stavu registrace předplatných](get-subscription-registration-status.md)|
|{baseURL}/v1/customers/{ID_tenanta_zákazníka}/transfers|[Získání všech převodů zákazníka](get-all-of-a-customer-s-transfers.md)|
|{baseURL}/v1/productUpgrades/{id_upgradu}/status|[Získání stavu upgradu produktů](get-product-upgrade-status.md)|
|{baseURL}/v1/customers/{ID_zákazníka}/předplatná/{ID_předplatného}/převody|[Získání seznamu nabídek převod zkušebních verzí](get-a-list-of-trial-conversion-offers.md)|


### <a name="error-code-response"></a>Odpověď s kódem chyby:
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a>Příklad protokolu aktivit

Pro osvědčené postupy při analýze denních změn doporučujeme dotazovat se na záznam auditu pro konkrétní den. 

V odpovědi získáte výsledek se změnami konkrétního typu operace.Můžete filtrovat podle operace, o kterou vám jde. Pokud vás například zajímá nově vytvořený zákazník, můžete se podívat na operationType = "add_customer".  

Seznam typů operací a prostředků najdete v následujících dokumentacích k rozhraní API.  

- [Auditování prostředků](auditing-resources.md)  

- [Získání záznamu aktivity partnerského centra podle uživatele](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a>Příklad odpovědi

**Požadavek**:  
```http
Http Get call:  https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50 

Authorization: Bearer <token> 

Accept: application/json 

MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893 

MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14 

X-Locale: en-US 

Host: api.partnercenter.microsoft.com 

Connection: Keep-Alive 
```

**Odpověď**:    
```http
{ 

    "totalCount": 17, 

    "items": [ 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_e905b566-4779-4e57-944c-7b1b5312705b_updatecustomeruserlicenses_637346859797753934", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "e905b566-4779-4e57-944c-7b1b5312705b", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "FulfillmentService", 

            "resourceType": "license", 

            "operationType": "update_customer_user_licenses", 

            "operationDate": "2020-09-02T23:26:19.7753934Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "CustomerUserId", 

                    "value": "933808c7-b165-496c-a24e-1a4b7846fab4" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_ia80zlkxp6ewoqpp35pbqjlhqv9iigvz1_createorder_637346662909268372", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "order", 

            "resourceNewValue": "{\"Id\":\"Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"AlternateId\":\"64144d300bde\",\"ReferenceCustomerId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"BillingCycle\":\"monthly\",\"CurrencyCode\":\"USD\",\"CurrencySymbol\":\"$\",\"LineItems\":[{\"LineItemNumber\":0,\"ProvisioningContext\":null,\"OfferId\":\"DZH318Z0C964:0001:DZH318Z0BZDG\",\"SubscriptionId\":\"f428d44a-d08b-348b-579e-ce92a6362c7b\",\"ParentSubscriptionId\":null,\"TermDuration\":\"P1M\",\"TransactionType\":\"New\",\"FriendlyName\":\"SaaS custom meter offer - Bronze\",\"Quantity\":1,\"Pricing\":null,\"PartnerIdOnRecord\":null,\"RenewsTo\":null,\"Links\":{\"Product\":{\"Uri\":\"/products/DZH318Z0C964?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Sku\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Availability\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001/availabilities/DZH318Z0BZDG?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ActivationLinks\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/lineitems/0/activationlinks\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}}}],\"CreationDate\":\"2020-09-02T17:58:01.7755853Z\",\"Status\":\"pending\",\"TransactionType\":\"UserPurchase\",\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ProvisioningStatus\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/provisioningstatus\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"PatchOperation\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"PATCH\",\"Body\":null,\"Headers\":[]}},\"Client\":{\"marketplaceCountry\":\"US\",\"deviceFamily\":\"UniversalStore-PartnerCenter\",\"name\":\"Partner Center Web\"},\"Attributes\":{\"ObjectType\":\"Order\"}}", 

            "operationType": "create_order", 

            "originalCorrelationId": "96514ebe-c1b2-4865-cb46-2c2d20a2e911", 

            "operationDate": "2020-09-02T17:58:10.9268372Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "OrderId", 

                    "value": "Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1" 

                }, 

                { 

                    "key": "AlternateId", 

                    "value": "64144d300bde" 

                }, 

                { 

                    "key": "BillingCycle", 

                    "value": "Monthly" 

                }, 

                { 

                    "key": "OfferId-0", 

                    "value": "DZH318Z0C964:0001:DZH318Z0BZDG" 

                }, 

                { 

                    "key": "SubscriptionId-0", 

                    "value": "f428d44a-d08b-348b-579e-ce92a6362c7b" 

                }, 

                { 

                    "key": "SubscriptionName-0", 

                    "value": "SaaS custom meter offer - Bronze" 

                }, 

                { 

                   "key": "Quantity-0", 

                    "value": "1" 

                }, 

                { 

                    "key": "PartnerOnRecord-0", 

                    "value": null 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                           { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_86bddccf-9a53-40c6-907c-08067a3f8da7_addcustomer_637346648528069005", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "customer", 

            "resourceNewValue": "{\"Id\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"CommerceId\":\"9dd78b4f-f98a-44b4-a2fa-2b82ac58d24c\",\"CompanyProfile\":{\"TenantId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"Domain\":\"CustomMetersStagingTest.onmicrosoft.com\",\"CompanyName\":\"CustomMetersStagingTest\",\"Address\":null,\"Email\":null,\"OrganizationRegistrationNumber\":null,\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/profiles/company\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}},\"Attributes\":{\"ObjectType\":\"CustomerCompanyProfile\"}},\"BillingProfile\":{\"Id\":\"4beafd7b-cdab-5bdc-52ed-02e16edf2e7a\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"Email\":\"CustomMetersStagingTest@CustomMetersStagingTest.com\",\"Culture\":\"en-US\",\"Language\":\"en\",\"CompanyName\":\"CustomMetersStagingTest\",\"DefaultAddress\":{\"Id\":null,\"Country\":\"US\",\"Region\":null,\"City\":\"Seattle\",\"State\":\"WA\",\"District\":null,\"AddressLine1\":\"CustomMetersStagingTest\",\"AddressLine2\":null,\"AddressLine3\":null,\"PostalCode\":\"98122\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"EmailAddress\":null,\"PhoneNumber\":null,\"MiddleName\":null},\"Attributes\":{\"Etag\":\"-2279334701316321663\",\"ObjectType\":\"CustomerBillingProfile\"}},\"RelationshipToPartner\":\"reseller\",\"AllowDelegatedAccess\":true,\"UserCredentials\":{\"userName\":\"admin\",\"password\":\"\"},\"AssociatedPartnerId\":null,\"CustomDomains\":null,\"Attributes\":{\"ObjectType\":\"Customer\"}}", 

            "operationType": "add_customer", 

            "originalCorrelationId": "7550d9ea-e64a-416f-e49b-3670c516cf69", 

            "operationDate": "2020-09-02T17:34:12.8069005Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "PrimaryDomainName", 

                    "value": "CustomMetersStagingTest.onmicrosoft.com" 

                }, 

                { 

                    "key": "Relationship", 

                    "value": "Reseller" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                            

        ... 

    ], 

    "links": { 

        "self": { 

            "uri": "/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50", 

            "method": "GET", 

            "headers": [] 

        } 

    }, 

    "attributes": { 

        "objectType": "Collection" 

    } 

} 
```
 

