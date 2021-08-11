---
title: PřevodSchůdnost prostředků
description: Partner může vytvořit převod, když zákazník požádá o převod předplatného s partnerem na jiného partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ffe72aa04de17cf6e45e49e9fdbec8ba08da2deed89f5d54425a17825c91a53a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996644"
---
# <a name="transfereligibility-resources"></a>PřevodSchůdnost prostředků

Partner může vytvořit převod, když zákazník požádá o převod předplatného s partnerem na jiného partnera. Pomocí možnosti TransferEligibility (Nárok na převod) zkontrolujte, jestli má předplatné nárok na převod.

## <a name="transfereligibility"></a>PřevodOchemiitelnost

Popisuje přenositelnost.

| Vlastnost              | Typ             | Description                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | řetězec           | Identifikátor předplatného zákazníka.                                                  |
| isEligible            | bool             | Určuje, jestli má předplatné nárok na převod.                         |
| Důvod                | řetězec           | Vlastnost reason vysvětluje, proč předplatné nemá nárok na převod. |