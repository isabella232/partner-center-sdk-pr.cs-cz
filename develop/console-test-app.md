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
# <a name="console-test-app"></a><span data-ttu-id="d51ab-104">Aplikace pro testování konzoly</span><span class="sxs-lookup"><span data-stu-id="d51ab-104">Console test app</span></span>

<span data-ttu-id="d51ab-105">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="d51ab-105">**Applies to:**</span></span>

- <span data-ttu-id="d51ab-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="d51ab-106">Partner Center</span></span>
- <span data-ttu-id="d51ab-107">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d51ab-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d51ab-108">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="d51ab-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d51ab-109">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d51ab-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d51ab-110">Testovací aplikace konzoly je k dispozici v jazycích C# a Java a poskytuje ukázkové kódy pro všechny scénáře podporované rozhraními API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="d51ab-110">The console test app is provided in C# and Java, it provides sample codes for all of the scenarios supported by the Partner Center APIs.</span></span> <span data-ttu-id="d51ab-111">Můžete ho také použít k testování.</span><span class="sxs-lookup"><span data-stu-id="d51ab-111">You can also use it for testing.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="d51ab-112">Získání kódu</span><span class="sxs-lookup"><span data-stu-id="d51ab-112">Get the code</span></span>

<span data-ttu-id="d51ab-113">Stáhněte si vzorový kód pro testovací aplikaci konzoly.</span><span class="sxs-lookup"><span data-stu-id="d51ab-113">Download the sample code for the console test app.</span></span>

## <a name="net"></a><span data-ttu-id="d51ab-114">.NET</span><span class="sxs-lookup"><span data-stu-id="d51ab-114">.NET</span></span>

<span data-ttu-id="d51ab-115">[Stáhněte si vzorový kód](https://go.microsoft.com/fwlink/p/?LinkId=746682) a podle potřeby ho upravte.</span><span class="sxs-lookup"><span data-stu-id="d51ab-115">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=746682) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d51ab-116">Než sestavíte aplikaci, aktualizujte hodnoty v souboru *App.config* tak, aby odrážely ověřovací informace Azure AD, které jste vytvořili v [partnerském centru](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d51ab-116">Before you build the application, update the values in the *App.config* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d51ab-117">Konkrétně byste měli použít nastavení účtu izolovaného prostoru pro integraci při prvotním vývoji nebo pro testování v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="d51ab-117">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="d51ab-118">V části **ScenarioSettings** v souboru *App.config* můžete nastavit parametry, které budou automaticky předány do scénářů, které spustíte.</span><span class="sxs-lookup"><span data-stu-id="d51ab-118">Under **ScenarioSettings** in the *App.config* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="d51ab-119">Chcete-li upravit seznam scénářů, které jsou spuštěny, odkomentujte řádky v **IPartnerScenario \[ \] mainScenarios** nebo v jednotlivých metodách **Get scénářů** nalezených v souboru *program.cs* .</span><span class="sxs-lookup"><span data-stu-id="d51ab-119">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.cs* file.</span></span>

## <a name="java"></a><span data-ttu-id="d51ab-120">Java</span><span class="sxs-lookup"><span data-stu-id="d51ab-120">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="d51ab-121">[Stáhněte si vzorový kód](https://go.microsoft.com/fwlink/p/?LinkId=2026887) a podle potřeby ho upravte.</span><span class="sxs-lookup"><span data-stu-id="d51ab-121">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=2026887) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d51ab-122">Než sestavíte aplikaci, aktualizujte hodnoty v *SamplesConfigurations.jsv* souboru tak, aby odrážely ověřovací informace Azure AD, které jste vytvořili v [partnerském centru](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d51ab-122">Before you build the application, update the values in the *SamplesConfigurations.json* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d51ab-123">Konkrétně byste měli použít nastavení účtu izolovaného prostoru pro integraci při prvotním vývoji nebo pro testování v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="d51ab-123">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="d51ab-124">V části **ScenarioSettings** *SamplesConfiguration.js* v souboru můžete nastavit parametry, které budou automaticky předány do scénářů, které spustíte.</span><span class="sxs-lookup"><span data-stu-id="d51ab-124">Under **ScenarioSettings** in the *SamplesConfiguration.json* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="d51ab-125">Chcete-li upravit seznam scénářů, které jsou spuštěny, odkomentujte řádky v **IPartnerScenario \[ \] mainScenarios** nebo v jednotlivých metodách **Get scénářů** , které se nacházejí v souboru *program. Java* .</span><span class="sxs-lookup"><span data-stu-id="d51ab-125">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.java* file.</span></span>

## <a name="what-to-change"></a><span data-ttu-id="d51ab-126">Co se má změnit</span><span class="sxs-lookup"><span data-stu-id="d51ab-126">What to change</span></span>

<span data-ttu-id="d51ab-127">Pomocí následujících seznamů určete, co se v ukázkovém kódu mění nebo nemění.</span><span class="sxs-lookup"><span data-stu-id="d51ab-127">Use the following lists to determine what to change or not change in the sample code.</span></span>

### <a name="partnerservicesettings"></a><span data-ttu-id="d51ab-128">PartnerServiceSettings</span><span class="sxs-lookup"><span data-stu-id="d51ab-128">PartnerServiceSettings</span></span>

<span data-ttu-id="d51ab-129">Pro **PartnerServiceSettings** se neměňte:</span><span class="sxs-lookup"><span data-stu-id="d51ab-129">For **PartnerServiceSettings**, don't change:</span></span>

- <span data-ttu-id="d51ab-130">**PartnerServiceApiEndpoint**</span><span class="sxs-lookup"><span data-stu-id="d51ab-130">**PartnerServiceApiEndpoint**</span></span>
- <span data-ttu-id="d51ab-131">**AuthenticationAuthorityEndpoint**</span><span class="sxs-lookup"><span data-stu-id="d51ab-131">**AuthenticationAuthorityEndpoint**</span></span>
- <span data-ttu-id="d51ab-132">**GraphEndpoint**</span><span class="sxs-lookup"><span data-stu-id="d51ab-132">**GraphEndpoint**</span></span>
- <span data-ttu-id="d51ab-133">**CommonDomain**</span><span class="sxs-lookup"><span data-stu-id="d51ab-133">**CommonDomain**</span></span>

<span data-ttu-id="d51ab-134">Všechna tato nastavení jsou nutná pro správné fungování ukázkových volání rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="d51ab-134">All of these settings are necessary for the sample API calls to properly function.</span></span>

### <a name="userauthentication"></a><span data-ttu-id="d51ab-135">UserAuthentication</span><span class="sxs-lookup"><span data-stu-id="d51ab-135">UserAuthentication</span></span>

<span data-ttu-id="d51ab-136">V případě **UserAuthentication** je potřeba změnit:</span><span class="sxs-lookup"><span data-stu-id="d51ab-136">For **UserAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="d51ab-137">**ApplicationId** (vaše Azure Active Directory ID aplikace používané pro přihlášení)</span><span class="sxs-lookup"><span data-stu-id="d51ab-137">**ApplicationId** (your Azure Active Directory application ID used for login)</span></span>
- <span data-ttu-id="d51ab-138">**Username** (uživatelské jméno ve službě Active Directory)</span><span class="sxs-lookup"><span data-stu-id="d51ab-138">**UserName** (your active directory username)</span></span>
- <span data-ttu-id="d51ab-139">**Heslo** (heslo služby Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d51ab-139">**Password** (your active directory password).</span></span>

<span data-ttu-id="d51ab-140">Neměnit:</span><span class="sxs-lookup"><span data-stu-id="d51ab-140">Don't change:</span></span>

- <span data-ttu-id="d51ab-141">**ResourceUrl**</span><span class="sxs-lookup"><span data-stu-id="d51ab-141">**ResourceUrl**</span></span>
- <span data-ttu-id="d51ab-142">**RedirectUrl**</span><span class="sxs-lookup"><span data-stu-id="d51ab-142">**RedirectUrl**</span></span>

### <a name="appauthentication"></a><span data-ttu-id="d51ab-143">AppAuthentication</span><span class="sxs-lookup"><span data-stu-id="d51ab-143">AppAuthentication</span></span>

<span data-ttu-id="d51ab-144">V případě **AppAuthentication** je potřeba změnit:</span><span class="sxs-lookup"><span data-stu-id="d51ab-144">For **AppAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="d51ab-145">**ApplicationId** (vaše ID aplikace služby Active Directory používané pro přihlášení k aplikaci)</span><span class="sxs-lookup"><span data-stu-id="d51ab-145">**ApplicationId** (your active directory application ID used for application login)</span></span>
- <span data-ttu-id="d51ab-146">**ApplicationSecret** (váš tajný klíč aplikace služby Active Directory použitý pro přihlášení k aplikaci)</span><span class="sxs-lookup"><span data-stu-id="d51ab-146">**ApplicationSecret** (your active directory application secret used for application login)</span></span>
- <span data-ttu-id="d51ab-147">**Doména** (doména služby Active Directory, na které je aplikace hostovaná)</span><span class="sxs-lookup"><span data-stu-id="d51ab-147">**Domain** (your active directory domain on which the application is hosted)</span></span>

### <a name="scenariosettings"></a><span data-ttu-id="d51ab-148">ScenarioSettings</span><span class="sxs-lookup"><span data-stu-id="d51ab-148">ScenarioSettings</span></span>

<span data-ttu-id="d51ab-149">Pro **ScenarioSettings** se neměňte:</span><span class="sxs-lookup"><span data-stu-id="d51ab-149">For **ScenarioSettings**, don't change:</span></span>

- <span data-ttu-id="d51ab-150">**CustomerDomainSuffix** (přípona domény použitá při vytváření nového zákazníka)</span><span class="sxs-lookup"><span data-stu-id="d51ab-150">**CustomerDomainSuffix** (the domain suffix used when creating a new customer)</span></span>

<span data-ttu-id="d51ab-151">Volitelná nastavení.</span><span class="sxs-lookup"><span data-stu-id="d51ab-151">Optional settings.</span></span> <span data-ttu-id="d51ab-152">Pokud necháte pole prázdné, bude nutné tyto informace při spuštění scénáře, kde je to potřeba, zacházet:</span><span class="sxs-lookup"><span data-stu-id="d51ab-152">If left blank, this information will need to be inputted when running a scenario where necessary):</span></span>

- <span data-ttu-id="d51ab-153">**CustomerIdToDelete** (ID zákazníka používaného k odstranění)</span><span class="sxs-lookup"><span data-stu-id="d51ab-153">**CustomerIdToDelete** (the ID of the customer used for deletion)</span></span>
- <span data-ttu-id="d51ab-154">**DefaultCustomerId** (ID zákazníka pro použití ve scénářích souvisejících se zákazníky)</span><span class="sxs-lookup"><span data-stu-id="d51ab-154">**DefaultCustomerId** (the customer ID to use in customer-related scenarios)</span></span>
- <span data-ttu-id="d51ab-155">**DefaultInvoiceID** (ID faktury pro použití ve scénářích faktury)</span><span class="sxs-lookup"><span data-stu-id="d51ab-155">**DefaultInvoiceID** (the invoice ID to use in invoice scenarios)</span></span>
- <span data-ttu-id="d51ab-156">**PartnerMpnId** (ID MPN partnera pro použití v nepřímých partnerských scénářích)</span><span class="sxs-lookup"><span data-stu-id="d51ab-156">**PartnerMpnId** (the partner MPN ID to use in indirect partner scenarios)</span></span>
- <span data-ttu-id="d51ab-157">**DefaultServiceRequestId** (ID žádosti o službu, která se má použít ve scénářích žádosti o služby)</span><span class="sxs-lookup"><span data-stu-id="d51ab-157">**DefaultServiceRequestId** (the service request ID to use in service request scenarios)</span></span>
- <span data-ttu-id="d51ab-158">**DefaultSupportTopicID** (ID tématu podpory, které se použije ve scénářích žádosti o služby)</span><span class="sxs-lookup"><span data-stu-id="d51ab-158">**DefaultSupportTopicID** (the support topic ID to use in service request scenarios)</span></span>
- <span data-ttu-id="d51ab-159">**DefaultOfferID** (ID nabídky, která se má použít v nabídkových scénářích)</span><span class="sxs-lookup"><span data-stu-id="d51ab-159">**DefaultOfferID** (the offer ID to use in offer scenarios)</span></span>
- <span data-ttu-id="d51ab-160">**DefaultOrderID** (ID objednávky, které se má použít ve scénářích pořadí)</span><span class="sxs-lookup"><span data-stu-id="d51ab-160">**DefaultOrderID** (the order ID to use in order scenarios)</span></span>
- <span data-ttu-id="d51ab-161">**DefaultSubscriptionID** (ID předplatného, které se má použít ve scénářích předplatného)</span><span class="sxs-lookup"><span data-stu-id="d51ab-161">**DefaultSubscriptionID** (the subscription ID to use in subscription scenarios)</span></span>

<span data-ttu-id="d51ab-162">Volitelné pro změnu.</span><span class="sxs-lookup"><span data-stu-id="d51ab-162">Optional to change.</span></span> <span data-ttu-id="d51ab-163">Všechna tato nastavení určují počet položek na stránku při načítání stránkovaného obsahu:</span><span class="sxs-lookup"><span data-stu-id="d51ab-163">All of these settings specify the amount of entries per page when retrieving paged content:</span></span>

- <span data-ttu-id="d51ab-164">**CustomerPageSize**</span><span class="sxs-lookup"><span data-stu-id="d51ab-164">**CustomerPageSize**</span></span>
- <span data-ttu-id="d51ab-165">**InvoicePageSize**</span><span class="sxs-lookup"><span data-stu-id="d51ab-165">**InvoicePageSize**</span></span>
- <span data-ttu-id="d51ab-166">**ServiceRequestPageSize**</span><span class="sxs-lookup"><span data-stu-id="d51ab-166">**ServiceRequestPageSize**</span></span>
- <span data-ttu-id="d51ab-167">**DefaultOfferPageSize**</span><span class="sxs-lookup"><span data-stu-id="d51ab-167">**DefaultOfferPageSize**</span></span>
- <span data-ttu-id="d51ab-168">**SubscriptionPageSize**</span><span class="sxs-lookup"><span data-stu-id="d51ab-168">**SubscriptionPageSize**</span></span>
