---
title: Aplikace pro testování konzoly
description: Tato testovací aplikace konzoly poskytuje vzorový kód pro všechny scénáře podporované rozhraními API partnerského centra. Můžete ho také použít k testování.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b35167104deeede50107d59fca6112c10dc7b4bf
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974025"
---
# <a name="console-test-app"></a><span data-ttu-id="05661-104">Aplikace pro testování konzoly</span><span class="sxs-lookup"><span data-stu-id="05661-104">Console test app</span></span>

<span data-ttu-id="05661-105">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="05661-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="05661-106">Testovací aplikace konzoly je k dispozici v jazycích C# a Java a poskytuje ukázkové kódy pro všechny scénáře podporované rozhraními API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="05661-106">The console test app is provided in C# and Java, it provides sample codes for all of the scenarios supported by the Partner Center APIs.</span></span> <span data-ttu-id="05661-107">Můžete ho také použít k testování.</span><span class="sxs-lookup"><span data-stu-id="05661-107">You can also use it for testing.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="05661-108">Získání kódu</span><span class="sxs-lookup"><span data-stu-id="05661-108">Get the code</span></span>

<span data-ttu-id="05661-109">Stáhněte si vzorový kód pro testovací aplikaci konzoly.</span><span class="sxs-lookup"><span data-stu-id="05661-109">Download the sample code for the console test app.</span></span>

## <a name="net"></a><span data-ttu-id="05661-110">.NET</span><span class="sxs-lookup"><span data-stu-id="05661-110">.NET</span></span>

<span data-ttu-id="05661-111">[Stáhněte si vzorový kód](https://go.microsoft.com/fwlink/p/?LinkId=746682) a podle potřeby ho upravte.</span><span class="sxs-lookup"><span data-stu-id="05661-111">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=746682) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05661-112">Než sestavíte aplikaci, aktualizujte hodnoty v souboru *App.config* tak, aby odrážely ověřovací informace Azure AD, které jste vytvořili v [partnerském centru](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="05661-112">Before you build the application, update the values in the *App.config* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="05661-113">Konkrétně byste měli použít nastavení účtu izolovaného prostoru pro integraci při prvotním vývoji nebo pro testování v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="05661-113">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="05661-114">V části **ScenarioSettings** v souboru *App.config* můžete nastavit parametry, které budou automaticky předány do scénářů, které spustíte.</span><span class="sxs-lookup"><span data-stu-id="05661-114">Under **ScenarioSettings** in the *App.config* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="05661-115">Chcete-li upravit seznam scénářů, které jsou spuštěny, odkomentujte řádky v **IPartnerScenario \[ \] mainScenarios** nebo v jednotlivých metodách **Get scénářů** , které se nacházejí v souboru *program. cs* .</span><span class="sxs-lookup"><span data-stu-id="05661-115">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.cs* file.</span></span>

## <a name="java"></a><span data-ttu-id="05661-116">Java</span><span class="sxs-lookup"><span data-stu-id="05661-116">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="05661-117">[Stáhněte si vzorový kód](https://go.microsoft.com/fwlink/p/?LinkId=2026887) a podle potřeby ho upravte.</span><span class="sxs-lookup"><span data-stu-id="05661-117">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=2026887) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05661-118">Než sestavíte aplikaci, aktualizujte hodnoty v *SamplesConfigurations.jsv* souboru tak, aby odrážely ověřovací informace Azure AD, které jste vytvořili v [partnerském centru](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="05661-118">Before you build the application, update the values in the *SamplesConfigurations.json* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="05661-119">Konkrétně byste měli použít nastavení účtu izolovaného prostoru pro integraci při prvotním vývoji nebo pro testování v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="05661-119">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="05661-120">V části **ScenarioSettings** *SamplesConfiguration.js* v souboru můžete nastavit parametry, které budou automaticky předány do scénářů, které spustíte.</span><span class="sxs-lookup"><span data-stu-id="05661-120">Under **ScenarioSettings** in the *SamplesConfiguration.json* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="05661-121">Chcete-li upravit seznam scénářů, které jsou spuštěny, odkomentujte řádky v **IPartnerScenario \[ \] mainScenarios** nebo v jednotlivých metodách **Get scénářů** , které se nacházejí v souboru *program. Java* .</span><span class="sxs-lookup"><span data-stu-id="05661-121">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.java* file.</span></span>

## <a name="what-to-change"></a><span data-ttu-id="05661-122">Co se má změnit</span><span class="sxs-lookup"><span data-stu-id="05661-122">What to change</span></span>

<span data-ttu-id="05661-123">Pomocí následujících seznamů určete, co se v ukázkovém kódu mění nebo nemění.</span><span class="sxs-lookup"><span data-stu-id="05661-123">Use the following lists to determine what to change or not change in the sample code.</span></span>

### <a name="partnerservicesettings"></a><span data-ttu-id="05661-124">PartnerServiceSettings</span><span class="sxs-lookup"><span data-stu-id="05661-124">PartnerServiceSettings</span></span>

<span data-ttu-id="05661-125">Pro **PartnerServiceSettings** se neměňte:</span><span class="sxs-lookup"><span data-stu-id="05661-125">For **PartnerServiceSettings**, don't change:</span></span>

- <span data-ttu-id="05661-126">**PartnerServiceApiEndpoint**</span><span class="sxs-lookup"><span data-stu-id="05661-126">**PartnerServiceApiEndpoint**</span></span>
- <span data-ttu-id="05661-127">**AuthenticationAuthorityEndpoint**</span><span class="sxs-lookup"><span data-stu-id="05661-127">**AuthenticationAuthorityEndpoint**</span></span>
- <span data-ttu-id="05661-128">**GraphEndpoint**</span><span class="sxs-lookup"><span data-stu-id="05661-128">**GraphEndpoint**</span></span>
- <span data-ttu-id="05661-129">**CommonDomain**</span><span class="sxs-lookup"><span data-stu-id="05661-129">**CommonDomain**</span></span>

<span data-ttu-id="05661-130">Všechna tato nastavení jsou nutná pro správné fungování ukázkových volání rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="05661-130">All of these settings are necessary for the sample API calls to properly function.</span></span>

### <a name="userauthentication"></a><span data-ttu-id="05661-131">UserAuthentication</span><span class="sxs-lookup"><span data-stu-id="05661-131">UserAuthentication</span></span>

<span data-ttu-id="05661-132">V případě **UserAuthentication** je potřeba změnit:</span><span class="sxs-lookup"><span data-stu-id="05661-132">For **UserAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="05661-133">**ApplicationId** (vaše Azure Active Directory ID aplikace používané pro přihlášení)</span><span class="sxs-lookup"><span data-stu-id="05661-133">**ApplicationId** (your Azure Active Directory application ID used for login)</span></span>
- <span data-ttu-id="05661-134">**Username** (uživatelské jméno ve službě Active Directory)</span><span class="sxs-lookup"><span data-stu-id="05661-134">**UserName** (your active directory username)</span></span>
- <span data-ttu-id="05661-135">**Heslo** (heslo služby Active Directory).</span><span class="sxs-lookup"><span data-stu-id="05661-135">**Password** (your active directory password).</span></span>

<span data-ttu-id="05661-136">Neměnit:</span><span class="sxs-lookup"><span data-stu-id="05661-136">Don't change:</span></span>

- <span data-ttu-id="05661-137">**ResourceUrl**</span><span class="sxs-lookup"><span data-stu-id="05661-137">**ResourceUrl**</span></span>
- <span data-ttu-id="05661-138">**RedirectUrl**</span><span class="sxs-lookup"><span data-stu-id="05661-138">**RedirectUrl**</span></span>

### <a name="appauthentication"></a><span data-ttu-id="05661-139">AppAuthentication</span><span class="sxs-lookup"><span data-stu-id="05661-139">AppAuthentication</span></span>

<span data-ttu-id="05661-140">V případě **AppAuthentication** je potřeba změnit:</span><span class="sxs-lookup"><span data-stu-id="05661-140">For **AppAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="05661-141">**ApplicationId** (vaše ID aplikace služby Active Directory používané pro přihlášení k aplikaci)</span><span class="sxs-lookup"><span data-stu-id="05661-141">**ApplicationId** (your active directory application ID used for application login)</span></span>
- <span data-ttu-id="05661-142">**ApplicationSecret** (váš tajný klíč aplikace služby Active Directory použitý pro přihlášení k aplikaci)</span><span class="sxs-lookup"><span data-stu-id="05661-142">**ApplicationSecret** (your active directory application secret used for application login)</span></span>
- <span data-ttu-id="05661-143">**Doména** (doména služby Active Directory, na které je aplikace hostovaná)</span><span class="sxs-lookup"><span data-stu-id="05661-143">**Domain** (your active directory domain on which the application is hosted)</span></span>

### <a name="scenariosettings"></a><span data-ttu-id="05661-144">ScenarioSettings</span><span class="sxs-lookup"><span data-stu-id="05661-144">ScenarioSettings</span></span>

<span data-ttu-id="05661-145">Pro **ScenarioSettings** se neměňte:</span><span class="sxs-lookup"><span data-stu-id="05661-145">For **ScenarioSettings**, don't change:</span></span>

- <span data-ttu-id="05661-146">**CustomerDomainSuffix** (přípona domény použitá při vytváření nového zákazníka)</span><span class="sxs-lookup"><span data-stu-id="05661-146">**CustomerDomainSuffix** (the domain suffix used when creating a new customer)</span></span>

<span data-ttu-id="05661-147">Volitelná nastavení.</span><span class="sxs-lookup"><span data-stu-id="05661-147">Optional settings.</span></span> <span data-ttu-id="05661-148">Pokud necháte pole prázdné, bude nutné tyto informace při spuštění scénáře, kde je to potřeba, zacházet:</span><span class="sxs-lookup"><span data-stu-id="05661-148">If left blank, this information will need to be inputted when running a scenario where necessary):</span></span>

- <span data-ttu-id="05661-149">**CustomerIdToDelete** (ID zákazníka používaného k odstranění)</span><span class="sxs-lookup"><span data-stu-id="05661-149">**CustomerIdToDelete** (the ID of the customer used for deletion)</span></span>
- <span data-ttu-id="05661-150">**DefaultCustomerId** (ID zákazníka pro použití ve scénářích souvisejících se zákazníky)</span><span class="sxs-lookup"><span data-stu-id="05661-150">**DefaultCustomerId** (the customer ID to use in customer-related scenarios)</span></span>
- <span data-ttu-id="05661-151">**DefaultInvoiceID** (ID faktury pro použití ve scénářích faktury)</span><span class="sxs-lookup"><span data-stu-id="05661-151">**DefaultInvoiceID** (the invoice ID to use in invoice scenarios)</span></span>
- <span data-ttu-id="05661-152">**PartnerMpnId** (ID MPN partnera pro použití v nepřímých partnerských scénářích)</span><span class="sxs-lookup"><span data-stu-id="05661-152">**PartnerMpnId** (the partner MPN ID to use in indirect partner scenarios)</span></span>
- <span data-ttu-id="05661-153">**DefaultServiceRequestId** (ID žádosti o službu, která se má použít ve scénářích žádosti o služby)</span><span class="sxs-lookup"><span data-stu-id="05661-153">**DefaultServiceRequestId** (the service request ID to use in service request scenarios)</span></span>
- <span data-ttu-id="05661-154">**DefaultSupportTopicID** (ID tématu podpory, které se použije ve scénářích žádosti o služby)</span><span class="sxs-lookup"><span data-stu-id="05661-154">**DefaultSupportTopicID** (the support topic ID to use in service request scenarios)</span></span>
- <span data-ttu-id="05661-155">**DefaultOfferID** (ID nabídky, která se má použít v nabídkových scénářích)</span><span class="sxs-lookup"><span data-stu-id="05661-155">**DefaultOfferID** (the offer ID to use in offer scenarios)</span></span>
- <span data-ttu-id="05661-156">**DefaultOrderID** (ID objednávky, které se má použít ve scénářích pořadí)</span><span class="sxs-lookup"><span data-stu-id="05661-156">**DefaultOrderID** (the order ID to use in order scenarios)</span></span>
- <span data-ttu-id="05661-157">**DefaultSubscriptionID** (ID předplatného, které se má použít ve scénářích předplatného)</span><span class="sxs-lookup"><span data-stu-id="05661-157">**DefaultSubscriptionID** (the subscription ID to use in subscription scenarios)</span></span>

<span data-ttu-id="05661-158">Volitelné pro změnu.</span><span class="sxs-lookup"><span data-stu-id="05661-158">Optional to change.</span></span> <span data-ttu-id="05661-159">Všechna tato nastavení určují počet položek na stránku při načítání stránkovaného obsahu:</span><span class="sxs-lookup"><span data-stu-id="05661-159">All of these settings specify the amount of entries per page when retrieving paged content:</span></span>

- <span data-ttu-id="05661-160">**CustomerPageSize**</span><span class="sxs-lookup"><span data-stu-id="05661-160">**CustomerPageSize**</span></span>
- <span data-ttu-id="05661-161">**InvoicePageSize**</span><span class="sxs-lookup"><span data-stu-id="05661-161">**InvoicePageSize**</span></span>
- <span data-ttu-id="05661-162">**ServiceRequestPageSize**</span><span class="sxs-lookup"><span data-stu-id="05661-162">**ServiceRequestPageSize**</span></span>
- <span data-ttu-id="05661-163">**DefaultOfferPageSize**</span><span class="sxs-lookup"><span data-stu-id="05661-163">**DefaultOfferPageSize**</span></span>
- <span data-ttu-id="05661-164">**SubscriptionPageSize**</span><span class="sxs-lookup"><span data-stu-id="05661-164">**SubscriptionPageSize**</span></span>
