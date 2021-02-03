---
title: Prostředky nasazení zařízení
description: Prostředky související s nasazením zařízení v partnerském centru
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a464cdad3979c305df16a3bdc9133ce70a7ac688
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766679"
---
# <a name="device-deployment-resources"></a>Prostředky nasazení zařízení

**Platí pro:**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo

Následující prostředky souvisejí s nasazením zařízení.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**ConfigurationPolicy** poskytuje informace o zásadách konfigurace.

| Vlastnost             | Typ                                                           | Description                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | řetězec                                       | Řetězec ve formátu GUID, který identifikuje zásadu.                                  |
| name                 | řetězec                                       | Popisný název zásady.                                                    |
| category             | řetězec                                       | Kategorie.                                                                        |
| description          | řetězec                                       | Popis zásady.                                                              |
| devicesAssignedCount | číslo                                       | Počet zařízení, která jsou přiřazena k této zásadě.                                       |
| policySettings       | pole řetězců                             | Nastavení zásad: "žádné", "odebrat \_ \_ předinstalované výrobci OEM", "OOBE \_ Uživatel \_ není \_ místním \_ správcem", "Přeskočit \_ expresní \_ nastavení", "Přeskočit \_ registraci OEM \_ ", "Přeskočit \_ smlouvu EULA".    |
| createdDate          | řetězec ve formátu data a času standardu UTC               | Datum a čas, kdy byla zásada vytvořena.                                            |
| lastModifiedDate     | řetězec ve formátu data a času standardu UTC               | Datum a čas poslední změny zásady                                      |
| atributy           | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                                            |

## <a name="device"></a>Zařízení

**Zařízení** poskytuje informace o zařízení.

| Vlastnost            | Typ                                                           | Description                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | řetězec                                                         | Řetězec ve formátu GUID, který identifikuje zařízení.                      |
| serialNumber        | řetězec                                                         | Sériové číslo jednoznačně přidružené k zařízení.                   |
| productKey          | řetězec                                                         | Kód Product Key jednoznačně přidružený k zařízení                     |
| hardwareHash        | řetězec                                                         | Hodnota hash hardwaru je jedinečně přidružená k zařízení.                   |
| modelName           | řetězec                                                         | Název modelu, který je přidružený k zařízení.                               |
| oemManufacturerName | řetězec                                                         | Jméno výrobce OEM přidruženého k zařízení.             |
| Zásady            | pole objektů                                               | Seznam zásad přiřazených k zařízení.                             |
| uploadedDate        | řetězec ve formátu data a času standardu UTC                                 | Datum a čas odeslání podrobností o zařízení.                      |
| allowedOperations   | pole řetězců                                               | Seznam metod HTTP povolených v zařízení se synchronizuje jako GET, PATCH, DELETE. |
| atributy          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atributy metadat.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails** popisuje stav zařízení dávkového nahrání informací o jednotlivých zařízeních v seznamu zařízení.

| Vlastnost        | Typ     | Description                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | řetězec   | Řetězec ve formátu GUID, který je přidružený k dávce nahraných zařízení. |
| status          | řetězec   | Stav dávkového nahrávání: "neznámé", "zařazeno", "zpracování", "dokončeno", "dokončeno \_ s \_ chybami". |
| startedTime     | řetězec ve formátu data a času standardu UTC | Datum a čas spuštění procesu dávkového nahrání.   |
| completedTime   | řetězec ve formátu data a času standardu UTC  | Datum a čas dokončení procesu dávkového nahrání.   |
| devicesStatus   | pole prostředků [DeviceUploadDetails](#deviceuploaddetails) | Pole objektů, které určují stav jednotlivých odeslání informací o zařízení. |
| atributy      | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**DeviceUploadDetails** popisuje stav nahrávání informací o zařízení.

| Vlastnost         | Typ                    | Description                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | řetězec                  | Řetězec ve formátu GUID, který je přidružen k zařízení. |
| serialNumber     | řetězec                  | Sériové číslo jednoznačně přidružené k zařízení. |
| productKey       | řetězec                  | Kód Product Key jednoznačně přidružený k zařízení |
| status           | řetězec                  | Stav nahrání informací o zařízení: "probíhá", "dokončeno", "dokončeno \_ s \_ chybami". |
| errorCode        | řetězec                  | Kód chyby stavu HTTP se vrátí v případě, že se nahrávání zařízení nepovede. |
| errorDescription | řetězec                  | Popis chyby HTTP, pokud nahrávání zařízení selhalo. |
| atributy       | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.   |

## <a name="devicebatch"></a>DeviceBatch

**DeviceBatch** představuje kolekci zařízení.

| Vlastnost     | Typ                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | řetězec                                                         | Řetězec ve formátu GUID, který je přidružen k dávce zařízení. |
| createdBy    | řetězec                                                         | Název tenanta, který kolekci vytvořil.                   |
| creationDate | řetězec ve formátu data a času standardu UTC                                 | Data a čas vytvoření kolekce.                    |
| Počet zařízení  | číslo                                                         | Počet zařízení v kolekci.                              |
| devicesLink  | [Odkaz](utility-resources.md#link)                              | Odkaz na zařízení obsažená v této dávce.                        |
| atributy   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atributy metadat.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**DeviceBatchCreationRequest** poskytuje informace potřebné k vytvoření dávky zařízení a jejímu naplnění pomocí zařízení.

| Vlastnost     | Typ                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| ID dávky      | řetězec                                                         | Řetězec ve formátu GUID, který je přidružen k dávce zařízení. |
| zařízení      | pole objektů [zařízení](#device)                             | Každý objekt určuje zařízení. Jsou přijaty následující kombinace polí pro identifikaci zařízení: hardwareHash + productKey, hardwareHash + sériové, hardwareHash + productKey + sériové, pouze hardwareHash, pouze productKey, sériové + oemManufacturerName + model. |
| atributy   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atributy metadat.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest** poskytuje informace potřebné k aktualizaci seznamu zařízení se zásadami.

| Vlastnost     | Typ                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| zařízení      | pole objektů [zařízení](#device)                             | Každý objekt určuje zařízení. Jsou vyžadovány následující vlastnosti: ID, zásady. |
| atributy   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atributy metadat.                                              |
