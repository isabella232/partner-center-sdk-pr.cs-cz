---
title: Vytvoření plánu Azure
description: Vývojáři můžou prostřednictvím rozhraní API partnerského centra koupit, vytvořit a spravovat plány Azure.
ms.date: 01/02/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: mowrim
ms.author: mowrim
ms.openlocfilehash: 372b94ac7217899ca560cf943bf11a7e8906872d
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766856"
---
# <a name="create-an-azure-plan"></a>Vytvoření plánu Azure

**Platí pro:**

* Partnerské centrum

Plán Azure můžete koupit, vytvořit a spravovat pomocí rozhraní API partnerského centra. Tento proces je podobný jako při vytváření předplatného Microsoft Azure (MS-AZR-0145P). Musíte [získat položku katalogu pro plán Azure](#get-the-catalog-item-for-azure-plan)a pak [vytvořit a odeslat objednávku](#create-and-submit-an-order).

## <a name="prerequisites"></a>Požadavky

* Přihlašovací údaje pro [ověření partnerského centra](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.
* Identifikátor zákazníka. Pokud nemáte identifikátor zákazníka, postupujte podle kroků v části [získání seznamu zákazníků](get-a-list-of-customers.md). Případně se přihlaste do partnerského centra, vyberte zákazníka ze seznamu zákazníků, vyberte možnost **účet** a uložte své **ID společnosti Microsoft**.
* [Potvrzení souhlasu zákazníka s zákaznickou smlouvou Microsoftu](/partner-center/confirm-customer-agreement).

## <a name="get-the-catalog-item-for-azure-plan"></a>Získat položku katalogu pro plán Azure

Než budete moct vytvořit plán Azure pro zákazníka, musíte načíst odpovídající položku katalogu. Můžete načíst položku katalogu pomocí stávajících rozhraní API katalogu pro partnerský Center s následujícími modely prostředků.

* **[Produkt](product-resources.md#product)**: seskupovací konstrukce pro kupní zboží nebo služby. Produkt sám o sobě není položka, která je k nákupu.
* **[SKU](product-resources.md#sku)**: kupní jednotka (SKU) na skladě v rámci produktu. SKU reprezentují různé tvary produktu.
* **[Dostupnost](product-resources.md#availability)**: konfigurace, ve které je k DISpozici SKU k nákupu (například země, Měna nebo odvětví odvětví).

Pokud chcete získat položku katalogu pro plán Azure, proveďte následující kroky:

1. Identifikujte a načtěte identifikátor *produktu* pro plán Azure. Postupujte podle kroků v části [získání seznamu produktů](get-a-list-of-products.md) a zadání **targetView** jako **MicrosoftAzure**. (Pokud už znáte identifikátor *produktu* pro plán Azure, můžete místo toho použít postup v části [získání produktu pomocí ID produktu](get-a-product-by-id.md) .)

2. Načtěte **SKU** z produktu pro plán Azure. Postupujte podle kroků v části [získání seznamu SKU pro produkt](get-a-list-of-skus-for-a-product.md). Pokud už znáte identifikátor SKU pro plán Azure, můžete místo toho postupovat podle kroků v části [získání SKU pomocí ID SKU](get-a-sku-by-id.md) .

3. Načtěte **dostupnost** z SKU pro plán Azure. Postupujte podle kroků v části [získání seznamu dostupnosti pro skladovou](get-a-list-of-availabilities-for-a-sku.md)položku. Pokud už znáte identifikátor potřebné dostupnosti, můžete místo toho postupovat podle kroků v části [získání dostupnosti pomocí ID dostupnosti](get-an-availability-by-id.md) . *Nezapomeňte si poznamenat hodnotu vlastnosti **CatalogItemId** dostupnosti pro plán Azure. Tuto hodnotu budete potřebovat k vytvoření objednávky.*

## <a name="create-and-submit-an-order"></a>Vytvoření a odeslání objednávky

K odeslání objednávky plánu Azure použijte tento postup:

1. [Vytvořte košík](create-a-cart.md) pro uložení kolekce položek katalogu, které máte v úmyslu koupit. Při vytváření [košíku](cart-resources.md#cart)se [položky řádku vozíku](cart-resources.md#cartlineitem) automaticky seskupují podle toho, co se dá koupit společně ve stejném [pořadí](order-resources.md#order). (Můžete také [Aktualizovat košík](update-a-cart.md).)

2. [Podívejte se na košík](checkout-a-cart.md), který má za následek vytvoření [objednávky](order-resources.md#order).

## <a name="get-order-details"></a>Získat podrobnosti objednávky

[Pomocí ID objednávky můžete načíst podrobnosti o jednotlivých objednávkách](get-an-order-by-id.md). Můžete také [načíst seznam všech objednávek pro konkrétního zákazníka](get-all-of-a-customer-s-orders.md).

>[!NOTE]
>Po odeslání objednávky dojde k prodlevě až 15 minut, než se objednávka objeví v seznamu objednávek zákazníka.

## <a name="manage-azure-plans"></a>Správa plánů Azure

Po úspěšném zpracování objednávky se pro plán Azure vytvoří prostředek **odběru** partnerského centra. Pomocí následujících metod můžete spravovat prostředky **předplatného** partnerského centra pro správu plánu Azure:

* [Získání předplatných zákazníka](get-all-of-a-customer-s-subscriptions.md)
* [Získání seznamu předplatných podle objednávky](get-a-list-of-subscriptions-by-order.md)

Při vytvoření plánu Azure v partnerském centru se v Azure vytvoří taky odpovídající předplatné Azure Usage. Můžete také vytvořit další předplatná Azure v rámci stejného plánu Azure pomocí webu Azure Portal a rozhraní API Azure. Identifikátory všech předplatných Azure, které jsou přidružené k plánu Azure, můžete získat podle kroků v části [získání seznamu oprávnění Azure pro předplatné partnerského centra](get-a-list-of-azure-entitlements-for-subscription.md) .

## <a name="lifecycle-management"></a>Správa životního cyklu

Stávající plán Azure můžete pozastavit pomocí postupu v části [pozastavení předplatného](suspend-a-subscription.md).

*Stávající plán Azure můžete pozastavit jenom v případě, že už k němu nejsou přidružené žádné aktivní prostředky využití, včetně předplatných Azure a rezervací Azure.*

Podrobnosti o tom, jak zakázat odběry využití Azure, najdete v tématu [Azure API při správě životního cyklu předplatného](/rest/api/resources/subscriptions).

Pokud chcete odebrat existující rezervace Azure, musíte [Zrušit rezervace](/partner-center/azure-reservations-manage#cancel-or-exchange-a-reservation).
Po pozastavení plánu Azure ho můžete znovu aktivovat.

Podrobnosti o tom, jak znovu aktivovat plán Azure, najdete v tématu [Opětovná aktivace pozastaveného předplatného](reactivate-a-suspended-a-subscription.md) .

## <a name="transition-existing-csp-offers-to-azure-plan"></a>Převod stávajících nabídek CSP na plán Azure

Pro stávajícího zákazníka s předplatným Microsoft Azure (MS-AZR-0145P) nemůžete vytvořit plán Azure. V novém komerčním prostředí v programu CSP v Partnerském centru však můžete [zákazníka převést ze stávajících nabídek Azure CSP na služby Azure v rámci plánu Azure](/partner-center/azure-plan-transition). Pokud chcete převést stávajícího zákazníka, použijte rozhraní API pro upgrade produktů a postupujte následovně:

* [Zkontrolujte, jestli je zákazník způsobilý k přechodu na plán Azure](get-eligibility-for-product-upgrade.md).
* [Zahajte pro zákazníka upgrade produktu](create-product-upgrade-entity.md).
* [Zkontrolujte stav upgradu produktu](get-product-upgrade-status.md).

## <a name="azure-spending"></a>Útrata v Azure

Můžete sledovat [výdaje na Azure](azure-spending.md) pomocí dotazů na shrnutí využití a podrobné záznamy o využití pomocí následujících metod:

* [Získání souhrnu využití pro partnera](get-a-partner-usage-summary.md)
* [Získání všech záznamů o zákaznickém využití pro partnera](get-a-customer-s-usage-records.md)
* [Získání souhrnu zákaznického využití](get-a-customer-usage-summary.md)
* [Získání všech záznamů o využití předplatných pro zákazníka](get-a-customer-subscription-s-usage-records.md)
* [Získání souhrnu využití předplatných](get-a-customer-subscription-usage-summary.md)
* [Získat data o využití pro předplatné podle prostředku](get-a-customer-subscription-resource-usage-records.md)
* [Získání dat o využití pro předplatné podle měřiče](get-a-customer-subscription-meter-usage-records.md)
* [Získání prostředků záznamů o využití měřičů](meter-usage-resources.md)
* [Získání prostředků záznamů o využití prostředků](resource-usage-resources.md)

Můžete také nastavit a spravovat rozpočty využití zákazníka pomocí následujících metod:

* [Získání rozpočtu zákaznického využití](get-a-customer-s-usage-spending-budget.md)
* [Aktualizace rozpočtu zákaznického využití](update-a-customer-s-usage-spending-budget.md)

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
