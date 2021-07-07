---
title: Nároky na prostředky
description: Popisuje zdroje související s oprávněním.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a5ddf5dcd1189f686c5d41c05d7c66abc46605cc
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906358"
---
# <a name="entitlement-resources"></a>Nároky na prostředky

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

## <a name="entitlement"></a>Nárok

Tento prostředek představuje produkty, pro které má zákazník právo k použití z důvodu nákupu partnerů v položkách z katalogu.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | Odkaz na objednávku, který má za následek nárok. |
| productId | řetězec | ID produktu. |
| skuID | řetězec | ID SKU. |
| quantity | int | Množství nároků (nezahrnuje nesplněné/přenesené nároky). |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | Seznam podrobností o množství nároků (počet položek a stav každého množství). |
| entitlementType | řetězec | Typ nároku. (Aktualizováno na řetězec z [EntitlementType](#entitlementtype) v sadě SDK 1,8.) |
| entitledArtifacts | [Artefakt](#artifact)<IEnumerable> | Seznam artefaktů přidružených k oprávnění |
| IncludedEntitlements | Rozhraní IEnumerable<[nárok](#artifact)> | Seznam oprávnění, která jsou implicitně zahrnutá v důsledku nákupu ProductId/SkuId z katalogu. |
| ExpiryDate | řetězec ve formátu data a času standardu UTC  | Datum vypršení platnosti oprávnění (je-li k dispozici). |

## <a name="referenceorder"></a>ReferenceOrder

Odkaz na objednávku pro nárok.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| id | řetězec | ID odkazovaného pořadí |
| lineItemId | řetězec | ID odkazované položky řádku objednávky |
| alternateId | řetězec | Alternativní ID položky odkazovaného řádku objednávky |

## <a name="quantitydetail"></a>QuantityDetail

Představuje podrobnosti o množství nároků.

| Vlastnost | Typ | Description |
|----------|------|-------------|
| quantity | int | Počet položek |
| status | řetězec | Stav množství. |

## <a name="entitlementtype"></a>EntitlementType

> [!IMPORTANT]
> Zastaralé v sadě SDK v 1.9

[Výčet](/dotnet/api/system.enum) s hodnotami, které určují typ nároku.

| Hodnota | Popis |
|-------|-------------|
| Software | Označuje typ nároků související se softwarem. |
| VirtualMachineReservedInstance | Označuje typ nároku související s Azure Reserved Virtual Machine Instances. |

## <a name="artifact"></a>Artefakt

Artefakt přidružený k oprávnění

| Vlastnost | Typ | Description |
|----------|------|-------------|
| artifactType | řetězec | Typ artefaktu (Aktualizováno na řetězec z [ArtifactType](#artifacttype) v sadě SDK v 1.8) |
| dynamicAttributes | &lt;Řetězec slovníku, objekt&gt; | Dynamické atributy obsahující hodnoty specifické pro ArtifactType. například pokud artifactType = "reservedinstance", tato vlastnost bude obsahovat "reservationType" = "virtualmachines" nebo "reservationType" = "sqldatabases", který označuje rezervovanou instanci virtuálního počítače nebo rezervovanou instanci Azure SQL. (K dispozici od verze SDK v 1.9) |

## <a name="artifacttype"></a>ArtifactType

> [!IMPORTANT]
> Zastaralé v sadě SDK v 1.9

[Výčet](/dotnet/api/system.enum) s hodnotami, které určují typ artefaktu nároku.

| Hodnota                          | Popis                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Označuje pomůcky artefaktů s načítáním Azure Reserved Virtual Machine Instances. |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

Artefakt přidružený k oprávnění rezervované instance Azure Dědí z třídy [artefaktů](#artifact) .

| Vlastnost   | Typ                           | Description                                        |
|------------|--------------------------------|----------------------------------------------------|
| odkaz       | [Propojit](./utility-resources.md#link) | Odkaz pro získání podrobností o všech přidružených artefaktech.   |
| Resourceid | řetězec                         | ID objednávky rezervace Azure nebo prostředku. |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Představuje entitu vrácenou při vyvolání propojení artefaktu rezervované instance Azure.

|   Vlastnost   |           Typ           |                          Description                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     typ     |          řetězec          |                     Typ artefaktu.                     |
| Rezervace | Ienumerable<Reservation> | Označuje identifikátor objednávky prostředku Azure nebo rezervace. |

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
|   appliedScopes   |      Ienumerable<string>       | Seznam použitých rozsahů přidružených k rezervaci. (K dispozici pouze v případě, že scopeType není sdílené.) |
|     quantity      |              int               |                             Počet virtuálních počítačů v rezervaci                             |
|  datum_vypršení_platnostiAčas   | řetězec ve formátu data a času UTC |                                    Datum vypršení platnosti rezervace.                                     |
| effectiveDateTime | řetězec ve formátu data a času UTC |                                   Datum platnosti rezervace.                                   |
| provisioningState (Stav zřizování) |             řetězec             |                                 Stav zřizování rezervace.                                 |
