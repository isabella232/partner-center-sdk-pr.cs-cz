---
title: Prostředky produktů
description: Prostředky představující kupní zboží nebo služby. Zahrnuje prostředky pro popis typu produktu a tvaru (SKU) a pro kontrolu dostupnosti produktu v inventáři.
ms.date: 02/16/2016
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3790d8f5ef154c637dfd3f3d014322d314757f26
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456065"
---
# <a name="products-resources"></a>Prostředky produktů

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
| Podtyp         | [ItemType](#itemtype)         | Nepovinný parametr. Objekt, který popisuje kategorizaci podtypu pro tento typ položky.     |

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
| dynamicAttributes      | páry klíč/hodnota  | Slovník dynamických vlastností, které se vztahují na tuto položku. Vlastnosti v tomto slovníku jsou dynamické a můžou se měnit bez předchozího upozornění. Neměli byste vytvářet silné závislosti na konkrétních klíčích existujících v hodnotě této vlastnosti.    |
| odkazy                  | [ResourceLinks](utility-resources.md#resourcelinks) | Odkazy na prostředky obsažené v této SKU.                   |
| AttestationProperties                  | [AttestationProperties](#attestationproperties) | Vlastnosti ověření identity pro SKU                   |

## <a name="dynamic-sku-attributes"></a>Dynamické atributy SKU

Významné vlastnosti týkající se nových produktů a služeb založených na licenci pro Commerce.

> [!Note] 
> Nové obchodní změny jsou momentálně dostupné jenom pro partnery, kteří jsou součástí M365/D365 New Commerce Experience Technical Preview.

| Vlastnost        | Typ                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
|hasConstraints|boolean|Popisuje, zda SKU obsahuje assetContraints|
|Doplněk|boolean|Popisuje, zda je SKU doplňkem.|
|prerequisiteSkus|pole řetězců|Popisuje produkty a SKU, se kterými může doplněk pracovat|
|upgradeTargetOffers|pole řetězců|Seznam produktů a SKU, na které se položka může upgradovat|
|converstionInstructions|seznam converstionInstructions|Seznam pokynů, které se vztahují na operace v operaci|

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
| RenewalInstructions     | RenewalInstruction                                              | Představuje pokyny k obnovení pro danou dostupnost. |
| product      | [Product](#product) (Produkt)               | Produkt, ke kterému je tato dostupnost odpovídat. |
| skladové          | [Skladové](#sku)            | SKU, které tato dostupnost odpovídá. |
| uvedenými           | pole [pojem](#term) prostředků  | Kolekce podmínek, které se vztahují k této dostupnosti. |
| odkazy           | [ResourceLinks](utility-resources.md#resourcelinks) | Odkazy na prostředky obsažené v dostupnosti. |

## <a name="renewal-instruction"></a>Pokyny pro obnovení

> [!Note] 
> Nové obchodní změny jsou aktuálně dostupné jenom pro partnery, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview
> 

Představuje pokyny k prodloužení pro danou dostupnost.

| Vlastnost        | Typ                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------|
| applicableTermIds       | pole řetězců                       | ID termínů, na která se pokyny vztahují |
| RenewalOptions       | pole RenewalOption                     | Možnosti definující prodloužení |

## <a name="renewaloption"></a>RenewalOption    

> [!Note] 
> Nové obchodní změny jsou aktuálně dostupné jenom pro partnery, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview
> 

Představuje pokyny k prodloužení pro danou dostupnost.

| Vlastnost        | Typ                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------|
| renewToId       | Řetězec       | Představuje produkt a SKU, na které se má obnovit |
| isAutoRenewable       | Logická hodnota       | Jestli je možné dostupnost automaticky obnovit nebo ne |

## <a name="term"></a>Pojem

Představuje termín, pro který je možné zakoupit dostupnost.

| Vlastnost              | Typ                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| doba trvání              | řetězec                                      | Reprezentace doby trvání období podle STANDARDu ISO 8601. Aktuální podporované hodnoty jsou P1M (1 měsíc), P1Y (1 rok) a P3Y (3 roky). |
| description           | řetězec                                      | Popis výrazu           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

Představuje požadavek na kontrolu inventáře u určitých položek katalogu.

| Vlastnost         | Typ                                                | Description                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems (položky cíle)      | pole [InventoryItem](#inventoryitem)            | Seznam položek katalogu, které bude vyhodnocovat kontrola inventáře.                           |
| inventoryContext | páry klíč/hodnota                                     | Slovník kontextových hodnot, které jsou potřeba k provedení kontrol inventáře. Každá [SKU](#sku) produktů definuje, které hodnoty (pokud existují) jsou potřeba k provedení této operace.  |
| Odkazy            | [Odkazy na prostředky](utility-resources.md#resourcelinks) | Odkazy na prostředky obsažené v žádosti o kontrolu inventáře.                            |

## <a name="inventoryitem"></a>InventoryItem

Představuje jednu položku v operaci kontroly inventáře. Tento prostředek se používá k určení cílových položek ve vstupní žádosti a používá se také k reprezentaci výstupních výsledků operace kontroly inventáře.

| Vlastnost         | Typ                                                              | Description                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | řetězec                                                            | (Povinné) ID [produktu](#product).                            |
| ID SKU            | řetězec                                                            | ID [SKU](#sku). Při použití tohoto prostředku jako vstupu do žádosti o inventář je tato hodnota volitelná. Pokud tuto hodnotu nezadáte, budou se všechny skladové položky v rámci produktu považovat za cílové položky operace kontroly inventáře.      |
| isRestricted (je vrestricted)     | bool                                                              | Určuje, jestli byla u této položky nalezena omezená zásoba.            |
| Omezení     | pole [InventoryRestriction](#inventoryrestriction)            | Podrobnosti o všech omezeních, která jsou pro tuto položku nalezena. Tato vlastnost se naplní pouze v **případě, že isRestricted** = "true". |

## <a name="inventoryrestriction"></a>InventoryRestriction

Představuje podrobnosti omezení inventáře. To platí jenom pro výsledky výstupu kontroly inventáře, ne pro vstupní požadavky.

| Vlastnost         | Typ                  | Description                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode (kód důvodu)       | řetězec                | Kód, který identifikuje důvod omezení.                                    |
| description      | řetězec                | Popis omezení inventáře                                               |
| properties       | páry klíč/hodnota       | Slovník vlastností, které mohou obsahovat další podrobnosti o omezení.           |

## <a name="billingcycletype"></a>BillingCycleType

Hodnota [Enum/dotnet/api/system.enum) s hodnotami, které označují typ fakturačního cyklu.

| Hodnota              | Pozice     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Neznámý            | 0            | Inicializátor výčtu.                                                                          |
| měsíčně            | 1            | Označuje, že se partnerovi budou účtovat měsíční poplatky.                                        |
| ročně             | 2            | Označuje, že partner bude účtován ročně.                                       |
| Žádné               | 3            | Indikuje, že se partner nebude účtovat. Tato hodnota se dá použít pro položky zkušební verze.    |
| Jednorázová            | 4            | Indikuje, že se partner účtuje jednou za jeden čas.                                       |

## <a name="attestationproperties"></a>AttestationProperties

Představuje typ ověření identity a v případě potřeby k nákupu.

| Vlastnost              | Typ                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| attestationType              | řetězec                                      | Určuje typ ověření identity. pro Windows 365 je hodnota Windows365. text ověření Windows 365 je "rozumím, že každá osoba, která používá Windows 365 Business s Windowsm hybridním zvýhodněním, musí mít na primárním pracovním zařízení nainstalovanou platnou kopii Windows 10/11 Pro." |
| enforceAttestation           | boolean                                      | Určuje, zda je pro nákup vyžadováno ověření identity.           |
