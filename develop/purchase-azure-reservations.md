---
title: Nákup rezervací Azure
description: rezervace azure můžete koupit pro zákazníka pomocí rozhraní API partnerského centra prostřednictvím stávajícího předplatného Microsoft Azure (MS-AZR-0145P) nebo plánu Azure.
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0b9ce4a808ac12c32bd67888fc92808baeb0e575
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547763"
---
# <a name="purchase-azure-reservations"></a>Nákup rezervací Azure

**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud for US Government

k nákupu rezervace azure pro zákazníka pomocí rozhraní API partnerského centra musíte mít pro ně stávající předplatné Microsoft Azure (**AZR-0145P**) nebo plán Azure.

> [!NOTE]
> Rezervace Azure nejsou k dispozici na následujících trzích:
>
> | Nedostupné trhy            | Nedostupné trhy (pokračování...) | Nedostupné trhy (pokračování...)      |
> |--------------------------------|-----------------------------------|------------------------------------------|
> | Ostrovy Aland                  | Grónsko                         | Papua-Nová Guinea                         |
> | Americká Samoa                 | Grenada                           | Pitcairnovy ostrovy                         |
> | Andorra                        | Guadeloupe                        | Réunion                                  |
> | Anguilla                       | Guam                              | Ruská federace                       |
> | Antarktida                     | Guernsey                          | Saba                                     |
> | Antigua a Barbuda            | Guinea                            | Svatý Bartoloměj                         |
> | Aruba                          | Guinea-Bissau                     | Svatá Lucie                              |
> | Benin                          | Guyana                            | Svatý Martin (Francie)                             |
> | Bhútán                         | Haiti                             | Saint Pierre a Miquelon                |
> | Bonaire                        | Heardův ostrov a McDonaldovy ostrovy | Svatý Vincenc a Grenadiny         |
> | Bouvetův ostrov                  | Ostrov Man                       | Samoa                                    |
> | Brazílie                         | Jan Mayen                         | San Marino                               |
> | Britské indickooceánské území | Jersey                            | Svatý Tomáš a Princův ostrov                    |
> | Britské Panenské ostrovy         | Kiribati                          | Seychely                               |
> | Burkina Faso                   | Kosovo                            | Sierra Leone                             |
> | Burundi                        | Laos                              | Svatý Eustach                           |
> | Kambodža                       | Lesotho                           | Svatý Martin (Nizozemsko)                             |
> | Středoafrická republika       | Libérie                           | Šalamounovy ostrovy                          |
> | Čad                           | Madagaskar                        | Somálsko                                  |
> | Čína                          | Malawi                            | Jižní Georgie a Jižní Sandwichovy ostrovy |
> | Vánoční ostrov               | Maledivy                          | Jižní Súdán                              |
> | Kokosové ostrovy        | Mali                              | Svatá Helena, Ascension a Tristan da Cunha   |
> | Komory                        | Marshallovy ostrovy                  | Surinam                                 |
> | Kongo                          | Martinik                        | Špicberky                                 |
> | Konžská demokratická republika                    | Mauritánie                        | Svazijsko                                |
> | Cookovy ostrovy                   | Mayotte                           | Timor Leste                              |
> | Džibutsko                       | Mikronésie                        | Togo                                     |
> | Dominika                       | Montserrat                        | Tokelau                                  |
> | Rovníková Guinea              | Mosambik                        | Tonga                                    |
> | Eritrea                        | Myanmar                           | Ostrovy Turks a Caicos                 |
> | Falklandské ostrovy               | Nauru                             | Tuvalu                                   |
> | Francouzská Guyana                  | Nová Kaledonie                     | Odlené ostrovy USA                    |
> | Francouzská Polynésie               | Niger                             | Vanuatu                                  |
> | Francouzská jižní území    | Niue                              | Vatikán                             |
> | Gabon                          | Norfolk                    | Wallis a Futuna                        |
> | Gambie                         | Severní Mariany          | Jemen                                    |
> | Gibraltar                      | Palau                             | &nbsp;                                   |
>

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného pro aktivní předplatné Azure CSP nebo plán Azure.

## <a name="how-to-purchase-microsoft-azure-reservations"></a>Jak zakoupit Microsoft Azure rezervace

Jakmile najdete aktivní předplatné Azure CSP, ke které chcete přidat rezervaci Azure, pomocí následujících kroků ji zakupte:

1. [Povolení –](#enablement) Zaregistrujte aktivní předplatné Azure CSP, abyste jim umožnili nákup rezervací Azure.

2. [Zjišťování](#discovery) – Vyhledejte a vyberte produkty rezervací Azure a skladové jednotky (SKU), které chcete koupit, a zkontrolujte jejich dostupnost.

3. [Odeslání objednávky](#order-submission) – vytvořte nákupní košík s položkami v objednávce a odešlete ho.

4. [Získat podrobnosti objednávky](#get-order-details) – můžete zkontrolovat podrobnosti objednávky, všechny objednávky zákazníka nebo zobrazit objednávky podle typu fakturačního cyklu.

Po zakoupení rezervací Azure vám následující scénáře ukážou, jak spravovat jejich životní cyklus získáním informací o vašich nárocích na rezervace Azure a jak načíst výpisy zůstatků, faktury a souhrny faktur.

- [Správa životního cyklu](#lifecycle-management)
- [Faktura a odsouhlasení](#invoice-and-reconciliation)

## <a name="enablement"></a>Enablement

Povolení znamená přidružení stávajícího předplatného Microsoft Azure **(MS-AZR-0145P)** k rezervované instanci virtuálního počítače Azure registrací předplatného, aby bylo možné povolit rezervace Azure. Registrace je předpokladem pro nákup Azure Reserved VM Instances.

K podpoře následujících úloh se vyžaduje předplatné:

1. Pokud chcete zkontrolovat, jestli má zákazník nárok na nasazení prostředků, a Azure Reserved VM Instances v oblasti, nebo ne.

2. K zajištění priority kapacity pro nasazení v předplatném. To se vztahuje pouze na jeden obor Azure Reserved VM Instances s vybranou **možností priority** kapacity.

Jakmile najdete aktivní předplatné, ke které chcete přidat rezervaci Azure, musíte předplatné zaregistrovat, aby bylo pro rezervace Azure povolené. Pokud chcete zaregistrovat [existující prostředek předplatného,](subscription-resources.md) aby byl povolený pro objednávání rezervací Azure, podívejte se na stránku [Registrace předplatného.](register-a-subscription.md)

Po registraci předplatného byste měli zkontrolovat stav registrace a ověřit, že se proces registrace dokončil. Pokud to chcete udělat, podívejte [se na stránku Získání stavu registrace předplatného.](get-subscription-registration-status.md)

> [!NOTE]
> Při nákupu Microsoft Azure pro zákazníka s plánem Azure musíte nejprve zaregistrovat plán Azure. Podobně jako u předplatného **Microsoft Azure (MS-AZR-0145P)** je plán Azure reprezentovaný Partnerské centrum [předplatného.](subscription-resources.md) Proto můžete k registraci [](register-a-subscription.md) plánu Azure použít stejnou metodu registrace předplatného.

## <a name="discovery"></a>Zjišťování

Po povolení předplatného pro nákup rezervací Azure jste připraveni vybrat produkty a skladové položky a zkontrolovat jejich dostupnost pomocí následujících Partnerské centrum API:

- [Produkt](product-resources.md#product) – seskupovací konstrukce pro nákup zboží nebo služeb. Samotný produkt není položka, kterou je možné zakoupit.

- [SKU](product-resources.md#sku) – nákupní SKU v rámci produktu. Ty představují různé tvary produktu.

- [Dostupnost](product-resources.md#availability) – Konfigurace, ve které je skladová položku k dispozici pro nákup (například země, měna a segment odvětví).

Před nákupem rezervace Azure proveďte následující kroky:

1. Identifikujte a načtěte produkt a SKU, které chcete koupit. Můžete to udělat tak, že nejprve vy napíšete produkty a skladové položky, nebo pokud už znáte ID produktu a skladové položky, vyberte je.

   - [Získání seznamu produktů (podle země)](get-a-list-of-products.md)
   - [Získání produktu s použitím ID produktu](get-a-product-by-id.md)
   - [Získání seznamu skladových položek pro produkt (podle země)](get-a-list-of-skus-for-a-product.md)
   - [Získání SKU pomocí ID SKU](get-a-sku-by-id.md)

2. Zkontrolujte skladovou hodnotu skladové položky. Tento krok je nutný jenom pro skladové položky označené požadavkem **InventoryCheck.**

   - [Kontrola inventáře](check-inventory.md)

3. [Načtěte dostupnost](product-resources.md#availability) pro [SKU](product-resources.md#sku). Při zadávání objednávky budete potřebovat **CatalogItemId** dostupnosti. K získání této hodnoty použijte jedno z následujících rozhraní API:

   - [Získání seznamu dostupností pro skladovou položku (podle země)](get-a-list-of-availabilities-for-a-sku.md)
   - [Získání dostupnosti pomocí ID dostupnosti](get-an-availability-by-id.md)

> [!IMPORTANT]
> Každý Microsoft Azure rezervace má různé dostupnosti pro předplatné Microsoft Azure **(MS-AZR-0145P)** a plán Azure. Pokud chcete získat seznam produktů [(podle země)](get-a-list-of-products.md)nebo Získat seznam skladových položek [(SKU)](get-a-list-of-skus-for-a-product.md)pro produkt (podle země) nebo Získat seznam dostupnosti pro skladovou položku [(podle země),](get-a-list-of-availabilities-for-a-sku.md) které se vztahují pouze na plán Azure, zadejte parametr reservationScope=AzurePlan.

## <a name="order-submission"></a>Odeslání objednávky

Pokud chcete odeslat objednávku rezervace Azure, proveďte následující úlohy:

1. Vytvořte košík pro kolekci položek katalogu, které chcete koupit. Když vytvoříte košík, [](cart-resources.md#cartlineitem) [řádkové](cart-resources.md)položky košíku se automaticky seskupí podle toho, co je možné zakoupit společně ve stejné [objednávce](order-resources.md).

   - [Vytvoření nákupního košíku](create-a-cart.md)
   - [Aktualizace nákupního košíku](update-a-cart.md)

2. Podívejte se na košík. Kontrola košíku vede k vytvoření [objednávky](order-resources.md).

   - [Pokladna košíku](checkout-a-cart.md)

## <a name="get-order-details"></a>Získání podrobností objednávky

Po vytvoření objednávky rezervace Azure můžete načíst podrobnosti o jednotlivé objednávce pomocí ID objednávky nebo získat seznam objednávek pro zákazníka. Mezi časem odeslané objednávky a zobrazením v seznamu objednávek zákazníka je zpoždění až 15 minut.

- K získání podrobností o jednotlivé objednávce pomocí ID objednávky. Viz [získání objednávky podle ID](get-an-order-by-id.md).

- Chcete-li získat seznam objednávek pro zákazníka pomocí ID zákazníka. Viz [get all of a customer's orders](get-all-of-a-customer-s-orders.md).

- Pokud chcete získat seznam objednávek [](product-resources.md#billingcycletype) pro zákazníka podle typu fakturačního cyklu, což vám umožní samostatně zobrazit výpis objednávek rezervací Azure (jednoúčtové poplatky) a ročních nebo měsíčních fakturovaných objednávek. Viz získání [seznamu objednávek podle typu fakturačního cyklu a zákazníka.](get-a-list-of-orders-by-customer-and-billing-cycle-type.md)

## <a name="lifecycle-management"></a>Správa životního cyklu

V rámci správy životního cyklu rezervací Azure v Partnerské centrum můžete načíst informace [](entitlement-resources.md)o vašich nárocích za rezervaci Azure a získat podrobnosti o rezervacích pomocí ID objednávky rezervace. Příklady, jak to provést, najdete v tématu [Získání oprávnění](get-a-collection-of-entitlements.md).   

## <a name="invoice-and-reconciliation"></a>Faktura a odsouhlasení

Následující scénáře ukazují, jak programově zobrazit [](invoice-resources.md)faktury zákazníka a získat zůstatky a souhrny účtu, které zahrnují poplatky za rezervace Azure.

### <a name="balance-and-payment"></a>Zůstatek a platba

Pokud chcete získat aktuální zůstatek účtu ve výchozím typu měny, který je zůstatek na opakujících se i časových poplatcích (rezervace Azure), podívejte se na část Získání aktuálního zůstatku [účtu.](get-the-reseller-s-current-account-balance.md)

### <a name="multi-currency-balance-and-payment"></a>Zůstatek a platba ve více měnách

Pokud chcete získat zůstatek aktuálního účtu a kolekci souhrnů faktur obsahujících souhrn faktur s opakovanými i časovými poplatky pro jednotlivé typy měn zákazníka, podívejte se na část Získání souhrnů [faktur.](get-invoice-summaries.md)

### <a name="invoices"></a>Faktury

Pokud chcete získat kolekci faktur, které zobrazují opakované i jedno časové poplatky, podívejte se na část [Získání kolekce faktur.](get-a-collection-of-invoices.md) 

### <a name="single-invoice"></a>Jedna faktura

Pokud chcete načíst konkrétní fakturu pomocí ID faktury, podívejte se [na stránku Získání faktury podle ID](get-invoice-by-id.md).  

### <a name="reconciliation"></a>Odsouhlasení

Pokud chcete získat kolekci podrobností o řádkové položce faktury (položky řádku odsouhlasení) pro konkrétní ID faktury, podívejte se na část [Získání položek řádku faktury.](get-invoiceline-items.md)  

### <a name="download-an-invoice-as-a-pdf"></a>Stažení faktury ve formátu PDF

Pokud chcete načíst výpis faktury ve formuláři PDF pomocí ID faktury, podívejte se na [stránku Získání výpisu faktury.](get-invoice-statement.md)
