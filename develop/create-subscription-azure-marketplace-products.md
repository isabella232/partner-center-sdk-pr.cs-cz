---
title: Vytvoření předplatného pro produkty komerčního marketplace
description: Vývojáři mohou vytvořit a spravovat předplatné pro produkty komerčního marketplace pomocí Partnerské centrum API.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7e7a4b96f509ae99cd4933963c04b0f660d7d76410ee86c31256c62b290f122f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991374"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a>Vytvoření předplatného pro produkty komerčního marketplace

Předplatné pro produkty komerčního marketplace můžete vytvořit pomocí Partnerské centrum API. Musíte získat [seznam nabídek](#get-a-list-of-offers-for-a-market)pro [](#create-and-submit-an-order) trh, vytvořit a odeslat objednávku pro předplatné komerčního marketplace a pak [načíst aktivační odkaz](#get-activation-link).

Můžete také provádět [správu životního cyklu a](#lifecycle-management) spravovat [faktury](#invoice-and-reconciliation) za tato předplatná.

## <a name="prerequisites"></a>Požadavky

* [Partnerské centrum přihlašovací údaje](partner-center-authentication.md) pro ověřování. Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.
* Identifikátor zákazníka. Pokud identifikátor zákazníka nemáte, postupujte podle kroků v části [Získání seznamu zákazníků.](get-a-list-of-customers.md) Případně se přihlaste k Partnerské centrum, v seznamu zákazníků vyberte zákazníka, vyberte Účet a pak uložte **jeho Microsoft ID**. 

## <a name="get-a-list-of-offers-for-a-market"></a>Získání seznamu nabídek pro trh

Dostupné nabídky pro trh můžete zkontrolovat pomocí následujících Partnerské centrum API:

* **[Produkt:](product-resources.md#product)** Seskupovací konstrukce pro nákup zboží nebo služeb. Samotný produkt není položka, kterou si můžete koupit.
* **[SKU:](product-resources.md#sku)** SKU (Purchasable Stock Keeping Unit) v rámci produktu. Ty představují různé tvary produktu.
* **[Dostupnost:](product-resources.md#availability)** Konfigurace, ve které je skladová položku k dispozici pro nákup (například země, měna nebo segment odvětví).

Než si zakoupíte rezervaci Azure, proveďte následující kroky:

1. Identifikujte a načtěte produkt a SKU, které chcete koupit. Pokud již znáte ID produktu a ID SKU, vyberte je.

    * [Získání seznamu produktů](get-a-list-of-products.md)
    * [Získání produktu s použitím ID produktu](get-a-product-by-id.md)
    * [Získání seznamu skladových položek pro produkt](get-a-list-of-skus-for-a-product.md)
    * [Získání SKU pomocí ID SKU](get-a-sku-by-id.md)

    > [!NOTE]
    > Produkty na komerčním marketplace můžete identifikovat podle jejich vlastnosti **ProductType** **hodnoty "Azure"** a jejich vlastnosti **SubType** **typu "SaaS".**

2. Pokud jsou skladové položky označené požadavkem **InventoryCheck,** zkontrolujte skladové položky [v inventáři.](check-inventory.md)

    > [!NOTE]
    > V tuto chvíli nejsou k dispozici žádné produkty komerčního marketplace, které podporují kontrolu inventáře nebo jsou označené požadavkem **InventoryCheck.**

3. Načtěte dostupnost pro SKU. Při zadávání objednávky budete potřebovat **CatalogItemId** dostupnosti, kterou můžete načíst prostřednictvím následujících rozhraní API:

    * [Získání seznamu dostupnosti pro SKU](get-a-list-of-availabilities-for-a-sku.md)
    * [Získání dostupnosti pomocí ID dostupnosti](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a>Vytvoření a odeslání objednávky

Pokud chcete odeslat objednávku rezervace Azure, postupujte takto:

1. [Vytvořte košík pro](create-a-cart.md) kolekci položek katalogu, které chcete koupit. Když vytvoříte [košík,](cart-resources.md#cart) [](cart-resources.md#cartlineitem) řádkové položky košíku se automaticky seskupí podle toho, co je možné zakoupit společně ve stejné [objednávce.](order-resources.md#order) (Můžete také [aktualizovat košík.)](update-a-cart.md)
2. [Podívejte se na košík](checkout-a-cart.md), jehož výsledkem je vytvoření [objednávky](order-resources.md#order).

### <a name="get-order-details"></a>Získání podrobností objednávky

Podrobnosti o [jednotlivé objednávce můžete načíst pomocí ID objednávky](get-an-order-by-id.md). Můžete také [načíst seznam všech objednávek pro konkrétního zákazníka](get-all-of-a-customer-s-orders.md).

> [!NOTE]
> Po odeslané objednávce existuje zpoždění až 15 minut, než se objednávka objeví v seznamu objednávek tohoto zákazníka.

## <a name="get-activation-link"></a>Získání odkazu na aktivaci

Partner nebo zákazník musí aktivovat předplatná pro Azure Marketplace produkty. Aktivační odkaz [můžete získat podle řádkové položky objednávky](get-activation-link-by-order-line-item.md). Můžete také získat [předplatné podle ID](get-a-subscription-by-id.md)  a pak vytvořit aktivační odkaz vytvořením výčtu jeho vlastnosti Links.

## <a name="lifecycle-management"></a>Správa životního cyklu

Životní cyklus předplatných produktů na komerčním marketplace můžete spravovat následujícími způsoby:

* [Zrušení předplatného na komerčním marketplace](cancel-an-azure-marketplace-subscription.md)
* [Povolení nebo zakázání funkce autoenew pro předplatné komerčního marketplace](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a>Správa množství

Množství předplatného komerčního marketplace musí být v mezích definovaných přidruženými [skladové](product-resources.md#sku) položky (viz atributy **minimumQuantity** a **maximumQuantity).** Pokud chcete aktualizovat množství předplatného komerčního marketplace, použijte následující metodu:

* [Změna objemu předplatného](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a>Faktura a odsouhlasení

Faktury zákazníků (včetně [poplatků za](invoice-resources.md) předplatná produktů na komerčním marketplace) můžete spravovat následujícími způsoby:

* [Získání fakturovaných řádkových položek spotřeby na komerčním marketplace](get-invoice-billed-consumption-lineitems.md)
* [Získání odkazů na odhad faktury](get-invoice-estimate-links.md)
* [Získání nefakturovaných řádkových položek spotřeby na komerčním marketplace](get-invoice-unbilled-consumption-lineitems.md)
* [Získání nevyfakturovaných řádových položek s vyrovnáním na faktuře](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a>Testování s využitím účtu sandboxu pro integraci

Po vytvoření předplatného produktů SaaS na komerčním marketplace musíte v produkčním prostředí načíst individuální aktivační odkaz ze služby Partnerské centrum a navštívit web vydavatele a dokončit proces nastavení. Fakturace předplatného začne až po dokončení nastavení.

V prostředí sandboxu CSP neexistuje žádná integrace s isvédy. Pokud se pokusíte načíst aktivační odkaz z Partnerské centrum, vrátí se fiktivní odkaz. Tento fiktivní odkaz nelze použít k dokončení procesu instalace na webu vydavatele. Pokud chcete účet sandboxu pro integraci použít k otestování fakturace předplatných na komerční marketplace produktů SaaS, použijte k aktivaci předplatného následující metodu. Fakturace předplatného začne po úspěšné aktivaci:

* [Aktivace předplatného sandboxu pro produkty komerčního marketplace](activate-sandbox-subscription-azure-marketplace-products.md)

