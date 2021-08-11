---
title: Nákup položek katalogu
description: Jak zakoupit položky katalogu pomocí rozhraní API partnerského centra
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 34560ceff2721a805d50cd4bf0702f6e7cf6f473db3f38ee52ea439b7355b786
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997330"
---
# <a name="purchase-catalog-items"></a>Nákup položek katalogu

Následující scénář ukazuje obecný proces nákupu položek z katalogu pomocí rozhraní API partnerského centra.

## <a name="discovery"></a>Zjišťování

Vyberte produkty a skladové jednotky (SKU) a ověřte jejich dostupnost pomocí následujících modelů rozhraní API partnerského centra:

- [Produkt](product-resources.md#product) – seskupovací konstrukce pro kupní zboží nebo služby. Produkt sám o sobě není položkou, která je k nákupu.
- [SKU](product-resources.md#sku) – skladová SKU v rámci produktu. Tyto prvky jsou znázorněny v různých tvarech produktu.
- [Dostupnost](product-resources.md#availability) – konfigurace, v níž je k DISpozici SKU k nákupu (například země, měna a odvětví).

Pokud chcete položku zakoupit z katalogu, proveďte následující kroky:

1. Identifikujte a načtěte produkt a SKU, které chcete koupit.

   - [Získat seznam produktů](get-a-list-of-products.md)
   - [Získat produkt s použitím ID produktu](get-a-product-by-id.md)
   - [Získat seznam SKU pro produkt](get-a-list-of-skus-for-a-product.md)
   - [Získání SKU pomocí ID SKU](get-a-sku-by-id.md)

2. Zkontroluje inventář SKU. Tento krok je potřeba jenom pro skladové položky, které jsou označené hodnotou **InventoryCheck** ve vlastnosti [purchasePrerequisites](product-resources.md#sku) .

   - [Kontrola inventáře](check-inventory.md)

3. Načtěte [dostupnost](product-resources.md#availability) pro [skladovou](product-resources.md#sku)položku. Při zadávání objednávky budete potřebovat **CatalogItemIdi** dostupnosti. Chcete-li získat tuto hodnotu, použijte jednu z následujících rozhraní API:

   - [Získat seznam dostupnosti pro SKU](get-a-list-of-availabilities-for-a-sku.md)
   - [Získání dostupnosti pomocí ID dostupnosti](get-an-availability-by-id.md)

## <a name="order-submission"></a>Odeslání objednávky

Chcete-li odeslat své pořadí položek katalogu, postupujte následovně:

1. Vytvořte [košík](cart-resources.md) pro uložení kolekce položek katalogu, které máte v úmyslu koupit. Při vytváření košíku se [položky řádku vozíku](cart-resources.md#cartlineitem) automaticky seskupují podle toho, co se dá koupit společně ve stejném [pořadí](order-resources.md).

   - [Vytvoření nákupního košíku](create-a-cart.md)
   - [Aktualizace nákupního košíku](update-a-cart.md)

2. Podívejte se na košík. Při rezervaci vozíku dojde k vytvoření [objednávky](order-resources.md).

   - [Rezervace košíku](checkout-a-cart.md)

## <a name="get-order-details"></a>Získat podrobnosti objednávky

Podrobnosti o jednotlivých objednávkách můžete načíst pomocí ID objednávky nebo získat seznam objednávek pro zákazníka. Mezi časem odeslání objednávky a jejím zobrazením v seznamu objednávek zákazníka nastane zpoždění až 15 minut.

- Podrobnosti o jednotlivých objednávkách pomocí ID objednávek získáte v tématu [získání objednávky podle ID](get-an-order-by-id.md) .

- V tématu [získání všech objednávek zákazníka](get-all-of-a-customer-s-orders.md) získáte seznam objednávek pro zákazníka pomocí zákaznického ID.

- V tématu [získání seznamu objednávek podle zákazníka a fakturačního cyklu](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) můžete získat seznam objednávek pro zákazníka podle [typu fakturačního cyklu](product-resources.md#billingcycletype) , což vám umožní vypsat objednávky položek katalogu (jednorázové poplatky) a roční nebo měsíční Fakturované objednávky samostatně.

## <a name="lifecycle-management"></a>Správa životního cyklu

V rámci správy životního cyklu položek katalogu v partnerském centru můžete načíst informace o vašich [nárokech](entitlement-resources.md)na položky katalogu a získat podrobnosti o rezervacích pomocí ID objednávky rezervace. Příklady toho, jak to udělat, najdete v tématu [získání nároků](get-a-collection-of-entitlements.md).   

## <a name="invoice-and-reconciliation"></a>Faktura a odsouhlasení

V následujících scénářích se dozvíte, jak programově zobrazit [faktury](invoice-resources.md)zákazníka a získat bilanci a souhrny účtů, které zahrnují jednorázové poplatky za katalogové položky.

### <a name="balance-and-payment"></a>Zůstatek a platba

Pokud chcete získat aktuální zůstatek k účtu ve vašem výchozím typu měny, který je saldem poplatků za periodické i jednorázové (položky katalogu), podívejte se na téma [získání aktuálního zůstatku účtu](get-the-reseller-s-current-account-balance.md).

### <a name="multi-currency-balance-and-payment"></a>Zůstatek a platba na více měn

K získání aktuálního zůstatku účtu a shromáždění souhrnů faktury, které obsahují souhrn faktury s pravidelným i jednorázovým poplatkem pro každý typ měny vašeho zákazníka, najdete informace v tématu [získání souhrnů faktury](get-invoice-summaries.md).

### <a name="invoices"></a>Faktury

Chcete-li získat kolekci faktur, které zobrazují jak opakované, tak jednorázové poplatky, přečtěte si téma [získání kolekce faktur](get-a-collection-of-invoices.md). 

### <a name="single-invoice"></a>Jedna faktura

Pokud chcete načíst konkrétní fakturu pomocí ID faktury, přečtěte si téma [získání faktury podle ID](get-invoice-by-id.md).  

### <a name="reconciliation"></a>Párován

Chcete-li získat kolekci podrobností o položce řádku faktury (položky řádku odsouhlasení) pro konkrétní ID faktury, přečtěte si téma [získání položek řádků faktury](get-invoiceline-items.md).  

### <a name="download-an-invoice-as-a-pdf"></a>Stažení faktury jako PDF

Chcete-li načíst výpis faktury ve formátu PDF pomocí ID faktury, přečtěte si téma [získání výpisu faktury](get-invoice-statement.md).
