---
title: Nároky na prostředky
description: Popisuje zdroje související s oprávněním.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 428ac6f8b4d67894092119a6246279045a04dac0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766851"
---
# <a name="entitlement-resources"></a>Nároky na prostředky

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

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
| dynamicAttributes | &lt;Řetězec slovníku, objekt&gt; | Dynamické atributy obsahující hodnoty specifické pro ArtifactType. Například pokud artifactType = "reservedinstance", tato vlastnost bude obsahovat "reservationType" = "VirtualMachines" nebo "reservationType" = "sqldatabases" označuje rezervovanou instanci virtuálního počítače nebo rezervovanou instanci Azure SQL. (K dispozici od verze SDK v 1.9) |

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
| odkaz       | [Odkaz](./utility-resources.md#link) | Odkaz pro získání všech přidružených podrobností artefaktu.   |
| Prostředku | řetězec                         | ID objednávky nebo prostředku rezervace Azure |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Představuje entitu, která se vrátila při vyvolání odkazu na artefakt rezervované instance Azure.

|   Vlastnost   |           Typ           |                          Description                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     typ     |          řetězec          |                     Typ artefaktu                     |
| rezervace | Rozhraní<Reservation> | Indikuje identifikátor objednávky prostředku Azure nebo rezervace. |

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
| odkaz       | [Odkaz](utility-resources.md#link) | Odkaz pro získání všech přidružených podrobností artefaktu.   |
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
|   appliedScopes   |      Rozhraní<string>       | Seznam použitých oborů přidružených k rezervaci. (K dispozici, jenom když není sdílená scopeType.) |
|     quantity      |              int               |                             Počet virtuálních počítačů v rezervaci.                             |
|  expiryDateTime   | řetězec ve formátu data a času standardu UTC |                                    Datum vypršení platnosti rezervace.                                     |
| effectiveDateTime | řetězec ve formátu data a času standardu UTC |                                   Datum platnosti rezervace                                   |
| provisioningState |             řetězec             |                                 Stav zřizování rezervace.                                 |
