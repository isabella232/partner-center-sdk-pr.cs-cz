---
title: Webová výkladní skříň pro zákazníky CSP
description: Tento ukázkový kód webu ukazuje pracovní online obchod pro zákazníky, kteří si můžou koupit předplatné produktů Microsoftu.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 07020c365db2ad578e7ff75602519d06eabb2a3bebf0913899fcd8b5345a0365
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995199"
---
# <a name="csp-customer-web-storefront"></a>Webová výkladní skříň pro zákazníky CSP

**Platí pro**: partnerské Centrum

Nevztahuje **se na**: Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Tato ukázková aplikace se vztahuje jenom na globální instanci partnerského centra.

[Partnerský prezentace](https://github.com/Microsoft/Partner-Center-Storefront) je **ukázkový web** pro online obchod, který můžou zákazníci použít k nákupu předplatných produktů Microsoftu. Tento **vzorový kód** můžete upravit pro vlastní použití, abyste mohli [Konfigurovat nabídky](#configure-offers), [Přidat branding](#configure-branding)a [Přidat způsob platby](#configure-payment-types).

## <a name="sample-code"></a>Ukázka kódu

Stáhněte si [vzorový kód prezentace partnerského centra](https://github.com/Microsoft/Partner-Center-Storefront) z GitHub.

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

Tento ukázkový web sleduje následující informace společnosti a značky v *BrandingConfiguration. cs* a *PortalBranding. cs*:

- Název organizace
- Logo organizace
- Obrázek záhlaví
- Smlouva o ochraně osobních údajů
- Kontaktní e-mail
- Kontaktní telefonní číslo
- E-mail podpory
- Telefonní číslo podpory

### <a name="configure-payment-types"></a>Konfigurace typů plateb

aplikace aktuálně používá PayPal bránu, která je implementovaná v *PayPalGateway. cs*.