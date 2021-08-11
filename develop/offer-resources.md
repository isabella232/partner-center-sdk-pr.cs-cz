---
title: Prostředky nabídky
description: Popisuje produkt uvedený v katalogu prodejců, který mohou nabídnout svým zákazníkům.
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bcc5b60b7d1e3e13c38bd4014a81c2af254daa1d01ef33351b680463c3fee4a6
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997902"
---
# <a name="offer-resources"></a>Prostředky nabídky

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Popisuje produkt uvedený v katalogu prodejců, který mohou nabídnout svým zákazníkům.

## <a name="offer"></a>Nabídka

| Vlastnost                    | Typ                      | Description                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                          | řetězec                    | Identifikátor nabídky                                                                                           |
| name                        | řetězec                    | Název nabídky                                                                                                 |
| description                 | řetězec                    | Popis nabídky                                                                                     |
| minimumQuantity             | int                       | Minimální dostupné množství.                                                                                 |
| maximumQuantity             | int                       | Maximální množství k dispozici.                                                                                 |
| Rank                        | int                       | Pořadí nabídky nebo Priorita v porovnání s jinými kategoriemi ve stejné produktové lince. Tato vlastnost by měla být nastavena pouze v případě, že je pro danou produktovou řadu k dispozici více než jedna nabídka.  |
| identifikátor URI                         | řetězec                    | Identifikátor URI nabídky                                                                                                  |
| locale                      | řetězec                    | Národní prostředí, ve kterém se nabídka vztahuje.                                                                          |
| country                     | řetězec                    | Země nebo oblast, kde se nabídka vztahuje.                                                                    |
| category                    | [OfferCategory](#offercategory)           | Kategorie nabídky                                                                   |
| limitUnitOfMeasure          | řetězec                    | Hodnota, která určuje typ omezení nákupu. Mezi možné hodnoty patří:<br/> "None" – počet předplatných založených na zakoupené nabídce není nijak omezen.<br/> "Souběžný" – počet předplatných, která mohou existovat v klientovi zákazníka v daném čase, včetně předplatných, která jsou aktivní nebo zrušená. Tato hodnota se vztahuje hlavně na malé obchodní nabídky, kde počty licencí jsou menší než 300. Předplatná de-provisionioned se nepočítají.<br/> "Doba života" – počet předplatných, která mohou existovat po dobu života tenanta zákazníka. Tato hodnota je nejvíce platná pro zkušební verze. Předplatná de-provisionioned se nepočítají.      |
| limit                       | int                       | Počet předplatných, která lze zakoupit v rámci této nabídky na základě limitUnitOfMeasure.                |
| prerequisiteOffers          | řetězec                    | Požadované nabídky.                                                                                        |
| Doplněk                     | boolean                   | Hodnota, která označuje, zda je tato instance doplňkem.                                                           |
| hasAddOns                   | boolean                   | Hodnota, která označuje, zda tato nabídka obsahuje nějaké doplňky                                                           |
| isAvailableForPurchase      | boolean                   | Hodnota, která označuje, jestli je tato instance dostupná k nákupu.                                             |
| fakturace                     | řetězec                    | Určuje typ fakturace pro nákup položky řádku: "none", "Usage" nebo "License".                           |
| supportedBillingCycles      | pole řetězců          | Označuje fakturační cykly podporované pro tuto nabídku. Podporované hodnoty jsou názvy členů nalezené v [BillingCycleType](product-resources.md#billingcycletype) .   |
| isAutoRenewable             | boolean                   | Hodnota, která označuje, zda se nabídka automaticky obnoví.                                                      |
| upgradeTargetOffers         | pole řetězců          | Seznam nabídek, na které lze tuto nabídku upgradovat.                                                          |
| conversionTargetOffers      | pole řetězců          | Seznam nabídek, na které lze tuto nabídku převést                                                         |
| reselleeQualifications      | pole řetězců          | Kvalifikace vyžadovaná zákazníkem, aby mohl partner koupit nabídku pro daného zákazníka.     |
| resellerQualifications      | pole řetězců          | Kvalifikace požadovaná partnerem, aby bylo možné zakoupit nabídku pro zákazníka.                       |
| salesGroupId                | řetězec                    | Řetězec použitý k seskupení nabídek do samostatných objednávek.                                                             |
| Zkušební verze                     | boolean                   | Hodnota, která označuje, zda se jedná o zkušební nabídku                                                               |
| product                     | [OfferProduct](#offerproduct)           | Získá produkt nabídky.                                                                           |
| Jednotkách UnitType                    | řetězec                    | Typ jednotky                                                                                      |
| odkazy                       | [OfferLinks](#offerlinks)               | Odkaz "Další informace" této nabídky                                                                    |
| atributy                  | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající nabídce                         |
| AttestationProperties       | [AttestationProperties](#attestationproperties) | Vlastnosti ověření identity pro SKU                   |

## <a name="offercategory"></a>OfferCategory

Popisuje kategorizaci nabídky. To zahrnuje pořadí nebo prioritu této kategorie nabídky ve srovnání s ostatními ve stejné produktové lince.

| Vlastnost   | Typ                                                           | Description                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | řetězec                                                         | Identifikátor kategorie                                                                                                                                                   |
| name       | řetězec                                                         | Název kategorie                                                                                                                                                         |
| Rank       | int                                                            | Pořadí kategorií nebo Priorita v porovnání s jinými kategoriemi v rámci jedné nabídky. Tato vlastnost by měla být nastavena pouze v případě, že je pro danou nabídku k dispozici více než jedna kategorie nabídky. |
| locale     | řetězec                                                         | Národní prostředí, ve kterém se nabídka vztahuje.                                                                                                                        |
| country    | řetězec                                                         | Země nebo oblast, kde se nabídka vztahuje.                                                                                                                   |
| odkazy      | [ResourceLinks](utility-resources.md#resourcelinks)           | Odkazy na prostředky odpovídající OfferCategory.                                                                                                                     |
| atributy | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající OfferCategory.                                                                                                                |

## <a name="offerlinks"></a>OfferLinks

Obsahuje odkazy na Další informace o této nabídce.

| Vlastnost  | Typ | Description                 |
|-----------|------|-----------------------------|
| learnMore | Odkaz | Odkaz Další informace      |
| samorozbalující      | Odkaz | Identifikátor URI pro sebe                |
| generace      | Odkaz | Další stránka položek     |
| předchozí  | Odkaz | Předchozí stránka položek |

## <a name="offerproduct"></a>OfferProduct

Produkt nebo služba, ke kterým může být přidružena více než jedna nabídka, každá s různými sadami funkcí a zaměřená na různé potřeby zákazníků.

| Vlastnost | Typ   | Description              |
|----------|--------|--------------------------|
| Id       | řetězec | Identifikátor kategorie |
| Name     | řetězec | Název kategorie       |
| Jednotka     | řetězec | Jednotka produktu.        |

## <a name="attestationproperties"></a>AttestationProperties

Představuje typ ověření identity a v případě potřeby k nákupu.

| Vlastnost              | Typ                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| attestationType              | řetězec                                      | Určuje typ ověření identity. pro Windows 365 je hodnota Windows365. text ověření Windows 365 je "rozumím, že každá osoba, která používá Windows 365 Business s Windowsm hybridním zvýhodněním, musí mít na primárním pracovním zařízení nainstalovanou platnou kopii Windows 10/11 Pro." |
| enforceAttestation           | boolean                                      | Určuje, zda je pro nákup vyžadováno ověření identity.           |

