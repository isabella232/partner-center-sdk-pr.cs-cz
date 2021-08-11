---
title: Prostředky nasazení zařízení
description: Prostředky související s Partnerské centrum nasazením zařízení
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e8e2429fea88a89873955d9af9253492934e40e5be1a1b7600446485d13f5bd7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994842"
---
# <a name="device-deployment-resources"></a>Prostředky nasazení zařízení

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud (Německo)

Následující zdroje informací souvisejí s nasazením zařízení.

## <a name="configurationpolicy"></a>Zásady konfigurace

**ConfigurationPolicy** poskytuje informace o zásadách konfigurace.

| Vlastnost             | Typ                                                           | Description                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | řetězec                                       | Řetězec formátovaný identifikátorem GUID, který identifikuje zásadu.                                  |
| name                 | řetězec                                       | Popisný název zásady.                                                    |
| category             | řetězec                                       | Kategorie.                                                                        |
| description          | řetězec                                       | Popis zásady.                                                              |
| devicesAssignedCount | číslo                                       | Počet zařízení přiřazených k této zásadám                                       |
| nastavení zásad       | pole řetězců                             | Nastavení zásad: none,"remove \_ oem \_ preinstalls", "oobe \_ user not local \_ admin", skip express \_ \_ \_ \_ settings", "skip \_ oem \_ registration", "skip \_ eula".    |
| datum vytvoření          | řetězec ve formátu data a času UTC               | Datum a čas vytvoření zásady                                            |
| lastModifiedDate     | řetězec ve formátu data a času UTC               | Datum a čas poslední změny zásady                                      |
| atributy           | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat.                                            |

## <a name="device"></a>Zařízení

**Zařízení** poskytuje informace o zařízení.

| Vlastnost            | Typ                                                           | Description                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | řetězec                                                         | Řetězec ve formátu GUID, který identifikuje zařízení.                      |
| serialNumber        | řetězec                                                         | Sériové číslo jednoznačně přidružené k zařízení.                   |
| Productkey          | řetězec                                                         | Kód Product Key jednoznačně přidružený k zařízení.                     |
| hardwareHash        | řetězec                                                         | Hodnota hash hardwaru jedinečně přidružená k zařízení.                   |
| název_modelu           | řetězec                                                         | Název modelu přidružený k zařízení.                               |
| oemManufacturerName | řetězec                                                         | Název výrobce OEM přidruženého k zařízení.             |
| Zásady            | pole objektů                                               | Seznam zásad přiřazených k zařízení.                             |
| datum nahrání        | řetězec ve formátu data a času UTC                                 | Datum a čas nahrání podrobností o zařízení.                      |
| allowedOperations   | pole řetězců                                               | Seznam metod HTTP povolených v synchronizaci zařízení jako GET, PATCH, DELETE. |
| atributy          | [Atributy prostředků](utility-resources.md#resourceattributes)  | Atributy metadat.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails** popisuje stav dávkového nahrávání informací o jednotlivých zařízeních v seznamu zařízení.

| Vlastnost        | Typ     | Description                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| ID batchTrackingId | řetězec   | Řetězec ve formátu GUID, který je přidružený k dávce nahraných zařízení. |
| status          | řetězec   | Stav dávkového nahrávání: "neznámý", "zařazený do fronty", "zpracování", "dokončeno", \_ "dokončeno \_ s chybami". |
| čas spuštění     | řetězec ve formátu data a času UTC | Datum a čas zahájení procesu dávkového nahrávání   |
| completedTime (čas dokončení)   | řetězec ve formátu data a času UTC  | Datum a čas dokončení procesu dávkového nahrávání   |
| stav zařízení   | pole prostředků [DeviceUploadDetails](#deviceuploaddetails) | Pole objektů, které určují stav jednotlivých nahrávek informací o zařízení. |
| atributy      | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat.  |

## <a name="deviceuploaddetails"></a>Podrobnosti o deviceuploaddetails

**DeviceUploadDetails** popisuje stav nahrávání informací o zařízení.

| Vlastnost         | Typ                    | Description                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | řetězec                  | Řetězec ve formátu GUID, který je přidružený k zařízení. |
| serialNumber     | řetězec                  | Sériové číslo jednoznačně přidružené k zařízení. |
| Productkey       | řetězec                  | Kód Product Key jednoznačně přidružený k zařízení. |
| status           | řetězec                  | Stav nahrávání informací o zařízení: Probíhá, Dokončeno, Dokončeno \_ \_ s chybami. |
| Errorcode        | řetězec                  | Pokud nahrávání zařízení selže, vrátí se kód chyby stavu HTTP. |
| Popis chyby | řetězec                  | Popis chyby HTTP, pokud se nahrávání zařízení nezdaří. |
| atributy       | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat.   |

## <a name="devicebatch"></a>DeviceBatch

**DeviceBatch** představuje kolekci zařízení.

| Vlastnost     | Typ                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | řetězec                                                         | Řetězec formátovaný identifikátorem GUID, který je přidružený k dávce zařízení. |
| createdBy (vytvořil)    | řetězec                                                         | Název tenanta, který kolekci vytvořil.                   |
| datum vytvoření | řetězec ve formátu data a času UTC                                 | Data a čas vytvoření kolekce.                    |
| deviceCount  | číslo                                                         | Počet zařízení v kolekci                              |
| zařízeníOdkaz  | [Odkaz](utility-resources.md#link)                              | Odkaz na zařízení obsažená v této dávce.                        |
| atributy   | [Atributy prostředků](utility-resources.md#resourceattributes)  | Atributy metadat.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**DeviceBatchCreationRequest** poskytuje informace potřebné k vytvoření dávky zařízení a naplní ji zařízeními.

| Vlastnost     | Typ                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| ID dávky      | řetězec                                                         | Řetězec formátovaný identifikátorem GUID, který je přidružený k dávce zařízení. |
| zařízení      | pole [objektů](#device) zařízení                             | Každý objekt určuje zařízení. Akceptují se následující kombinace polí pro identifikaci zařízení: hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, jenom hardwareHash, jenom productKey, serialNumber + oemManufacturerName + modelName. |
| atributy   | [Atributy prostředků](utility-resources.md#resourceattributes)  | Atributy metadat.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest** poskytuje informace potřebné k aktualizaci seznamu zařízení pomocí zásad.

| Vlastnost     | Typ                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| zařízení      | pole [objektů](#device) zařízení                             | Každý objekt určuje zařízení. Jsou vyžadovány následující vlastnosti: Id, Zásady. |
| atributy   | [Atributy prostředků](utility-resources.md#resourceattributes)  | Atributy metadat.                                              |
