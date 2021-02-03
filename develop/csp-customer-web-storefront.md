---
title: Webová výkladní skříň pro zákazníky CSP
description: Tento ukázkový kód webu ukazuje pracovní online obchod pro zákazníky, kteří si můžou koupit předplatné produktů Microsoftu.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd488b9b9bf2c1df4bebc8513d230a02b06b2ce4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766684"
---
# <a name="csp-customer-web-storefront"></a>Webová výkladní skříň pro zákazníky CSP

**Platí pro:**

- Partnerské centrum

> [!NOTE]
> Tato ukázková aplikace se vztahuje jenom na globální instanci partnerského centra. Netýká se partnerského centra pro Microsoft Cloud Německo nebo partnerského centra pro Microsoft Cloud pro státní správu USA.

[Partnerský prezentace](https://github.com/Microsoft/Partner-Center-Storefront) je **ukázkový web** pro online obchod, který můžou zákazníci použít k nákupu předplatných produktů Microsoftu. Tento **vzorový kód** můžete upravit pro vlastní použití, abyste mohli [Konfigurovat nabídky](#configure-offers), [Přidat branding](#configure-branding) a [Přidat způsob platby](#configure-payment-types).

## <a name="sample-code"></a>Ukázka kódu

Stáhněte si [vzorový kód prezentace partnerského centra](https://github.com/Microsoft/Partner-Center-Storefront) z GitHubu.

## <a name="configure-authentication"></a>Konfigurace ověřování

Než sestavíte aplikaci, aktualizujte následující hodnoty v souboru Web.config tak, aby odrážely ověřovací informace Azure AD, které jste vytvořili v [partnerském centru](partner-center-authentication.md). Měli byste použít nastavení účtu izolovaného prostoru pro integraci při prvotním vývoji nebo pro testování v produkčním prostředí (TiP).

- **partnerCenter. applicationId**
- **partnerCenter.applicationSecret**
- **partnerCenter. Domain**
- **webportes. clientId**
- **webportes. clientSecret**
- **webportes. Domain**
- **webportes. azureStorageConnectionString**

## <a name="configure-offers"></a>Konfigurovat nabídky

V **OfferCatalogViewModel** můžete nakonfigurovat sadu nabídek (**MicrosoftOffer**).

## <a name="configure-branding"></a>Konfigurace brandingu

Tento ukázkový web sleduje v *BrandingConfiguration.cs* a *PortalBranding.cs* následující informace o společnosti a značce:

- Název organizace
- Logo organizace
- Obrázek záhlaví
- Smlouva o ochraně osobních údajů
- Kontaktní e-mail
- Kontaktní telefonní číslo
- E-mail podpory
- Telefonní číslo podpory

### <a name="configure-payment-types"></a>Konfigurace typů plateb

Aplikace aktuálně používá bránu PayPal implementovanou v *PayPalGateway.cs*.