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
# <a name="csp-customer-web-storefront"></a><span data-ttu-id="bbfd4-103">Webová výkladní skříň pro zákazníky CSP</span><span class="sxs-lookup"><span data-stu-id="bbfd4-103">CSP customer web storefront</span></span>

<span data-ttu-id="bbfd4-104">**Platí pro:** Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="bbfd4-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="bbfd4-105">**Neplatí pro: Partnerské centrum** Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="bbfd4-105">**Does not apply to**: Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bbfd4-106">Tato ukázková aplikace se vztahuje pouze na globální instanci Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="bbfd4-106">This sample app applies only to the global instance of Partner Center.</span></span>

<span data-ttu-id="bbfd4-107">Webová [Partnerské centrum je ukázkový](https://github.com/Microsoft/Partner-Center-Storefront)  web pro online obchod, který zákazníci mohou použít k nákupu předplatných produktů Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="bbfd4-107">The [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) is a **sample website** for an online store that customers can use to buy subscriptions to Microsoft products.</span></span> <span data-ttu-id="bbfd4-108">Tento vzorový kód **můžete upravit** pro vlastní použití a nakonfigurovat [nabídky,](#configure-offers)přidat [značku](#configure-branding)a přidat [způsob platby](#configure-payment-types).</span><span class="sxs-lookup"><span data-stu-id="bbfd4-108">You can modify this **sample code** for your own use to [configure the offers](#configure-offers), [add branding](#configure-branding), and [add a payment method](#configure-payment-types).</span></span>

## <a name="sample-code"></a><span data-ttu-id="bbfd4-109">Ukázka kódu</span><span class="sxs-lookup"><span data-stu-id="bbfd4-109">Sample code</span></span>

<span data-ttu-id="bbfd4-110">Stáhněte [si Partnerské centrum kódu z GitHub.](https://github.com/Microsoft/Partner-Center-Storefront)</span><span class="sxs-lookup"><span data-stu-id="bbfd4-110">Download the [Partner Center storefront sample code](https://github.com/Microsoft/Partner-Center-Storefront) from GitHub.</span></span>

## <a name="configure-authentication"></a><span data-ttu-id="bbfd4-111">Konfigurace ověřování</span><span class="sxs-lookup"><span data-stu-id="bbfd4-111">Configure authentication</span></span>

<span data-ttu-id="bbfd4-112">Před sestavením aplikace aktualizujte následující hodnoty v souboru Web.config tak, aby odrážely ověřovací informace Azure AD, které jste vytvořili [v Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="bbfd4-112">Before you build the application, update the following values in the Web.config file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bbfd4-113">Nastavení účtu sandboxu pro integraci byste měli použít během raného vývoje nebo testování v produkčním prostředí (TiP).</span><span class="sxs-lookup"><span data-stu-id="bbfd4-113">You should use your integration sandbox account settings during early development or for testing in production (TiP).</span></span>

- <span data-ttu-id="bbfd4-114">**partnerCenter.applicationId**</span><span class="sxs-lookup"><span data-stu-id="bbfd4-114">**partnerCenter.applicationId**</span></span>
- <span data-ttu-id="bbfd4-115">**partnerCenter.applicationSecret**</span><span class="sxs-lookup"><span data-stu-id="bbfd4-115">**partnerCenter.applicationSecret**</span></span>
- <span data-ttu-id="bbfd4-116">**partnerCenter.domain**</span><span class="sxs-lookup"><span data-stu-id="bbfd4-116">**partnerCenter.domain**</span></span>
- <span data-ttu-id="bbfd4-117">**webPortal.clientId**</span><span class="sxs-lookup"><span data-stu-id="bbfd4-117">**webPortal.clientId**</span></span>
- <span data-ttu-id="bbfd4-118">**webPortal.clientSecret**</span><span class="sxs-lookup"><span data-stu-id="bbfd4-118">**webPortal.clientSecret**</span></span>
- <span data-ttu-id="bbfd4-119">**webPortal.domain**</span><span class="sxs-lookup"><span data-stu-id="bbfd4-119">**webPortal.domain**</span></span>
- <span data-ttu-id="bbfd4-120">**webPortal.azureStorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="bbfd4-120">**webPortal.azureStorageConnectionString**</span></span>

## <a name="configure-offers"></a><span data-ttu-id="bbfd4-121">Konfigurace nabídek</span><span class="sxs-lookup"><span data-stu-id="bbfd4-121">Configure offers</span></span>

<span data-ttu-id="bbfd4-122">Sadu nabídek (**MicrosoftOffer**) můžete nakonfigurovat v **modelu OfferCatalogViewModel.**</span><span class="sxs-lookup"><span data-stu-id="bbfd4-122">You can configure the set of offers (**MicrosoftOffer**) in the **OfferCatalogViewModel**.</span></span>

## <a name="configure-branding"></a><span data-ttu-id="bbfd4-123">Konfigurace brandingu</span><span class="sxs-lookup"><span data-stu-id="bbfd4-123">Configure branding</span></span>

<span data-ttu-id="bbfd4-124">Tento ukázkový web sleduje následující informace o společnosti a značce v *brandinguConfiguration.cs* a *PortalBranding.cs:*</span><span class="sxs-lookup"><span data-stu-id="bbfd4-124">This sample website tracks the following company and brand information in *BrandingConfiguration.cs* and *PortalBranding.cs*:</span></span>

- <span data-ttu-id="bbfd4-125">Název organizace</span><span class="sxs-lookup"><span data-stu-id="bbfd4-125">Organization name</span></span>
- <span data-ttu-id="bbfd4-126">Logo organizace</span><span class="sxs-lookup"><span data-stu-id="bbfd4-126">Organization logo</span></span>
- <span data-ttu-id="bbfd4-127">Obrázek záhlaví</span><span class="sxs-lookup"><span data-stu-id="bbfd4-127">Header image</span></span>
- <span data-ttu-id="bbfd4-128">Smlouva o ochraně osobních údajů</span><span class="sxs-lookup"><span data-stu-id="bbfd4-128">Privacy agreement</span></span>
- <span data-ttu-id="bbfd4-129">Kontaktní e-mail</span><span class="sxs-lookup"><span data-stu-id="bbfd4-129">Contact email</span></span>
- <span data-ttu-id="bbfd4-130">Kontaktní telefonní číslo</span><span class="sxs-lookup"><span data-stu-id="bbfd4-130">Contact phone number</span></span>
- <span data-ttu-id="bbfd4-131">E-mail podpory</span><span class="sxs-lookup"><span data-stu-id="bbfd4-131">Support email</span></span>
- <span data-ttu-id="bbfd4-132">Telefonní číslo podpory</span><span class="sxs-lookup"><span data-stu-id="bbfd4-132">Support phone number</span></span>

### <a name="configure-payment-types"></a><span data-ttu-id="bbfd4-133">Konfigurace typů plateb</span><span class="sxs-lookup"><span data-stu-id="bbfd4-133">Configure payment types</span></span>

<span data-ttu-id="bbfd4-134">Aplikace aktuálně používá bránu PayPal, která je implementovaná v *souboru PayPalGateway.cs.*</span><span class="sxs-lookup"><span data-stu-id="bbfd4-134">The app currently uses a PayPal gateway, implemented in *PayPalGateway.cs*.</span></span>