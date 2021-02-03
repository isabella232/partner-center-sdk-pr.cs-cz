---
title: Prostředky produktů
description: Prostředky představující kupní zboží nebo služby. Zahrnuje prostředky pro popis typu produktu a tvaru (SKU) a pro kontrolu dostupnosti produktu v inventáři.
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6a3cfacd3654e85a9824759295f97792ff740d85
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766827"
---
# <a name="products-resources"></a>Prostředky produktů

**Platí pro**

- Partnerské centrum

Prostředky představující kupní zboží nebo služby. Zahrnuje prostředky pro popis typu produktu a tvaru (SKU) a pro kontrolu dostupnosti produktu v inventáři.

## <a name="product"></a>Produkt

Představuje službu, která je k nebo platná. Produkt sám o sobě není položkou, která je k nákupu.

| Vlastnost           | Typ                          | Description                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| id                 | řetězec                        | ID pro tento produkt                                                 |
| title              | řetězec                        | Název produktu                                                       |
| description        | řetězec                        | Popis produktu                                                 |
| productType        | [ItemType](#itemtype)         | Objekt, který popisuje kategorizaci typů tohoto produktu.     |
| isMicrosoftProduct | bool                          | Označuje, zda se jedná o produkt společnosti Microsoft.                          |
| publisherName      | řetězec                        | Název vydavatele produktu, pokud je k dispozici                          |
| odkazy              | [ProductLinks](#productlinks) | Odkazy na prostředky obsažené v produktu.                         |

## <a name="itemtype"></a>ItemType

Představuje typ produktu.

| Vlastnost        | Typ                          | Description                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | řetězec                        | Identifikátor typu.                                                                 |
| displayName     | řetězec                        | Zobrazovaný název pro tento typ.                                                      |
| Podtyp         | [ItemType](#itemtype)         | Nepovinný parametr. Objekt, který popisuje kategorizaci dílčího typu pro tento typ položky.     |

## <a name="productlinks"></a>ProductLinks

Obsahuje seznam odkazů na [produkt](#product).

| Vlastnost        | Typ                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| SKU            | [Odkaz](utility-resources.md#link)                             | Odkaz pro přístup k podkladovým skladovým položkám          |
| odkazy           | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky obsažené v rámci tohoto prostředku.   |

## <a name="sku"></a>Skladová jednotka (SKU)

Představuje kupní jednotku (SKU), která je v produktu k disměrné jednotce. Tyto prvky jsou znázorněny v různých tvarech produktu.

| Vlastnost               | Typ             | Description                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| id                     | řetězec           | ID této SKU Toto ID je jedinečné jenom v rámci kontextu jeho nadřazeného produktu. |
| title                  | řetězec           | Název SKU.                                                                 |
| description            | řetězec           | Popis SKU.                                                           |
| productId              | řetězec           | ID nadřazeného [produktu](#product) , který obsahuje tuto sku                      |
| minimumQuantity        | int              | Minimální množství, které je povoleno pro nákup.                                            |
| maximumQuantity        | int              | Maximální povolené množství k nákupu.                                            |
| Zkušební verze                | bool             | Označuje, zda je tato SKU položkou zkušební verze.                                           |
| supportedBillingCycles | pole řetězců | Seznam podporovaných fakturačních cyklů pro tuto skladovou jednotku. Podporované hodnoty jsou názvy členů nalezené v [BillingCycleType](#billingcycletype). |
| purchasePrerequisites  | pole řetězců | Seznam požadovaných kroků nebo akcí, které jsou nutné před nákupem této položky. Podporované hodnoty jsou:<br/>  "InventoryCheck" – Určuje, že před pokusem o zakoupení této položky je nutné vyhodnotit inventář položky.<br/> "AzureSubscriptionRegistration" – označuje, že je potřeba předplatné Azure, a před tím, než se pokusíte koupit tuto položku, musí být zaregistrované.  |
| inventoryVariables     | pole řetězců | Seznam proměnných potřebných ke spuštění kontroly inventáře u této položky. Podporované hodnoty jsou:<br/> "CustomerId" – ID zákazníka, pro kterého se má koupit.<br/> "AzureSubscriptionId" – ID předplatného Azure, které se použije při nákupu rezervací Azure.</br> "ArmRegionName" – oblast, pro kterou chcete ověřit inventář. Tato hodnota musí odpovídat hodnotě "ArmRegionName" z DynamicAttributes SKU. |
| provisioningVariables  | pole řetězců | Seznam proměnných, které musí být poskytnuty do kontextu zřizování [položky řádku košíku](cart-resources.md#cartlineitem) při nákupu této položky. Podporované hodnoty jsou:<br/> Rozsah – rozsah nákupu rezervace Azure: "Single", "Shared".<br/> SubscriptionId – ID předplatného Azure, které se použije pro nákup rezervace Azure.<br/> "Doba trvání" – doba trvání rezervace Azure: "1Year", "3Year".  |
| dynamicAttributes      | páry klíč/hodnota  | Slovník dynamických vlastností, které se vztahují na tuto položku. Všimněte si, že vlastnosti v tomto slovníku jsou dynamické a mohou se měnit bez předchozího upozornění. Neměli byste vytvářet silné závislosti na konkrétních klíčích existujících v hodnotě této vlastnosti.    |
| odkazy                  | [ResourceLinks](utility-resources.md#resourcelinks) | Odkazy na prostředky obsažené v této SKU.                   |

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
| Měsíčně            | 1            | Indikuje, že se partner bude účtovat měsíčně.                                        |
| ročně             | 2            | Indikuje, že se partner bude účtovat ročně.                                       |
| Žádné               | 3            | Indikuje, že se partner nebude účtovat. Tato hodnota se dá použít pro položky zkušební verze.    |
| Jednorázová            | 4            | Indikuje, že se partner účtuje jednou za jeden čas.                                       |
