---
title: Nastavení přístupu k rozhraní API v Partnerském centru
description: Nastavte účty pro vývoj na základě sady SDK partnerského centra a testování v izolovaném prostoru integrace.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 873ff2ff9cecbfa92429958d3bfe2aa79fc3ad9a
ms.sourcegitcommit: d5de47c08ba661ba5de4935caa6843d7c2c91710
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/28/2020
ms.locfileid: "97766890"
---
# <a name="set-up-api-access-in-partner-center"></a>Nastavení přístupu k rozhraní API v Partnerském centru

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud for US Government
- Partnerské centrum pro Microsoft Cloud pro Německo

Tento článek popisuje účty, které potřebujete pro vývoj v rámci sady SDK pro partnerský server. Tento článek také vysvětluje, jak vytvořit [účet izolovaného prostoru (sandbox) integrace](#integration-sandbox-account) a testovat v izolovaném prostoru (sandbox) Integration.

>[!NOTE]
>K získání přístupu k rozhraním API musí být váš tenant tenant CSP a Vy musíte být buď nepřímým poskytovatelem, nebo přímým partnerem pro fakturaci.

## <a name="account-definitions"></a>Definice účtu

Pro usnadnění integrace a testování integrace rozhraní API podporuje partnerské Centrum dva druhy účtů:

### <a name="primary-partner-account"></a>Primární Partnerský účet

Tento účet vám umožní vytvářet reálné objednávky pro skutečné zákazníky. Pokud provedete nějaké změny nebo transakce, když jste přihlášeni k primárnímu účtu, pomocí sady SDK partnerského centra nebo uživatelského rozhraní partnerského řídicího panelu se budou považovat za oficiální objednávky pro skutečné zákazníky. Ve vaší faktuře se projeví i vaše společnost za jejich placení.

### <a name="integration-sandbox-account"></a>Účet sandboxu pro integraci

Tento účet je určen pro testování vašeho kódu a jeho integraci s rozhraními API partnerského centra předtím, než bude široce nasazen. Změny a transakce, které uděláte po přihlášení k účtu izolovaného prostoru (sandbox), se zobrazí ve vaší faktuře, ale nebudete muset platit částku faktury. PDF faktury bude mít zřeknutí se jako Neplaťte. JEDNÁ SE O FAKTURU IZOLOVANÉHO PROSTORU (SANDBOX) A NEVYŽADUJE SE ŽÁDNÁ AKCE. "

Účet izolovaného prostoru (sandbox) a primární účet se chovají nezávisle a nesdílí účty správců, uživatelské účty, zákazníky, objednávky, odběry nebo jiná data.

Izolovaný prostor integrace podporuje transakce s omezeným počtem zákazníků, objednávek, předplatných, licencí atd.

Pomocí zásad jsou účty izolovaného prostoru pro integraci jenom pro účely testování Integration.

Ve výchozím nastavení žádný účet sandboxu pro integraci neexistuje. Pokud plánujete použít sadu SDK partnerského centra, musíte si ji sami vytvořit sami.

## <a name="set-up-your-accounts"></a>Nastavení účtů

Tato část popisuje, jak nastavit primární Partnerský účet a účet izolovaného prostoru pro integraci pro sadu SDK pro partnerský server.

### <a name="create-an-integration-sandbox"></a>Vytvoření izolovaného prostoru integrace

1. Přihlaste se k řídicímu panelu partnera pomocí účtu globálního správce (váš primární Partnerský účet).

2. V nabídce **Nastavení** (ikona ozubeného kolečka) vyberte **nastavení partnera**.

3. Vyberte kartu **izolovaný prostor integrace** .

    >[!NOTE]
    >Pokud nevidíte možnost izolovaného prostoru pro integraci, možná nemáte účet globálního správce. Můžete použít také účet izolovaného prostoru pro integraci a izolovaný prostor integrace již byl nastaven.

4. Zadejte kontaktní informace pro účet správce izolovaného prostoru pro integraci. Pak zvolte **vytvořit účet**. Počkejte několik minut, než se zobrazí zpráva s potvrzením, že byl účet vytvořen.

5. Až se zobrazí zpráva s potvrzením, odhlaste se z řídicího panelu partnerského serveru.

6. Znovu se přihlaste pomocí nového účtu správce izolovaného prostoru pro integraci. Nezapomeňte použít formát **username@domain** vašich přihlašovacích údajů společně s heslem, které jste zadali.

7. Chcete-li dokončit nastavení účtu izolovaného prostoru (sandbox), vyberte možnost **nastavit účet** nad **aktuálními úkoly** .

### <a name="enable-api-access"></a>Povolit přístup přes rozhraní API

Po nastavení účtu musíte povolit přístup k rozhraní API, a teprve pak budete moct používat sadu SDK Partnerského centra se sandboxem pro integraci. Přístup k rozhraní API musíte povolit zvlášť pro svůj primární partnerský účet a účet sandboxu pro integraci.

1. Přihlaste se k řídicímu panelu partnerského serveru pomocí účtu globálního správce.

2. V nabídce **Nastavení** (ikona ozubeného kolečka) vyberte **nastavení partnera**.

3. Na stránce **Nastavení účtu** klikněte na možnost **Správa aplikací**.

4. Pokud ještě nemáte existující aplikaci, přidejte novou webovou aplikaci. Pokud máte existující webovou aplikaci, klikněte na tlačítko **Přidat klíč** .

5. Zkopírujte informace o registraci aplikace, zejména **klíč** , pokud vytváříte webovou aplikaci, a uložte ji na bezpečném místě.

6. Odhlaste se z řídicího panelu partnerů.

7. Přihlaste se zpátky pomocí účtu izolovaného prostoru (sandbox) Integration. Zopakováním kroků 2-5 povolte přístup k rozhraní API v izolovaném prostoru integrace.

## <a name="write-and-test-code"></a>Zápis a testování kódu

Můžete napsat kód a testovat kód v izolovaném prostoru integrace. K [nastavení ověřování partnerského centra](partner-center-authentication.md) pomocí služby Azure AD budete potřebovat následující informace.

| Název položky | Umístění položky |
| --------- | ------------- |
| ID aplikace/ID klienta | V nabídce **Nastavení** (ikona ozubeného kolečka) vyberte **nastavení partnera**. Na stránce **Nastavení účtu** vyberte **Správa aplikací**. ID aplikace/ID klienta je uvedené jako ID aplikace **registrované aplikace**. |
| Klíč | Pokud jste vytvořili webovou aplikaci v části [Povolení přístupu k rozhraní API](#enable-api-access), je to klíč, který jste uložili v kroku 5. |
| Doména | Doména pro izolovaný prostor integrace |

## <a name="run-tested-code"></a>Spustit testovaný kód

Pokud chcete používat vaše řešení se skutečnými Zákaznickými daty, musíte změnit přihlašovací údaje izolovaného prostoru (sandbox) na svůj primární účet partnerského účtu.

Až budete připraveni použít testovaný kód v primárním partnerském účtu, musíte získat token zabezpečení Azure AD. Tento token zabezpečení je založený na vaší aplikaci, klíči a doméně partnerského centra (namísto vaší aplikace, klíče a domény Integration sandbox).

1. Postupujte podle kroků v části [ověřování partnerského centra](partner-center-authentication.md) a získejte token zabezpečení služby Azure AD pomocí vašich primárních přihlašovacích údajů partnerského centra. (Dřív jste použili tento postup k získání tokenu zabezpečení Azure AD pro izolovaný prostor integrace.)

2. Nahraďte token zabezpečení Integration v kódu novým tokenem zabezpečení pro váš primární Partnerský účet.
