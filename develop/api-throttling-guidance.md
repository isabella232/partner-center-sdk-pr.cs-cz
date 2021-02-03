---
title: Pokyny k omezování rozhraní API
description: Pro partnery, kteří volají rozhraní API partnerského centra, se dozvíte, která rozhraní API mají vliv na omezování a osvědčené postupy rozhraní Microsoft API, abyste zabránili omezení nebo lepšímu omezování procesů.
ms.date: 09/09/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: a52751a97e699050075c1aac910cc51e94514f26
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/08/2020
ms.locfileid: "97767154"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a>Pokyny k omezování rozhraní API pro partnery, kteří volají rozhraní API partnerského centra 

**Platí pro**

- Partnerské centrum

Microsoft implementuje omezování rozhraní API, které umožňuje zajistit jednotnější výkon v časovém intervalu pro partnery, kteří volají rozhraní API partnerského centra. Omezování omezuje počet požadavků na službu v časovém intervalu, aby nedocházelo k nadměrnému využití prostředků. I když je partnerské Centrum navrženo tak, aby zpracovával velký počet požadavků, pokud se k zahlcení počtu požadavků vychází z několika partnerů, omezování pomáhá udržet optimální výkon a spolehlivost pro všechny partnery.  

Omezení omezování se liší v závislosti na scénáři. Pokud například provádíte velký objem zápisů, je možnost omezování větší než v případě, že provádíte pouze čtení.

## <a name="what-happens-when-throttling-occurs"></a>Co se stane, když dojde k omezování? 

Po překročení prahové hodnoty omezuje Partnerská centra všechny další požadavky od tohoto klienta po určitou dobu. Chování omezování závisí na typu a počtu požadavků.   

### <a name="common-throttling-scenarios"></a>Běžné scénáře omezování 

Mezi nejběžnější příčiny omezení klientů patří: 

- **Velký počet žádostí o rozhraní API na ID tenanta partnera**: u některých rozhraní API partnerského centra se omezování určuje podle ID partnerského tenanta. příliš mnoho volání těchto rozhraní API na stejném ID partnerského tenanta bude mít za následek překročení prahové hodnoty omezování.  

- **Velký počet požadavků pro rozhraní API na ID tenanta partnera na ID tenanta zákazníka**: u jiných rozhraní API se omezování určuje podle ID partnerského tenanta/kombinace ID tenanta zákazníka; v těchto případech dojde k tomu, že provedení příliš velkého počtu volání proti stejnému ID tenanta zákazníka bude mít za následek omezení, zatímco volání jiných zákazníků budou úspěšná.

## <a name="best-practices-to-avoid-throttling"></a>Osvědčené postupy pro zamezení omezování 
 
Postupy programování, jako je průběžné cyklické dotazování prostředku pro kontrolu aktualizací a pravidelné prohledávání kolekcí prostředků pro kontrolu nových nebo odstraněných prostředků, mají větší vliv na omezování a sníží celkový výkon. Souběžná volání rozhraní API mohou vést k vysokému počtu požadavků za jednotku času, což způsobí také omezení požadavků. Místo toho byste měli využít sledování změn a oznámení změn. Kromě toho byste měli být schopni využít protokoly aktivit k detekci změn. Další informace najdete v [protokolech aktivit partnerského centra](get-a-record-of-partner-center-activity-by-user.md) .  Důrazně doporučujeme, aby partneři zvážili použití rozhraní API protokolu aktivit pro zajištění vyšší efektivity a zabránili omezování. Viz také příklad použití protokolů aktivit níže.

## <a name="best-practices-to-handle-throttling"></a>Osvědčené postupy pro zpracování omezování

Níže jsou uvedené osvědčené postupy pro omezení zpracování: 

- Snižte stupeň paralelismu. 
- Snižte frekvenci volání. 
- Vyhněte se okamžitým opakovaným pokusům, protože všechny požadavky se budou nacházet oproti omezením využití. 

Při implementaci zpracování chyb k detekci omezování využijte kód chyby HTTP 429. Neúspěšná odpověď zahrnuje hlavičku Retry-After odpovědi. Zálohování požadavků pomocí opakovaného zpoždění je nejrychlejší způsob, jak obnovit omezení. 

Pokud chcete použít prodlevu po opakování, udělejte toto: 

1. Počkejte, než bude stanovený počet sekund v hlavičce Retry-After. 

2. Opakujte požadavek.  

3. Pokud se žádost znovu nepovede s kódem chyby 429, pořád se vám omezí. Zkuste to znovu s exponenciálním omezení rychlosti, použijte doporučené zpoždění Retry-After a zkuste požadavek zopakovat, dokud to neproběhne úspěšně.

4. Pokud používáte sadu SDK, obdržíte výjimku se stavovým kódem 429, když se vaše žádost omezuje. Ve výjimce použijte vlastnost RetryAfter a opakujte požadavek po uplynutí této doby.


## <a name="apis-currently-impacted-by-throttling"></a>Rozhraní API, která v současnosti ovlivňují omezování

V dlouhodobém běhu budou všechna samostatná rozhraní API partnerského centra, která volají koncový bod "api.partnercenter.microsoft.com/", omezená. Omezení omezování se v současné době uplatní jenom u několika rozhraní API uvedených níže. Partnerské centrum bude shromažďovat telemetrii na každé z rozhraní API a bude dynamicky upravovat limity omezování. V následující tabulce jsou uvedena rozhraní API, kde je omezování aktuálně vynutilo.  


|**Operace**| **Dokumentace k Partnerskému centru**|       
|------------------------|----------------------------|
|{baseURL}/v1/Customers/{customer_id}/Orders|[vytvoření objednávky](create-an-order.md)|
|{baseURL}/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription}/upgrades|[převod předplatného](transition-a-subscription.md)|
|{baseURL}/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID}|[zakoupení doplňku k předplatnému](purchase-an-add-on-to-a-subscription.md)|
|{baseURL}/v1/Customers/{Customer-ID}/carts/{Cart-ID}|[Vytvoření košíku](create-a-cart.md)|
|{baseURL}/v1/Customers/{Customer-ID}/carts/{Cart-ID}/Checkout|[rezervace košíku](checkout-a-cart.md)|
|{baseURL}/v1/Customers/{Customer-ID}/carts/{Cart-ID}|[aktualizace košíku](update-a-cart.md)|
|{baseURL}/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrations|[registrace předplatného](register-a-subscription.md)|
|{baseURL}/v1/productupgrades|[vytvořit entitu upgradu produktu](create-product-upgrade-entity.md)|
|{baseURL}/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/Conversions |[převod zkušebního předplatného na placené](convert-a-trial-subscription-to-paid.md)|
|{baseURL}/v1/Customers/{Customer-tenant-ID}|[získat zákazníka podle ID](get-a-customer-by-id.md)|
|{baseURL}/v1/productUpgrades/eligibility|[získat nárok na upgrade produktu](get-eligibility-for-product-upgrade.md)|
|{baseURL}/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription} |[Spravovat předplatné](manage-orders.md#manage-a-subscription)|


### <a name="error-code-response"></a>Odpověď kódu chyby:
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a>Příklad protokolu aktivit

Osvědčeným postupem při analýze každodenních změn doporučujeme zadat dotaz na záznam auditu pro určitý den. 

V odpovědi se zobrazí výsledek se změnami konkrétního typu operace.Můžete filtrovat podle toho, o jakou operaci máte starosti. Pokud vás například zajímá nově vytvořeného zákazníka, můžete se podívat na typem operace OperationType = "add_customer".  

Seznam typem operace OperationType/prostředků najdete níže v dokumentaci k rozhraní API.  

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
 

