---
title: Koupit nové služby založené na licencích pro Commerce
description: Vývojáři mohou pomocí rozhraní API partnerského centra zakoupit, vytvořit a spravovat nové služby založené na licencích pro obchodní licence.
ms.date: 02/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: dd3aebdb0a670449d3a39f67fc2ad6c7ef8df8e5
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457296"
---
# <a name="purchasing-new-commerce-license-based-services"></a>Nákup nových služeb založených na licencích pro Commerce

**Platí pro:**

* Partnerské centrum

> [!Note] 
> Nové obchodní změny jsou aktuálně k dispozici pouze partnerům, kteří jsou součástí M365/D365 New Commerce Experience Technical Preview.

Pomocí rozhraní API partnerského centra si můžete koupit, vytvořit a spravovat nové služby založené na licencování pro obchod s obchodními prostředími. Tento postup je podobný jako u nabídek Azure plánů a Marketplace.

## <a name="prerequisites"></a>Požadavky

* Přihlašovací údaje pro [ověření partnerského centra](partner-center-authentication.md) Nové prostředí pro obchod podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.
* Identifikátor zákazníka. Pokud nemáte identifikátor zákazníka, postupujte podle kroků v části [získání seznamu zákazníků](get-a-list-of-customers.md). Případně se přihlaste do partnerského centra, vyberte zákazníka ze seznamu zákazníků, vyberte možnost **účet** a uložte své **ID společnosti Microsoft**.
* [Potvrzení souhlasu zákazníka s zákaznickou smlouvou Microsoftu](/partner-center/confirm-customer-agreement).

## <a name="get-the-catalog-item-for-new-commerce-license-based-services"></a>Získat položku katalogu pro nové služby založené na licenci Commerce

Musíte načíst nové položky katalogu služeb založených na licencích pro Commerce. Načtěte položky katalogu pomocí stávajících rozhraní API pro katalog partnerských Center s následujícími modely prostředků:

* **[Produkt](product-resources.md#product)**: seskupovací konstrukce pro kupní zboží nebo služby. Produkt sám o sobě není položka, která je k nákupu.
* **[SKU](product-resources.md#sku)**: kupní jednotka (SKU) na skladě v rámci produktu. SKU reprezentují různé tvary produktu.
* **[Dostupnost](product-resources.md#availability)**: konfigurace, ve které je k DISpozici SKU k nákupu (například země, Měna nebo odvětví odvětví).

Chcete-li získat položky katalogu pro nové nabídky služeb založených na licencích pro obchodní licence:

1. Postupujte podle kroků v části [získání seznamu produktů](get-a-list-of-products.md) pro produkty a určete **targetView** jako **OnlineServices**. (Pokud už znáte identifikátor produktu pro nabídku, kterou chcete koupit, můžete místo toho použít postup v části [získání produktu pomocí ID produktu](get-a-product-by-id.md) .)

2. Načtěte **SKU** z produktu pro nabídku, kterou hledáte. Postupujte podle kroků v části [získání seznamu SKU pro produkt](get-a-list-of-skus-for-a-product.md). (Pokud už znáte identifikátor SKU požadované nabídky, můžete místo toho postupovat podle kroků v části [získání SKU pomocí ID SKU](get-a-sku-by-id.md) .)

3. Načte **dostupnost** z SKU pro nabídku. Různé nabídky podporují konkrétní výrazy. Některé skladové položky mají více než jednu dostupnost. Postupujte podle kroků v části [získání seznamu dostupnosti pro skladovou](get-a-list-of-availabilities-for-a-sku.md)položku. (Pokud už znáte identifikátor potřebné dostupnosti, můžete místo toho postupovat podle kroků v části [získání dostupnosti pomocí ID dostupnosti](get-an-availability-by-id.md) .) Nezapomeňte *si poznamenat hodnotu vlastnosti **CatalogItemId** dostupnosti pro tuto nabídku. Tuto hodnotu budete potřebovat k vytvoření objednávky*.

## <a name="create-and-submit-an-order"></a>Vytvoření a odeslání objednávky

K odeslání objednávky plánu Azure (včetně nových obchodních objednávek) použijte následující postup:

1. [Vytvořte košík](create-a-cart.md) pro uložení kolekce položek katalogu, které máte v úmyslu koupit. Při vytváření [košíku](cart-resources.md#cart)se [položky řádku vozíku](cart-resources.md#cartlineitem) automaticky seskupují podle toho, co se dá koupit společně ve stejném [pořadí](order-resources.md#order). (Můžete také [Aktualizovat košík](update-a-cart.md).)

2. [Podívejte se na košík](checkout-a-cart.md), který má za následek vytvoření [objednávky](order-resources.md#order).

## <a name="get-order-details"></a>Získat podrobnosti objednávky

[Pomocí ID objednávky můžete načíst podrobnosti o jednotlivých objednávkách](get-an-order-by-id.md). Můžete také [načíst seznam všech objednávek pro konkrétního zákazníka](get-all-of-a-customer-s-orders.md).

>[!NOTE]
>Po odeslání objednávky dojde k prodlevě až 15 minut, než se objednávka objeví v seznamu objednávek zákazníka. V současné době mohou partneři EU zakoupit jenom nové nabídky pro obchod: 1. Noví zákazníci 2. Stávající zákazníci, kteří nemají existující plán Azure, Marketplace, předplatné softwaru ani software v jiné měně, než je měna země partnera.

## <a name="manage-new-commerce-subscriptions"></a>Správa nových předplatných Commerce

Po úspěšném zpracování objednávky se pro plán Azure vytvoří prostředek **odběru** partnerského centra. Pomocí následujících metod můžete spravovat prostředky **předplatného** partnerského centra pro správu plánu Azure:

* [Získání předplatných zákazníka](get-all-of-a-customer-s-subscriptions.md)
* [Získání seznamu předplatných podle objednávky](get-a-list-of-subscriptions-by-order.md)

Existují rozdíly a nové funkce, které jsou specifické pro nové obchodování.

## <a name="invoice-and-reconciliation"></a>Faktura a odsouhlasení

Můžete spravovat faktury a data o odsouhlasení pomocí následujících metod:

* [Získání kolekce faktur](get-a-collection-of-invoices.md)
* [Získání odkazů na odhad faktury](get-invoice-estimate-links.md)
* [Získat fakturu podle ID](get-invoice-by-id.md)
* [Získání výkazů faktur](get-invoice-statement.md)
* [Získání přehledu faktur](get-invoice-summaries.md)
* [Získání fakturovaných řádkových položek spotřeby na faktuře](get-invoice-billed-consumption-lineitems.md)
* [Získání nefakturovaných řádkových položek spotřeby na faktuře](get-invoice-unbilled-consumption-lineitems.md)
* [Získat položky řádku rekognoskaci s fakturací](get-invoiceline-items.md)
* [Získání nefakturovaných řádkových položek odsouhlasení](get-invoice-unbilled-recon-lineitems.md)
