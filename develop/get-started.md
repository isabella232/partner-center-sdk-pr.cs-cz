---
title: Začínáme
description: Součástí SDK pro Partnerské centrum spravované rozhraní API a REST API pro partnery ke správě dat zákazníků, předplatných a objednávek.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b5d05f26d63574ef876519091dc1c33c05f36e25
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548749"
---
# <a name="get-started"></a><span data-ttu-id="d07b1-103">Začínáme</span><span class="sxs-lookup"><span data-stu-id="d07b1-103">Get started</span></span>

<span data-ttu-id="d07b1-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d07b1-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d07b1-105">Součástí SDK pro Partnerské centrum spravované rozhraní API a REST API pro partnery ke správě dat zákazníků, předplatných a objednávek.</span><span class="sxs-lookup"><span data-stu-id="d07b1-105">The Partner Center SDK includes a managed API and a REST API for partners to use to manage customer, subscription, and order data.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="d07b1-106">Získání kódu</span><span class="sxs-lookup"><span data-stu-id="d07b1-106">Get the code</span></span>

[<span data-ttu-id="d07b1-107">Stažení SDK pro Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="d07b1-107">Download the Partner Center SDK</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> <span data-ttu-id="d07b1-108">Přístup rozhraní API Partnerské centrum pro nepřímé prodejce není podporovaný scénář.</span><span class="sxs-lookup"><span data-stu-id="d07b1-108">API access to Partner Center for indirect resellers isn't a supported scenario.</span></span>

## <a name="determine-your-version-of-partner-center"></a><span data-ttu-id="d07b1-109">Určení verze Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="d07b1-109">Determine your version of Partner Center</span></span>

<span data-ttu-id="d07b1-110">Některé verze Partnerské centrum nemají k dispozici celou sadu SDK.</span><span class="sxs-lookup"><span data-stu-id="d07b1-110">Some versions of Partner Center do not have the entire SDK available.</span></span> <span data-ttu-id="d07b1-111">Další informace najdete v tématu [Vývoj pro Partnerské centrum pro národní cloud Microsoftu.](developing-for-partner-center-for-microsoft-national-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="d07b1-111">For more information, see [Developing for Partner Center for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).</span></span>

## <a name="get-the-samples"></a><span data-ttu-id="d07b1-112">Získání ukázek</span><span class="sxs-lookup"><span data-stu-id="d07b1-112">Get the samples</span></span>

<span data-ttu-id="d07b1-113">Další informace o fragmentech kódu jazyka C#, ukázkách REST a ukázkové aplikaci najdete v [Partnerské centrum ukázkách.](partner-center-samples.md)</span><span class="sxs-lookup"><span data-stu-id="d07b1-113">For more information about C# snippets, REST samples, and the sample app, see [Partner Center samples](partner-center-samples.md).</span></span>

## <a name="test-vs-production"></a><span data-ttu-id="d07b1-114">Test vs. production</span><span class="sxs-lookup"><span data-stu-id="d07b1-114">Test vs. production</span></span>

<span data-ttu-id="d07b1-115">Při počátečním psaní a testování kódu byste měli použít svůj účet sandboxu pro integraci (a odpovídající tokeny), aby se vám nechtěně neplatily nové poplatky, za které zodpovídá vaše společnost.</span><span class="sxs-lookup"><span data-stu-id="d07b1-115">While you are initially writing and testing your code, you should use your integration sandbox account (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying.</span></span> <span data-ttu-id="d07b1-116">Další informace o tomto testovacím prostředí najdete v tématu [Nastavení přístupu k rozhraní API v Partnerské centrum](set-up-api-access-in-partner-center.md).</span><span class="sxs-lookup"><span data-stu-id="d07b1-116">For more information about this testing environment, see [Set up API access in Partner Center](set-up-api-access-in-partner-center.md).</span></span>

<span data-ttu-id="d07b1-117">Po otestování vašeho řešení a jeho použití na účtech skutečných zákazníků budete muset tokeny aktualizovat, abyste mohli používat klientskou aplikaci a tajný klíč Azure AD, které odpovídají vašemu primárnímu Partnerské centrum účtu.</span><span class="sxs-lookup"><span data-stu-id="d07b1-117">When your solution is tested and ready to use on real customer accounts, you'll have to update your tokens so that you're using an Azure AD client app and secret that correspond to your Primary Partner Center account.</span></span>

<span data-ttu-id="d07b1-118">Tipy a návrhy týkající se testování a ladění, včetně dalších informací o TiP (Test-in-Production) a Sandboxu pro integraci, najdete v tématu Testování a [ladění.](test-and-debug.md)</span><span class="sxs-lookup"><span data-stu-id="d07b1-118">For tips and suggestions about testing and debugging, including more information about Test-in-Production (TiP) and the Integration Sandbox, see [Test and debug](test-and-debug.md).</span></span>

## <a name="configure-your-authentication"></a><span data-ttu-id="d07b1-119">Konfigurace ověřování</span><span class="sxs-lookup"><span data-stu-id="d07b1-119">Configure your authentication</span></span>

<span data-ttu-id="d07b1-120">Pokud chcete nakonfigurovat ověřování Azure AD, abyste mohli používat rozhraní API Partnerské centrum, podívejte se na [Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d07b1-120">To configure your Azure AD authentication so that you can use the Partner Center APIs, see [Partner Center authentication](partner-center-authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d07b1-121">Microsoft představuje zabezpečenou a škálovatelnou architekturu pro ověřování partnerů CSP (Cloud Solution Provider) a dodavatelů ovládacích panelů (CPV) prostřednictvím architektury Microsoft Azure multi-factor authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="d07b1-121">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>
<span data-ttu-id="d07b1-122">Partnerské centrum ověřování používá Azure AD a k použití Partnerské centrum API musíte správně nakonfigurovat nastavení ověřování.</span><span class="sxs-lookup"><span data-stu-id="d07b1-122">Partner Center uses Azure AD for authentication, and to use the Partner Center APIs you must configure your authentication settings correctly.</span></span>
>
> <span data-ttu-id="d07b1-123">Další informace najdete v tématu [Povolení zabezpečeného aplikačního modelu](enable-secure-app-model.md).</span><span class="sxs-lookup"><span data-stu-id="d07b1-123">For more information, see [Enable secure application model](enable-secure-app-model.md).</span></span>

## <a name="get-help"></a><span data-ttu-id="d07b1-124">Získání pomoci</span><span class="sxs-lookup"><span data-stu-id="d07b1-124">Get help</span></span>

<span data-ttu-id="d07b1-125">Partneři mohou získat podporu ve [skupině SDK pro Partnerské centrum Yammer .](https://go.microsoft.com/fwlink/p/?LinkID=717360)</span><span class="sxs-lookup"><span data-stu-id="d07b1-125">Partners can get support at the [Partner Center SDK Yammer group](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span></span> <span data-ttu-id="d07b1-126">K získání přizpůsobenější nápovědy můžou vývojáři využít výhody podpory MPN nebo Premier Support.</span><span class="sxs-lookup"><span data-stu-id="d07b1-126">To get more personalized help, developers can use their MPN support benefits or Premier Support.</span></span>

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a><span data-ttu-id="d07b1-127">Připojení k programu pro uživatele rozhraní API a sady SDK pro Partnerské centrum v rané fázi</span><span class="sxs-lookup"><span data-stu-id="d07b1-127">Join the Partner Center API and SDK Early Adopter Program</span></span>

<span data-ttu-id="d07b1-128">Informace o tom, jak můžete spolupracovat s Microsoftem na vývoji partnerských funkcí a možností, najdete v tématu Připojení k rozhraní API pro Partnerské centrum a programu pro včasné přijetí sady [SDK.](early-adopter-program.md)</span><span class="sxs-lookup"><span data-stu-id="d07b1-128">To find out how you can collaborate with Microsoft on the development of Partner features and capabilities, see [Join the Partner Center API and SDK Early Adopter Program](early-adopter-program.md).</span></span>
