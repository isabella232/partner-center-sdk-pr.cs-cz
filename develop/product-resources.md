---
title: Zdroje informací o produktech
description: Prostředky, které představují nákupní zboží nebo služby. Obsahuje zdroje informací pro popis typu a tvaru produktu (SKU) a pro kontrolu dostupnosti produktu v inventáři.
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b0269b55810a57dc3a4897027a9817baaebc8ed5f4e98dc66e2eadfa210f362f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997443"
---
# <a name="products-resources"></a>Zdroje informací o produktech

Prostředky, které představují nákupní zboží nebo služby. Obsahuje zdroje informací pro popis typu a tvaru produktu (SKU) a pro kontrolu dostupnosti produktu v inventáři.

## <a name="product"></a>Produkt

Představuje nákupní zboží nebo službu. Samotný produkt není položka, kterou je možné zakoupit.

| Vlastnost           | Typ                          | Description                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| id                 | řetězec                        | ID pro tento produkt.                                                 |
| title              | řetězec                        | Název produktu                                                       |
| description        | řetězec                        | Popis produktu                                                 |
| productType        | [Itemtype](#itemtype)         | Objekt, který popisuje kategorizaci typů tohoto produktu.     |
| isMicrosoftProduct | bool                          | Určuje, jestli se jedná o produkt Microsoftu.                          |
| publisherName      | řetězec                        | Název vydavatele produktu, pokud je k dispozici.                          |
| Odkazy              | [Odkazy na produkty](#productlinks) | Odkazy na prostředky obsažené v rámci produktu.                         |

## <a name="itemtype"></a>ItemType

Představuje typ produktu.

| Vlastnost        | Typ                          | Description                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | řetězec                        | Identifikátor typu.                                                                 |
| displayName     | řetězec                        | Zobrazovaný název tohoto typu.                                                      |
| Podtypu         | [Itemtype](#itemtype)         | Nepovinný parametr. Objekt, který popisuje kategorizaci podtypu pro tento typ položky.     |

## <a name="productlinks"></a>Odkazy na produkty

Obsahuje seznam odkazů pro [produkt](#product).

| Vlastnost        | Typ                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| Sku            | [Odkaz](utility-resources.md#link)                             | Odkaz pro přístup k podkladovým skladovým cenovým cenovým cenovým cenům          |
| Odkazy           | [Odkazy na prostředky](utility-resources.md#resourcelinks)           | Odkazy na prostředky obsažené v tomto prostředku.   |

## <a name="sku"></a>Skladová jednotka (SKU)

Představuje nákupní skladovou jednotku (SKU) v rámci produktu. Ty představují různé tvary produktu.

| Vlastnost               | Typ             | Description                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| id                     | řetězec           | ID této SKU. Toto ID je jedinečné pouze v kontextu svého nadřazeného produktu. |
| title                  | řetězec           | Název SKU                                                                 |
| description            | řetězec           | Popis SKU                                                           |
| productId              | řetězec           | ID nadřazeného [produktu,](#product) který obsahuje tuto SKU.                      |
| minimumQuantity        | int              | Minimální povolené množství pro nákup.                                            |
| maximumQuantity        | int              | Maximální povolené množství pro nákup.                                            |
| isTrial (aplikace isTrial)                | bool             | Určuje, jestli se jedná o položku zkušební verze.                                           |
| supportedBillingCycles | pole řetězců | Seznam podporovaných fakturačních cyklů pro tuto SKU. Podporované hodnoty jsou názvy členů, které najdete v [části BillingCycleType](#billingcycletype). |
| purchasePrerequisites  | pole řetězců | Seznam požadovaných kroků nebo akcí, které jsou potřeba před nákupem této položky. Podporované hodnoty jsou:<br/>  "InventoryCheck" – Označuje, že se má inventář položky vyhodnotit před pokusem o nákup této položky.<br/> AzureSubscriptionRegistration – Označuje, že předplatné Azure je potřeba a musí být zaregistrované, než se pokusíte koupit tuto položku.  |
| inventoryVariables     | pole řetězců | Seznam proměnných potřebných k provedení kontroly inventáře pro tuto položku. Podporované hodnoty jsou:<br/> "CustomerId" – ID zákazníka, pro kterého se má koupit.<br/> "AzureSubscriptionId" – ID předplatného Azure, které se použije při nákupu rezervací Azure.</br> "ArmRegionName" – oblast, pro kterou chcete ověřit inventář. Tato hodnota musí odpovídat hodnotě "ArmRegionName" z DynamicAttributes SKU. |
| provisioningVariables  | pole řetězců | Seznam proměnných, které musí být poskytnuty do kontextu zřizování [položky řádku košíku](cart-resources.md#cartlineitem) při nákupu této položky. Podporované hodnoty jsou:<br/> Rozsah – rozsah nákupu rezervace Azure: "Single", "Shared".<br/> SubscriptionId – ID předplatného Azure, které se použije pro nákup rezervace Azure.<br/> "Doba trvání" – doba trvání rezervace Azure: "1Year", "3Year".  |
| dynamicAttributes      | páry klíč/hodnota  | Slovník dynamických vlastností, které se vztahují na tuto položku. Vlastnosti v tomto slovníku jsou dynamické a můžou se měnit bez předchozího upozornění. Neměli byste vytvářet silné závislosti na konkrétních klíčích existujících v hodnotě této vlastnosti.    |
| odkazy                  | [ResourceLinks](utility-resources.md#resourcelinks) | Odkazy na prostředky obsažené v této SKU.                   |
| AttestationProperties                  | [AttestationProperties](#attestationproperties) | Vlastnosti ověření identity pro SKU                   |

## <a name="availability"></a>Dostupnost

Představuje konfiguraci, ve které je k dispozici SKU k nákupu (například země, měna a odvětví).

| Vlastnost        | Typ                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| id              | řetězec                        | ID pro tuto dostupnost Toto ID je jedinečné jenom v kontextu jeho nadřazeného [produktu](#product) a [SKU](#sku). **Poznámka:** Toto ID se může v průběhu času měnit. Tuto hodnotu byste měli spoléhat jenom v krátkém časovém intervalu po jeho načtení.  |
| productId       | řetězec                        | ID [produktu](#product) , který obsahuje tuto dostupnost.           |
| skuId           | řetězec                        | ID [SKU](#sku) , které obsahuje tuto dostupnost.                   |
| catalogItemId   | řetězec                        | Jedinečný identifikátor této položky v katalogu Toto je ID, které se musí naplnit do vlastností [OrderLineItem. hodnotami OfferId](order-resources.md#orderlineitem) nebo [CartLineItem. CatalogItemId](cart-resources.md#cartlineitem) při nákupu nadřazené [SKU](#sku). **Poznámka:** Toto ID se může v průběhu času měnit. Tuto hodnotu byste měli spoléhat jenom v krátké době po jejím načtení. Měl by k němu být přistupovaná a použitá v době nákupu.  |
| defaultCurrency | řetězec                        | Výchozí měna podporovaná pro tuto dostupnost.                               |
| segment         | řetězec                        | Segment odvětví pro tuto dostupnost. Podporované hodnoty jsou: komerční, vzdělávací, státní, nezisková. |
| country         | řetězec                                              | Země nebo oblast (ve formátu kódu země ISO), kde se tato dostupnost vztahuje. |
| k diskupnímu   | bool                                                | Označuje, zda je tato dostupnost dostupná. |
| Obnovitelné     | bool                                                | Označuje, zda je tato dostupnost obnovitelné. |
| product      | [Product](#product) (Produkt)               | Produkt, ke kterému je tato dostupnost odpovídat. |
| skladové          | [Skladové](#sku)            | SKU, které tato dostupnost odpovídá. |
| uvedenými           | pole [pojem](#term) prostředků  | Kolekce podmínek, které se vztahují k této dostupnosti. |
| odkazy           | [ResourceLinks](utility-resources.md#resourcelinks) | Odkazy na prostředky obsažené v dostupnosti. |

## <a name="term"></a>Pojem

Představuje období, pro které lze zakoupit dostupnost.

| Vlastnost              | Typ                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| doba trvání              | řetězec                                      | ISO 8601 reprezentace doby trvání období. Aktuální podporované hodnoty jsou P1M (1 měsíc), P1Y (1 rok) a P3Y (3 roky). |
| description           | řetězec                                      | Popis termínu.           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

Představuje požadavek na kontrolu inventáře s určitými položkami katalogu.

| Vlastnost         | Typ                                                | Description                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | pole [InventoryItem](#inventoryitem)            | Seznam položek katalogu, které budou zjišťovány při kontrole inventáře.                           |
| inventoryContext | páry klíč/hodnota                                     | Slovník hodnot kontextu, které jsou nutné k provedení kontroly inventáře. Každá [SKU](#sku) produktů bude definovat, které hodnoty (pokud existují) jsou nutné k provedení této operace.  |
| odkazy            | [ResourceLinks](utility-resources.md#resourcelinks) | Odkazy na prostředky obsažené v žádosti o kontrolu inventáře.                            |

## <a name="inventoryitem"></a>InventoryItem

Představuje jednu položku v operaci kontroly inventáře. Tento prostředek se používá k určení cílových položek ve vstupním požadavku a používá se také k reprezentaci výstupních výsledků operace kontroly inventáře.

| Vlastnost         | Typ                                                              | Description                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | řetězec                                                            | Požadovanou ID [produktu](#product)                            |
| skuId            | řetězec                                                            | ID [SKU](#sku). Při použití tohoto prostředku jako vstupu pro požadavek na inventář je tato hodnota volitelná. Pokud tato hodnota není zadaná, budou se všechny SKU v rámci produktu považovat za cílové položky operace kontroly inventáře.      |
| Omezení     | bool                                                              | Určuje, zda byla tato položka nalezena s omezeným inventářem.            |
| podléhající     | pole [InventoryRestriction](#inventoryrestriction)            | Podrobnosti o všech omezeních, která jsou pro tuto položku k dispozici. Tato vlastnost bude naplněna pouze v případě **omezení** = "true". |

## <a name="inventoryrestriction"></a>InventoryRestriction

Představuje podrobnosti omezení inventáře. To platí jenom pro výsledky výstupu kontroly inventáře, ne pro vstupní požadavky.

| Vlastnost         | Typ                  | Description                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | řetězec                | Kód, který identifikuje důvod omezení.                                    |
| description      | řetězec                | Popis omezení inventáře.                                               |
| properties       | páry klíč/hodnota       | Slovník vlastností, které mohou poskytnout další podrobnosti o omezení.           |

## <a name="billingcycletype"></a>BillingCycleType

[Enum/dotnet/API/System. Enum) s hodnotami, které označují typ fakturačního cyklu.

| Hodnota              | Pozice     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Neznámý            | 0            | Inicializátor výčtu.                                                                          |
| měsíčně            | 1            | Indikuje, že se partner bude účtovat měsíčně.                                        |
| ročně             | 2            | Indikuje, že se partner bude účtovat ročně.                                       |
| Žádná               | 3            | Indikuje, že se partner nebude účtovat. Tato hodnota se dá použít pro položky zkušební verze.    |
| Jednorázová            | 4            | Indikuje, že se partner účtuje jednou za jeden čas.                                       |

## <a name="attestationproperties"></a>AttestationProperties

Představuje typ ověření identity a v případě potřeby k nákupu.

| Vlastnost              | Typ                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| attestationType              | řetězec                                      | Určuje typ ověření identity. pro Windows 365 je hodnota Windows365. text ověření Windows 365 je "rozumím, že každá osoba, která používá Windows 365 Business s Windowsm hybridním zvýhodněním, musí mít na primárním pracovním zařízení nainstalovanou platnou kopii Windows 10/11 Pro." |
| enforceAttestation           | boolean                                      | Určuje, zda je pro nákup vyžadováno ověření identity.           |
