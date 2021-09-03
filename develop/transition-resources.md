---
title: Přechod prostředků
description: Popisuje prostředky, které se používají k převodu nových předplatných Commerce.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 44867be3823414ab43957e789c0cd29aef44d956
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457293"
---
# <a name="transition-resources"></a>Přechod prostředků

**Platí pro**

- Partnerské centrum

**Příslušné role**

- Globální správce
- Agent správce

> [!Note] 
> Nové obchodní změny jsou aktuálně k dispozici pouze partnerům, kteří jsou součástí M365/D365 New Commerce Experience Technical Preview.

Popisuje prostředky, které se používají k přechodu z jednoho nového předplatného Commerce na jiný.

## <a name="transitioneliblity"></a>TransitionEliblity

Popisuje chování jednotlivých prostředků přechodu v rámci předplatného.

| Vlastnost          | Typ                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| CatalogItemId | řetězec                  | ID položky katalogu, která se má zkontrolovat |
| Nadpis  | řetězec                  | Název SKU |
| Description | řetězec                  | Popis SKU |
| Množství | integer                 | Množství nové nabídky, která se má koupit |
| Eligibilities | seznam TransitionEligibilityDetail | Seznam podrobností o způsobilosti přechodu. | 

## <a name="transitioneligibilitydetail"></a>TransitionEligibilityDetail

Popisuje chování zdroje podrobností o způsobilosti jednotlivých přechodů.

| Vlastnost          | Typ                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| Oprávněné | boolean | Vrátí nárok, který je platný, nebo ne. |
| TransitionType | TransitionType | Typ přechodu. Může být transition_with_license_transfer nebo transition_only. |
| Chyby | Seznam TransitionErrors | Atributy metadat odpovídající chybě. |

## <a name="transition"></a>Transition

Popisuje chování jednotlivých prostředků přechodu v rámci předplatného.

| Vlastnost          | Typ                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| FromCatalogItemId | řetězec                  | Z ID položky katalogu |
| ToCatalogItemId   | řetězec                  | Do ID položky katalogu. |
| ToSubscriptionId  | řetězec                  | Do ID předplatného. Tato hodnota se naplní jenom v případě, že se předplatné mění. V současné době upgrade vyžaduje jenom starší verze, ale moderní částečný přechod taky. |
| Množství          | integer                 | Množství, které je převáděno do cílové položky katalogu. |
| TransitionType    | řetězec              | Typ přechodu. Možné hodnoty – transition_only, transition_with_license_transfer.   |
| Události            | seznam TransitionEvents | Události přechodu. |

## <a name="transitionevent"></a>TransitionEvent

Popisuje důvod, proč nelze provést upgrade.

| Vlastnost          | Typ               | Popis                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|------------------------------------------------------------------------------|
| Název | řetězec | Název události přechodu. Možné hodnoty Conversion nebo LicenseReassignment. |
| Status | řetězec  | Stav události přechodu. Možné hodnoty: probíhá, dokončeno nebo chyba.  |
| Timestamp | DateTime | Časové razítko UTC události. |
| Chyby | Seznam TransitionErrors | Atributy metadat odpovídající chybě. |

## <a name="transitionerror"></a>TransitionError

Představuje chybu způsobilosti převodu předplatného. Poskytuje důvod, proč nelze provést přechod.

| Vlastnost          | Typ               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|--------------------------------------------------------------|
| Kód | TransitionErrorCode | Kód chyby přidružený k problému. |
| Description | řetězec  | Popisný text popisující chybu. |

