---
title: Možnosti izolovaného prostoru pro vztah prodejce
description: Partner izolovaného prostoru (sandbox) má schopnost podporovat vztahy mezi partnerem a zákazníkem.
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: aa6c4fb9ef71bacfad7e0f1510fec15f6af60a05
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547389"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a><span data-ttu-id="0c6ce-103">Možnosti izolovaného prostoru pro vztah prodejce</span><span class="sxs-lookup"><span data-stu-id="0c6ce-103">Sandbox capabilities for Reseller relationship</span></span>

<span data-ttu-id="0c6ce-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0c6ce-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0c6ce-105">Tento článek vysvětluje, co je podporováno v izolovaném prostoru (sandbox) pro vztahy prodejců mezi partnerem a zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-105">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0c6ce-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0c6ce-106">Prerequisites</span></span>

- <span data-ttu-id="0c6ce-107">Přihlašovací údaje účtu partnerského centra</span><span class="sxs-lookup"><span data-stu-id="0c6ce-107">Partner Center account credentials.</span></span> <span data-ttu-id="0c6ce-108">Scénář izolovaného prostoru (sandbox) podporuje ověřování jak pro samostatnou aplikaci, tak i pro přihlašovací údaje uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-108">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="0c6ce-109">ID zákazníka (Customer-tenant-ID).</span><span class="sxs-lookup"><span data-stu-id="0c6ce-109">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="0c6ce-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard/home)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="0c6ce-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0c6ce-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0c6ce-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="0c6ce-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0c6ce-114">ID společnosti Microsoft je stejné jako ID zákazníka (Customer-tenant-ID).</span><span class="sxs-lookup"><span data-stu-id="0c6ce-114">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="0c6ce-115">Před odstraněním zákazníka z karantény integrace s tipem se musí zrušit všechny nákupní objednávky Azure Reserved Virtual Machine Instances a softwaru.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-115">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="0c6ce-116">Scénáře podporující vztah prodejce</span><span class="sxs-lookup"><span data-stu-id="0c6ce-116">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="0c6ce-117">Partneři izolovaného prostoru (sandboxu) a nepřímá poskytovatelé můžou vytvářet relace s zákazníkem izolovaného prostoru.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-117">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="0c6ce-118">Partneři izolovaného prostoru (sandboxu) a nepřímá poskytovatelé můžou pozvat zákazníky izolovaného prostoru</span><span class="sxs-lookup"><span data-stu-id="0c6ce-118">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>

3. <span data-ttu-id="0c6ce-119">Partner s přímým přístupem k izolovanému prostoru a nepřímá poskytovatelé můžou odebrat vztah prodejce z uživatelského rozhraní a rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-119">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="0c6ce-120">V izolovaném prostoru odeberte vztah prodejce, který bude volat odstranění přístupového bodu zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-120">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="0c6ce-121">Tato akce odebere vztah a odstraní tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-121">This will remove the relationship and delete the customer tenant.</span></span> <span data-ttu-id="0c6ce-122">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="0c6ce-122">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>


    ### <a name="in-the-sandbox"></a><span data-ttu-id="0c6ce-123">V izolovaném prostoru</span><span class="sxs-lookup"><span data-stu-id="0c6ce-123">In the Sandbox</span></span>

    <span data-ttu-id="0c6ce-124">**Partneři s přímým účtováním**:</span><span class="sxs-lookup"><span data-stu-id="0c6ce-124">**Direct bill partners**:</span></span>

    - <span data-ttu-id="0c6ce-125">Může přidat existující zákazníky.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-125">Can add existing customers</span></span>

    - <span data-ttu-id="0c6ce-126">Vztahy s novými zákazníky nejde vyžádat.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-126">Cannot request relationships with new customers</span></span>

    <span data-ttu-id="0c6ce-127">**Nepřímí zprostředkovatelé**:</span><span class="sxs-lookup"><span data-stu-id="0c6ce-127">**Indirect providers**:</span></span>

    - <span data-ttu-id="0c6ce-128">Může přidat existující zákazníky.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-128">Can add existing customers</span></span>

    - <span data-ttu-id="0c6ce-129">Vztahy s novými zákazníky nejde vyžádat.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-129">Cannot request relationships with new customers</span></span>

    - <span data-ttu-id="0c6ce-130">Nemůže mít relaci s nepřímým prodejcem.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-130">Cannot have a relationship with an Indirect reseller</span></span>

    <span data-ttu-id="0c6ce-131">**Nepřímý prodejce**:</span><span class="sxs-lookup"><span data-stu-id="0c6ce-131">**Indirect reseller**:</span></span> 

    -   <span data-ttu-id="0c6ce-132">Můžou mít relace s existujícími zákazníky.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-132">Can have relationships with existing customers</span></span>

    -   <span data-ttu-id="0c6ce-133">Nejde požádat o nové relace ani přidat nové zákazníky.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-133">Cannot request new relationships or add new customers</span></span>

    ### <a name="in-partner-center"></a><span data-ttu-id="0c6ce-134">V partnerském centru</span><span class="sxs-lookup"><span data-stu-id="0c6ce-134">In Partner Center</span></span>

    <span data-ttu-id="0c6ce-135">**Partneři s přímým účtováním**:</span><span class="sxs-lookup"><span data-stu-id="0c6ce-135">**Direct bill partners**:</span></span>

    -   <span data-ttu-id="0c6ce-136">Může přidat nové zákazníky.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-136">Can add new customers</span></span>

    -   <span data-ttu-id="0c6ce-137">Může vyžádat vztahy s novými zákazníky.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-137">Can request relationships with new customers</span></span>

    <span data-ttu-id="0c6ce-138">**Nepřímí zprostředkovatelé**:</span><span class="sxs-lookup"><span data-stu-id="0c6ce-138">**Indirect providers**:</span></span>

    -   <span data-ttu-id="0c6ce-139">Může přidat nové zákazníky.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-139">Can add new customers</span></span>

    -   <span data-ttu-id="0c6ce-140">Může vyžádat vztahy s novými zákazníky.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-140">Can request relationships with new customers</span></span>

    -   <span data-ttu-id="0c6ce-141">Může mít relace s nepřímými prodejci</span><span class="sxs-lookup"><span data-stu-id="0c6ce-141">Can have relationships with indirect resellers</span></span>

    <span data-ttu-id="0c6ce-142">**Nepřímí prodejci**:</span><span class="sxs-lookup"><span data-stu-id="0c6ce-142">**Indirect resellers**:</span></span>

    -   <span data-ttu-id="0c6ce-143">Nejde přidat nové zákazníky.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-143">Can’t add new customers</span></span>

    -   <span data-ttu-id="0c6ce-144">Může vyžádat vztahy s novými zákazníky.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-144">Can request relationships with new customers</span></span>


<span data-ttu-id="0c6ce-145">Podrobnější informace pro zákazníka získáte pomocí [vztahu odebrat prodejce](remove-a-reseller-relationship-with-a-customer.md) .</span><span class="sxs-lookup"><span data-stu-id="0c6ce-145">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="0c6ce-146">Existují však určité rozdíly mezi funkcemi produktu a izolovaného prostoru (sandbox).</span><span class="sxs-lookup"><span data-stu-id="0c6ce-146">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0c6ce-147">SYNTAXE ŽÁDOSTI</span><span class="sxs-lookup"><span data-stu-id="0c6ce-147">REQUEST SYNTAX</span></span>

|<span data-ttu-id="0c6ce-148">**Metoda**</span><span class="sxs-lookup"><span data-stu-id="0c6ce-148">**Method**</span></span>|<span data-ttu-id="0c6ce-149">**Odstranit**</span><span class="sxs-lookup"><span data-stu-id="0c6ce-149">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="0c6ce-150">Odstranit</span><span class="sxs-lookup"><span data-stu-id="0c6ce-150">Delete</span></span>|<span data-ttu-id="0c6ce-151">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="0c6ce-151">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="0c6ce-152">Tělo žádosti není žádné</span><span class="sxs-lookup"><span data-stu-id="0c6ce-152">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0c6ce-153">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="0c6ce-153">Response success and error codes</span></span>

<span data-ttu-id="0c6ce-154">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0c6ce-155">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="0c6ce-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0c6ce-156">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](./error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0c6ce-156">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c6ce-157">Další kroky</span><span class="sxs-lookup"><span data-stu-id="0c6ce-157">Next steps</span></span>

- [<span data-ttu-id="0c6ce-158">Aktivovat předplatná izolovaného prostoru pro Azure Marketplace produkty</span><span class="sxs-lookup"><span data-stu-id="0c6ce-158">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="0c6ce-159">Zrušení objednávky z izolovaného prostoru</span><span class="sxs-lookup"><span data-stu-id="0c6ce-159">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="0c6ce-160">Testování a ladění</span><span class="sxs-lookup"><span data-stu-id="0c6ce-160">Test and debug</span></span>](test-and-debug.md)