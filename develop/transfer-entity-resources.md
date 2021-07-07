---
title: Prostředky TransferEntity
description: Partner vytvoří převod, když zákazník chce, aby jeho předplatné s partnerem bylo převedeno na jiného partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 544b9682bb0e1428fad088c818a62492198897b2
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530136"
---
# <a name="transferentity-resources"></a>Prostředky TransferEntity

Partner vytvoří převod, když zákazník chce, aby jeho předplatné s partnerem bylo převedeno na jiného partnera.

## <a name="transferentity"></a>TransferEntity (Přenosováentita)

Popisuje hodnotu transferEntity.

| Vlastnost              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | řetězec           | Identifikátor transferEntity zadaný po úspěšném vytvoření transferEntity.                               |
| čas vytvoření           | DateTime         | Datum vytvoření transferEntity ve formátu data a času. Použije se při úspěšném vytvoření transferEntity.      |
| lastModifiedTime      | DateTime         | Datum poslední aktualizace transferEntity ve formátu data a času. Použije se při úspěšném vytvoření transferEntity. |
| lastModifiedUser      | řetězec           | Uživatel, který naposledy aktualizoval transferEntity. Použije se při úspěšném vytvoření transferEntity.                          |
| customerName          | řetězec           | Nepovinný parametr. Jméno zákazníka, jehož předplatná se převádějí.                                              |
| customerTenantId      | řetězec           | Identifikátor GUID naformátovaný jako customer-id, který identifikuje zákazníka. Použije se při úspěšném vytvoření transferEntity.         |
| partnertenantid       | řetězec           | Identifikátor GUID naformátovaný jako partner-ID, který identifikuje partnera.                                                                   |
| sourcePartnerName     | řetězec           | Nepovinný parametr. Název organizace partnera, která iniciuje převod.                                           |
| sourcePartnerTenantId | řetězec           | Identifikátor GUID naformátovaný jako partner-ID, který identifikuje partnera, který zahájí převod.                                           |
| targetPartnerName     | řetězec           | Nepovinný parametr. Název organizace partnera, na kterou se převod cílí.                                         |
| targetPartnerTenantId | řetězec           | Identifikátor GUID naformátovaný jako partner-ID, který identifikuje partnera, na kterého se přenos cílí.                                  |
| položky řádku             | Pole objektů | Pole prostředků [TransferLineItem.](#transferlineitem)                                                   |
| status                | řetězec           | Stav transferEntity. Možné hodnoty jsou Aktivní (je možné je odstranit nebo odeslat) a Dokončeno (už je hotové). Použije se při úspěšném vytvoření transferEntity.|

## <a name="transferlineitem"></a>TransferLineItem

Představuje jednu položku obsaženou v transferEntity.

| Vlastnost             | Typ                             | Description                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| id                   | řetězec                           | Jedinečný identifikátor položky řádku převodu. Použije se při úspěšném vytvoření transferEntity.   |
| subscriptionId       | řetězec                           | Identifikátor předplatného.                                                                            |
| quantity             | int                              | Počet licencí nebo instancí                                                                    |
| billingCycle         | Objekt                           | Typ fakturačního cyklu nastavený pro aktuální období                                                   |
| Friendlyname         | řetězec                           | Nepovinný parametr. Popisný název položky definované partnerem, který pomáhá jednoznačně rozpoznat.                   |
| id partneraZáznam    | řetězec                           | ID partnera v záznamu (MPNID) při nákupu, ke které dojde při přijetí převodu.                 |
| ID nabídky              | řetězec                           | Identifikátor nabídky.    |
| addonItems           | Seznam objektů **TransferLineItem** | Kolekce řádových položek transferEntity pro doplňky, které se přenesou spolu se základním předplatným, které se převádí. Použije se při úspěšném vytvoření transferEntity.|
| chyba přenosu        | řetězec                           | Použije se po přijetí transferEntity v případě chyby.                |
| status               | řetězec           | Stav položky řádku v transferEntity.|

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