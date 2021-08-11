---
title: Hlavičky rozhraní REST pro Partnerské centrum
description: Přečtěte si o hlavičkách požadavků HTTP REST a hlavičkách odpovědí REST podporovaných Partnerské centrum REST API.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9c9483e761465be1a60003dcd44cef46af3e99634d99d804d43d101d6b8ef700
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993809"
---
# <a name="partner-center-rest-and-response-headers-supported-by-the-partner-center-rest-api"></a>Partnerské centrum hlavičky REST a odpovědi podporované Partnerské centrum REST API 

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Následující hlavičky požadavku HTTP a odpovědi jsou podporovány Partnerské centrum REST API. Ne všechna volání rozhraní API přijímají všechny hlavičky.

## <a name="rest-request-headers"></a>Hlavičky požadavků REST

Následující hlavičky požadavků HTTP podporuje Partnerské centrum REST API.

| Hlavička                       | Description                                                                                                                                                                                                                                                                            | Typ hodnoty |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Authorization:               | Povinná hodnota. Autorizační token ve tvaru Bearer &lt; token &gt; .                                                                                                                                                                                                                    | řetězec     |
| Přijmout:                      | Určuje typ požadavku a odpovědi application/json.                                                                                                                                                                                                                           | řetězec     |
| MS-RequestId:                | Jedinečný identifikátor pro volání, který slouží k zajištění id-nájekt. Pokud dojde k časovém limitu, mělo by volání opakování obsahovat stejnou hodnotu. Po přijetí odpovědi (úspěch nebo neúspěch firmy) by se hodnota měla resetovat pro další volání.                                            | Identifikátor GUID       |
| MS-CorrelationId:            | Jedinečný identifikátor volání, který je užitečný v protokolech a trasování sítě pro řešení chyb. Hodnota by měla být resetována pro každé volání. Všechny operace by měly tuto hlavičku obsahovat. Další informace najdete v tématu Informace o ID korelace v tématu Testování a [ladění.](test-and-debug.md) | Identifikátor GUID       |
| MS-Contract-Version:         | Povinná hodnota. Určuje požadovanou verzi rozhraní API. obecně api-version: v1, pokud není v části [Scénáře uvedeno jinak.](scenarios.md)                                                                                                                                  | řetězec     |
| If-Match (Pokud odpovídá):                    | Používá se pro řízení souběžnosti. Některá volání rozhraní API vyžadují předání ETagu prostřednictvím If-Match rozhraní. ETag je obvykle u prostředku, a proto vyžaduje GET-ting nejnovější. Další informace najdete v tématu Informace o záchytce ETag v [tématu Testování a ladění.](test-and-debug.md)                | řetězec     |
| Aplikace MS-PartnerCenter | Nepovinný parametr. Určuje název aplikace, která používá Partnerské centrum REST API.                                                                                                                                                                                             | řetězec     |
| X-národní prostředí:                    | Nepovinný parametr. Určuje jazyk, ve kterém se vrátí sazby. Výchozí hodnota je en-US. Seznam podporovaných hodnot najdete v tématu Partnerské centrum [a národní prostředí.](partner-center-supported-languages-and-locales.md)                                                                                                                                                                                                  | řetězec     |

## <a name="rest-response-headers"></a>Hlavičky odpovědi REST

Následující hlavičky odpovědi HTTP může vrátit Partnerské centrum REST API.

| Hlavička            | Description                                                                                                                                                                                                                                 | Typ hodnoty |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Přijmout:           | Určuje typ požadavku a odpovědi application/json.                                                                                                                                                                                | řetězec     |
| MS-RequestId:     | Jedinečný identifikátor pro volání, který slouží k zajištění id-nájekt. Pokud dojde k časovém limitu, mělo by volání opakování obsahovat stejnou hodnotu. Po přijetí odpovědi (úspěch nebo neúspěch firmy) by se hodnota měla resetovat pro další volání. | Identifikátor GUID       |
| MS-CorrelationId: | Jedinečný identifikátor volání. Tato hodnota je užitečná při řešení potíží s protokoly a trasováním sítě, abyste zjistili chybu. Hodnota by měla být resetována pro každé volání. Všechny operace by měly tuto hlavičku obsahovat.                                                       | Identifikátor GUID       |
