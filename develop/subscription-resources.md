---
title: Prostředky předplatného
description: Prostředky předplatného mohou poskytovat další informace o předplatných v průběhu životního cyklu, jako je podpora, refundace nebo nároky Azure.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 461df9cdb909fc44be9069cb7eb4b41fa2a5f170
ms.sourcegitcommit: 3ee00d9fe9da6b9df0fb7027ae506e2abe722770
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2021
ms.locfileid: "129417283"
---
# <a name="subscription-resources"></a>Prostředky předplatného

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Předplatné umožňuje zákazníkovi používat službu po určitou dobu. Ne všechna pole se použijí pro všechna předplatná. Mnoho polí se používá pouze v určitých bodech životního cyklu, například v případě, že je předplatné pozastavené nebo zrušené.

## <a name="subscription"></a>Předplatné

>[!NOTE]
>U **prostředku předplatného** platí omezení rychlosti 500 požadavků za minutu na identifikátor tenanta.

Prostředek **Předplatné** představuje životní cyklus předplatného a zahrnuje vlastnosti, které definují stavy v průběhu životního cyklu předplatného.

| Vlastnost             | Typ                                                          | Popis                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | řetězec                                                        | Identifikátor předplatného.                                                                                                                                                  |
| ID nabídky              | řetězec                                                        | Identifikátor nabídky.                                                                                                                                                         |
| entitlementId (ID nároku)        | řetězec                                                        | Identifikátor nároku (ID předplatného Azure).                                                                                                                        |
| název_nabídky            | řetězec                                                        | Název nabídky                                                                                                                                                               |
| Friendlyname         | řetězec                                                        | Popisný název předplatného definovaného partnerem, který pomáhá jednoznačně rozpoznat.                                                                                           |
| quantity             | číslo                                                        | Množství Například v případě fakturace na základě licencí je tato vlastnost nastavená na počet licencí.                                                            |
| Unittype             | řetězec                                                        | Jednotky definující množství pro předplatné.                                                                                                                             |
| parentSubscriptionId | řetězec                                                        | Získá nebo nastaví identifikátor nadřazeného předplatného.                                                                                                                              |
| datum vytvoření         | řetězec                                                        | Získá nebo nastaví datum vytvoření ve formátu data a času.                                                                                                                          |
| effectiveStartDate   | řetězec ve formátu data a času UTC                                | Získá nebo nastaví efektivní počáteční datum pro toto předplatné ve formátu data a času. Slouží k obnovení data migrovaných předplatných nebo k jeho sladění s jiným.                |
| datum ukončení závazku    | řetězec ve formátu data a času UTC                                | Koncové datum závazku pro toto předplatné ve formátu data a času. U předplatných, která není možné automaticky obnovit, představuje datum daleko, daleko do budoucna.       |
| status               | řetězec                                                        | Stav předplatného: žádné, Aktivní, Čekající, Pozastaveno, Platnost vypršela nebo Odstraněno.                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Získá hodnotu určující, jestli se odběr obnovil automaticky.                                                                                                    |
| typ fakturace          | řetězec                                                        | Určuje, jak se předplatné účtuje: "žádné", "využití" nebo "licence".                                                                                                      |
| billingCycle         | řetězec                                                        | Určuje frekvenci, s jakou se partner účtuje za tuto objednávku. Podporované hodnoty jsou názvy členů, které najdete v [**části BillingCycleType**](product-resources.md#billingcycletype). |
| hasPurchasableAddons | boolean                                                       | Získá nebo nastaví hodnotu určující, jestli má předplatné doplňky, které je možné koupit.                                                                                             |
| isTrial (aplikace isTrial)              | boolean                                                       | Hodnota určující, jestli se jedná o zkušební předplatné.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | Hodnota, která určuje, jestli se jedná o produkt Microsoftu.                                                                                                                       |
| publisherName        | řetězec                                                        | Název vydavatele.                                                                                                                                                           |
| akce              | pole řetězců                                              | Získá nebo nastaví akce, které jsou povoleny. Možné hodnoty: edit (upravit), cancel (zrušit).                                                                                                  |
| ID partnera            | řetězec                                                        | ID MPN záznamu prodejce použitého v modelu nepřímého partnera.                                                                                                     |
| suspensionReasons    | pole řetězců                                              | Jen pro čtení. Pokud bylo předplatné pozastavené, indikuje důvod.                                                                                                                  |
| contractType (Typ kontraktu)         | řetězec                                                        | Jen pro čtení. Typ kontraktu: "subscription", "productKey" nebo "redemptionCode".                                                                                           |
| refundOptions        | pole prostředků [RefundOption](#refundoption)   | Jen pro čtení. Sada možností refundace, které jsou k dispozici pro toto předplatné.                                                                                              |
| Odkazy                | [Odkazy na předplatné](#subscriptionlinks)                       | Získá nebo nastaví odkazy na předplatné.                                                                                                                                          |
| Kódobjednávky              | řetězec                                                        | ID objednávky, která byla umístěna za účelem zahájení odběru.                                                                                                                |
| termDuration         | řetězec                                                        | Reprezentace doby trvání období podle STANDARDu ISO 8601. Aktuální podporované hodnoty jsou **P1M (1** měsíc), **P1Y** (1 rok) a **P3Y** (3 roky).                                                        |
| atributy           | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat odpovídající předplatnému.                                                                                                                    |
| renewalTermDuration  | řetězec                                                        | Reprezentace doby trvání období podle STANDARDu ISO 8601. Aktuální podporované hodnoty jsou **P1M (1** měsíc) a **P1Y** (1 rok).                                                        |
| Typ produktu  | [Itemtype](product-resources.md#itemtype)                             | Jen pro čtení. Typ produktu, pro který se předplatné používá.     |
| consumptionType (typ spotřeby)  | pole prostředků [nadage](subscription-resources.md#overage)   | Získá nebo nastaví nadage pro daného zákazníka.     |

## <a name="subscriptionlinks"></a>Odkazy na předplatné

Prostředek **SubscriptionLinks** popisuje kolekci odkazů připojených k prostředku předplatného.

| Vlastnost           | Typ                               | Popis                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [Odkaz](utility-resources.md#link) | Získá nebo nastaví nabídku.               |
| parentSubscription (nadřazenépředřazení) | [Odkaz](utility-resources.md#link) | Získá nebo nastaví nadřazené předplatné. |
| product            | [Odkaz](utility-resources.md#link) | Získá produkt přidružený k předplatnému. |
| Sku                | [Odkaz](utility-resources.md#link) | Získá SKU produktu přidružené k předplatnému. |
| dostupnosti       | [Odkaz](utility-resources.md#link) | Získá dostupnost SKU produktu přidruženou k předplatnému. |
| aktivační odkazy    | [Odkaz](utility-resources.md#link) | Získá seznam aktivačních odkazů přidružených k předplatnému. |
| Vlastní               | [Odkaz](utility-resources.md#link) | Identifikátor URI sebe sama.                         |
| Další               | [Odkaz](utility-resources.md#link) | Další stránka položek               |
| Předchozí           | [Odkaz](utility-resources.md#link) | Předchozí stránka položek           |

## <a name="subscriptionprovisioningstatus"></a>Stav zřizování předplatného

Prostředek **SubscriptionProvisioningStatus** poskytuje informace o stavu zřizování předplatného.

| Vlastnost   | Typ                                                           | Popis                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| ID SKU      | řetězec                                                         | Řetězec formátovaný identifikátorem GUID, který identifikuje SKU produktu.             |
| status     | řetězec                                                         | Označuje stav zřizování: "success", "pending" nebo "failed". |
| quantity   | číslo                                                         | Poskytuje množství předplatných po zřízení.               |
| Enddate    | řetězec ve formátu data a času UTC                                 | Koncové datum odběru.                                    |
| atributy | [Atributy prostředků](utility-resources.md#resourceattributes)  | Atributy metadat.                                             |

## <a name="subscriptionregistrationstatus"></a>Stav registrace předplatného

Prostředek **SubscriptionRegistrationStatus** popisuje kolekci odkazů připojených k prostředku předplatného.

| Vlastnost           | Typ                               | Popis                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | řetězec                             | Identifikátor předplatného.                                                          |
| status             | řetězec                             | Označuje stav registrace: "registered", "registering" nebo "notregistered".    |

## <a name="supportcontact"></a>PodporaKontakt

Prostředek **SupportContact** představuje kontakt podpory pro předplatné zákazníka.

| Vlastnost        | Typ                                                           | Popis                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | řetězec                                                         | Řetězec ve formátu GUID, který označuje identifikátor tenanta kontaktu podpory. |
| supportMpnId    | řetězec                                                         | Identifikátor MPN (Microsoft Partner Network) kontaktu.                       |
| name            | řetězec                                                         | Název kontaktu podpory.                                                |
| Odkazy           | [Odkazy na prostředky](utility-resources.md#resourcelinks)            | Odkazy související s kontaktem podpory.                                              |
| atributy      | [Atributy prostředků](utility-resources.md#resourceattributes)  | Atributy metadat. Obsahuje objectType: SupportContact.              |

## <a name="overage"></a>Překročení

Prostředek **nadage představuje** nadprodejní předplatné, ke které je možné přiřadit nadage předplatného podle toho, jestli je přiřazený, a prodejce.

| Vlastnost        | Typ               | Popis                                                                     |
|-----------------|--------------------|---------------------------------------------------------------------------------|
| id předplatného azureEnti zaměněn | řetězec       | Řetězec formátovaný identifikátorem GUID, který označuje identifikátor předplatného consumption. |
| ID partnera    | řetězec            | Identifikátor Microsoft Partner Network (MPN) prodejce přidruženého k předplatnému.        |
| typ    | řetězec       | Typ nadbytku může být PhoneServices.       |
| nadage (nadage)            | boolean      | Hodnota, která určuje, jestli je povolené nadáčení.       |
| Odkazy           | [Odkazy na prostředky](utility-resources.md#resourcelinks)            | Odkazy související s nadávkem                          |
| atributy      | [Atributy prostředků](utility-resources.md#resourceattributes)  | Atributy metadat. Obsahuje "objectType": "Overage".  |



## <a name="registersubscription"></a>RegisterSubscription

Prostředek **RegisterSubscription** vrátí odkaz, který můžete použít k dotazování stavu registrace předplatného. Stav registrace se vrátí v textu odpovědi úspěšného přijatého požadavku na registraci předplatného Azure.

| Vlastnost                | Typ                               | Popis                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | object                             | Vrátí stavový kód HTTP 202 Přijato s hlavičkou Location obsahující odkaz na dotaz na stav registrace. Například `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"`. |

## <a name="refundoption"></a>RefundOption

Prostředek **RefundOption** představuje možnou možnost refundace pro předplatné.

| Vlastnost          | Typ | Popis                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| typ | řetězec | Typ refundace Podporované hodnoty jsou Partial (Částečná) a Full (Úplné). |
| expiresAfter      | řetězec ve formátu data a času UTC | Časové razítko, kdy vyprší platnost této možnosti. Pokud má hodnotu null, znamená to, že nemá žádné vypršení platnosti. |

## <a name="azureentitlement"></a>AzureEnti pro správu

Prostředek **AzureEnti pro předplatné** představuje nároky Azure.

| Vlastnost          | Typ | Popis                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| id | řetězec | Identifikátor nároku |
| Friendlyname      | řetězec | Popisný název nároku. |
| status | řetězec | Stav nároku |
| subscriptionId | řetězec | Identifikátor předplatného, do které nárok patří. |
