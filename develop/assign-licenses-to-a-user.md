---
title: Přiřazení licencí uživateli
description: Naučte se, jak přiřadit licence uživateli zákazníka prostřednictvím rozhraní API partnerského centra, jako je například použití \# rozhraní API jazyka C nebo REST.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6eb0b953b9157e48074415bb3207e2946cfb2ab4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/13/2020
ms.locfileid: "97767087"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a><span data-ttu-id="8f68b-103">Přiřazení licencí uživateli prostřednictvím partnerských rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="8f68b-103">Assign licenses to a user via Partner Center APIs</span></span>

<span data-ttu-id="8f68b-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="8f68b-104">**Applies to:**</span></span>

- <span data-ttu-id="8f68b-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="8f68b-105">Partner Center</span></span>

<span data-ttu-id="8f68b-106">Jak přiřadit licence uživateli zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8f68b-106">How to assign licenses to a customer user.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f68b-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8f68b-107">Prerequisites</span></span>

- <span data-ttu-id="8f68b-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8f68b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8f68b-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="8f68b-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="8f68b-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8f68b-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8f68b-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="8f68b-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8f68b-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="8f68b-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8f68b-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="8f68b-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8f68b-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="8f68b-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8f68b-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8f68b-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8f68b-116">Identifikátor uživatele zákazníka</span><span class="sxs-lookup"><span data-stu-id="8f68b-116">A customer user identifier.</span></span> <span data-ttu-id="8f68b-117">Toto ID identifikuje uživatele, kterému chcete přiřadit licenci.</span><span class="sxs-lookup"><span data-stu-id="8f68b-117">This ID identifies the user to whom to assign the license.</span></span>

- <span data-ttu-id="8f68b-118">Identifikátor SKU produktu, který identifikuje produkt pro licenci.</span><span class="sxs-lookup"><span data-stu-id="8f68b-118">A product SKU identifier that identifies the product for the license.</span></span>

## <a name="assigning-licenses-through-code"></a><span data-ttu-id="8f68b-119">Přiřazování licencí prostřednictvím kódu</span><span class="sxs-lookup"><span data-stu-id="8f68b-119">Assigning licenses through code</span></span>

<span data-ttu-id="8f68b-120">Když přiřadíte licence uživateli, musíte si vybrat z kolekce předplatitelů předplatných SKU zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8f68b-120">When you assign licenses to a user, you must choose from the customer's collection of subscribed SKUs.</span></span> <span data-ttu-id="8f68b-121">Po identifikaci produktů, které chcete přiřadit, musíte získat ID SKU produktu pro každý produkt, aby bylo možné provést přiřazení.</span><span class="sxs-lookup"><span data-stu-id="8f68b-121">Then, having identified the products that you want to assign, you must obtain the product SKU ID for each product in order to make the assignments.</span></span> <span data-ttu-id="8f68b-122">Každá instance [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) obsahuje vlastnost [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) , ze které můžete odkazovat na objekt [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) a získat [**ID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).</span><span class="sxs-lookup"><span data-stu-id="8f68b-122">Each [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) instance contains a [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) property from which you can reference the [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) object and get the [**ID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).</span></span>

<span data-ttu-id="8f68b-123">Požadavek na přiřazení licence musí obsahovat licence z jedné skupiny licencí.</span><span class="sxs-lookup"><span data-stu-id="8f68b-123">A license assignment request must contain licenses from a single license group.</span></span> <span data-ttu-id="8f68b-124">Nemůžete například přiřadit licence z [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) a **skupina2** ve stejné žádosti.</span><span class="sxs-lookup"><span data-stu-id="8f68b-124">For example, you cannot assign licenses from [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) and **Group2** in the same request.</span></span> <span data-ttu-id="8f68b-125">Pokus o přiřazení licencí z více než jedné skupiny v rámci jedné žádosti se nezdaří s příslušnou chybou.</span><span class="sxs-lookup"><span data-stu-id="8f68b-125">An attempt to assign licenses from more than one group in a single request will fail with an appropriate error.</span></span> <span data-ttu-id="8f68b-126">Pokud chcete zjistit, jaké licence jsou k dispozici v rámci skupiny licencí, přečtěte si téma [získání seznamu dostupných licencí podle skupiny licencí](get-a-list-of-available-licenses-by-license-group.md).</span><span class="sxs-lookup"><span data-stu-id="8f68b-126">To find out what licenses are available by license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

<span data-ttu-id="8f68b-127">Tady je postup, jak přiřadit licence prostřednictvím kódu:</span><span class="sxs-lookup"><span data-stu-id="8f68b-127">Here are the steps to assign licenses through code:</span></span>

1. <span data-ttu-id="8f68b-128">Vytvořte instanci objektu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) .</span><span class="sxs-lookup"><span data-stu-id="8f68b-128">Instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object.</span></span> <span data-ttu-id="8f68b-129">Pomocí tohoto objektu určíte SKU produktu a plány služeb, které chcete přiřadit.</span><span class="sxs-lookup"><span data-stu-id="8f68b-129">You use this object to specify the product SKU and service plans to assign.</span></span>

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. <span data-ttu-id="8f68b-130">Naplňte vlastnosti objektu, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="8f68b-130">Populate the object properties as shown below.</span></span> <span data-ttu-id="8f68b-131">Tento kód předpokládá, že již máte ID SKU produktu a že budou přiřazeny všechny dostupné plány služeb (to znamená, že žádné nebudou vyloučeny).</span><span class="sxs-lookup"><span data-stu-id="8f68b-131">This code assumes that you already have the product SKU ID, and that all of the available service plans will be assigned (that is, none will be excluded).</span></span>

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. <span data-ttu-id="8f68b-132">Pokud nemáte ID SKU produktu, bude nutné načíst kolekci předplaceného SKU a získat ID SKU produktu z jednoho z nich.</span><span class="sxs-lookup"><span data-stu-id="8f68b-132">If you don't have the product SKU ID, you need to retrieve the collection of subscribed SKUs and get the product SKU ID from one of them.</span></span> <span data-ttu-id="8f68b-133">Tady je příklad, pokud znáte název SKU produktu.</span><span class="sxs-lookup"><span data-stu-id="8f68b-133">Here is an example if you know the product SKU name.</span></span>

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. <span data-ttu-id="8f68b-134">Dále vytvořte instanci nového seznamu typu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)a přidejte do něj objekt License.</span><span class="sxs-lookup"><span data-stu-id="8f68b-134">Next, instantiate a new list of type [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment), and add the license object.</span></span> <span data-ttu-id="8f68b-135">Můžete přiřadit více než jednu licenci tím, že je přidáte do seznamu jednotlivě.</span><span class="sxs-lookup"><span data-stu-id="8f68b-135">You can assign more than one license by adding each individually to the list.</span></span> <span data-ttu-id="8f68b-136">Licence zahrnuté v tomto seznamu musí být ze stejné skupiny licencí.</span><span class="sxs-lookup"><span data-stu-id="8f68b-136">The licenses included in this list must be from the same license group.</span></span>

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. <span data-ttu-id="8f68b-137">Vytvořte instanci [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) a přiřaďte seznam přiřazení licencí k vlastnosti [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .</span><span class="sxs-lookup"><span data-stu-id="8f68b-137">Create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. <span data-ttu-id="8f68b-138">Zavolejte metodu [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) a předejte objekt aktualizace licence, jak je znázorněno níže, aby bylo možné přiřadit licence.</span><span class="sxs-lookup"><span data-stu-id="8f68b-138">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object as shown below to assign the licenses.</span></span>

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a><span data-ttu-id="8f68b-139">C\#</span><span class="sxs-lookup"><span data-stu-id="8f68b-139">C\#</span></span>

<span data-ttu-id="8f68b-140">Chcete-li přiřadit licenci uživateli zákazníka, nejprve vytvořte instanci objektu [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) a naplňte vlastnosti [**skuId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) a [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) .</span><span class="sxs-lookup"><span data-stu-id="8f68b-140">To assign a license to a customer user, first instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object, and populate the [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) and [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) properties.</span></span> <span data-ttu-id="8f68b-141">Pomocí tohoto objektu určíte skladovou jednotku produktu, kterou chcete přiřadit, a plány služby, které se mají vyloučit.</span><span class="sxs-lookup"><span data-stu-id="8f68b-141">You use this object to specify the product SKU to assign and service plans to exclude.</span></span> <span data-ttu-id="8f68b-142">Dále vytvořte instanci nového seznamu typu **LicenseAssignment** a přidejte do seznamu objekt licence.</span><span class="sxs-lookup"><span data-stu-id="8f68b-142">Next, instantiate a new list of type **LicenseAssignment**, and add the license object to the list.</span></span> <span data-ttu-id="8f68b-143">Pak vytvořte instanci [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) a přiřaďte seznam přiřazení licencí k vlastnosti [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .</span><span class="sxs-lookup"><span data-stu-id="8f68b-143">Then create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

<span data-ttu-id="8f68b-144">Dále použijte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka k identifikaci zákazníka a metodu [**Users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID uživatele k identifikaci uživatele.</span><span class="sxs-lookup"><span data-stu-id="8f68b-144">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="8f68b-145">Pak z vlastnosti [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) Získejte rozhraní pro zákaznické operace aktualizace uživatelských licencí.</span><span class="sxs-lookup"><span data-stu-id="8f68b-145">Then get an interface to customer user license update operations from the [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) property.</span></span>

<span data-ttu-id="8f68b-146">Nakonec voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) a předáním objektu aktualizace licence přiřaďte licenci.</span><span class="sxs-lookup"><span data-stu-id="8f68b-146">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object to assign the license.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerUserId;
// string selectedCustomerId;
// string selectedProductSkuId;

// Instantiate and populate a LicenseAssignment object.
LicenseAssignment license = new LicenseAssignment();
license.SkuId = selectedProductSkuId;
license.ExcludedPlans = null;

// Instantiate a list of licenses to assign and add the license to it.
List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
licenseList.Add(license);

// Instantiate a LicenseUpdate object and add the list of licenses to assign.
LicenseUpdate updateLicense = new LicenseUpdate();
updateLicense.LicensesToAssign = licenseList;

// Update the user licenses.
var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
```

<span data-ttu-id="8f68b-147">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8f68b-147">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8f68b-148">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: CustomerUserAssignLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="8f68b-148">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8f68b-149">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="8f68b-149">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8f68b-150">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="8f68b-150">Request syntax</span></span>

| <span data-ttu-id="8f68b-151">Metoda</span><span class="sxs-lookup"><span data-stu-id="8f68b-151">Method</span></span>   | <span data-ttu-id="8f68b-152">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="8f68b-152">Request URI</span></span>                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8f68b-153">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="8f68b-153">**POST**</span></span> | <span data-ttu-id="8f68b-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenseupdates HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8f68b-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="8f68b-155">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="8f68b-155">URI parameters</span></span>

<span data-ttu-id="8f68b-156">K identifikaci zákazníka a uživatele použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="8f68b-156">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="8f68b-157">Název</span><span class="sxs-lookup"><span data-stu-id="8f68b-157">Name</span></span>        | <span data-ttu-id="8f68b-158">Typ</span><span class="sxs-lookup"><span data-stu-id="8f68b-158">Type</span></span>   | <span data-ttu-id="8f68b-159">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8f68b-159">Required</span></span> | <span data-ttu-id="8f68b-160">Popis</span><span class="sxs-lookup"><span data-stu-id="8f68b-160">Description</span></span>                                       |
|-------------|--------|----------|---------------------------------------------------|
| <span data-ttu-id="8f68b-161">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="8f68b-161">customer-id</span></span> | <span data-ttu-id="8f68b-162">řetězec</span><span class="sxs-lookup"><span data-stu-id="8f68b-162">string</span></span> | <span data-ttu-id="8f68b-163">Yes</span><span class="sxs-lookup"><span data-stu-id="8f68b-163">Yes</span></span>      | <span data-ttu-id="8f68b-164">ID formátovaného identifikátoru GUID identifikující zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8f68b-164">A GUID formatted ID that identifies the customer.</span></span> |
| <span data-ttu-id="8f68b-165">user-id</span><span class="sxs-lookup"><span data-stu-id="8f68b-165">user-id</span></span>     | <span data-ttu-id="8f68b-166">řetězec</span><span class="sxs-lookup"><span data-stu-id="8f68b-166">string</span></span> | <span data-ttu-id="8f68b-167">Yes</span><span class="sxs-lookup"><span data-stu-id="8f68b-167">Yes</span></span>      | <span data-ttu-id="8f68b-168">ID formátované identifikátorem GUID, které uživatele identifikuje.</span><span class="sxs-lookup"><span data-stu-id="8f68b-168">A GUID formatted ID that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="8f68b-169">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="8f68b-169">Request headers</span></span>

<span data-ttu-id="8f68b-170">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8f68b-170">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8f68b-171">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="8f68b-171">Request body</span></span>

<span data-ttu-id="8f68b-172">Do textu žádosti zadejte prostředek [LicenseUpdate](license-resources.md#licenseupdate) , který určuje, jaké licence se mají přiřadit.</span><span class="sxs-lookup"><span data-stu-id="8f68b-172">Include a [LicenseUpdate](license-resources.md#licenseupdate) resource in the request body that specifies the licenses to assign.</span></span>

### <a name="request-example"></a><span data-ttu-id="8f68b-173">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="8f68b-173">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/554526aa-cf5e-46fa-95df-98dbc55d8a1e/licenseupdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 183
Expect: 100-continue

{
    "LicensesToAssign": [{
            "ExcludedPlans": null,
            "SkuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "LicensesToRemove": null,
    "LicenseWarnings": null,
    "Attributes": {
        "ObjectType": "LicenseUpdate"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="8f68b-174">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="8f68b-174">REST response</span></span>

<span data-ttu-id="8f68b-175">V případě úspěchu se vrátí stavový kód odpovědi HTTP 201 a tělo odpovědi obsahuje prostředek [LicenseUpdate](license-resources.md#licenseupdate) s informacemi o licenci.</span><span class="sxs-lookup"><span data-stu-id="8f68b-175">If successful, an HTTP response status code 201 is returned and the response body contains a [LicenseUpdate](license-resources.md#licenseupdate) resource with the license information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8f68b-176">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="8f68b-176">Response success and error codes</span></span>

<span data-ttu-id="8f68b-177">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="8f68b-177">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8f68b-178">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="8f68b-178">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8f68b-179">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8f68b-179">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="8f68b-180">Příklad odpovědi (úspěch)</span><span class="sxs-lookup"><span data-stu-id="8f68b-180">Response example (success)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 139
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CV: 5AnzcZQrvUqCq3kd.0
MS-ServerId: 030020525
Date: Thu, 20 Apr 2017 21:50:39 GMT

{
    "licensesToAssign": [{
            "skuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "licenseWarnings": [],
    "attributes": {
        "objectType": "LicenseUpdate"
    }
}
```

### <a name="response-example-license-isnt-available"></a><span data-ttu-id="8f68b-181">Příklad odpovědi (licence není k dispozici)</span><span class="sxs-lookup"><span data-stu-id="8f68b-181">Response example (license isn't available)</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 341
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: f4f3b748-8b22-4d07-a5a1-dceb32824192
MS-CV: 5npA0K22CUmWPOzB.0
MS-ServerId: 102030524
Date: Thu, 20 Apr 2017 22:12:36 GMT

{
    "code": 60012,
    "description": "We&#39;re sorry, it looks like you've run out of licenses. Buy more licenses, and then try again.",
    "data": ["LicenseQuotaExceededException : Subscription with Account 0c39d6d5-c70d-4c55-bc02-f620844f3fd1 and SKU f8a1db68-be16-40ed-86d5-cb42ce701560 does not have any available licenses left."],
    "source": "PartnerFD"
}
```
