---
title: Partnerské centrum poznámky k verzi sady .NET SDK
description: Poznámky k nejnovější verzi sady .NET SDK Partnerské centrum.
ms.date: 07/07/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6fc6182638cb2cc5457bdfada37b928c88e1ca786e401f7eb8d5309a0abd9310
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991214"
---
# <a name="net-sdk-release-notes"></a>Poznámky k verzi sady .NET SDK

Následující poznámky k verzi jsou k dispozici pro nové verze [sady Microsoft Partnerské centrum .NET SDK.](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter) Ukázky [.NET SDK najdete na](https://github.com/Microsoft/Partner-Center-DotNet-Samples) GitHub. Referenční informace k [Partnerské centrum .NET API](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) najdete v prohlížeči rozhraní .NET API.

## <a name="version-201"></a>Verze 2.0.1

[Sada Microsoft Partnerské centrum .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v2.0.1 je teď obecně dostupné. K [dispozici GitHub aktualizované](https://github.com/Microsoft/Partner-Center-DotNet-Samples) ukázky. V této verzi jsou zahrnuté následující změny:

> [!NOTE]
> Některé změny zavedené v rámci nových obchodních prostředí (NCE), které jsou aktuálně k dispozici pouze na základě pozvánek partnerům, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview. Partneři, kteří nejsou součástí privátní verze New Commerce Preview, by si neměli všimnout dopadu a měli by být zpětně kompatibilní.

### <a name="common"></a>Společné
* Změna odkazu na knihovnu ověřování – Odkaz se změnil z knihovny Azure Active Directory Authentication Library[(ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)na knihovnu Microsoft Authentication Library[(MSAL).](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)

  Je třeba provést následující změny, aby se zajistilo správné spuštění MSAL ve vaší aplikaci nebo ukázce .NET:

  * Přidání `https://login.microsoftonline.com/common/oauth2/nativeclient` jako RedirectUrl pro mobilní a desktopové aplikace
  * Do **části** UserAuthentication v konfiguračním souboru aplikace přidejte Domain. 

    Doména je id Azure Active Directory domény nebo tenanta, ve které se vytvořila aplikace Azure AD.

* [Kódy chyb](error-codes.md) – Přidání nového kódu chyby 
  * 408: Časový limit požadavku
  * 504: Časový limit brány 

### <a name="manage-billing"></a>Správa vyúčtování

* [Řádkové položky faktury](get-invoiceline-items.md) – nové atributy přidané do následujících rozhraní API:
  * `GET /invoices/{invoice-id}/lineitems?provider={provider}&invoicelineitemtype=billinglineitems`
  * `GET /invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems`

  Nové atributy: 
  * ProductQualifiers
  * subscriptionStartDate
  * subscriptionEndDate
  * ID odkazu
  * creditReasonCode (vztahuje se pouze na NCE)
  * ID povýšení 


* [Daily rated usage Line-items](get-invoice-billed-consumption-lineitems.md) – nové atributy přidané do následujícího rozhraní API: 
  * `GET /invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems`
  
  Nové atributy: 
  * hasPartnerEarnedCredit (platí pouze pro NCE)
  * creditType (vztahuje se pouze na NCE)
  * rateOfCredit (vztahuje se pouze na NCE)


### <a name="manage-orders"></a>Správa objednávek

* [Prostředky předplatného](subscription-resources.md) – Přidaná nová vlastnost. 
  * CancellationAllowedUntilDate – (vztahuje se pouze na NCE)

* Transition Resources (platí jenom pro NCE) – Přidaná nová vlastnost 
  * FromSubscriptionId

### <a name="manage-customer-accounts"></a>Správa zákaznických účtů

* [Ověření adresy –](validate-an-address.md) Odpověď se změnila z logické hodnoty na nový model pro rozhraní API:
  * `POST /validations/address`
  
  Nový model odpovědí: 
  * AddressValidationResponse

* Synchronní rozhraní API kvalifikace zákazníka je zastaralé.  


## <a name="version-1170"></a>Verze 1.17.0

[Sada Microsoft Partnerské centrum .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) verze 1.17.0 je teď obecně dostupné. K [dispozici GitHub aktualizované](https://github.com/Microsoft/Partner-Center-DotNet-Samples) ukázky. V této verzi jsou zahrnuté následující změny:

* Audit byl aktualizován – Přidání nových typů operací pro znalost, kdy zákazník schválil a ukončil DAP
  * [DapAdminRelationshipApproved](auditing-resources.md)
  * [DapAdminRelationshipTerminated](auditing-resources.md)

* Audit byl aktualizován – Přidání nových typů prostředků a operací pro podporu scénáře role adresáře zákazníka
  * Typ prostředku[CustomerDirectoryRole](auditing-resources.md)
  * Typy operací[AddUserMember](auditing-resources.md)a[RemoveUserMember](auditing-resources.md)

* Aktualizace sady SDK pro účet zákazníků – Podpora následujících rozhraní API
  * GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus
  * GET /customers/{id-tenanta zákazníka}/kvalifikace 
  * POST /customers/{customer_id}/qualifications?code={validationCode}

* **Následující změny zavedené v rámci nového obchodování jsou v současné době k dispozici pouze na základě pozvánek pro partnery, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview.** Partneři, kteří nejsou součástí privátní verze New Commerce Preview, by si neměli všimnout dopadu a měli by být zpětně kompatibilní.
  * Catalog Changes (Změny katalogu):
    * GET /products/{id-produktu}/skus/{sku-id}
  * Nákup a správa:
    * GET /customers/{customerId}/subscriptions
    * GET /customers/{customerId}/subscriptions/{subscriptionId}
    * PATCH /customers/{customerId}/subscriptions/{subscriptionId}
    * GET /customers/{customerId}/subscriptions/{subscriptionId}/transitionelibilities
    * GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions
    * POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions


## <a name="version-1163"></a>Verze 1.16.3

[Sada Microsoft Partnerské centrum .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) verze 1.16.3 je teď obecně dostupné. K [dispozici GitHub aktualizované](https://github.com/Microsoft/Partner-Center-DotNet-Samples) ukázky. V této verzi jsou zahrnuté následující změny:

* SelfServePolicies – přidání nových funkcí
  * [GetSelfServePolicies](get-a-self-serve-policy-by-id.md)
  * [GetListOfSelfServicePolicies](get-a-list-of-self-serve-policies.md)
  * [CreateSelfServePolicies](create-a-self-serve-policy.md)
  * [UpdateSelfServePolicies](update-a-self-serve-policy.md)
  * [DeleteSelfServePolicies](delete-a-self-serve-policy.md)

* Profil společnosti zákazníků
  * Přidání [OrganizationRegistrationNumber](create-a-customer.md)

* CustomerBillingProfile.DefaultAddress
  * Přidání middleName

## <a name="version-1162"></a>Verze 1.16.2

[Sada Microsoft Partnerské centrum .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) verze 1.16.2 je teď obecně dostupné. K [dispozici GitHub aktualizované](https://github.com/Microsoft/Partner-Center-DotNet-Samples) ukázky. V této verzi jsou zahrnuté následující změny:

* Aktualizujte podporované typy operací pro záznam auditu. Nově přidané jsou tyto:
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship
  * DeleteTipCustomer
  * CreateRelatedReferral
  * UpdateRelatedReferral

* Vytváření žádostí o služby je teď zastaralé
* Témata podpory jsou teď zastaralá.


## <a name="version-1161"></a>Verze 1.16.1

[Sada Microsoft Partnerské centrum .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) verze 1.16.1 je teď obecně dostupné. K [dispozici GitHub aktualizované](https://github.com/Microsoft/Partner-Center-DotNet-Samples) ukázky. V této verzi jsou zahrnuté následující změny:

Migrovali jsme stávající microsoftovou SDK pro Partnerské centrum z .NET Framework na .NET Standard 2.0. Díky tomu bude sada SDK kompatibilní s existujícími aplikacemi pomocí .NET Framework verze 4.6.1 a vyšší. Sada SDK bude podporovat .NET Core 2.0 a vyšší. Před [přenosem do existujících](/dotnet/standard/net-standard) aplikací zkontrolujte podporu implementace .NET.   


## <a name="version-1153"></a>Verze 1.15.3
[Sada Microsoft Partnerské centrum .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) verze 1.15.3 je teď obecně dostupné. K dispozici jsou také [aktualizovaná GitHub rozhraní](https://github.com/Microsoft/Partner-Center-DotNet-Samples) REST API a další ukázky. V této verzi jsou zahrnuté následující změny:

* Partnerská smlouva
  * Přidání možnosti nepřímých poskytovatelů ověřit [Smlouva s partnerem Microsoftu nepřímých prodejců](verify-indirect-reseller-mpa-status.md)
* Produkty
  * Následující dvě rozhraní byla nesprávně umístěna v oboru názvů Microsoft.Store.PartnerCenter.Products. Teď se nacházejí v oboru názvů Microsoft.Store.PartnerCenter.Customers.Products.
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
