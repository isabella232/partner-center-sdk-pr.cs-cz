---
title: Začínáme
description: Součástí SDK pro Partnerské centrum spravované rozhraní API a REST API pro partnery ke správě dat zákazníků, předplatných a objednávek.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 340b46978d71bdf5fa6f6795d69fe0721d808c4eb2650744e82510c208dd5b8f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989691"
---
# <a name="get-started"></a>Začínáme

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Součástí SDK pro Partnerské centrum spravované rozhraní API a REST API pro partnery ke správě dat zákazníků, předplatných a objednávek.

## <a name="get-the-code"></a>Získání kódu

[Stažení SDK pro Partnerské centrum](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> Přístup rozhraní API Partnerské centrum pro nepřímé prodejce není podporovaný scénář.

## <a name="determine-your-version-of-partner-center"></a>Určení verze Partnerské centrum

Některé verze Partnerské centrum nemají k dispozici celou sadu SDK. Další informace najdete v tématu [Vývoj pro Partnerské centrum pro národní cloud Microsoftu.](developing-for-partner-center-for-microsoft-national-cloud.md)

## <a name="get-the-samples"></a>Získání ukázek

Další informace o fragmentech kódu jazyka C#, ukázkách REST a ukázkové aplikaci najdete v [Partnerské centrum ukázkách.](partner-center-samples.md)

## <a name="test-vs-production"></a>Test vs. production

Při počátečním psaní a testování kódu byste měli použít svůj účet sandboxu pro integraci (a odpovídající tokeny), aby se vám nechtěně neplatily nové poplatky, za které zodpovídá vaše společnost. Další informace o tomto testovacím prostředí najdete v tématu [Nastavení přístupu k rozhraní API v Partnerské centrum](set-up-api-access-in-partner-center.md).

Po otestování vašeho řešení a jeho použití na účtech skutečných zákazníků budete muset tokeny aktualizovat, abyste mohli používat klientskou aplikaci a tajný klíč Azure AD, které odpovídají vašemu primárnímu Partnerské centrum účtu.

Tipy a návrhy týkající se testování a ladění, včetně dalších informací o TiP (Test-in-Production) a Sandboxu pro integraci, najdete v tématu Testování a [ladění.](test-and-debug.md)

## <a name="configure-your-authentication"></a>Konfigurace ověřování

Pokud chcete nakonfigurovat ověřování Azure AD, abyste mohli používat rozhraní API Partnerské centrum, podívejte se na [Partnerské centrum ověřování.](partner-center-authentication.md)

> [!IMPORTANT]
> Microsoft představuje zabezpečenou a škálovatelnou architekturu pro ověřování partnerů CSP (Cloud Solution Provider) a dodavatelů ovládacích panelů (CPV) prostřednictvím architektury Microsoft Azure multi-factor authentication (MFA).
Partnerské centrum ověřování používá Azure AD a k použití Partnerské centrum API musíte správně nakonfigurovat nastavení ověřování.
>
> Další informace najdete v tématu [Povolení zabezpečeného aplikačního modelu](enable-secure-app-model.md).

## <a name="get-help"></a>Získání pomoci

Partneři mohou získat podporu ve [skupině SDK pro Partnerské centrum Yammer .](https://go.microsoft.com/fwlink/p/?LinkID=717360) K získání přizpůsobenější nápovědy můžou vývojáři využít výhody podpory MPN nebo Premier Support.

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a>Připojení k programu pro uživatele rozhraní API a sady SDK pro Partnerské centrum v rané fázi

Informace o tom, jak můžete spolupracovat s Microsoftem na vývoji partnerských funkcí a možností, najdete v tématu Připojení k rozhraní API pro Partnerské centrum a programu pro včasné přijetí sady [SDK.](early-adopter-program.md)
