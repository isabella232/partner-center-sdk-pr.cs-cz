---
title: Aplikace pro testování konzoly
description: Tato konzolová testovací aplikace poskytuje vzorový kód pro všechny scénáře podporované Partnerské centrum API. Můžete ho také použít pro testování.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 53a014608303e432be251de0845857547170a5464a1952bb4fde9ff7beb8ae95
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991952"
---
# <a name="console-test-app"></a>Aplikace pro testování konzoly

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Konzolová testovací aplikace je k dispozici v jazyce C# a Java, poskytuje ukázkové kódy pro všechny scénáře podporované rozhraními API Partnerské centrum rozhraní API. Můžete ho také použít pro testování.

## <a name="get-the-code"></a>Získání kódu

Stáhněte si vzorový kód pro konzolovou testovací aplikaci.

## <a name="net"></a>.NET

[Stáhněte si vzorový kód](https://go.microsoft.com/fwlink/p/?LinkId=746682) a podle potřeby ho upravte.

> [!IMPORTANT]
> Před sestavením aplikace aktualizujte hodnoty v souboru *App.config* tak, aby odrážely ověřovací informace Azure AD, které jste vytvořili [v Partnerské centrum ověřování.](partner-center-authentication.md) Konkrétně byste měli použít nastavení účtu sandboxu pro integraci během raného vývoje nebo pro testování v produkčním prostředí.

V **části ScenarioSettings** v *App.config* souboru můžete nastavit parametry, které se automaticky předá do scénářů, které spustíte.

Pokud chcete upravit seznam spuštěných scénářů, zakomentujte řádky v hlavních scénářích **IPartnerScenario \[ \]** nebo v jednotlivých metodách **Get Scenarios,** které najdete v *souboru Program.cs.*

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[Stáhněte si vzorový kód](https://go.microsoft.com/fwlink/p/?LinkId=2026887) a podle potřeby ho upravte.

> [!IMPORTANT]
> Před sestavením aplikace aktualizujte hodnoty v souboru *SamplesConfigurations.json* tak, aby odrážely ověřovací informace Azure AD, které jste vytvořili v [Partnerské centrum ověřování.](partner-center-authentication.md) Konkrétně byste měli použít nastavení účtu sandboxu pro integraci během raného vývoje nebo pro testování v produkčním prostředí.

V **části ScenarioSettings** v *SamplesConfiguration.jssouboru* můžete nastavit parametry, které budou automaticky předány do scénářů, které spustíte.

Pokud chcete upravit seznam spuštěných scénářů, zakomentujte řádky v hlavních scénářích **IPartnerScenario \[ \]** nebo v jednotlivých metodách **Get Scenarios,** které najdete v souboru *Program.java.*

## <a name="what-to-change"></a>Co změnit

Pomocí následujících seznamů určete, co změnit nebo ne změnit ve vzorových kódech.

### <a name="partnerservicesettings"></a>PartnerServiceSettings

V **části PartnerServiceSettings** neměňte:

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

Všechna tato nastavení jsou nezbytná pro správné fungování volání ukázkového rozhraní API.

### <a name="userauthentication"></a>Ověření uživatele

Pro **UserAuthentication** musíte změnit:

- **ApplicationId** (ID Azure Active Directory vaší aplikace použité pro přihlášení)
- **Uživatelské jméno** (vaše uživatelské jméno služby Active Directory)
- **Heslo** (heslo služby Active Directory).

Neměňte:

- **ResourceUrl**
- **Redirecturl**

### <a name="appauthentication"></a>AppAuthentication

Pro **AppAuthentication** musíte změnit:

- **ApplicationId** (ID aplikace Active Directory použité pro přihlášení k aplikaci)
- **ApplicationSecret** (tajný klíč aplikace Active Directory použitý pro přihlášení k aplikaci)
- **Doména** (doména služby Active Directory, ve které je aplikace hostovaná)

### <a name="scenariosettings"></a>Nastavení scénáře

V **části ScenarioSettings**(Nastavení scénáře) neměňte:

- **CustomerDomainSuffix** (přípona domény použitá při vytváření nového zákazníka)

Volitelná nastavení. Pokud je toto pole prázdné, bude potřeba tyto informace zadat při spuštění scénáře, kde je to potřeba):

- **CustomerIdToDelete** (ID zákazníka použitého k odstranění)
- **DefaultCustomerId** (ID zákazníka, které se má použít ve scénářích souvisejících se zákazníkem)
- **DefaultInvoiceID** (ID faktury, které se má použít ve scénářích faktur)
- **PartnerMpnId** (ID MPN partnera pro použití v nepřímých partnerských scénářích)
- **DefaultServiceRequestId** (ID žádosti o služby, které se má použít ve scénářích žádostí o služby)
- **DefaultSupportTopicID** (ID tématu podpory, které se má použít ve scénářích žádostí o služby)
- **DefaultOfferID** (ID nabídky, které se má použít ve scénářích nabídek)
- **DefaultOrderID** (ID objednávky, které se má použít ve scénářích objednávek)
- **DefaultSubscriptionID** (ID předplatného, které se má použít ve scénářích předplatného)

Volitelné ke změně. Všechna tato nastavení určují množství položek na stránku při načítání stránkovaných obsahu:

- **CustomerPageSize**
- **InvoicePageSize**
- **Velikost stránky ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**
