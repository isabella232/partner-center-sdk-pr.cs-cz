---
title: Možnosti sandboxu pro vztah prodejce
description: Partnerský sandbox může podporovat vztahy mezi partnerem a zákazníkem.
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9bef4a15685ebbdc2212988f5ac5724b946cfd54
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2021
ms.locfileid: "110243380"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a><span data-ttu-id="89705-103">Možnosti sandboxu pro vztah prodejce</span><span class="sxs-lookup"><span data-stu-id="89705-103">Sandbox capabilities for Reseller relationship</span></span>

<span data-ttu-id="89705-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="89705-104">**Applies to:**</span></span>

- <span data-ttu-id="89705-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="89705-105">Partner Center</span></span>
- <span data-ttu-id="89705-106">Partnerské centrum provozované společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="89705-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="89705-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="89705-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="89705-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="89705-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="89705-109">Tento článek vysvětluje, co sandbox podporuje pro vztahy prodejce mezi partnerem a zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="89705-109">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="89705-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="89705-110">Prerequisites</span></span>

- <span data-ttu-id="89705-111">Partnerské centrum přihlašovací údaje účtu.</span><span class="sxs-lookup"><span data-stu-id="89705-111">Partner Center account credentials.</span></span> <span data-ttu-id="89705-112">Scénář sandboxu podporuje ověřování pomocí samostatné aplikace i přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="89705-112">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="89705-113">ID zákazníka (customer-tenant-id)</span><span class="sxs-lookup"><span data-stu-id="89705-113">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="89705-114">Pokud ID zákazníka neznáme, můžete ho hledat na řídicím panelu Partnerské centrum [.](https://partner.microsoft.com/dashboard/home)</span><span class="sxs-lookup"><span data-stu-id="89705-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="89705-115">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="89705-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="89705-116">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="89705-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="89705-117">Na stránce Účtu zákazníka vyhledejte ID **Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="89705-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="89705-118">ID Microsoftu je stejné jako ID zákazníka (customer-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="89705-118">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="89705-119">Všechny Azure Reserved Virtual Machine Instances a nákupní objednávky softwaru se musí před odstraněním zákazníka z sandboxu integrace tipů zrušit.</span><span class="sxs-lookup"><span data-stu-id="89705-119">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="89705-120">Scénáře podporující vztah prodejce</span><span class="sxs-lookup"><span data-stu-id="89705-120">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="89705-121">Partneři s přímým vyúčtováním sandboxu a nepřímí poskytovatelé mohou vytvářet vztahy se zákazníkem sandboxu.</span><span class="sxs-lookup"><span data-stu-id="89705-121">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="89705-122">Partneři sandboxu s přímým vyúčtováním a nepřímí poskytovatelé nemohou pozvat zákazníky sandboxu.</span><span class="sxs-lookup"><span data-stu-id="89705-122">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>

3. <span data-ttu-id="89705-123">Partneři s přímým vyúčtováním sandboxu a nepřímí poskytovatelé zprostředkovatelé mohou odebrat vztah prodejce Partnerské centrum uživatelském rozhraní a rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="89705-123">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="89705-124">Sandbox Remove Reseller Relationship zavolá příkaz Delete customer AP (Odstranit přístupový bod zákazníka).</span><span class="sxs-lookup"><span data-stu-id="89705-124">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="89705-125">Tím odeberete relaci a odstraníte tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="89705-125">This will remove the relationship as well as delete the customer tenant.</span></span> <span data-ttu-id="89705-126">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="89705-126">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>


    ### <a name="in-the-sandbox"></a><span data-ttu-id="89705-127">V izolovaném prostoru</span><span class="sxs-lookup"><span data-stu-id="89705-127">In the Sandbox</span></span>

    <span data-ttu-id="89705-128">**Partneři s přímým účtováním**:</span><span class="sxs-lookup"><span data-stu-id="89705-128">**Direct bill partners**:</span></span>

    - <span data-ttu-id="89705-129">Může přidat existující zákazníky.</span><span class="sxs-lookup"><span data-stu-id="89705-129">Can add existing customers</span></span>

    - <span data-ttu-id="89705-130">Vztahy s novými zákazníky nejde vyžádat.</span><span class="sxs-lookup"><span data-stu-id="89705-130">Cannot request relationships with new customers</span></span>

    <span data-ttu-id="89705-131">**Nepřímí zprostředkovatelé**:</span><span class="sxs-lookup"><span data-stu-id="89705-131">**Indirect providers**:</span></span>

    - <span data-ttu-id="89705-132">Může přidat existující zákazníky.</span><span class="sxs-lookup"><span data-stu-id="89705-132">Can add existing customers</span></span>

    - <span data-ttu-id="89705-133">Vztahy s novými zákazníky nejde vyžádat.</span><span class="sxs-lookup"><span data-stu-id="89705-133">Cannot request relationships with new customers</span></span>

    - <span data-ttu-id="89705-134">Nemůže mít relaci s nepřímým prodejcem.</span><span class="sxs-lookup"><span data-stu-id="89705-134">Cannot have a relationship with an Indirect reseller</span></span>

    <span data-ttu-id="89705-135">**Nepřímý prodejce**:</span><span class="sxs-lookup"><span data-stu-id="89705-135">**Indirect reseller**:</span></span> 

    -   <span data-ttu-id="89705-136">Můžou mít relace s existujícími zákazníky.</span><span class="sxs-lookup"><span data-stu-id="89705-136">Can have a relationships with existing customers</span></span>

    -   <span data-ttu-id="89705-137">Nejde požádat o nové relace ani přidat nové zákazníky.</span><span class="sxs-lookup"><span data-stu-id="89705-137">Cannot request new relationships or add new customers</span></span>

    ### <a name="in-partner-center"></a><span data-ttu-id="89705-138">V partnerském centru</span><span class="sxs-lookup"><span data-stu-id="89705-138">In Partner Center</span></span>

    <span data-ttu-id="89705-139">**Partneři s přímým účtováním**:</span><span class="sxs-lookup"><span data-stu-id="89705-139">**Direct bill partners**:</span></span>

    -   <span data-ttu-id="89705-140">Může přidat nové zákazníky.</span><span class="sxs-lookup"><span data-stu-id="89705-140">Can add new customers</span></span>

    -   <span data-ttu-id="89705-141">Může vyžádat vztahy s novými zákazníky.</span><span class="sxs-lookup"><span data-stu-id="89705-141">Can request relationships with new customers</span></span>

    <span data-ttu-id="89705-142">**Nepřímí zprostředkovatelé**:</span><span class="sxs-lookup"><span data-stu-id="89705-142">**Indirect providers**:</span></span>

    -   <span data-ttu-id="89705-143">Může přidat nové zákazníky.</span><span class="sxs-lookup"><span data-stu-id="89705-143">Can add new customers</span></span>

    -   <span data-ttu-id="89705-144">Může vyžádat vztahy s novými zákazníky.</span><span class="sxs-lookup"><span data-stu-id="89705-144">Can request relationships with new customers</span></span>

    -   <span data-ttu-id="89705-145">Může mít relace s nepřímými prodejci</span><span class="sxs-lookup"><span data-stu-id="89705-145">Can have relationships with indirect resellers</span></span>

    <span data-ttu-id="89705-146">**Nepřímí prodejci**:</span><span class="sxs-lookup"><span data-stu-id="89705-146">**Indirect resellers**:</span></span>

    -   <span data-ttu-id="89705-147">Nejde přidat nové zákazníky.</span><span class="sxs-lookup"><span data-stu-id="89705-147">Can’t add new customers</span></span>

    -   <span data-ttu-id="89705-148">Může vyžádat vztahy s novými zákazníky.</span><span class="sxs-lookup"><span data-stu-id="89705-148">Can request relationships with new customers</span></span>


<span data-ttu-id="89705-149">Podrobnější informace pro zákazníka získáte pomocí [vztahu odebrat prodejce](remove-a-reseller-relationship-with-a-customer.md) .</span><span class="sxs-lookup"><span data-stu-id="89705-149">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="89705-150">Existují však určité rozdíly mezi funkcemi produktu a izolovaného prostoru (sandbox).</span><span class="sxs-lookup"><span data-stu-id="89705-150">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="89705-151">SYNTAXE ŽÁDOSTI</span><span class="sxs-lookup"><span data-stu-id="89705-151">REQUEST SYNTAX</span></span>

|<span data-ttu-id="89705-152">**Metoda**</span><span class="sxs-lookup"><span data-stu-id="89705-152">**Method**</span></span>|<span data-ttu-id="89705-153">**Odstranit**</span><span class="sxs-lookup"><span data-stu-id="89705-153">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="89705-154">Odstranit</span><span class="sxs-lookup"><span data-stu-id="89705-154">Delete</span></span>|<span data-ttu-id="89705-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="89705-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="89705-156">Tělo žádosti není žádné</span><span class="sxs-lookup"><span data-stu-id="89705-156">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="89705-157">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="89705-157">Response success and error codes</span></span>

<span data-ttu-id="89705-158">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="89705-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="89705-159">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="89705-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="89705-160">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](./error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="89705-160">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="89705-161">Další kroky</span><span class="sxs-lookup"><span data-stu-id="89705-161">Next steps</span></span>

- [<span data-ttu-id="89705-162">Aktivovat předplatná izolovaného prostoru pro Azure Marketplace produkty</span><span class="sxs-lookup"><span data-stu-id="89705-162">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="89705-163">Zrušení objednávky z izolovaného prostoru</span><span class="sxs-lookup"><span data-stu-id="89705-163">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="89705-164">Testování a ladění</span><span class="sxs-lookup"><span data-stu-id="89705-164">Test and debug</span></span>](test-and-debug.md)