---
title: Prostředky TransferEntity
description: Partner vytvoří přenos, pokud chce zákazník předplatné s partnerem přenést na jiného partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96c43d255fcd31e6dc4de50baa0e19f5d8855685
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766824"
---
# <a name="transferentity-resources"></a>Prostředky TransferEntity

**Platí pro:**

- Partnerské centrum

Partner vytvoří přenos, pokud chce zákazník předplatné s partnerem přenést na jiného partnera.

## <a name="transferentity"></a>TransferEntity

Popisuje transferEntity.

| Vlastnost              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | řetězec           | TransferEntity identifikátor, který je poskytnut po úspěšném vytvoření transferEntity.                               |
| createdTime           | DateTime         | Datum, kdy byl transferEntity vytvořen, ve formátu data a času. Použito po úspěšném vytvoření transferEntity.      |
| Časposledníúpravy      | DateTime         | Datum poslední aktualizace transferEntity ve formátu data a času. Použito po úspěšném vytvoření transferEntity. |
| lastModifiedUser      | řetězec           | Uživatel, který transferEntity naposledy aktualizoval. Použito po úspěšném vytvoření transferEntity.                          |
| customerName          | řetězec           | Nepovinný parametr. Jméno zákazníka, jehož odběry se přenáší.                                              |
| customerTenantId      | řetězec           | Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka. Použito po úspěšném vytvoření transferEntity.         |
| partnertenantid       | řetězec           | ID partnera naformátovaného identifikátorem GUID, který identifikuje partnera.                                                                   |
| sourcePartnerName     | řetězec           | Nepovinný parametr. Název organizace partnera, který iniciuje přenos.                                           |
| sourcePartnerTenantId | řetězec           | ID partnera naformátovaného identifikátorem GUID, který identifikuje partnera iniciující přenos.                                           |
| targetPartnerName     | řetězec           | Nepovinný parametr. Název organizace partnera, na kterou je přenos zaměřen.                                         |
| targetPartnerTenantId | řetězec           | ID partnera formátovaného identifikátorem GUID, který identifikuje partnera, kterému je směrován cíl přenosu.                                  |
| Položky řádku             | Pole objektů | Pole prostředků [TransferLineItem](#transferlineitem)                                                   |
| status                | řetězec           | Stav transferEntity. Možné hodnoty jsou "aktivní" (lze je odstranit/odeslat) a "dokončeno" (již bylo dokončeno). Použito po úspěšném vytvoření transferEntity.|

## <a name="transferlineitem"></a>TransferLineItem

Představuje jednu položku obsaženou v transferEntity.

| Vlastnost             | Typ                             | Description                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| id                   | řetězec                           | Jedinečný identifikátor pro položku na lince přenosu. Použito po úspěšném vytvoření transferEntity.   |
| subscriptionId       | řetězec                           | Identifikátor předplatného.                                                                            |
| quantity             | int                              | Počet licencí nebo instancí.                                                                    |
| billingCycle         | Objekt                           | Typ fakturačního cyklu nastaveného pro aktuální období.                                                   |
| friendlyName         | řetězec                           | Nepovinný parametr. Popisný název položky definované partnerem, který vám umožní určit nejednoznačnost.                   |
| partnerIdOnRecord    | řetězec                           | PartnerId na záznamu (MPNID) při nákupu, který se stane při přijetí přenosu.                 |
| Hodnotami OfferId              | řetězec                           | Identifikátor nabídky    |
| addonItems           | Seznam objektů **TransferLineItem** | Kolekce položek řádku transferEntity pro doplňky, které se přenesou spolu se základním předplatným, které se přenáší. Použito po úspěšném vytvoření transferEntity.|
| transferError        | řetězec                           | Používá se po přijetí transferEntity v případě chyby.                |
| status               | řetězec           | Stav LineItem v transferEntity.|

## <a name="transfersubmitresult"></a>TransferSubmitResult

Představuje výsledek přijetí přenosu.

| Vlastnost          | Typ                                                  | Description                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| orders            | Seznam objektů [objednávky](order-resources.md#order)    | Kolekce objednávek.          |
| transferErrors    | Seznam objektů [TransferError](#transfererror)      | Kolekce chyb přenosu. |

## <a name="transfererror"></a>TransferError

Představuje chybu, ke které dojde při přijetí přenosu.

| Vlastnost          | Typ   | Description                                     |
|-------------------|--------|-------------------------------------------------|
| transferGroupId   | řetězec | ID skupiny objednávek objednávky s chybou. |
| kód              | int    | Kód chyby                                 |
| description       | řetězec | Popis chyby.                   |
| Položky řádku         | Seznam objektů **TransferLineItem** | Kolekce položek transferEntity řádků, které jsou součástí chyby přenosu.|

## <a name="transfererrorcode"></a>TransferErrorCode

[Enum/dotnet/API/System. Enum) s hodnotami, které označují typ chyby pořadí.

| Hodnota | Pozice | Description |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | V kontextu požadavku chybí token partnera. |
| InvalidInput | 800002 | Neplatný vstup žádosti |
| ServiceException | 800003 | Neočekávaná chyba služby |
| InvalidOfferId | 800004 | Neplatné ID nabídky |
| CreateOrderError | 800005 | Vytvoření objednávky není úspěšné. |
| MpnIdNotFound | 800015 | ID MPN se nenašlo. |
| NotValidIndirectResellerMpnId | 800016 | ID MPN není platný nepřímý prodejce. |
| TransferIdNotFound | 900100   | Požadavek na přenos nebyl nalezen.   |
| TransferNotAllowedIfStatusIsInProgress | 900101 | Požadavek na přenos již probíhá.|
| TransferNotAllowedIfStatusIsCompleted | 900102 | Žádost o přenos je už dokončená.|
| TransferCreateOrderError | 900103 | Pořadí přenosů neproběhlo úspěšně.|
| TransferProcessedByAnotherRequest | 900104 | Přenos se zpracovává jiným požadavkem.|