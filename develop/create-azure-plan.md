---
title: Vytvoření plánu Azure
description: Vývojáři mohou plány Azure nakupovat, vytvářet a spravovat programově pomocí Partnerské centrum API.
ms.date: 07/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: mowrim
ms.author: mowrim
ms.openlocfilehash: b77b067c7eb150ab1ad9904915e87c3fc55c104a
ms.sourcegitcommit: 1fce45e6cafbc4c228042523ae28aac651a73757
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/23/2021
ms.locfileid: "114483054"
---
# <a name="create-an-azure-plan"></a>Vytvoření plánu Azure

Plán Azure můžete zakoupit, vytvořit a spravovat pomocí rozhraní PARTNERSKÉ CENTRUM API. Postup se podobá vytvoření předplatného Microsoft Azure[(MS-AZR-0145P).](https://go.microsoft.com/fwlink/p/?linkid=2164140) Musíte získat [položku katalogu pro plán Azure](#get-the-catalog-item-for-azure-plan)a pak vytvořit a odeslat [objednávku](#create-and-submit-an-order).

## <a name="prerequisites"></a>Požadavky

* [Partnerské centrum přihlašovací údaje](partner-center-authentication.md) pro ověřování. Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.
* Identifikátor zákazníka. Pokud identifikátor zákazníka nemáte, postupujte podle kroků v části [Získání seznamu zákazníků.](get-a-list-of-customers.md) Případně se přihlaste k Partnerské centrum, vyberte zákazníka ze seznamu zákazníků, vyberte Účet a pak uložte **jeho Microsoft ID**. 
* [Potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu](/partner-center/confirm-customer-agreement).

## <a name="get-the-catalog-item-for-azure-plan"></a>Získání položky katalogu pro plán Azure

Před vytvořením plánu Azure pro zákazníka musíte načíst odpovídající položku katalogu. Položku katalogu můžete načíst pomocí existujících rozhraní API Partnerské centrum katalogu s využitím následujících modelů prostředků.

* **[Produkt:](product-resources.md#product)** Seskupovací konstrukce pro nákup zboží nebo služeb. Samotný produkt není položka, kterou si můžete koupit.
* **[SKU:](product-resources.md#sku)** SKU (Purchasable Stock Keeping Unit) v rámci produktu. SKU představují různé tvary produktu.
* **[Dostupnost:](product-resources.md#availability)** Konfigurace, ve které je skladová položku k dispozici pro nákup (například země, měna nebo segment odvětví).

Pokud chcete získat položku katalogu pro plán Azure, proveďte následující kroky:

1. Identifikujte a *načtěte* identifikátor produktu pro plán Azure. Postupujte podle kroků v [části Získání seznamu produktů a](get-a-list-of-products.md) jako **targetView** zadejte **MicrosoftAzure.** (Pokud už identifikátor *produktu* pro plán Azure znáte, můžete místo toho postupovat podle kroků v části Získání produktu [pomocí ID](get-a-product-by-id.md) produktu.)

2. **Načtěte SKU** z produktu pro plán Azure. Postupujte podle kroků [v části Získání seznamu skladových položek pro produkt](get-a-list-of-skus-for-a-product.md). Pokud už znáte identifikátor SKU pro plán Azure, můžete místo toho postupovat podle kroků v části Získání SKU pomocí [ID SKU.](get-a-sku-by-id.md)

3. **Načtěte dostupnost** ze SKU pro plán Azure. Postupujte podle kroků [v části Získání seznamu dostupnosti pro SKU](get-a-list-of-availabilities-for-a-sku.md). Pokud už znáte identifikátor pro dostupnost, kterou potřebujete, můžete místo toho použít postup v části Získání dostupnosti [pomocí ID](get-an-availability-by-id.md) dostupnosti. *Nezapomeňte si poznamenat hodnotu vlastnosti **CatalogItemId** dostupnosti plánu Azure. Tuto hodnotu budete potřebovat k vytvoření objednávky.*

## <a name="create-and-submit-an-order"></a>Vytvoření a odeslání objednávky

Pokud chcete odeslat objednávku plánu Azure, postupujte takto:

1. [Vytvořte košík pro](create-a-cart.md) kolekci položek katalogu, které chcete koupit. Když vytvoříte [košík,](cart-resources.md#cart) [](cart-resources.md#cartlineitem) řádkové položky košíku se automaticky seskupí podle toho, co je možné zakoupit společně ve stejné [objednávce](order-resources.md#order). (Můžete také [aktualizovat košík.)](update-a-cart.md)

2. [Podívejte se na košík](checkout-a-cart.md), jehož výsledkem je vytvoření [objednávky](order-resources.md#order).

## <a name="get-order-details"></a>Získání podrobností objednávky

Podrobnosti o [jednotlivé objednávce můžete načíst pomocí ID objednávky](get-an-order-by-id.md). Můžete také [načíst seznam všech objednávek pro konkrétního zákazníka](get-all-of-a-customer-s-orders.md).

>[!NOTE]
>Po odeslané objednávce existuje zpoždění až 15 minut, než se objednávka objeví v seznamu objednávek tohoto zákazníka.

## <a name="manage-azure-plans"></a>Správa plánů Azure

Po úspěšném zpracování objednávky se pro  Partnerské centrum Azure vytvoří prostředek předplatného. Ke správě plánu Azure můžete použít následující Partnerské centrum **prostředků** předplatného:

* [Získání předplatných zákazníka](get-all-of-a-customer-s-subscriptions.md)
* [Získání seznamu předplatných podle objednávky](get-a-list-of-subscriptions-by-order.md)

Když se v Azure vytvoří plán Azure Partnerské centrum, vytvoří se v Azure také odpovídající předplatné využití Azure. Můžete také vytvořit další předplatná využití Azure v rámci stejného plánu Azure pomocí Azure Portal a rozhraní API Azure. Identifikátory všech předplatných využití Azure přidružených k plánu Azure můžete získat pomocí postupu v části Získání seznamu oprávnění Azure pro Partnerské centrum [předplatného.](get-a-list-of-azure-entitlements-for-subscription.md)

## <a name="lifecycle-management"></a>Správa životního cyklu

Existující plán Azure můžete pozastavit podle kroků v části [Pozastavení předplatného.](suspend-a-subscription.md)

*Stávající plán Azure můžete pozastavit pouze v případě, že už k tomuto plánu nejsou přidružené žádné aktivní prostředky využití, včetně předplatných využití Azure a rezervací Azure.*

Podrobnosti o tom, jak zakázat předplatná využití Azure, najdete v tématu [Azure API o správě životního cyklu předplatného.](/rest/api/resources/subscriptions)

Pokud chcete odebrat existující rezervace Azure, [musíte rezervace zrušit.](/partner-center/azure-reservations-manage#cancel-or-exchange-a-reservation)
Po pozastavení můžete plán Azure znovu aktivovat.

Podrobnosti o tom, jak znovu aktivovat plán Azure, najdete v tématu [Opětovná aktivace pozastaveného předplatného.](reactivate-a-suspended-a-subscription.md)

## <a name="transition-existing-csp-offers-to-azure-plan"></a>Převod stávajících nabídek CSP na plán Azure

Pro stávajícího zákazníka s předplatným Microsoft Azure (MS-AZR-0145P) nemůžete vytvořit plán Azure. V novém komerčním prostředí v programu CSP v Partnerském centru však můžete [zákazníka převést ze stávajících nabídek Azure CSP na služby Azure v rámci plánu Azure](/partner-center/azure-plan-transition). Pokud chcete převést stávajícího zákazníka, použijte rozhraní API pro upgrade produktů a postupujte následovně:

* [Zkontrolujte, jestli je zákazník způsobilý k přechodu na plán Azure](get-eligibility-for-product-upgrade.md).
* [Zahajte pro zákazníka upgrade produktu](create-product-upgrade-entity.md).
* [Zkontrolujte stav upgradu produktu](get-product-upgrade-status.md).

## <a name="azure-spending"></a>Útrata v Azure

Útratu [za Azure můžete sledovat](azure-spending.md) dotazem na souhrn využití a podrobné záznamy o využití pomocí následujících metod:

* [Získání souhrnu využití pro partnera](get-a-partner-usage-summary.md)
* [Získání všech záznamů o zákaznickém využití pro partnera](get-a-customer-s-usage-records.md)
* [Získání souhrnu zákaznického využití](get-a-customer-usage-summary.md)
* [Získání všech záznamů o využití předplatných pro zákazníka](get-a-customer-subscription-s-usage-records.md)
* [Získání souhrnu využití předplatných](get-a-customer-subscription-usage-summary.md)
* [Získat data o využití pro předplatné podle prostředku](get-a-customer-subscription-resource-usage-records.md)
* [Získání dat o využití pro předplatné podle měřiče](get-a-customer-subscription-meter-usage-records.md)
* [Získání prostředků záznamů o využití měřičů](meter-usage-resources.md)
* [Získání prostředků záznamů o využití prostředků](resource-usage-resources.md)

Rozpočet využití zákazníků můžete také nastavit a spravovat následujícími způsoby:

* [Získání rozpočtu zákaznického využití](get-a-customer-s-usage-spending-budget.md)
* [Aktualizace rozpočtu zákaznického využití](update-a-customer-s-usage-spending-budget.md)

## <a name="invoice-and-reconciliation"></a>Faktura a odsouhlasení

Faktury a data odsouhlasení můžete spravovat následujícími způsoby:

* [Získání kolekce faktur](get-a-collection-of-invoices.md)
* [Získání odkazů na odhad faktury](get-invoice-estimate-links.md)
* [Získání faktury podle ID](get-invoice-by-id.md)
* [Získání výkazů faktur](get-invoice-statement.md)
* [Získání přehledu faktur](get-invoice-summaries.md)
* [Získání fakturovaných řádkových položek spotřeby na faktuře](get-invoice-billed-consumption-lineitems.md)
* [Získání nefakturovaných řádkových položek spotřeby na faktuře](get-invoice-unbilled-consumption-lineitems.md)
* [Získání řádkovaných položek odsoustavy fakturovaných faktur](get-invoiceline-items.md)
* [Získání nefakturovaných řádkových položek odsouhlasení](get-invoice-unbilled-recon-lineitems.md)
