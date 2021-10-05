---
title: Prostředky produktů
description: Prostředky představující kupní zboží nebo služby. Zahrnuje prostředky pro popis typu produktu a tvaru (SKU) a pro kontrolu dostupnosti produktu v inventáři.
ms.date: 02/16/2016
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 20e2d7bcaf1041f186f0723d7ff453bebbe46dd2
ms.sourcegitcommit: f112efee7344d739bdbf385adba0c554ea2a63e3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2021
ms.locfileid: "129439357"
---
# <a name="products-resources"></a>Prostředky produktů

Prostředky představující kupní zboží nebo služby. Zahrnuje prostředky pro popis typu produktu a tvaru (SKU) a pro kontrolu dostupnosti produktu v inventáři.

## <a name="product"></a>Produkt

Představuje službu, která je k nebo platná. Produkt sám o sobě není položkou, která je k nákupu.

| Vlastnost           | Typ                          | Popis                                                              |
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

| Vlastnost        | Typ                          | Popis                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | řetězec                        | Identifikátor typu.                                                                 |
| displayName     | řetězec                        | Zobrazovaný název pro tento typ.                                                      |
| Podtyp         | [ItemType](#itemtype)         | Nepovinný parametr. Objekt, který popisuje kategorizaci podtypu pro tento typ položky.     |

## <a name="productlinks"></a>ProductLinks

Obsahuje seznam odkazů na [produkt](#product).

| Vlastnost        | Typ                                                          | Popis                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| SKU            | [Propojit](utility-resources.md#link)                             | Odkaz pro přístup k podkladovým skladovým položkám          |
| odkazy           | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky obsažené v rámci tohoto prostředku.   |

## <a name="sku"></a>Skladová jednotka (SKU)

Představuje kupní jednotku (SKU), která je v produktu k disměrné jednotce. Tyto prvky jsou znázorněny v různých tvarech produktu.

| Vlastnost               | Typ             | Popis                                                                           |
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
| inventoryVariables     | pole řetězců | Seznam proměnných potřebných ke spuštění kontroly inventáře u této položky. Podporované hodnoty jsou:<br/> "CustomerId" – ID zákazníka, pro který se nákup bude nakupovat.<br/> AzureSubscriptionId – ID předplatného Azure, které se použije k nákupu rezervace Azure.</br> ArmRegionName – oblast, pro kterou chcete ověřit inventář. Tato hodnota se musí shodovat s armregionname ze SKU DynamicAttributes. |
| provisioningVariables (Proměnné zřizování)  | pole řetězců | Seznam proměnných, které je nutné poskytnuta [](cart-resources.md#cartlineitem) do kontextu zřizování řádkové položky košíku při nákupu této položky. Podporované hodnoty jsou:<br/> Rozsah – rozsah nákupu rezervace Azure: Jeden, Sdílený.<br/> SubscriptionId – ID předplatného Azure, které se použije k nákupu rezervace Azure.<br/> "Doba trvání" – doba trvání rezervace Azure: "1Year", "3Year".  |
| dynamicAttributes      | páry klíč/hodnota  | Slovník dynamických vlastností, které platí pro tuto položku. Vlastnosti v tomto slovníku jsou dynamické a mohou se změnit bez předchozího upozornění. Neměli byste vytvářet silné závislosti na konkrétních klíčích existujících v hodnotě této vlastnosti.    |
| Odkazy                  | [Odkazy na prostředky](utility-resources.md#resourcelinks) | Odkazy na prostředky obsažené ve SKU.                   |
| AttestationProperties                  | [AttestationProperties](#attestationproperties) | Vlastnosti ověření pro SKU.                   |
| consumptionType (typ spotřeby)                  | řetězec | Je k dispozici pouze v případě, že SKU podporuje spotřebu, jako *je například nadage .*               |

## <a name="dynamic-sku-attributes"></a>Atributy dynamické SKU

Významné vlastnosti, které jsou relevantní pro nové produkty a služby založené na komerčních licencích

> [!Note] 
> Nové obchodní změny jsou aktuálně dostupné jenom pro partnery, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview

| Vlastnost        | Typ                        | Popis                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
|hasConstraints|boolean|Popisuje, jestli SKU obsahuje assetContraints.|
|isAddon|boolean|Popisuje, jestli je SKU doplňkem.|
|prerequisiteSkus|pole řetězců|Popisuje produkty a SKU, se které může doplněk pracovat.|
|upgradeTargetOffers|pole řetězců|Seznam produktů a SKU, na které se položka může upgradovat|
|converstionInstructions|seznam converstionInstructions|Seznam pokynů použitelných pro operace conversat|

## <a name="availability"></a>Dostupnost

Představuje konfiguraci, ve které je skladová položku k dispozici pro nákup (například země, měna a segment odvětví).

| Vlastnost        | Typ                        | Popis                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| id              | řetězec                        | ID pro tuto dostupnost. Toto ID je jedinečné pouze v kontextu nadřazeného [produktu](#product) a [SKU](#sku). **Poznámka:** Toto ID se může v průběhu času měnit. Na tuto hodnotu byste se měli spoléhat jen v krátkém časovém intervalu po načtení.  |
| productId       | řetězec                        | ID [produktu, který](#product) obsahuje tuto dostupnost.           |
| ID SKU           | řetězec                        | ID [SKU, která](#sku) obsahuje tuto dostupnost.                   |
| catalogItemId   | řetězec                        | Jedinečný identifikátor této položky v katalogu. Toto je ID, které se musí naplnit do vlastností [OrderLineItem.OfferId](order-resources.md#orderlineitem) nebo [CartLineItem.CatalogItemId](cart-resources.md#cartlineitem) při nákupu nadřazené [SKU](#sku). **Poznámka:** Toto ID se může v průběhu času měnit. Na tuto hodnotu byste se měli spoléhat jen krátce po načtení. Měla by být přístupná a měla by se používat pouze v době nákupu.  |
| výchozí souběžnost | řetězec                        | Výchozí měna podporovaná pro tuto dostupnost.                               |
| segment         | řetězec                        | Segment odvětví pro tuto dostupnost. Podporované hodnoty jsou: Komerční, Vzdělávací, Státní správa, Nezisková organizace. |
| country         | řetězec                                              | Země nebo oblast (ve formátu ISO s kódem země), na které se tato dostupnost vztahuje. |
| isPurchasable   | bool                                                | Určuje, jestli je tato dostupnost možné zakoupit. |
| isRenewable     | bool                                                | Určuje, jestli je tato dostupnost obnovitelné. |
| RenewalInstructions     | RenewalInstruction                                              | Představuje pokyny k prodloužení pro danou dostupnost. |
| product      | [Product](#product) (Produkt)               | Produkt, který tato dostupnost odpovídá. |
| Sku          | [Sku](#sku)            | SKU, které tato dostupnost odpovídá. |
| Podmínky           | pole [prostředků termínu](#term)  | Kolekce podmínek, které se na tuto dostupnost vztahují. |
| Odkazy           | [Odkazy na prostředky](utility-resources.md#resourcelinks) | Propojení prostředků obsažená v rámci dostupnosti. |

## <a name="renewal-instruction"></a>Pokyny k prodloužení

> [!Note] 
> Nové obchodní změny jsou aktuálně dostupné jenom pro partnery, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview
> 

Představuje pokyny k prodloužení pro danou dostupnost.

| Vlastnost        | Typ                        | Popis                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------|
| applicableTermIds       | pole řetězců                       | ID termínů, na která se pokyny vztahují |
| RenewalOptions       | pole RenewalOption                     | Možnosti definující prodloužení |

## <a name="renewaloption"></a>RenewalOption    

> [!Note] 
> Nové obchodní změny jsou aktuálně dostupné jenom pro partnery, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview
> 

Představuje pokyny k prodloužení pro danou dostupnost.

| Vlastnost        | Typ                        | Popis                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------|
| renewToId       | Řetězec       | Představuje produkt a SKU, na které se má obnovit |
| isAutoRenewable       | Logická hodnota       | Jestli je možné dostupnost automaticky obnovit nebo ne |

## <a name="term"></a>Pojem

Představuje termín, pro který je možné zakoupit dostupnost.

| Vlastnost              | Typ                                        | Popis                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| doba trvání              | řetězec                                      | Reprezentace doby trvání období podle STANDARDu ISO 8601. Aktuální podporované hodnoty jsou P1M (1 měsíc), P1Y (1 rok) a P3Y (3 roky). |
| description           | řetězec                                      | Popis výrazu           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

Představuje požadavek na kontrolu inventáře u určitých položek katalogu.

| Vlastnost         | Typ                                                | Popis                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems (položky cíle)      | pole [InventoryItem](#inventoryitem)            | Seznam položek katalogu, které bude vyhodnocovat kontrola inventáře.                           |
| inventoryContext | páry klíč/hodnota                                     | Slovník kontextových hodnot, které jsou potřeba k provedení kontrol inventáře. Každá [skladová](#sku) hodnota produktů definuje, které hodnoty (pokud existují) jsou potřeba k provedení této operace.  |
| Odkazy            | [Odkazy na prostředky](utility-resources.md#resourcelinks) | Odkazy na prostředky obsažené v žádosti o kontrolu inventáře.                            |

## <a name="inventoryitem"></a>InventoryItem

Představuje jednu položku v operaci kontroly inventáře. Tento prostředek se používá k určení cílových položek ve vstupní žádosti a používá se také k reprezentaci výstupních výsledků operace kontroly inventáře.

| Vlastnost         | Typ                                                              | Popis                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | řetězec                                                            | (Povinné) ID [produktu](#product).                            |
| ID SKU            | řetězec                                                            | ID [SKU](#sku). Při použití tohoto prostředku jako vstupu do žádosti o inventář je tato hodnota volitelná. Pokud tuto hodnotu nezadáte, budou se všechny skladové položky v rámci produktu považovat za cílové položky operace kontroly inventáře.      |
| isRestricted (je vrestricted)     | bool                                                              | Určuje, jestli byla u této položky nalezena omezená zásoba.            |
| Omezení     | pole [InventoryRestriction](#inventoryrestriction)            | Podrobnosti o všech omezeních, která jsou pro tuto položku nalezena. Tato vlastnost se naplní pouze v **případě, že isRestricted** = "true". |

## <a name="inventoryrestriction"></a>InventoryRestriction

Představuje podrobnosti omezení inventáře. To platí jenom pro výsledky výstupu kontroly inventáře, ne pro vstupní požadavky.

| Vlastnost         | Typ                  | Popis                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode (kód důvodu)       | řetězec                | Kód, který identifikuje důvod omezení.                                    |
| description      | řetězec                | Popis omezení inventáře                                               |
| properties       | páry klíč/hodnota       | Slovník vlastností, které mohou obsahovat další podrobnosti o omezení.           |

## <a name="billingcycletype"></a>BillingCycleType

Hodnota [Enum/dotnet/api/system.enum) s hodnotami, které označují typ fakturačního cyklu.

| Hodnota              | Pozice     | Popis                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Neznámý            | 0            | Inicializátor výčtu.                                                                          |
| měsíčně            | 1            | Označuje, že se partnerovi budou účtovat měsíční poplatky.                                        |
| ročně             | 2            | Označuje, že partner bude účtován ročně.                                       |
| Žádné               | 3            | Označuje, že partnerovi se nebudou účtovat žádné poplatky. Tato hodnota se může použít pro zkušební položky.    |
| Někdejší            | 4            | Označuje, že partnerovi se budou účtovat poplatky jednou.                                       |

## <a name="attestationproperties"></a>AttestationProperties

Představuje typ ověření, a pokud je vyžadován pro nákup.

| Vlastnost              | Typ                                        | Popis                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| attestationType              | řetězec                                      | Označuje typ ověření. Například Windows 365 je hodnota Windows365. Windows ověření 365 je, že "Chápu, že každá osoba, která používá Windows 365 Business s zvýhodněním hybridního využití Windows, musí mít také na svém primárním pracovním zařízení nainstalovanou platnou kopii Windows 10/11 Pro". |
| vynucení ověření           | boolean                                      | Určuje, jestli se k nákupu vyžaduje ověření.           |
