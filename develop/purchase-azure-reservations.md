---
title: Nákup rezervací Azure
description: Rezervace Azure můžete koupit pro zákazníka pomocí rozhraní API partnerského centra prostřednictvím stávajícího předplatného Microsoft Azure (MS-AZR-0145P) nebo plánu Azure.
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c09f65ae5105a74be41a7ec45824e3889217a1c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766745"
---
# <a name="purchase-azure-reservations"></a>Nákup rezervací Azure

**Platí pro:**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud for US Government

K nákupu rezervace Azure pro zákazníka pomocí rozhraní API partnerského centra musíte mít pro ně stávající předplatné Microsoft Azure (**AZR-0145P**) nebo plán Azure.

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
> | Francouzská Guyana                  | Nová Kaledonie                     | Odlehlé ostrovy USA                    |
> | Francouzská Polynésie               | Niger                             | Vanuatu                                  |
> | Francouzská jižní území    | Niue                              | Vatikán                             |
> | Gabon                          | Norfolk                    | Wallis a Futuna                        |
> | Gambie                         | Severní Mariany          | Jemen                                    |
> | Gibraltar                      | Palau                             | &nbsp;                                   |
>

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného pro aktivní předplatné Azure CSP nebo plán Azure.

## <a name="how-to-purchase-microsoft-azure-reservations"></a>Jak zakoupit Microsoft Azure rezervace

Jakmile zjistíte aktivní předplatné CSP Azure, ke kterému chcete přidat rezervaci Azure, použijte k nákupu následující postup:

1. [Povolení](#enablement) – umožňuje zaregistrovat aktivní předplatné Azure CSP a povolit ho pro nákup rezervací Azure.

2. [Zjišťování](#discovery) – vyhledejte a vyberte produkty rezervace Azure a skladové jednotky, které chcete koupit, a ověřte jejich dostupnost.

3. [Odeslání objednávky](#order-submission) – umožňuje vytvořit nákupní košík s položkami v objednávce a odeslat ho.

4. [Získat podrobnosti objednávky](#get-order-details) – Projděte si podrobnosti o objednávce, všech objednávkách pro zákazníka nebo zobrazení objednávky podle fakturačního cyklu.

Po zakoupení rezervacích Azure se v následujících scénářích dozvíte, jak spravovat životní cyklus tím, že získáte informace o vašich nárokech na rezervaci Azure a jak načíst výpisy zůstatků, faktury a souhrny faktur.

- [Správa životního cyklu](#lifecycle-management)
- [Faktura a odsouhlasení](#invoice-and-reconciliation)

## <a name="enablement"></a>Enablement

Povolení znamená přidružení stávajícího předplatného služby Microsoft Azure (**MS-AZR-0145P**) k rezervované instanci virtuálního počítače Azure pomocí registrace předplatného, aby bylo povoleno rezervace Azure. Registrace je předpokladem pro zakoupení Azure Reserved VM Instances.

Odběr je vyžadován z následujících důvodů:

1. Chcete-li zjistit, jestli má zákazník nárok na nasazení prostředků, a proto si Azure Reserved VM Instances koupit v nějaké oblasti.

2. Pro zajištění priority kapacity pro nasazení v rámci předplatného. To platí jenom pro jeden obor Azure Reserved VM Instances s vybranou možností **Priorita kapacity** .

Jakmile identifikujete aktivní předplatné, do kterého chcete přidat rezervaci Azure, musíte předplatné zaregistrovat, aby bylo povolené pro rezervace Azure. Pokud chcete zaregistrovat stávající prostředek [předplatného](subscription-resources.md) tak, aby byl povolen pro řazení rezervací Azure, přečtěte si téma [registrace předplatného](register-a-subscription.md).

Po registraci předplatného byste měli ověřit, že je proces registrace dokončený, a to tak, že zkontroluje stav registrace. Postup najdete v tématu [získání stavu registrace předplatného](get-subscription-registration-status.md).

> [!NOTE]
> Při nákupu Microsoft Azure rezervace pro zákazníka s plánem Azure je třeba nejprve zaregistrovat plán Azure. Podobně jako u předplatného služby Microsoft Azure (**MS-AZR-0145P**) je plán Azure reprezentován prostředkem [předplatného](subscription-resources.md) partnerského centra. Proto můžete použít stejnou [registraci metody předplatného](register-a-subscription.md) k registraci plánu Azure.

## <a name="discovery"></a>Zjišťování

Po povolení předplatného pro nákup rezervací Azure jste připraveni vybrat produkty a SKU a ověřit jejich dostupnost pomocí následujících modelů rozhraní API partnerského centra:

- [Produkt](product-resources.md#product) – seskupovací konstrukce pro kupní zboží nebo služby. Produkt sám o sobě není položkou, která je k nákupu.

- [SKU](product-resources.md#sku) – skladová jednotka (SKU), která je v rámci produktu kupní. Tyto prvky jsou znázorněny v různých tvarech produktu.

- [Dostupnost](product-resources.md#availability) – konfigurace, v níž je k dispozici skladová položka k nákupu (například země, měna a oborové segmenty).

Před nákupem rezervace Azure proveďte následující kroky:

1. Identifikujte a načtěte produkt a SKU, které chcete koupit. Můžete to provést tak, že nejprve vydáte seznam Products a SKU, nebo pokud už znáte ID produktu a SKU, vyberte je.

   - [Získání seznamu produktů (podle země)](get-a-list-of-products.md)
   - [Získat produkt s použitím ID produktu](get-a-product-by-id.md)
   - [Získání seznamu skladových položek pro produkt (podle země)](get-a-list-of-skus-for-a-product.md)
   - [Získání SKU pomocí ID SKU](get-a-sku-by-id.md)

2. Zkontroluje inventář SKU. Tento krok je potřeba jenom pro skladové položky, které jsou označené předpokladem pro **InventoryCheck** .

   - [Kontrola inventáře](check-inventory.md)

3. Načtěte [dostupnost](product-resources.md#availability) pro [skladovou](product-resources.md#sku)položku. Při zadávání objednávky budete potřebovat **CatalogItemIdi** dostupnosti. Chcete-li získat tuto hodnotu, použijte jednu z následujících rozhraní API:

   - [Získání seznamu dostupností pro skladovou položku (podle země)](get-a-list-of-availabilities-for-a-sku.md)
   - [Získání dostupnosti pomocí ID dostupnosti](get-an-availability-by-id.md)

> [!IMPORTANT]
> Každý Microsoft Azure produkt rezervace má různé dostupnosti pro předplatné Microsoft Azure (**MS-AZR-0145P**) a plán Azure. Pokud chcete [získat seznam produktů (podle země)](get-a-list-of-products.md)nebo [získat seznam SKU pro produkt (podle země)](get-a-list-of-skus-for-a-product.md)nebo [získat seznam dostupnosti pro skladovou položku (podle země)](get-a-list-of-availabilities-for-a-sku.md) , která platí jenom pro plán Azure, zadejte parametr reservationScope = AzurePlan.

## <a name="order-submission"></a>Odeslání objednávky

Pokud chcete odeslat objednávku rezervace Azure, udělejte toto:

1. Vytvořte košík pro uložení kolekce položek katalogu, které máte v úmyslu koupit. Při vytváření [košíku](cart-resources.md)se [položky řádku vozíku](cart-resources.md#cartlineitem) automaticky seskupují podle toho, co se dá koupit společně ve stejném [pořadí](order-resources.md).

   - [Vytvoření nákupního košíku](create-a-cart.md)
   - [Aktualizace nákupního košíku](update-a-cart.md)

2. Podívejte se na košík. Při rezervaci vozíku dojde k vytvoření [objednávky](order-resources.md).

   - [Rezervace košíku](checkout-a-cart.md)

## <a name="get-order-details"></a>Získat podrobnosti objednávky

Po vytvoření objednávky rezervace Azure můžete načíst podrobnosti o jednotlivých objednávkách pomocí ID objednávky nebo získat seznam objednávek pro zákazníka. Mezi časem odeslání objednávky a jejím zobrazením v seznamu objednávek zákazníka nastane zpoždění až 15 minut.

- Získat podrobnosti o jednotlivých objednávkách pomocí ID objednávky. Viz, [získání objednávky podle ID](get-an-order-by-id.md).

- Získat seznam objednávek pro zákazníka pomocí ID zákazníka. Přečtěte si téma [získání všech objednávek zákazníka](get-all-of-a-customer-s-orders.md).

- Chcete-li získat seznam objednávek pro zákazníka podle [fakturačního cyklu](product-resources.md#billingcycletype) , což vám umožní vypsat objednávky rezervace Azure (jednorázové poplatky) a roční nebo měsíční Fakturované objednávky samostatně. Viz, [získání seznamu objednávek podle typu zákazník a fakturační cyklus](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Správa životního cyklu

V rámci správy životního cyklu rezervací Azure v partnerském centru můžete načítat informace o vašich [nárokech](entitlement-resources.md)na rezervaci Azure a získat podrobnosti o rezervacích pomocí ID objednávky rezervace. Příklady toho, jak to udělat, najdete v tématu [získání nároků](get-a-collection-of-entitlements.md).   

## <a name="invoice-and-reconciliation"></a>Faktura a odsouhlasení

V následujících scénářích se dozvíte, jak programově zobrazit [faktury](invoice-resources.md)zákazníka a získat bilanci a souhrny účtů, které zahrnují jednorázové poplatky za rezervace Azure.

### <a name="balance-and-payment"></a>Zůstatek a platba

Pokud chcete získat aktuální zůstatek k účtu ve vašem výchozím typu měny, který je vyrovnaný z poplatků za periodické i jednorázové (rezervace Azure), přečtěte si téma [získání aktuálního zůstatku účtu](get-the-reseller-s-current-account-balance.md) .

### <a name="multi-currency-balance-and-payment"></a>Zůstatek a platba na více měn

K získání aktuálního zůstatku účtu a shromáždění souhrnů faktury, které obsahují souhrn faktury s pravidelným i jednorázovým poplatkem pro každý typ měny vašeho zákazníka, najdete informace v tématu [získání souhrnů faktury](get-invoice-summaries.md).

### <a name="invoices"></a>Faktury

Chcete-li získat kolekci faktur, které zobrazují jak opakující se, tak jednorázové časové poplatky, přečtěte si téma [získání kolekce faktur](get-a-collection-of-invoices.md). 

### <a name="single-invoice"></a>Jedna faktura

Pokud chcete načíst konkrétní fakturu pomocí ID faktury, přečtěte si téma [získání faktury podle ID](get-invoice-by-id.md).  

### <a name="reconciliation"></a>Párován

Chcete-li získat kolekci podrobností o položce řádku faktury (položky řádku odsouhlasení) pro konkrétní ID faktury, přečtěte si téma [získání položek řádků faktury](get-invoiceline-items.md).  

### <a name="download-an-invoice-as-a-pdf"></a>Stažení faktury jako PDF

Chcete-li načíst výpis faktury ve formátu PDF pomocí ID faktury, přečtěte si téma [získání výpisu faktury](get-invoice-statement.md).
