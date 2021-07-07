---
title: Vytvoření předplatného pro produkty z komerčního tržiště
description: Vývojáři můžou vytvořit a spravovat předplatné pro produkty z komerčního tržiště pomocí rozhraní API partnerského centra.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ae2e4b0a1ffa2e63e68864887093673e32079d9f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973362"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a>Vytvoření předplatného pro produkty z komerčního tržiště

Předplatné pro produkty komerčního tržiště můžete vytvořit pomocí rozhraní API partnerského centra. Musíte [získat seznam nabídek pro trh](#get-a-list-of-offers-for-a-market), [vytvořit a odeslat objednávku](#create-and-submit-an-order) pro předplatné komerčního tržiště a pak [načíst aktivační odkaz](#get-activation-link).

Můžete také [provádět správu životního cyklu](#lifecycle-management) a [spravovat faktury](#invoice-and-reconciliation) pro tyto odběry.

## <a name="prerequisites"></a>Požadavky

* Přihlašovací údaje pro [ověření partnerského centra](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.
* Identifikátor zákazníka. Pokud nemáte identifikátor zákazníka, postupujte podle kroků v části [získání seznamu zákazníků](get-a-list-of-customers.md). Případně se přihlaste do partnerského centra, vyberte zákazníka ze seznamu zákazníků, vyberte možnost **účet** a uložte své **ID společnosti Microsoft**.

## <a name="get-a-list-of-offers-for-a-market"></a>Získání seznamu nabídek pro trh

Dostupné nabídky pro trh můžete vyhledat pomocí následujících modelů rozhraní API partnerského centra:

* **[Produkt](product-resources.md#product)**: seskupovací konstrukce pro kupní zboží nebo služby. Produkt sám o sobě není položka, která je k nákupu.
* **[SKU](product-resources.md#sku)**: kupní jednotka (SKU) na skladě v rámci produktu. Tyto prvky jsou znázorněny v různých tvarech produktu.
* **[Dostupnost](product-resources.md#availability)**: konfigurace, ve které je k DISpozici SKU k nákupu (například země, Měna nebo odvětví odvětví).

Než zakoupíte rezervaci Azure, proveďte následující kroky:

1. Identifikujte a načtěte produkt a SKU, které chcete koupit. Pokud už znáte ID produktu a ID skladové položky, vyberte je.

    * [Získat seznam produktů](get-a-list-of-products.md)
    * [Získat produkt s použitím ID produktu](get-a-product-by-id.md)
    * [Získat seznam SKU pro produkt](get-a-list-of-skus-for-a-product.md)
    * [Získání SKU pomocí ID SKU](get-a-sku-by-id.md)

    > [!NOTE]
    > Produkty z komerčního tržiště můžete identifikovat jejich **ProductType** vlastností **"Azure"** a jejich vlastností **podtypu** **"SaaS"**.

2. Pokud jsou skladové jednotky označené **InventoryCheck** podmínkou, podívejte se na [inventář skladové](check-inventory.md)položky.

    > [!NOTE]
    > V tuto chvíli nejsou k dispozici žádné produkty z komerčního tržiště, které podporují kontrolu inventáře nebo jsou označené **InventoryCheck** požadavky.

3. Načtěte dostupnost pro SKLADOVOU položku. Při umísťování objednávky budete potřebovat **CatalogItemId** dostupnost, kterou můžete načíst prostřednictvím následujících rozhraní API:

    * [Získat seznam dostupnosti pro SKU](get-a-list-of-availabilities-for-a-sku.md)
    * [Získání dostupnosti pomocí ID dostupnosti](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a>Vytvoření a odeslání objednávky

K odeslání vaší objednávky rezervace Azure použijte tento postup:

1. [Vytvořte košík](create-a-cart.md) pro uložení kolekce položek katalogu, které máte v úmyslu koupit. Při vytváření [košíku](cart-resources.md#cart)se [položky řádku vozíku](cart-resources.md#cartlineitem) automaticky seskupují podle toho, co se dá koupit společně ve stejném [pořadí](order-resources.md#order). (Můžete také [Aktualizovat košík](update-a-cart.md).)
2. [Podívejte se na košík](checkout-a-cart.md), který má za následek vytvoření [objednávky](order-resources.md#order).

### <a name="get-order-details"></a>Získat podrobnosti objednávky

[Pomocí ID objednávky můžete načíst podrobnosti o jednotlivých objednávkách](get-an-order-by-id.md). Můžete také [načíst seznam všech objednávek pro konkrétního zákazníka](get-all-of-a-customer-s-orders.md).

> [!NOTE]
> Po odeslání objednávky dojde k prodlevě až 15 minut, než se objednávka objeví v seznamu objednávek zákazníka.

## <a name="get-activation-link"></a>Získat aktivační odkaz

Partner nebo zákazník musí aktivovat odběry Azure Marketplace produktů. Můžete [získat aktivační odkaz podle položky řádku objednávky](get-activation-link-by-order-line-item.md). Můžete taky [získat předplatné podle ID](get-a-subscription-by-id.md)a potom **vytvořit jeho vlastnost Links** a vytvořit tak aktivační odkaz.

## <a name="lifecycle-management"></a>Správa životního cyklu

Životní cyklus předplatných můžete spravovat na komerční produkty z webu Marketplace pomocí následujících metod:

* [Zrušení předplatného na komerčním marketplace](cancel-an-azure-marketplace-subscription.md)
* [Povolení nebo zakázání autorenew pro předplatné komerčního tržiště](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a>Správa množství

Množství předplatného komerčního tržiště musí být v mezích definovaných přiřazenými [SKU](product-resources.md#sku) (viz atributy **minimumQuantity** a **maximumQuantity** ). Pokud chcete aktualizovat množství předplatného komerčního tržiště, použijte tuto metodu:

* [Změna objemu předplatného](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a>Faktura a odsouhlasení

Pomocí následujících metod můžete spravovat [faktury](invoice-resources.md) zákazníků (včetně poplatků za předplatné z komerčních produktů na webu Marketplace):

* [Získat položky řádkové spotřeby pro komerční web na faktuře](get-invoice-billed-consumption-lineitems.md)
* [Získání odkazů na odhad faktury](get-invoice-estimate-links.md)
* [Získat faktury za položky na řádcích spotřeby na komerční web Marketplace](get-invoice-unbilled-consumption-lineitems.md)
* [Získat nefakturovatelné položky řádku odsouhlasení faktury](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a>Test pomocí účtu izolovaného prostoru pro integraci

V produkčním prostředí, po vytvoření odběru pro komerční produkty SaaS na webu Marketplace, je potřeba načíst přizpůsobený aktivační odkaz z partnerského centra a přejít na web vydavatele, aby se proces instalace dokončil. Fakturace předplatného se zahájí až po dokončení instalace.

V prostředí izolovaného prostoru (sandbox) CSP není k dispozici žádná integrace s nezávislými prodejci softwaru. Pokud se pokusíte načíst aktivační odkaz z partnerského centra, vrátí se fiktivní odkaz. Tento fiktivní odkaz nelze použít k dokončení procesu instalace na webu vydavatele. Pokud chcete pomocí účtu izolovaného prostoru (sandbox) testovat účtování předplatných do komerčních produktů SaaS na webu Marketplace, použijte k aktivaci předplatného následující metodu. Fakturace předplatného se zahájí po úspěšné aktivaci:

* [Aktivace předplatného izolovaného prostoru pro produkty z komerčního tržiště](activate-sandbox-subscription-azure-marketplace-products.md)

