---
title: Prostředky nároků
description: Popisuje prostředky související s nárokem.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9582bb0d886078062ae14d0461accb8e0179bed2e33e9a264cc1da8b06383706
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989147"
---
# <a name="entitlement-resources"></a>Prostředky nároků

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

## <a name="entitlement"></a>Nárok

Tento prostředek představuje produkty, ke kterým má zákazník právo používat v závislosti na nákupu položek z katalogu partnerem.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| referenčníobjednávky | [Pořadíobjednávky odkazu](#referenceorder) | Odkaz na objednávku, který vyústil v nárok. |
| productId | řetězec | ID produktu. |
| skuID | řetězec | The ID of the SKU. |
| quantity | int | Množství nároků (nezahrnuje nevyplněné nebo převedené nároky). |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | Seznam podrobností o množství nároků (počet položek a stav každého množství) |
| entitlementType (typ nároku) | řetězec | Typ nároku. (Aktualizace na řetězec z [EntitlementType v](#entitlementtype) sadě SDK 1.8.) |
| entitledArtifacts | IEnumerable –<[artefaktu](#artifact)> | Seznam artefaktů přidružených k nároku. |
| Zahrnuté ádosti | IEnumerable<[nárok](#artifact)> | Seznam nároků, které jsou implicitně zahrnuty jako výsledek nákupu ProductId / SkuId z katalogu. |
| Datum vypršení platnosti | řetězec ve formátu data a času UTC  | Datum vypršení platnosti nároku (pokud je to dostupné). |

## <a name="referenceorder"></a>Pořadíobjednávky odkazu

Odkaz na objednávku nároku.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| id | řetězec | ID odkazovaného pořadí. |
| ID položky řádku | řetězec | ID odkazované řádkové položky objednávky. |
| alternativní ID | řetězec | Alternativní ID odkazované řádkové položky objednávky. |

## <a name="quantitydetail"></a>Podrobnosti o množství

Představuje podrobnosti o množství nároků.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| quantity | int | Počet položek |
| status | řetězec | Stav množství |

## <a name="entitlementtype"></a>Typ nároku

> [!IMPORTANT]
> Zastaralé v sadě SDK verze 1.9

Výčet [s](/dotnet/api/system.enum) hodnotami, které označují typ nároku.

| Hodnota | Popis |
|-------|-------------|
| Software | Označuje typ nároku související se softwarem. |
| VirtualMachineReservedInstance | Označuje typ nároku související s Azure Reserved Virtual Machine Instances. |

## <a name="artifact"></a>Artefakt

Artefakt přidružený k nároku.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| artifactType (typ artefaktu) | řetězec | Typ artefaktu. (Aktualizace na řetězec z [ArtifactType v](#artifacttype) sadě SDK verze 1.8) |
| dynamicAttributes | Řetězec &lt; slovníku, objekt&gt; | Dynamické atributy obsahující hodnoty specifické pro artifacttype Pokud například artifactType = "reservedinstance", bude tato vlastnost obsahovat "reservationType" = "virtualmachines" nebo "reservationType" = "sqldatabases" označující rezervovanou instanci virtuálního počítače nebo SQL rezervované instance Azure. (K dispozici od verze SDK v1.9) |

## <a name="artifacttype"></a>ArtifactType (Typ artefaktu)

> [!IMPORTANT]
> Zastaralé v sadě SDK verze 1.9

Výčet [s hodnotami,](/dotnet/api/system.enum) které označují typ artefaktu nároku.

| Hodnota                          | Popis                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Označuje, že artefakt pomáhá s načtením Azure Reserved Virtual Machine Instances. |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

Artefakt přidružený k nároku na rezervovanou instanci Azure. Dědí z [třídy Artifact.](#artifact)

| Vlastnost   | Typ                           | Description                                        |
|------------|--------------------------------|----------------------------------------------------|
| odkaz       | [Odkaz](./utility-resources.md#link) | Odkaz pro získání všech přidružených podrobností artefaktu.   |
| Prostředku | řetězec                         | ID objednávky nebo prostředku rezervace Azure |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Představuje entitu, která se vrátila při vyvolání odkazu na artefakt rezervované instance Azure.

|   Vlastnost   |           Typ           |                          Description                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     typ     |          řetězec          |                     Typ artefaktu                     |
| rezervace | `IEnumerable<Reservation>` | Indikuje identifikátor objednávky prostředku Azure nebo rezervace. |

## <a name="reservation"></a>Rezervace

Představuje jednotlivou rezervaci.

| Vlastnost          | Typ                           | Description                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | řetězec                         | ID rezervace                                         |
| scopeType         | řetězec                         | Typ oboru přidružený k rezervovanému virtuálnímu počítači. |
| displayName       | řetězec                         | Zobrazovaný název rezervace.                               |
| appliedScopes     | Rozhraní                    | Seznam použitých oborů přidružených k rezervaci. (K dispozici, jenom když není sdílená scopeType.) |
| quantity          | int                            | Počet virtuálních počítačů v rezervaci.                 |
| expiryDateTime    | řetězec ve formátu data a času standardu UTC | Datum vypršení platnosti rezervace.                                |
| effectiveDateTime | řetězec ve formátu data a času standardu UTC | Datum platnosti rezervace                             |
| provisioningState | řetězec                         | Stav zřizování rezervace.                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> Zastaralé v sadě SDK v 1.9

Artefakt přidružený k rezervované instanci virtuálního počítače Azure s rezervovaným oprávněním Dědí z třídy [artefaktů](#artifact) .

| Vlastnost   | Typ                              | Description                                        |
|------------|-----------------------------------|----------------------------------------------------|
| odkaz       | [Propojit](utility-resources.md#link) | Odkaz pro získání všech přidružených podrobností artefaktu.   |
| Prostředku | řetězec                            | ID objednávky nebo prostředku rezervace Azure |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> Zastaralé v sadě SDK v 1.9

Představuje entitu, která se vrátila při volání rezervovaného odkazu artefaktu instance virtuálního počítače Azure.

| Vlastnost                    | Typ                                                                 | Description           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| typ                        | [ArtifactType](#artifacttype)                                        | Typ artefaktu |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Indikuje identifikátor objednávky prostředku Azure nebo rezervace. |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> Zastaralé v sadě SDK v 1.9

Představuje jednotlivé rezervace virtuálních počítačů.

|     Vlastnost      |              Typ              |                                                Description                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             řetězec             |                                         ID rezervace                                         |
|     scopeType     |             řetězec             |                     Typ oboru přidružený k rezervovanému virtuálnímu počítači.                     |
|    displayName    |             řetězec             |                                    Zobrazovaný název rezervace.                                    |
|   appliedScopes   |      `IEnumerable<string>`       | Seznam použitých oborů přidružených k rezervaci. (K dispozici, jenom když není sdílená scopeType.) |
|     quantity      |              int               |                             Počet virtuálních počítačů v rezervaci.                             |
|  expiryDateTime   | řetězec ve formátu data a času standardu UTC |                                    Datum vypršení platnosti rezervace.                                     |
| effectiveDateTime | řetězec ve formátu data a času standardu UTC |                                   Datum platnosti rezervace                                   |
| provisioningState |             řetězec             |                                 Stav zřizování rezervace.                                 |
