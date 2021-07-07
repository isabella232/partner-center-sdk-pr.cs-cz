---
title: Webová výkladní skříň pro zákazníky CSP
description: Tento ukázkový kód webu ukazuje fungující online obchod pro zákazníky, kteří si kupují předplatná produktů Microsoftu.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d68f17d707731f426cb980a566b6478790d3507c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973328"
---
# <a name="csp-customer-web-storefront"></a>Webová výkladní skříň pro zákazníky CSP

**Platí pro:** Partnerské centrum

**Neplatí pro: Partnerské centrum** Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Tato ukázková aplikace se vztahuje pouze na globální instanci Partnerské centrum.

Webová [Partnerské centrum je ukázkový](https://github.com/Microsoft/Partner-Center-Storefront)  web pro online obchod, který zákazníci mohou použít k nákupu předplatných produktů Microsoftu. Tento vzorový kód **můžete upravit** pro vlastní použití a nakonfigurovat [nabídky,](#configure-offers)přidat [značku](#configure-branding)a přidat [způsob platby](#configure-payment-types).

## <a name="sample-code"></a>Ukázka kódu

Stáhněte [si Partnerské centrum kódu z GitHub.](https://github.com/Microsoft/Partner-Center-Storefront)

## <a name="configure-authentication"></a>Konfigurace ověřování

Před sestavením aplikace aktualizujte následující hodnoty v souboru Web.config tak, aby odrážely ověřovací informace Azure AD, které jste vytvořili [v Partnerské centrum ověřování.](partner-center-authentication.md) Nastavení účtu sandboxu pro integraci byste měli použít během raného vývoje nebo testování v produkčním prostředí (TiP).

- **partnerCenter.applicationId**
- **partnerCenter.applicationSecret**
- **partnerCenter.domain**
- **webPortal.clientId**
- **webPortal.clientSecret**
- **webPortal.domain**
- **webPortal.azureStorageConnectionString**

## <a name="configure-offers"></a>Konfigurace nabídek

Sadu nabídek (**MicrosoftOffer**) můžete nakonfigurovat v **modelu OfferCatalogViewModel.**

## <a name="configure-branding"></a>Konfigurace brandingu

Tento ukázkový web sleduje následující informace o společnosti a značce v *brandinguConfiguration.cs* a *PortalBranding.cs:*

- Název organizace
- Logo organizace
- Obrázek záhlaví
- Smlouva o ochraně osobních údajů
- Kontaktní e-mail
- Kontaktní telefonní číslo
- E-mail podpory
- Telefonní číslo podpory

### <a name="configure-payment-types"></a>Konfigurace typů plateb

Aplikace aktuálně používá bránu PayPal, která je implementovaná v *souboru PayPalGateway.cs.*