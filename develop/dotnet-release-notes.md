---
title: Zpráva k vydání verze pro partnerský Center .NET SDK
description: Poznámky k verzi pro nejnovější verzi sady SDK partnerského centra .NET.
ms.date: 09/18/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6be8f62e0c202a00b194f5af1dc8904006f8d637
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/08/2020
ms.locfileid: "97767155"
---
# <a name="net-sdk-release-notes"></a>Poznámky k verzi sady .NET SDK

Následující poznámky k verzi jsou k dispozici pro nové verze [sady Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter). [Ukázky sady .NET SDK](https://github.com/Microsoft/Partner-Center-DotNet-Samples) najdete na GitHubu. Reference k rozhraní [.NET API partnerského centra](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) najdete v prohlížeči rozhraní .NET API.

## <a name="version-1163"></a>1.16.3 verze

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v 1.16.3 je teď obecně dostupný. K dispozici jsou také aktualizované [ukázky GitHubu](https://github.com/Microsoft/Partner-Center-DotNet-Samples) . V této verzi jsou zahrnuté tyto změny:

* SelfServePolicies – přidala se nová funkce.
  * [GetSelfServePolicies](get-a-self-serve-policy-by-id.md)
  * [GetListOfSelfServicePolicies](get-a-list-of-self-serve-policies.md)
  * [CreateSelfServePolicies](create-a-self-serve-policy.md)
  * [UpdateSelfServePolicies](update-a-self-serve-policy.md)
  * [DeleteSelfServePolicies](delete-a-self-serve-policy.md)

* Profil společnosti pro zákazníky
  * Přidání [OrganizationRegistrationNumber](create-a-customer.md)

* CustomerBillingProfile.DefaultAddress
  * Přidání MiddleName

## <a name="version-1162"></a>1.16.2 verze

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v 1.16.2 je teď obecně dostupný. K dispozici jsou také aktualizované [ukázky GitHubu](https://github.com/Microsoft/Partner-Center-DotNet-Samples) . V této verzi jsou zahrnuté tyto změny:

* Aktualizuje podporované typy operací pro záznam auditu. Nově přidaná jsou:
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship
  * DeleteTipCustomer
  * CreateRelatedReferral
  * UpdateRelatedReferral

* Vytváření žádosti o služby je teď zastaralé.
* Témata podpory jsou nyní zastaralá.


## <a name="version-1161"></a>1.16.1 verze

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v 1.16.1 je teď obecně dostupný. K dispozici jsou také aktualizované [ukázky GitHubu](https://github.com/Microsoft/Partner-Center-DotNet-Samples) . V této verzi jsou zahrnuté tyto změny:

Migrovali jsme stávající sadu SDK partnerského centra Microsoft z .NET Framework na platformu .NET Standard 2,0. Sada SDK bude kompatibilní se stávajícími aplikacemi, a to pomocí .NET Framework 4.6.1 a vyšších. Sada SDK bude podporovat .NET Core 2,0 a vyšší. Před převedením na existující aplikace ověřte [podporu implementace rozhraní .NET](/dotnet/standard/net-standard) .   


## <a name="version-1153"></a>1.15.3 verze
[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v 1.15.3 je teď obecně dostupný. K dispozici jsou také aktualizované rozhraní REST API a [ukázky GitHubu](https://github.com/Microsoft/Partner-Center-DotNet-Samples) . V této verzi jsou zahrnuté tyto změny:

* Partnerská smlouva
  * Přidali jsme možnost nepřímých zprostředkovatelů [ověřit stav smluv o nepřímých prodejích u partnerů Microsoftu](verify-indirect-reseller-mpa-status.md).
* Produkty
  * Následující dvě rozhraní byly nesprávně umístěny do oboru názvů Microsoft. Store. PartnerCenter. Products. Teď se nacházejí v oboru názvů Microsoft. Store. PartnerCenter. Customers. Products.
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
