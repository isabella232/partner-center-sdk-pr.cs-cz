---
title: Nastavení přístupu k rozhraní API v Partnerském centru
description: Nastavte účty pro vývoj proti SDK pro Partnerské centrum a testování v sandboxu integrace.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2032984c26896b3927b916bb3c8542fb1d76fafbef88ed4b24795987616bbddf
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994757"
---
# <a name="set-up-api-access-in-partner-center"></a>Nastavení přístupu k rozhraní API v Partnerském centru

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud for US Government | Partnerské centrum pro Microsoft Cloud (Německo)

Tento článek popisuje účty, které potřebujete k vývoji pro SDK pro Partnerské centrum. Tento článek také vysvětluje, jak vytvořit účet [sandboxu pro integraci](#integration-sandbox-account) a otestovat ho v sandboxu pro integraci.

>[!NOTE]
>Abyste získali přístup k rozhraním API, váš tenant musí být tenant CSP a musíte být nepřímý poskytovatel nebo partner s přímým vyúčtováním.

## <a name="account-definitions"></a>Definice účtů

Pro lepší integraci a testování integrace rozhraní API Partnerské centrum podporuje dva druhy účtů:

### <a name="primary-partner-account"></a>Primární partnerský účet

V tomto účtu vytváříte skutečné objednávky pro skutečné zákazníky. Pokud při přihlášení k primárnímu účtu nebo pomocí uživatelského rozhraní řídicího panelu partnera nebo řídicího panelu SDK pro Partnerské centrum jakékoli změny nebo transakce, budou se považovat za oficiální objednávky skutečných zákazníků. Projeví se na vaší faktuře a vaše společnost za ně zodpovídá.

### <a name="integration-sandbox-account"></a>Účet sandboxu pro integraci

Tento účet je pro testování kódu a jeho integraci s rozhraními API Partnerské centrum před jeho širším nasazením. Změny a transakce, které jste provést při přihlášení k účtu sandboxu pro integraci, se zobrazí na faktuře, ale částku faktury platit nemusíte. Soubor PDF faktury bude mít právní omezení s textem NEZAPLATIT. JEDNÁ SE O FAKTURU ZA SANDBOX A NEVYŽADUJE SE ŽÁDNÁ AKCE.

Účet sandboxu pro integraci a primární účet se chová nezávisle a nesdílejí účty správců, uživatelské účty, zákazníky, objednávky, předplatná ani jiná data.

Integrační sandbox podporuje transakce s omezeným počtem zákazníků, objednávek, předplatných, licencí atd.

Podle zásad jsou účty sandboxu integrace jenom pro účely testování integrace.

Ve výchozím nastavení žádný účet sandboxu pro integraci neexistuje. Pokud plánujete používat tuto aplikaci, musíte si ji vytvořit SDK pro Partnerské centrum.

## <a name="set-up-your-accounts"></a>Nastavení účtů

Tato část popisuje, jak nastavit primární partnerský účet a účet sandboxu pro integraci pro SDK pro Partnerské centrum.

### <a name="create-an-integration-sandbox"></a>Vytvoření sandboxu pro integraci

1. Přihlaste se k řídicímu panelu pro partnery pomocí účtu globálního správce (primárního partnerského účtu).

2. V nabídce **Nastavení** (ikona ozubeného kola) zvolte **Nastavení účtu.**

3. Zvolte **kartu Sandbox integrace.**

    >[!NOTE]
    >Pokud možnost Sandbox integrace nevidíte, možná nemáte účet globálního správce. Můžete také používat účet sandboxu pro integraci a integrační sandbox už je nastavený.

4. Zadejte kontaktní informace pro účet správce sandboxu pro integraci. Pak zvolte **Vytvořit účet.** Počkejte několik minut, než se zobrazí potvrzovací zpráva o vytvoření účtu.

5. Po zobrazení potvrzovací zprávy se odhlásit z řídicího panelu partnera.

6. Znovu se přihlaste pomocí nového účtu správce sandboxu pro integraci. Nezapomeňte použít formát svých **username@domain** přihlašovacích údajů spolu s heslem, které jste zadali.

7. Zvolte **Nastavit účet nad aktuálními** úkoly **a** dokončete nastavení účtu sandboxu.

### <a name="enable-api-access"></a>Povolení přístupu k rozhraní API

Po nastavení účtu musíte povolit přístup k rozhraní API, a teprve pak budete moct používat sadu SDK Partnerského centra se sandboxem pro integraci. Přístup k rozhraní API musíte povolit zvlášť pro svůj primární partnerský účet a účet sandboxu pro integraci.

1. Přihlaste se k řídicímu panelu pro partnery pomocí účtu globálního správce.

2. V nabídce **Nastavení** (ikona ozubeného kola) vyberte **Nastavení účtu.**

3. Na stránce **Nastavení účtu** zvolte **Správa aplikací.**

4. Pokud ještě nemáte existující aplikaci, přidejte novou webovou aplikaci. Pokud máte existující webovou aplikaci, zvolte **tlačítko Přidat** klíč.

5. Zkopírujte informace o registraci  aplikace, zejména klíč, pokud vytváříte webovou aplikaci, a uložte je na bezpečném místě.

6. Odhlásit se z řídicího panelu pro partnery.

7. Znovu se přihlaste pomocí účtu sandboxu pro integraci. Opakováním kroků 2 až 5 povolte přístup k rozhraní API v sandboxu integrace.

## <a name="write-and-test-code"></a>Psaní a testování kódu

V sandboxu pro integraci můžete psát kód a testovat kód. K nastavení ověřování pomocí Azure AD [Partnerské centrum následující](partner-center-authentication.md) informace.

| Název položky | Umístění položky |
| --------- | ------------- |
| ID aplikace / ID klienta | V nabídce **Nastavení** (ikona ozubeného kola) vyberte **Nastavení účtu.** Na stránce **Nastavení účtu** vyberte **Správa aplikací.** ID aplikace nebo ID klienta je uvedené jako **ID registrované aplikace.** |
| Klíč | Pokud jste vytvořili webovou aplikaci v části [Povolení přístupu k rozhraní API,](#enable-api-access)jedná se o klíč, který jste si uložili v kroku 5. |
| Doména | Doména pro sandbox integrace. |

## <a name="run-tested-code"></a>Spuštění testovaného kódu

Pokud chcete řešení používat s reálnými zákaznickými daty, musíte změnit přihlašovací údaje sandboxu integrace na přihlašovací údaje primárního partnerského účtu.

Až budete připraveni použít testovaný kód v primárním partnerském účtu, musíte získat token zabezpečení Azure AD. Tento token zabezpečení je založený na vaší Partnerské centrum, klíči a doméně (místo vaší aplikace, klíče a domény sandboxu integrace).

1. Postupujte podle kroků v [Partnerské centrum ověřování](partner-center-authentication.md) a získejte token zabezpečení Azure AD pomocí primárních přihlašovacích Partnerské centrum účtu. (Dříve jste pomocí těchto kroků získali token zabezpečení Azure AD pro sandbox integrace.)

2. Nahraďte token zabezpečení integrace v kódu novým tokenem zabezpečení pro primární partnerský účet.
