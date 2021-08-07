---
title: Prostředky TransferEntity
description: Partner vytvoří převod, když zákazník chce, aby jeho předplatné s partnerem bylo převedeno na jiného partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3103c0e9f8e6850336d663a5a38274ce7391e30edd433d08f44071de31b5fc5e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990201"
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
| id                   | řetězec                           | Jedinečný identifikátor položky řádku přenosu. Použije se při úspěšném vytvoření transferEntity.   |
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
| orders            | Seznam objektů [Order](order-resources.md#order)    | Kolekce objednávek.          |
| transferErrors    | Seznam objektů [TransferError](#transfererror)      | Shromažďování chyb přenosu. |

## <a name="transfererror"></a>Chyba přenosu

Představuje chybu, ke které dochází při přijetí přenosu.

| Vlastnost          | Typ   | Description                                     |
|-------------------|--------|-------------------------------------------------|
| id skupiny přenosu   | řetězec | ID skupiny objednávek objednávky s chybou. |
| kód              | int    | Kód chyby                                 |
| description       | řetězec | Popis chyby.                   |
| položky řádku         | Seznam objektů **TransferLineItem** | Kolekce řádových položek transferEntity, které jsou součástí chyby přenosu.|

## <a name="transfererrorcode"></a>TransferErrorCode

[Enum/dotnet/api/system.enum) s hodnotami, které označují typ chyby pořadí.

| Hodnota | Pozice | Description |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | V kontextu žádosti chybí token partnera. |
| Neplatný vstup | 800002 | Neplatný vstup požadavku. |
| ServiceException | 800003 | Neočekávaná chyba služby. |
| Id nabídky InvalidOfferId | 800004 | Neplatné ID nabídky. |
| CreateOrderError | 800005 | Vytvoření objednávky není úspěšné. |
| MpnIdNotFound | 800015 | ID MPN se nenašlo. |
| NotValidIndirectResellerMpnId | 800016 | ID MPN není platným nepřímým prodejcem. |
| TransferIdNotFound | 900100   | Žádost o převod se nenašla.   |
| PřenosNotAllowedIfStatusIsInProgress | 900101 | Žádost o převod už probíhá.|
| TransferNotAllowedIfStatusIsCompleted | 900102 | Žádost o převod je už dokončená.|
| TransferCreateOrderError | 900103 | Objednávka převodu není úspěšná.|
| TransferProcessedByAnotherRequest | 900104 | Převod se zpracovává jinou žádostí.|