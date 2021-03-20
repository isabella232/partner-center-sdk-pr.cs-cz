---
title: Možnosti partnerského sandboxu, které podporují vztah s prodejci
description: Partner izolovaného prostoru (sandbox) má schopnost podporovat vztahy mezi partnerem a zákazníkem.
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: af46811b3615e1f904a9619de85b0aca7622490b
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711861"
---
# <a name="partner-sandbox-capabilities-that-support-reseller-relationship"></a><span data-ttu-id="05248-103">Možnosti partnerského sandboxu, které podporují vztah s prodejci</span><span class="sxs-lookup"><span data-stu-id="05248-103">Partner sandbox capabilities that support reseller relationship</span></span>

<span data-ttu-id="05248-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="05248-104">**Applies to:**</span></span>

- <span data-ttu-id="05248-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="05248-105">Partner Center</span></span>
- <span data-ttu-id="05248-106">Partnerské centrum provozované společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="05248-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="05248-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="05248-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="05248-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="05248-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="05248-109">Tento článek vysvětluje, co je podporováno v izolovaném prostoru (sandbox) pro vztahy prodejců mezi partnerem a zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="05248-109">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="05248-110">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="05248-110">Prerequisites</span></span>

- <span data-ttu-id="05248-111">Přihlašovací údaje účtu partnerského centra</span><span class="sxs-lookup"><span data-stu-id="05248-111">Partner Center account credentials.</span></span> <span data-ttu-id="05248-112">Scénář izolovaného prostoru (sandbox) podporuje ověřování jak pro samostatnou aplikaci, tak i pro přihlašovací údaje uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="05248-112">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="05248-113">ID zákazníka (Customer-tenant-ID).</span><span class="sxs-lookup"><span data-stu-id="05248-113">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="05248-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard/home)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="05248-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="05248-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="05248-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="05248-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="05248-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="05248-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="05248-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="05248-118">ID společnosti Microsoft je stejné jako ID zákazníka (Customer-tenant-ID).</span><span class="sxs-lookup"><span data-stu-id="05248-118">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="05248-119">Před odstraněním zákazníka z karantény integrace s tipem se musí zrušit všechny nákupní objednávky Azure Reserved Virtual Machine Instances a softwaru.</span><span class="sxs-lookup"><span data-stu-id="05248-119">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="05248-120">Scénáře podporující vztah prodejce</span><span class="sxs-lookup"><span data-stu-id="05248-120">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="05248-121">Partneři izolovaného prostoru (sandboxu) a nepřímá poskytovatelé můžou vytvářet relace s zákazníkem izolovaného prostoru.</span><span class="sxs-lookup"><span data-stu-id="05248-121">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="05248-122">Partneři izolovaného prostoru (sandboxu) a nepřímá poskytovatelé můžou pozvat zákazníky izolovaného prostoru</span><span class="sxs-lookup"><span data-stu-id="05248-122">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>



### <a name="in-the-sandbox"></a><span data-ttu-id="05248-123">V izolovaném prostoru</span><span class="sxs-lookup"><span data-stu-id="05248-123">In the Sandbox</span></span>

<span data-ttu-id="05248-124">**Partneři s přímým účtováním**:</span><span class="sxs-lookup"><span data-stu-id="05248-124">**Direct bill partners**:</span></span>

<span data-ttu-id="05248-125">• Může přidat existující zákazníky.</span><span class="sxs-lookup"><span data-stu-id="05248-125">•   Can add existing customers</span></span>

<span data-ttu-id="05248-126">• Nemůžou vyžádat relace s novými zákazníky.</span><span class="sxs-lookup"><span data-stu-id="05248-126">•   Cannot request relationships with new customers</span></span>

<span data-ttu-id="05248-127">**Nepřímí zprostředkovatelé**:</span><span class="sxs-lookup"><span data-stu-id="05248-127">**Indirect providers**:</span></span>

<span data-ttu-id="05248-128">• Může přidat existující zákazníky.</span><span class="sxs-lookup"><span data-stu-id="05248-128">•   Can add existing customers</span></span>

<span data-ttu-id="05248-129">• Nemůžou vyžádat relace s novými zákazníky.</span><span class="sxs-lookup"><span data-stu-id="05248-129">•   Cannot request relationships with new customers</span></span>

<span data-ttu-id="05248-130">• Nemůže mít relaci s nepřímým prodejcem</span><span class="sxs-lookup"><span data-stu-id="05248-130">•   Cannot have a relationship with an Indirect reseller</span></span>

<span data-ttu-id="05248-131">**Nepřímý prodejce**: (už brzy)</span><span class="sxs-lookup"><span data-stu-id="05248-131">**Indirect reseller**: (coming soon)</span></span>

<span data-ttu-id="05248-132">• Může mít relace s existujícími zákazníky.</span><span class="sxs-lookup"><span data-stu-id="05248-132">•   Can have a relationships with existing customers</span></span>

<span data-ttu-id="05248-133">• Nemůžete požádat o nové relace ani přidat nové zákazníky.</span><span class="sxs-lookup"><span data-stu-id="05248-133">•   Cannot request new relationships or add new customers</span></span>

### <a name="in-partner-center"></a><span data-ttu-id="05248-134">V partnerském centru</span><span class="sxs-lookup"><span data-stu-id="05248-134">In Partner Center</span></span>

<span data-ttu-id="05248-135">**Partneři s přímým účtováním**:</span><span class="sxs-lookup"><span data-stu-id="05248-135">**Direct bill partners**:</span></span>

<span data-ttu-id="05248-136">• Může přidat nové zákazníky.</span><span class="sxs-lookup"><span data-stu-id="05248-136">•   Can add new customers</span></span>

<span data-ttu-id="05248-137">• Může vyžádat relace s novými zákazníky</span><span class="sxs-lookup"><span data-stu-id="05248-137">•   Can request relationships with new customers</span></span>

<span data-ttu-id="05248-138">**Nepřímí zprostředkovatelé**:</span><span class="sxs-lookup"><span data-stu-id="05248-138">**Indirect providers**:</span></span>

<span data-ttu-id="05248-139">• Může přidat nové zákazníky.</span><span class="sxs-lookup"><span data-stu-id="05248-139">•   Can add new customers</span></span>

<span data-ttu-id="05248-140">• Může vyžádat relace s novými zákazníky</span><span class="sxs-lookup"><span data-stu-id="05248-140">•   Can request relationships with new customers</span></span>

<span data-ttu-id="05248-141">• Může mít relace s nepřímými prodejci.</span><span class="sxs-lookup"><span data-stu-id="05248-141">•   Can have relationships with indirect resellers</span></span>

<span data-ttu-id="05248-142">**Nepřímí prodejci**:</span><span class="sxs-lookup"><span data-stu-id="05248-142">**Indirect resellers**:</span></span>

<span data-ttu-id="05248-143">• Nemůžete přidávat nové zákazníky.</span><span class="sxs-lookup"><span data-stu-id="05248-143">•   Can’t add new customers</span></span>

<span data-ttu-id="05248-144">• Může vyžádat relace s novými zákazníky</span><span class="sxs-lookup"><span data-stu-id="05248-144">•   Can request relationships with new customers</span></span>

3. <span data-ttu-id="05248-145">Partner s přímým přístupem k izolovanému prostoru a nepřímá poskytovatelé můžou odebrat vztah prodejce z uživatelského rozhraní a rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="05248-145">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="05248-146">V izolovaném prostoru odeberte vztah prodejce, který bude volat odstranění přístupového bodu zákazníka.</span><span class="sxs-lookup"><span data-stu-id="05248-146">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="05248-147">Tato akce odebere vztah a odstraní tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="05248-147">This will remove the relationship as well as delete the customer tenant.</span></span> <span data-ttu-id="05248-148">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="05248-148">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>

<span data-ttu-id="05248-149">Podrobnější informace pro zákazníka získáte pomocí [vztahu odebrat prodejce](remove-a-reseller-relationship-with-a-customer.md) .</span><span class="sxs-lookup"><span data-stu-id="05248-149">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="05248-150">Existují však určité rozdíly mezi funkcemi produktu a izolovaného prostoru (sandbox).</span><span class="sxs-lookup"><span data-stu-id="05248-150">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="05248-151">SYNTAXE ŽÁDOSTI</span><span class="sxs-lookup"><span data-stu-id="05248-151">REQUEST SYNTAX</span></span>

|<span data-ttu-id="05248-152">**Metoda**</span><span class="sxs-lookup"><span data-stu-id="05248-152">**Method**</span></span>|<span data-ttu-id="05248-153">**Odstranit**</span><span class="sxs-lookup"><span data-stu-id="05248-153">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="05248-154">Odstranit</span><span class="sxs-lookup"><span data-stu-id="05248-154">Delete</span></span>|<span data-ttu-id="05248-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="05248-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="05248-156">Tělo žádosti není žádné</span><span class="sxs-lookup"><span data-stu-id="05248-156">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="05248-157">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="05248-157">Response success and error codes</span></span>

<span data-ttu-id="05248-158">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="05248-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="05248-159">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="05248-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="05248-160">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](./error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="05248-160">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="05248-161">Další kroky</span><span class="sxs-lookup"><span data-stu-id="05248-161">Next steps</span></span>

- [<span data-ttu-id="05248-162">Aktivovat předplatná izolovaného prostoru pro Azure Marketplace produkty</span><span class="sxs-lookup"><span data-stu-id="05248-162">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="05248-163">Zrušení objednávky z izolovaného prostoru</span><span class="sxs-lookup"><span data-stu-id="05248-163">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="05248-164">Testování a ladění</span><span class="sxs-lookup"><span data-stu-id="05248-164">Test and debug</span></span>](test-and-debug.md)