---
title: PřevodSchůdnost prostředků
description: Partner může vytvořit převod, když zákazník požádá o převod předplatného s partnerem na jiného partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f121d499abffb4c4dda688c2a91c25f83d2e863
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530204"
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