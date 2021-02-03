---
title: Začínáme
description: Sada SDK partnerského centra zahrnuje spravované rozhraní API a REST API pro partnery, kteří se používají ke správě dat zákazníků, předplatných a objednávek.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9c2af1e11dbda19489a27e37c7f3de8ede90fd1c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766770"
---
# <a name="get-started"></a>Začínáme

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Sada SDK partnerského centra zahrnuje spravované rozhraní API a REST API pro partnery, kteří se používají ke správě dat zákazníků, předplatných a objednávek.

## <a name="get-the-code"></a>Získání kódu

[Stáhnout sadu SDK partnerského centra](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> Přístup k rozhraní API partnerského centra pro nepřímý prodejce není podporovaným scénářem.

## <a name="determine-your-version-of-partner-center"></a>Určení verze partnerského centra

Některé verze partnerského centra nemají k dispozici celou sadu SDK. Další informace najdete v tématu [vývoj pro partnerského centra pro národní Cloud Microsoftu](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="get-the-samples"></a>Získat ukázky

Další informace o fragmentech kódu jazyka C#, ukázkách REST a ukázkové aplikaci najdete v tématu [ukázky partnerského centra](partner-center-samples.md).

## <a name="test-vs-production"></a>Testování vs. produkce

Když začnete psát a testovat kód, měli byste použít svůj účet izolovaného prostoru (a odpovídající tokeny), abyste omylem neúčtovali nové poplatky, za které vaše společnost zodpovídá za vyplácení. Další informace o tomto testovacím prostředí najdete v tématu [nastavení přístupu k rozhraní API v partnerském centru](set-up-api-access-in-partner-center.md).

Když je vaše řešení testováno a připraveno k použití na reálných zákaznických účtech, budete muset aktualizovat vaše tokeny, abyste používali klientskou aplikaci Azure AD a tajný klíč, které odpovídají vašemu primárnímu účtu partnerského centra.

Tipy a návrhy týkající se testování a ladění, včetně dalších informací o výrobě (TiP) a izolovaném prostoru Integration, naleznete v tématu [Test and Debug](test-and-debug.md).

## <a name="configure-your-authentication"></a>Konfigurace ověřování

Pokud chcete nakonfigurovat ověřování Azure AD, abyste mohli používat rozhraní API partnerského centra, Projděte si téma [ověřování v partnerském centru](partner-center-authentication.md).

> [!IMPORTANT]
> Microsoft zavádí zabezpečenou, škálovatelnou architekturu pro ověřování partnerů CSP (Cloud Solution Provider) a dodavatelů ovládacích panelů (CPV) prostřednictvím architektury Microsoft Azure Multi-Factor Authentication (MFA).
Partnerské centrum používá pro ověřování Azure AD a používá rozhraní API partnerského centra. musíte nakonfigurovat nastavení ověřování správně.
>
> Další informace najdete v tématu [povolení zabezpečeného modelu aplikace](enable-secure-app-model.md).

## <a name="get-help"></a>Získání pomoci

Partneři můžou získat podporu ve [skupině partnerských Center SDK Yammer](https://go.microsoft.com/fwlink/p/?LinkID=717360). Aby mohli vývojáři získat lépe přizpůsobenou nápovědu, můžou využít výhody podpory MPN nebo Premier Support.

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a>Připojení k programu pro uživatele rozhraní API a sady SDK pro Partnerské centrum v rané fázi

Pokud chcete zjistit, jak můžete s Microsoftem spolupracovat na vývoji partnerských funkcí a možností, podívejte se [do části zapojení rozhraní API partnerského centra a programu SDK pro včasnou](early-adopter-program.md)verzi.
