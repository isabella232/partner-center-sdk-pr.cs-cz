---
title: Hlavičky rozhraní REST pro Partnerské centrum
description: Přečtěte si o hlavičkách žádostí REST HTTP a hlavičkách odpovědí REST, které podporuje REST API partnerských Center.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9f506c8c610c2584912c24453288d0f3578b84e3
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/11/2020
ms.locfileid: "97767069"
---
# <a name="partner-center-rest-and-response-headers-supported-by-the-partner-center-rest-api"></a>Hlavičky a odpovědi partnerského centra podporované partnerským centrem REST API 

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Následující hlavičky požadavku HTTP a odpovědi jsou podporovány REST API partnerským centrem. Ne všechna volání rozhraní API přijímají všechny hlavičky.

## <a name="rest-request-headers"></a>Hlavičky žádosti REST

REST API partnerských Center podporuje následující hlavičky požadavků HTTP.

| Hlavička                       | Description                                                                                                                                                                                                                                                                            | Typ hodnoty |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Authorization:               | Povinná hodnota. Autorizační token v tokenu nosiče formuláře &lt; &gt; .                                                                                                                                                                                                                    | řetězec     |
| Vyjádřit                      | Určuje typ žádosti a odpovědi "Application/JSON".                                                                                                                                                                                                                           | řetězec     |
| MS-RequestId:                | Jedinečný identifikátor pro volání, který slouží k zajištění ID-účinnosti. Pokud dojde k vypršení časového limitu, volání opakování by mělo zahrnovat stejnou hodnotu. Po přijetí odpovědi (úspěch nebo obchodní selhání) by měla být hodnota pro další volání resetována.                                            | Identifikátor GUID       |
| MS-ID korelace:            | Jedinečný identifikátor pro volání, který je vhodný v protokolech a trasování sítě pro řešení chyb. Hodnota by měla být resetována pro každé volání. Všechny operace by měly zahrnovat tuto hlavičku. Další informace najdete v tématu informace o ID korelace v části [test a ladění](test-and-debug.md). | Identifikátor GUID       |
| Verze MS-Contract:         | Povinná hodnota. Určuje verzi rozhraní API, kterou požadujete; Obecně platí, že verze rozhraní API: V1 není-li uvedeno jinak v oddílu [scénáře](scenarios.md) .                                                                                                                                  | řetězec     |
| If-Match:                    | Používá se pro řízení souběžnosti. Některá volání rozhraní API vyžadují předání značky ETag přes hlavičku If-Match. Značka ETag je obvykle na prostředku a proto vyžaduje příkaz GET-nocení na nejnovější verzi. Další informace naleznete v informacích ETag v části [test a ladění](test-and-debug.md).                | řetězec     |
| MS-PartnerCenter-aplikace | Nepovinný parametr. Určuje název aplikace, která používá REST API partnerského centra.                                                                                                                                                                                             | řetězec     |
| X-národní prostředí:                    | Nepovinný parametr. Určuje jazyk, ve kterém se budou vracet sazby. Výchozí hodnota je "en-US". Seznam podporovaných hodnot najdete v tématu [podporované jazyky a národní prostředí partnerského centra](partner-center-supported-languages-and-locales.md).                                                                                                                                                                                                  | řetězec     |

## <a name="rest-response-headers"></a>Hlavičky odpovědí REST

Následující hlavičky HTTP odpovědi mohou být vráceny REST API partnerským centrem.

| Hlavička            | Description                                                                                                                                                                                                                                 | Typ hodnoty |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Vyjádřit           | Určuje typ žádosti a odpovědi "Application/JSON".                                                                                                                                                                                | řetězec     |
| MS-RequestId:     | Jedinečný identifikátor pro volání, který slouží k zajištění ID-účinnosti. Pokud dojde k vypršení časového limitu, volání opakování by mělo zahrnovat stejnou hodnotu. Po přijetí odpovědi (úspěch nebo obchodní selhání) by měla být hodnota pro další volání resetována. | Identifikátor GUID       |
| MS-ID korelace: | Jedinečný identifikátor pro volání. Tato hodnota je užitečná pro řešení potíží s protokoly a trasováním sítě, aby bylo možné najít chybu. Hodnota by měla být resetována pro každé volání. Všechny operace by měly zahrnovat tuto hlavičku.                                                       | Identifikátor GUID       |
