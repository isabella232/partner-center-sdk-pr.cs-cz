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
# <a name="csp-customer-web-storefront"></a><span data-ttu-id="95568-103">Webová výkladní skříň pro zákazníky CSP</span><span class="sxs-lookup"><span data-stu-id="95568-103">CSP customer web storefront</span></span>

<span data-ttu-id="95568-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="95568-104">**Applies to:**</span></span>

- <span data-ttu-id="95568-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="95568-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="95568-106">Tato ukázková aplikace se vztahuje jenom na globální instanci partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="95568-106">This sample app applies only to the global instance of Partner Center.</span></span> <span data-ttu-id="95568-107">Netýká se partnerského centra pro Microsoft Cloud Německo nebo partnerského centra pro Microsoft Cloud pro státní správu USA.</span><span class="sxs-lookup"><span data-stu-id="95568-107">It does not apply to Partner Center for Microsoft Cloud Germany or to Partner Center for Microsoft Cloud for US Government.</span></span>

<span data-ttu-id="95568-108">[Partnerský prezentace](https://github.com/Microsoft/Partner-Center-Storefront) je **ukázkový web** pro online obchod, který můžou zákazníci použít k nákupu předplatných produktů Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="95568-108">The [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) is a **sample website** for an online store that customers can use to buy subscriptions to Microsoft products.</span></span> <span data-ttu-id="95568-109">Tento **vzorový kód** můžete upravit pro vlastní použití, abyste mohli [Konfigurovat nabídky](#configure-offers), [Přidat branding](#configure-branding) a [Přidat způsob platby](#configure-payment-types).</span><span class="sxs-lookup"><span data-stu-id="95568-109">You can modify this **sample code** for your own use to [configure the offers](#configure-offers), [add branding](#configure-branding) and [add a payment method](#configure-payment-types).</span></span>

## <a name="sample-code"></a><span data-ttu-id="95568-110">Ukázka kódu</span><span class="sxs-lookup"><span data-stu-id="95568-110">Sample code</span></span>

<span data-ttu-id="95568-111">Stáhněte si [vzorový kód prezentace partnerského centra](https://github.com/Microsoft/Partner-Center-Storefront) z GitHubu.</span><span class="sxs-lookup"><span data-stu-id="95568-111">Download the [Partner Center storefront sample code](https://github.com/Microsoft/Partner-Center-Storefront) from GitHub.</span></span>

## <a name="configure-authentication"></a><span data-ttu-id="95568-112">Konfigurace ověřování</span><span class="sxs-lookup"><span data-stu-id="95568-112">Configure authentication</span></span>

<span data-ttu-id="95568-113">Než sestavíte aplikaci, aktualizujte následující hodnoty v souboru Web.config tak, aby odrážely ověřovací informace Azure AD, které jste vytvořili v [partnerském centru](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="95568-113">Before you build the application, update the following values in the Web.config file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="95568-114">Měli byste použít nastavení účtu izolovaného prostoru pro integraci při prvotním vývoji nebo pro testování v produkčním prostředí (TiP).</span><span class="sxs-lookup"><span data-stu-id="95568-114">You should use your integration sandbox account settings during early development or for testing in production (TiP).</span></span>

- <span data-ttu-id="95568-115">**partnerCenter. applicationId**</span><span class="sxs-lookup"><span data-stu-id="95568-115">**partnerCenter.applicationId**</span></span>
- <span data-ttu-id="95568-116">**partnerCenter.applicationSecret**</span><span class="sxs-lookup"><span data-stu-id="95568-116">**partnerCenter.applicationSecret**</span></span>
- <span data-ttu-id="95568-117">**partnerCenter. Domain**</span><span class="sxs-lookup"><span data-stu-id="95568-117">**partnerCenter.domain**</span></span>
- <span data-ttu-id="95568-118">**webportes. clientId**</span><span class="sxs-lookup"><span data-stu-id="95568-118">**webPortal.clientId**</span></span>
- <span data-ttu-id="95568-119">**webportes. clientSecret**</span><span class="sxs-lookup"><span data-stu-id="95568-119">**webPortal.clientSecret**</span></span>
- <span data-ttu-id="95568-120">**webportes. Domain**</span><span class="sxs-lookup"><span data-stu-id="95568-120">**webPortal.domain**</span></span>
- <span data-ttu-id="95568-121">**webportes. azureStorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="95568-121">**webPortal.azureStorageConnectionString**</span></span>

## <a name="configure-offers"></a><span data-ttu-id="95568-122">Konfigurovat nabídky</span><span class="sxs-lookup"><span data-stu-id="95568-122">Configure offers</span></span>

<span data-ttu-id="95568-123">V **OfferCatalogViewModel** můžete nakonfigurovat sadu nabídek (**MicrosoftOffer**).</span><span class="sxs-lookup"><span data-stu-id="95568-123">You can configure the set of offers (**MicrosoftOffer**) in the **OfferCatalogViewModel**.</span></span>

## <a name="configure-branding"></a><span data-ttu-id="95568-124">Konfigurace brandingu</span><span class="sxs-lookup"><span data-stu-id="95568-124">Configure branding</span></span>

<span data-ttu-id="95568-125">Tento ukázkový web sleduje v *BrandingConfiguration.cs* a *PortalBranding.cs* následující informace o společnosti a značce:</span><span class="sxs-lookup"><span data-stu-id="95568-125">This sample website tracks the following company and brand information in *BrandingConfiguration.cs* and *PortalBranding.cs*:</span></span>

- <span data-ttu-id="95568-126">Název organizace</span><span class="sxs-lookup"><span data-stu-id="95568-126">Organization name</span></span>
- <span data-ttu-id="95568-127">Logo organizace</span><span class="sxs-lookup"><span data-stu-id="95568-127">Organization logo</span></span>
- <span data-ttu-id="95568-128">Obrázek záhlaví</span><span class="sxs-lookup"><span data-stu-id="95568-128">Header image</span></span>
- <span data-ttu-id="95568-129">Smlouva o ochraně osobních údajů</span><span class="sxs-lookup"><span data-stu-id="95568-129">Privacy agreement</span></span>
- <span data-ttu-id="95568-130">Kontaktní e-mail</span><span class="sxs-lookup"><span data-stu-id="95568-130">Contact email</span></span>
- <span data-ttu-id="95568-131">Kontaktní telefonní číslo</span><span class="sxs-lookup"><span data-stu-id="95568-131">Contact phone number</span></span>
- <span data-ttu-id="95568-132">E-mail podpory</span><span class="sxs-lookup"><span data-stu-id="95568-132">Support email</span></span>
- <span data-ttu-id="95568-133">Telefonní číslo podpory</span><span class="sxs-lookup"><span data-stu-id="95568-133">Support phone number</span></span>

### <a name="configure-payment-types"></a><span data-ttu-id="95568-134">Konfigurace typů plateb</span><span class="sxs-lookup"><span data-stu-id="95568-134">Configure payment types</span></span>

<span data-ttu-id="95568-135">Aplikace aktuálně používá bránu PayPal implementovanou v *PayPalGateway.cs*.</span><span class="sxs-lookup"><span data-stu-id="95568-135">The app currently uses a PayPal gateway, implemented in *PayPalGateway.cs*.</span></span>