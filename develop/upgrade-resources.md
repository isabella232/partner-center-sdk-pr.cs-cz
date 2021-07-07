---
title: Upgradovat zdroje
description: Popisuje prostředky, které se používají k upgradu uživatele ze zdrojového předplatného na cílové předplatné.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c57994d1b1e7659df5e6448578422f6d9c21fee
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529813"
---
# <a name="upgrade-resources"></a>Upgradovat zdroje

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Popisuje prostředky, které se používají k upgradu uživatele ze zdrojového předplatného na cílové předplatné.

## <a name="upgrade"></a>Upgrade

Popisuje chování samostatného prostředku upgradu.

| Vlastnost      | Typ                   | Description                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Nabídka                  | Nabídka cílového předplatného.                                                        |
| UpgradeType   | řetězec                 | Typ upgradu: "none", " \_ pouze upgrade" nebo "upgrade \_ s \_ \_ přenosem licencí".         |
| Oprávněné    | boolean                | Určuje, zda může být upgrade proveden.                                                  |
| Množství      | integer                | Množství nové nabídky, která se má koupit Ve výchozím nastavení se jedná o množství zdrojového předplatného. |
| UpgradeErrors | pole UpgradeErrors | Důvodem je, že upgrade nelze provést, pokud je k dispozici.                                      |
| Atributy    | ResourceAttributes     | Atributy metadat odpovídající upgradu.                                        |

## <a name="upgradeerror"></a>UpgradeError

Popisuje důvod, proč nelze provést upgrade.

| Vlastnost          | Typ               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kód              | řetězec             | Kód chyby spojený s problémem: "ostatní", "oprávnění delegovaného \_ správce \_ " \_ zakázáno "," stav předplatného \_ \_ není \_ aktivní "," konfliktní \_ \_ typy služeb "," \_ konflikty souběžnosti "," \_ vyžadován kontext uživatele \_ "," odběr \_ přidané \_ Doplňky \_ "," \_ odběr \_ nemá \_ \_ žádné \_ cesty pro upgrade \_ \_ \_ \_ \_ \_ \_ "," předplatné není k dispozici "," předplatné není zřízené ", |
| Description       | řetězec             | Popisný text popisující chybu.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | řetězec             | Další podrobnosti týkající se chyby.                                                                                                                                                                                                                                                                                                                                                         |
| Atributy        | ResourceAttributes | Atributy metadat odpovídající chybě.                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>UpgradeResult

Popisuje výsledek procesu upgradu předplatného.

| Vlastnost             | Typ                        | Description                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | řetězec                      | Identifikátor zdrojového odběru.                                           |
| TargetSubscriptionID | řetězec                      | Identifikátor cílového předplatného.                                           |
| UpgradeType          | řetězec                      | Typ upgradu: "none", " \_ pouze upgrade" nebo "upgrade \_ s \_ \_ přenosem licencí". |
| UpgradeErrors        | pole UpgradeErrors      | V případě potřeby došlo k chybám při pokusu o provedení upgradu.           |
| LicenseErrors        | pole UserLicenseErrrors | V případě potřeby došlo k chybám při pokusu o migraci uživatelských licencí.          |
| Atributy           | ResourceAttributes          | Atributy metadat odpovídající licenci.                                |

## <a name="userlicenseerror"></a>UserLicenseError

Popisuje chyby způsobené neúspěšným přenosem uživatelských licencí.

| Vlastnost     | Typ                   | Description                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | řetězec                 | Jedinečný identifikovaný objekt uživatele.                                 |
| Name         | řetězec                 | Jméno uživatele                                                     |
| E-mail        | řetězec                 | E-mail uživatele                                                    |
| Chyby       | pole ServiceFaults | Seznam výjimek vyvolaných při pokusu o provedení převodu uživatelských licencí. |
| Atributy   | ResourceAttributes     | Atributy metadat odpovídající licenci.                     |

