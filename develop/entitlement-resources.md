---
title: Prostředky nároků
description: Popisuje prostředky související s nárokem.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 929004fff804675218e267bb928b432f7b1209bf
ms.sourcegitcommit: 84a6f701190f46d2adcf6edcaeaafa32d58fbaba
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2021
ms.locfileid: "113510104"
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
| odkaz       | [Odkaz](./utility-resources.md#link) | Odkaz pro získání podrobností o všech přidružených artefaktech.   |
| Resourceid | řetězec                         | ID objednávky rezervace Azure nebo prostředku. |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Představuje entitu vrácenou při vyvolání propojení artefaktu rezervované instance Azure.

|   Vlastnost   |           Typ           |                          Description                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     typ     |          řetězec          |                     Typ artefaktu.                     |
| Rezervace | `IEnumerable<Reservation>` | Označuje identifikátor objednávky prostředku Azure nebo rezervace. |

## <a name="reservation"></a>Rezervace

Představuje jednotlivou rezervaci.

| Vlastnost          | Typ                           | Description                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | řetězec                         | ID rezervace.                                         |
| scopeType (typ oboru)         | řetězec                         | Typ oboru přidruženého k rezervaci virtuálního počítače. |
| displayName       | řetězec                         | Zobrazovaný název rezervace                               |
| appliedScopes     | Ienumerable                    | Seznam použitých rozsahů přidružených k rezervaci. (K dispozici pouze v případě, že scopeType není sdílené.) |
| quantity          | int                            | Počet virtuálních počítačů v rezervaci                 |
| datum_vypršení_platnostiAčas    | řetězec ve formátu data a času UTC | Datum vypršení platnosti rezervace.                                |
| effectiveDateTime | řetězec ve formátu data a času UTC | Datum platnosti rezervace.                             |
| provisioningState (Stav zřizování) | řetězec                         | Stav zřizování rezervace.                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> Zastaralé v sadě SDK verze 1.9

Artefakt přidružený k nároku na rezervovanou instanci virtuálního počítače Azure Dědí z [třídy Artifact.](#artifact)

| Vlastnost   | Typ                              | Description                                        |
|------------|-----------------------------------|----------------------------------------------------|
| odkaz       | [Odkaz](utility-resources.md#link) | Odkaz pro získání podrobností o všech přidružených artefaktech.   |
| Resourceid | řetězec                            | ID objednávky rezervace Azure nebo prostředku. |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> Zastaralé v sadě SDK verze 1.9

Představuje entitu vrácenou při vyvolání propojení artefaktu rezervované instance virtuálního počítače Azure.

| Vlastnost                    | Typ                                                                 | Description           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| typ                        | [ArtifactType (Typ artefaktu)](#artifacttype)                                        | Typ artefaktu. |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Označuje identifikátor objednávky prostředku Azure nebo rezervace. |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> Zastaralé v sadě SDK verze 1.9

Představuje individuální rezervaci virtuálního počítače.

|     Vlastnost      |              Typ              |                                                Description                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             řetězec             |                                         ID rezervace.                                         |
|     scopeType (typ oboru)     |             řetězec             |                     Typ oboru přidruženého k rezervaci virtuálního počítače.                     |
|    displayName    |             řetězec             |                                    Zobrazovaný název rezervace                                    |
|   appliedScopes   |      `IEnumerable<string>`       | Seznam použitých rozsahů přidružených k rezervaci. (K dispozici pouze v případě, že scopeType není sdílené.) |
|     quantity      |              int               |                             Počet virtuálních počítačů v rezervaci                             |
|  datum_vypršení_platnostiAčas   | řetězec ve formátu data a času UTC |                                    Datum vypršení platnosti rezervace.                                     |
| effectiveDateTime | řetězec ve formátu data a času UTC |                                   Datum platnosti rezervace.                                   |
| provisioningState (Stav zřizování) |             řetězec             |                                 Stav zřizování rezervace.                                 |
