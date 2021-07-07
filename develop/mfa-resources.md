---
title: Prostředky požadavků na zabezpečení partnerů
description: Pochopte podrobnosti o přijetí vícefaktorového ověřování (MFA), aby splňovaly požadavky na zabezpečení partnerů.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: b41a0e46fa6e0643e82a5a2dbfb7141f54a0f824
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445540"
---
# <a name="partner-security-requirements-resources"></a>Prostředky požadavků na zabezpečení partnerů

Tento článek vám pomůže porozumět podrobnostem o přijetí vícefaktorového ověřování (MFA), které vaší organizaci pomůžou splnit stav požadavků na zabezpečení partnerů. 

## <a name="portal-request-without-mfa"></a>Požadavek na portál bez MFA

Určete uživatele, který přistupuje k portálu partnerského centra bez ověřování MFA.

| Vlastnost                            | Typ            | Popis                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | řetězec          | ID objektu uživatele                        |
| TenantId                            | řetězec          | ID tenanta CSP                         |
| Názvu                                 | řetězec          | Hlavní název uživatele                   |
| LastNonMfaCompliantLoginDateTime    | datetime        | Čas posledního přihlášení uživatele bez MFA |


## <a name="api-request-summarized-by-application"></a>Požadavek rozhraní API shrnutý aplikací

Souhrn požadavku rozhraní API, který provedla aplikace a přihlašovací údaje uživatele, agregované podle data žádosti a ID aplikace

| Vlastnost                            | Typ            | Description               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate                           | datetime        | Datum požadavku rozhraní API          |
| MfaCompliantRequestCount            | long            | Počet požadavků s MFA    |
| TotalRequestCount                   | long            | Celkový počet požadavků       |
| ApplicationId                       | řetězec          | ID aplikace        |
| ApplicationName                     | řetězec          | Název aplikace      |


## <a name="api-request-details"></a>Podrobnosti požadavku rozhraní API

Požadavek rozhraní API provedený přihlašovacími údaji aplikace + uživatele 

| Vlastnost                            | Typ            | Description                              |
|-------------------------------------|-----------------|------------------------------------------|
| Identifikátor                           | řetězec          | MS-RequestId                             |
| CorrelationId                       | řetězec          | MS-CorrelationId                         |
| OperationName                       | řetězec          | Cesta rozhraní API s metodou Request         |
| RequestDateTime                     | DateTime        | Doba požadavku na rozhraní API                     |
| Adresa                           | řetězec          | Zdrojová IP adresa                        |
| ObjectId                            | řetězec          | ID objektu uživatele                           |
| TenantId                            | řetězec          | ID tenanta CSP                            |
| Názvu                                 | řetězec          | Hlavní název uživatele                      |
| ApplicationId                       | řetězec          | Vaše aplikace                         |
| MfaCompliant                        | bool            | Indikuje požadavek s MFA nebo bez něj. |
