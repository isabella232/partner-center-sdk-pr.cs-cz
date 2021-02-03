---
title: Začínáme
description: Sada SDK partnerského centra zahrnuje spravované rozhraní API a REST API pro partnery, kteří se používají ke správě dat zákazníků, předplatných a objednávek.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9c2af1e11dbda19489a27e37c7f3de8ede90fd1c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766770"
---
# <a name="get-started"></a><span data-ttu-id="47e20-103">Začínáme</span><span class="sxs-lookup"><span data-stu-id="47e20-103">Get started</span></span>

<span data-ttu-id="47e20-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="47e20-104">**Applies To**</span></span>

- <span data-ttu-id="47e20-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="47e20-105">Partner Center</span></span>
- <span data-ttu-id="47e20-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="47e20-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="47e20-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="47e20-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="47e20-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="47e20-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="47e20-109">Sada SDK partnerského centra zahrnuje spravované rozhraní API a REST API pro partnery, kteří se používají ke správě dat zákazníků, předplatných a objednávek.</span><span class="sxs-lookup"><span data-stu-id="47e20-109">The Partner Center SDK includes a managed API and a REST API for partners to use to manage customer, subscription, and order data.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="47e20-110">Získání kódu</span><span class="sxs-lookup"><span data-stu-id="47e20-110">Get the code</span></span>

[<span data-ttu-id="47e20-111">Stáhnout sadu SDK partnerského centra</span><span class="sxs-lookup"><span data-stu-id="47e20-111">Download the Partner Center SDK</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> <span data-ttu-id="47e20-112">Přístup k rozhraní API partnerského centra pro nepřímý prodejce není podporovaným scénářem.</span><span class="sxs-lookup"><span data-stu-id="47e20-112">API access to Partner Center for indirect resellers isn't a supported scenario.</span></span>

## <a name="determine-your-version-of-partner-center"></a><span data-ttu-id="47e20-113">Určení verze partnerského centra</span><span class="sxs-lookup"><span data-stu-id="47e20-113">Determine your version of Partner Center</span></span>

<span data-ttu-id="47e20-114">Některé verze partnerského centra nemají k dispozici celou sadu SDK.</span><span class="sxs-lookup"><span data-stu-id="47e20-114">Some versions of Partner Center do not have the entire SDK available.</span></span> <span data-ttu-id="47e20-115">Další informace najdete v tématu [vývoj pro partnerského centra pro národní Cloud Microsoftu](developing-for-partner-center-for-microsoft-national-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="47e20-115">For more information, see [Developing for Partner Center for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).</span></span>

## <a name="get-the-samples"></a><span data-ttu-id="47e20-116">Získat ukázky</span><span class="sxs-lookup"><span data-stu-id="47e20-116">Get the samples</span></span>

<span data-ttu-id="47e20-117">Další informace o fragmentech kódu jazyka C#, ukázkách REST a ukázkové aplikaci najdete v tématu [ukázky partnerského centra](partner-center-samples.md).</span><span class="sxs-lookup"><span data-stu-id="47e20-117">For more information about C# snippets, REST samples, and the sample app, see [Partner Center samples](partner-center-samples.md).</span></span>

## <a name="test-vs-production"></a><span data-ttu-id="47e20-118">Testování vs. produkce</span><span class="sxs-lookup"><span data-stu-id="47e20-118">Test vs. production</span></span>

<span data-ttu-id="47e20-119">Když začnete psát a testovat kód, měli byste použít svůj účet izolovaného prostoru (a odpovídající tokeny), abyste omylem neúčtovali nové poplatky, za které vaše společnost zodpovídá za vyplácení.</span><span class="sxs-lookup"><span data-stu-id="47e20-119">While you are initially writing and testing your code, you should use your integration sandbox account (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying.</span></span> <span data-ttu-id="47e20-120">Další informace o tomto testovacím prostředí najdete v tématu [nastavení přístupu k rozhraní API v partnerském centru](set-up-api-access-in-partner-center.md).</span><span class="sxs-lookup"><span data-stu-id="47e20-120">For more information about this testing environment, see [Set up API access in Partner Center](set-up-api-access-in-partner-center.md).</span></span>

<span data-ttu-id="47e20-121">Když je vaše řešení testováno a připraveno k použití na reálných zákaznických účtech, budete muset aktualizovat vaše tokeny, abyste používali klientskou aplikaci Azure AD a tajný klíč, které odpovídají vašemu primárnímu účtu partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="47e20-121">When your solution is tested and ready to use on real customer accounts, you'll have to update your tokens so that you're using an Azure AD client app and secret that correspond to your Primary Partner Center account.</span></span>

<span data-ttu-id="47e20-122">Tipy a návrhy týkající se testování a ladění, včetně dalších informací o výrobě (TiP) a izolovaném prostoru Integration, naleznete v tématu [Test and Debug](test-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="47e20-122">For tips and suggestions about testing and debugging, including more information about Test-in-Production (TiP) and the Integration Sandbox, see [Test and debug](test-and-debug.md).</span></span>

## <a name="configure-your-authentication"></a><span data-ttu-id="47e20-123">Konfigurace ověřování</span><span class="sxs-lookup"><span data-stu-id="47e20-123">Configure your authentication</span></span>

<span data-ttu-id="47e20-124">Pokud chcete nakonfigurovat ověřování Azure AD, abyste mohli používat rozhraní API partnerského centra, Projděte si téma [ověřování v partnerském centru](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="47e20-124">To configure your Azure AD authentication so that you can use the Partner Center APIs, see [Partner Center authentication](partner-center-authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47e20-125">Microsoft zavádí zabezpečenou, škálovatelnou architekturu pro ověřování partnerů CSP (Cloud Solution Provider) a dodavatelů ovládacích panelů (CPV) prostřednictvím architektury Microsoft Azure Multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="47e20-125">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>
<span data-ttu-id="47e20-126">Partnerské centrum používá pro ověřování Azure AD a používá rozhraní API partnerského centra. musíte nakonfigurovat nastavení ověřování správně.</span><span class="sxs-lookup"><span data-stu-id="47e20-126">Partner Center uses Azure AD for authentication, and to use the Partner Center APIs you must configure your authentication settings correctly.</span></span>
>
> <span data-ttu-id="47e20-127">Další informace najdete v tématu [povolení zabezpečeného modelu aplikace](enable-secure-app-model.md).</span><span class="sxs-lookup"><span data-stu-id="47e20-127">For more information, see [Enable secure application model](enable-secure-app-model.md).</span></span>

## <a name="get-help"></a><span data-ttu-id="47e20-128">Získání pomoci</span><span class="sxs-lookup"><span data-stu-id="47e20-128">Get help</span></span>

<span data-ttu-id="47e20-129">Partneři můžou získat podporu ve [skupině partnerských Center SDK Yammer](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span><span class="sxs-lookup"><span data-stu-id="47e20-129">Partners can get support at the [Partner Center SDK Yammer group](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span></span> <span data-ttu-id="47e20-130">Aby mohli vývojáři získat lépe přizpůsobenou nápovědu, můžou využít výhody podpory MPN nebo Premier Support.</span><span class="sxs-lookup"><span data-stu-id="47e20-130">To get more personalized help, developers can use their MPN support benefits or Premier Support.</span></span>

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a><span data-ttu-id="47e20-131">Připojení k programu pro uživatele rozhraní API a sady SDK pro Partnerské centrum v rané fázi</span><span class="sxs-lookup"><span data-stu-id="47e20-131">Join the Partner Center API and SDK Early Adopter Program</span></span>

<span data-ttu-id="47e20-132">Pokud chcete zjistit, jak můžete s Microsoftem spolupracovat na vývoji partnerských funkcí a možností, podívejte se [do části zapojení rozhraní API partnerského centra a programu SDK pro včasnou](early-adopter-program.md)verzi.</span><span class="sxs-lookup"><span data-stu-id="47e20-132">To find out how you can collaborate with Microsoft on the development of Partner features and capabilities, see [Join the Partner Center API and SDK Early Adopter Program](early-adopter-program.md).</span></span>
