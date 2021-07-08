---
title: Provedení jednorázového nákupu
description: Použití rozhraní API partnerského centra pro jednorázovou koupi softwaru a rezervací produktů, jako jsou odběry softwaru, trvalá verze softwaru a rezervované instance virtuálních počítačů Azure.
ms.date: 10/09/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1ca2d5b7ad6ba1196d74a8cdb748ab808192d569
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548375"
---
# <a name="make-a-one-time-purchase"></a>Provedení jednorázového nákupu

**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud for US Government

Použití rozhraní API partnerského centra pro jednorázovou koupi softwaru a rezervací produktů, jako jsou odběry softwaru, trvalá verze softwaru a rezervované instance virtuálních počítačů Azure.

> [!NOTE]
> Odběry softwaru nejsou k dispozici na následujících trzích:
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
> | Francouzská Guyana                  | Nová Kaledonie                     | Odlehlé ostrovy USA                    |
> | Francouzská Polynésie               | Niger                             | Vanuatu                                  |
> | Francouzská jižní území    | Niue                              | Vatikán                             |
> | Gabon                          | Norfolk                    | Wallis a Futuna                        |
> | Gambie                         | Severní Mariany          | Jemen                                    |
> | Gibraltar                      | Palau                             | &nbsp;                                   |
>
&nbsp;
> [!NOTE]
> K nákupu trvalého softwaru je potřeba, abyste byli dřív kvalifikováni. Pokud chcete získat další informace, obraťte se na podporu.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="making-a-one-time-purchase"></a>Provedení jednorázového nákupu

Chcete-li provést jednorázové nákupy, použijte následující postup:

1. [Povolení](#enablement) – (jenom v případě rezervované instance virtuálního počítače Azure) zaregistrujete aktivní předplatné Azure CSP, abyste ho mohli zakoupit u svého rezervovaného produktu.

2. [Zjišťování](#discovery) – vyhledejte a vyberte produkty a SKU, které chcete koupit, a ověřte jejich dostupnost.

3. [Odeslání objednávky](#order-submission) – umožňuje vytvořit nákupní košík s položkami v objednávce a odeslat ho.

4. [Získat podrobnosti objednávky](#get-order-details) – Projděte si podrobnosti o objednávce, všech objednávkách pro zákazníka nebo zobrazení objednávky podle fakturačního cyklu.

Po provedení jednorázového nákupu vám v následujících scénářích ukážeme, jak spravovat životní cyklus svých produktů, a získat informace o vašich nárokech a o tom, jak získat výpisy zůstatků, faktury a souhrny faktur.

- [Správa životního cyklu](#lifecycle-management)

- [Faktura a odsouhlasení](#invoice-and-reconciliation)

## <a name="enablement"></a>Enablement

Jakmile identifikujete aktivní předplatné, ke kterému chcete přidat rezervovanou instanci virtuálního počítače Azure, musíte předplatné zaregistrovat, aby bylo povolené. Pokud chcete zaregistrovat stávající prostředek [předplatného](subscription-resources.md) , aby byl povolený, podívejte se na téma [registrace předplatného](register-a-subscription.md).

Po registraci předplatného byste měli ověřit, že je proces registrace dokončený, a to tak, že zkontroluje stav registrace. Tento krok najdete v tématu [získání stavu registrace předplatného](get-subscription-registration-status.md).

## <a name="discovery"></a>Zjišťování

Po povolení předplatného budete připraveni vybrat produkty a SKU a ověřit jejich dostupnost pomocí následujících modelů rozhraní API partnerského centra:

- [Produkt](product-resources.md#product) – seskupovací konstrukce pro kupní zboží nebo služby. Produkt sám o sobě není položkou, která je k nákupu.

- [SKU](product-resources.md#sku) – skladová jednotka (SKU), která je v rámci produktu kupní. SKU reprezentují různé tvary produktu.

- [Dostupnost](product-resources.md#availability) – konfigurace, v níž je k DISpozici SKU k nákupu (například země, měna a odvětví).

Před provedením jednorázového nákupu proveďte následující kroky:

1. Identifikujte a načtěte produkt a SKU, které chcete koupit. Tento krok můžete provést tak, že nejprve vydáte seznam Products a SKU, nebo pokud už znáte ID produktu a SKU, vyberte je.

   - [Získat seznam produktů](get-a-list-of-products.md)
   - [Získat produkt s použitím ID produktu](get-a-product-by-id.md)
   - [Získat seznam SKU pro produkt](get-a-list-of-skus-for-a-product.md)
   - [Získání SKU pomocí ID SKU](get-a-sku-by-id.md)

2. Zkontroluje inventář SKU. Tento krok je potřeba jenom pro skladové položky, které jsou označené předpokladem pro **InventoryCheck** .

   - [Kontrola inventáře](check-inventory.md)

3. Načtěte [dostupnost](product-resources.md#availability) pro [skladovou](product-resources.md#sku)položku. Při zadávání objednávky budete potřebovat **CatalogItemIdi** dostupnosti. Chcete-li získat tuto hodnotu, použijte jednu z následujících rozhraní API:

   - [Získat seznam dostupnosti pro SKU](get-a-list-of-availabilities-for-a-sku.md)
   - [Získání dostupnosti pomocí ID dostupnosti](get-an-availability-by-id.md)

## <a name="order-submission"></a>Odeslání objednávky

K odeslání objednávky použijte následující postup:

1. Vytvořte košík pro uložení kolekce položek katalogu, které máte v úmyslu koupit. Při vytváření [košíku](cart-resources.md)se [položky řádku vozíku](cart-resources.md#cartlineitem) automaticky seskupují podle toho, co se dá koupit společně ve stejném [pořadí](order-resources.md).

   - [Vytvoření nákupního košíku](create-a-cart.md)
   - [Aktualizace nákupního košíku](update-a-cart.md)

2. Podívejte se na košík. Při rezervaci vozíku dojde k vytvoření [objednávky](order-resources.md).

   - [Rezervace košíku](checkout-a-cart.md)

## <a name="get-order-details"></a>Získat podrobnosti objednávky

Po vytvoření objednávky můžete načíst podrobnosti o jednotlivých objednávkách pomocí ID objednávky nebo získat seznam objednávek pro zákazníka. Mezi časem odeslání objednávky a jejím zobrazením v seznamu objednávek zákazníka nastane zpoždění až 15 minut.

- Získat podrobnosti o jednotlivých objednávkách pomocí ID objednávky. Viz, [získání objednávky podle ID](get-an-order-by-id.md).

- Získat seznam objednávek pro zákazníka pomocí ID zákazníka. Přečtěte si téma [získání všech objednávek zákazníka](get-all-of-a-customer-s-orders.md).

- Chcete-li získat seznam objednávek pro zákazníka podle [fakturačního cyklu](product-resources.md#billingcycletype) , což vám umožní vypsat objednávky (jednorázové poplatky) a roční nebo měsíční Fakturované objednávky samostatně. Viz, [získání seznamu objednávek podle typu zákazník a fakturační cyklus](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Správa životního cyklu

V rámci správy životního cyklu jednorázových nákupů v partnerském centru můžete načíst informace o vašich [nárokech](entitlement-resources.md)a získat podrobnosti o rezervacích pomocí ID objednávky rezervace. Příklady toho, jak to udělat, najdete v tématu [získání nároků](get-a-collection-of-entitlements.md).

## <a name="invoice-and-reconciliation"></a>Faktura a odsouhlasení

V následujících scénářích se dozvíte, jak programově zobrazit [faktury](invoice-resources.md)zákazníka a získat zůstatky a souhrny účtu, které zahrnují jednorázové poplatky.

### <a name="balance-and-payment"></a>Zůstatek a platba

Pokud chcete získat aktuální zůstatek k účtu ve výchozím typu měny, který je zůstatkem pro periodické i jednorázové poplatky, přečtěte si téma [získání aktuálního zůstatku účtu](get-the-reseller-s-current-account-balance.md) .

### <a name="multi-currency-balance-and-payment"></a>Zůstatek a platba na více měn

K získání aktuálního zůstatku účtu a shromáždění souhrnů faktury, které obsahují souhrn faktury s pravidelným i jednorázovým poplatkem pro každý typ měny vašeho zákazníka, najdete informace v tématu [získání souhrnů faktury](get-invoice-summaries.md).

### <a name="invoices"></a>Faktury

Chcete-li získat kolekci faktur, které zobrazují jak opakující se, tak jednorázové časové poplatky, přečtěte si téma [získání kolekce faktur](get-a-collection-of-invoices.md).

### <a name="single-invoice"></a>Jedna faktura

Pokud chcete načíst konkrétní fakturu pomocí ID faktury, přečtěte si téma [získání faktury podle ID](get-invoice-by-id.md).

### <a name="reconciliation"></a>Párován

Chcete-li získat kolekci podrobností o položce řádku faktury (položky řádku odsouhlasení) pro konkrétní ID faktury, přečtěte si téma [získání položek řádků faktury](get-invoiceline-items.md).

### <a name="download-an-invoice-as-a-pdf"></a>Stažení faktury jako PDF

Pokud chcete načíst výpis faktury ve formuláři PDF pomocí ID faktury, podívejte se na [stránku Získání výpisu faktury.](get-invoice-statement.md)
