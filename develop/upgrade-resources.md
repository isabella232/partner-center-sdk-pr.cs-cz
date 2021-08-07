---
title: Upgradovat zdroje
description: Popisuje prostředky, které se používají k upgradu uživatele ze zdrojového předplatného na cílové předplatné.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1ea7499a21312378f4fad3d47eaa9e10993ee3ce7ddb1498f161fac16e09b8a5
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992465"
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

