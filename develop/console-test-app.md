---
title: Aplikace pro testování konzoly
description: Tato testovací aplikace konzoly poskytuje vzorový kód pro všechny scénáře podporované rozhraními API partnerského centra. Můžete ho také použít k testování.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e82bac3ccc22d0e7cf898e5b2d2e002c622584ae
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766811"
---
# <a name="console-test-app"></a>Aplikace pro testování konzoly

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Testovací aplikace konzoly je k dispozici v jazycích C# a Java a poskytuje ukázkové kódy pro všechny scénáře podporované rozhraními API partnerského centra. Můžete ho také použít k testování.

## <a name="get-the-code"></a>Získání kódu

Stáhněte si vzorový kód pro testovací aplikaci konzoly.

## <a name="net"></a>.NET

[Stáhněte si vzorový kód](https://go.microsoft.com/fwlink/p/?LinkId=746682) a podle potřeby ho upravte.

> [!IMPORTANT]
> Než sestavíte aplikaci, aktualizujte hodnoty v souboru *App.config* tak, aby odrážely ověřovací informace Azure AD, které jste vytvořili v [partnerském centru](partner-center-authentication.md). Konkrétně byste měli použít nastavení účtu izolovaného prostoru pro integraci při prvotním vývoji nebo pro testování v produkčním prostředí.

V části **ScenarioSettings** v souboru *App.config* můžete nastavit parametry, které budou automaticky předány do scénářů, které spustíte.

Chcete-li upravit seznam scénářů, které jsou spuštěny, odkomentujte řádky v **IPartnerScenario \[ \] mainScenarios** nebo v jednotlivých metodách **Get scénářů** nalezených v souboru *program.cs* .

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[Stáhněte si vzorový kód](https://go.microsoft.com/fwlink/p/?LinkId=2026887) a podle potřeby ho upravte.

> [!IMPORTANT]
> Než sestavíte aplikaci, aktualizujte hodnoty v *SamplesConfigurations.jsv* souboru tak, aby odrážely ověřovací informace Azure AD, které jste vytvořili v [partnerském centru](partner-center-authentication.md). Konkrétně byste měli použít nastavení účtu izolovaného prostoru pro integraci při prvotním vývoji nebo pro testování v produkčním prostředí.

V části **ScenarioSettings** *SamplesConfiguration.js* v souboru můžete nastavit parametry, které budou automaticky předány do scénářů, které spustíte.

Chcete-li upravit seznam scénářů, které jsou spuštěny, odkomentujte řádky v **IPartnerScenario \[ \] mainScenarios** nebo v jednotlivých metodách **Get scénářů** , které se nacházejí v souboru *program. Java* .

## <a name="what-to-change"></a>Co se má změnit

Pomocí následujících seznamů určete, co se v ukázkovém kódu mění nebo nemění.

### <a name="partnerservicesettings"></a>PartnerServiceSettings

Pro **PartnerServiceSettings** se neměňte:

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

Všechna tato nastavení jsou nutná pro správné fungování ukázkových volání rozhraní API.

### <a name="userauthentication"></a>UserAuthentication

V případě **UserAuthentication** je potřeba změnit:

- **ApplicationId** (vaše Azure Active Directory ID aplikace používané pro přihlášení)
- **Username** (uživatelské jméno ve službě Active Directory)
- **Heslo** (heslo služby Active Directory).

Neměnit:

- **ResourceUrl**
- **RedirectUrl**

### <a name="appauthentication"></a>AppAuthentication

V případě **AppAuthentication** je potřeba změnit:

- **ApplicationId** (vaše ID aplikace služby Active Directory používané pro přihlášení k aplikaci)
- **ApplicationSecret** (váš tajný klíč aplikace služby Active Directory použitý pro přihlášení k aplikaci)
- **Doména** (doména služby Active Directory, na které je aplikace hostovaná)

### <a name="scenariosettings"></a>ScenarioSettings

Pro **ScenarioSettings** se neměňte:

- **CustomerDomainSuffix** (přípona domény použitá při vytváření nového zákazníka)

Volitelná nastavení. Pokud necháte pole prázdné, bude nutné tyto informace při spuštění scénáře, kde je to potřeba, zacházet:

- **CustomerIdToDelete** (ID zákazníka používaného k odstranění)
- **DefaultCustomerId** (ID zákazníka pro použití ve scénářích souvisejících se zákazníky)
- **DefaultInvoiceID** (ID faktury pro použití ve scénářích faktury)
- **PartnerMpnId** (ID MPN partnera pro použití v nepřímých partnerských scénářích)
- **DefaultServiceRequestId** (ID žádosti o službu, která se má použít ve scénářích žádosti o služby)
- **DefaultSupportTopicID** (ID tématu podpory, které se použije ve scénářích žádosti o služby)
- **DefaultOfferID** (ID nabídky, která se má použít v nabídkových scénářích)
- **DefaultOrderID** (ID objednávky, které se má použít ve scénářích pořadí)
- **DefaultSubscriptionID** (ID předplatného, které se má použít ve scénářích předplatného)

Volitelné pro změnu. Všechna tato nastavení určují počet položek na stránku při načítání stránkovaného obsahu:

- **CustomerPageSize**
- **InvoicePageSize**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**
