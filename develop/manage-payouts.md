---
title: Správa výběrů pomocí rozhraní API služby výběr
description: Naučte se používat rozhraní API služby vydaných partnerským centrem pro přístup k datům z výběrů.
ms.date: 06/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: jasongroce
ms.author: sabaja
ms.openlocfilehash: 014a1e6a14b538b7557d58710b9132dd9e37de21
ms.sourcegitcommit: 7e2d2805c4cdd61785b1cdcca99cad10d5683153
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2021
ms.locfileid: "113592420"
---
# <a name="manage-payouts-using-the-payout-service-api"></a>Správa výběrů pomocí rozhraní API služby výběr

V tomto článku se dozvíte, jak můžete přistupovat k datům o druhu přes rozhraní API služby výběr namísto uživatelského rozhraní partnerského centra. Tato rozhraní API poskytují programový způsob, jak zajistit schopnost funkce [exportovat data](https://partner.microsoft.com/dashboard/payouts/reports/incentiveexport) v partnerském centru.

## <a name="available-apis"></a>Dostupná rozhraní API

Podívejte se na všechna dostupná rozhraní API na [výběrech partnerských](/rest/api/partner-center/partner-payouts)serverů.

## <a name="prerequisites"></a>Požadavky

- [Zaregistrujte aplikaci s identitou AAD/Microsoft](/graph/auth-register-app-v2) ve Azure Portal a přidejte do ní příslušné vlastníky a role.
- Nainstalujte [Visual Studio](https://visualstudio.microsoft.com/downloads/).

## <a name="register-an-application-with-the-microsoft-identity-platform"></a>Registrace aplikace na platformě Microsoft Identity Platform

[Microsoft identity platform](/azure/active-directory/develop/v2-overview) vám pomůže se sestavovat aplikace, které můžou uživatelé a zákazníci přihlašovat k používání svých identit microsoftu nebo účtů sociálních sítí, a poskytovat autorizovaný přístup k vašim vlastním rozhraním api nebo rozhraním api microsoftu, jako je Microsoft Graph.

1. Přihlaste se k webu [Azure Portal](https://portal.azure.com/) pomocí pracovního nebo školního účtu nebo osobního účtu Microsoft.

   Pokud vám váš účet poskytne přístup k více než jednomu klientovi, v pravém horním rohu vyberte svůj účet a nastavte svou relaci portálu na správného tenanta Azure AD.

2. v levém navigačním podokně vyberte službu Azure Active Directory a pak **Registrace aplikací** a pak **novou registraci**. Zobrazí se stránka **zaregistrovat aplikaci** .

   :::image type="content" source="./images/manage-payouts/new-app-registration.png" alt-text="Snímek obrazovky s informacemi o registraci aplikace v Azure Portal":::

3. Zadejte informace o registraci vaší aplikace:

   - Název: zadejte smysluplný název aplikace, který se zobrazí uživatelům aplikace.
   - Podporované typy účtů: vyberte, které účty bude vaše aplikace podporovat.

    | **Podporované typy účtu**                             | **Popis**                                                                                            |
    |---------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
    | Jenom účty v tomto organizačním adresáři          | Tuto možnost vyberte, pokud vytváříte obchodní aplikaci. Tato možnost není dostupná, pokud neregistrujete aplikaci v adresáři. Tato možnost se mapuje pouze na účty Azure AD s jedním tenantem.  Tato možnost je výchozí, pokud neprovádíte registraci aplikace mimo adresář. V případech, kdy je aplikace zaregistrovaná mimo adresář, jsou výchozí možností účty Azure AD s více tenanty a osobní účty Microsoft.             |
    | Účty v libovolném organizačním adresáři                | Tuto možnost vyberte, pokud chcete cílit na všechny zákazníky z řad firem a vzdělávacích institucí.  Tato možnost se mapuje pouze na účty Azure AD s více tenanty. Pokud jste při registraci aplikace použili možnost s účty Azure AD pouze s jedním tenantem, v okně Ověřování ji můžete převést na účet Azure AD s více tenanty a zpět na účet Azure AD s jedním tenantem.                                                                                                                                                  |
    | Účty v libovolném organizačním adresáři a osobní účty Microsoft | Tuto možnost vyberte, pokud chcete cílit na co nejširší okruh zákazníků. Tato možnost se mapuje na účty Azure AD s více tenanty a osobní účty Microsoft.  Pokud jste aplikaci zaregistrovali jako víceklientské a osobní účty Microsoft Azure AD, nemůžete tento výběr v uživatelském rozhraní změnit. Místo toho musíte ke změně podporovaných typů účtu použít editor manifestu aplikace.                                                                          |

   - *(volitelné)* Identifikátor URI pro přesměrování: Vyberte typ aplikace, kterou vytváříte, webový nebo veřejný klient (mobilní & Desktop) a pak zadejte identifikátor URI přesměrování (nebo adresu URL odpovědi) pro vaši aplikaci. (Adresa URL pro přesměrování je místo, kde se pošle odpověď na ověření po ověření uživatele.) 

      V případě webových aplikací zadejte základní adresu URL vaší aplikace. Například `http://localhost:31544` může být adresa URL pro webovou aplikaci spuštěnou na místním počítači. Uživatelé by se pomocí této adresy URL přihlašovali k webové klientské aplikaci.
      V případě veřejných klientských aplikací zadejte identifikátor URI, který Azure AD použije k vrácení odpovědí týkajících se tokenu. Zadejte konkrétní hodnotu pro vaši aplikaci, například `myapp://auth`.

4. Vyberte **Zaregistrovat**. Azure AD přiřadí vaší aplikaci jedinečné ID aplikace (klienta) a načte se stránka s přehledem aplikace.

   :::image type="content" source="./images/manage-payouts/register-an-application.png" alt-text="<alternativní text>":::

5. Pokud chcete do aplikace přidat funkce, můžete vybrat další možnosti konfigurace, včetně brandingu, certifikátů a tajných klíčů, oprávnění k rozhraní API a dalších.

## <a name="platform-specific-properties"></a>Vlastnosti specifické pro platformu

V následující tabulce jsou uvedeny vlastnosti, které je třeba nakonfigurovat a kopírovat pro různé typy aplikací. **Přiřazeno** znamená, že byste měli použít hodnotu přiřazenou službou Azure AD.

| Typ aplikace              | Platforma | ID aplikace (klienta) | Tajný klíč klienta | Identifikátor URI/adresa URL pro přesměrování | Implicitní Flow                                                         |
|-----------------------|----------|-------------------------|---------------|------------------|-----------------------------------------------------------------------|
| Nativní/mobilní         | Nativní   | Přiřazené                | No            | Přiřazené         | No                                                                    |
| Webová aplikace               | Web      | Přiřazené                | Yes           | Yes              | volitelné otevřené ID Připojení middleware ve výchozím nastavení používá hybridní tok (ano). |
| Jediná stránková aplikace (SPA) | Web      | Přiřazené                | Yes           | Yes              | Yes jednostránkové použít Open ID Připojení implicitní Flow                            |
| Služba/démon        | Web      | Přiřazené                | Yes           | Yes              | No                                                                    |

## <a name="create-a-service-principal"></a>Vytvoření instančního objektu

Pokud chcete získat přístup k prostředkům ve vašem předplatném, musíte aplikaci přiřadit roli. K tomu, abyste se mohli rozhodnout, která role nabízí správná oprávnění pro aplikaci, přečtěte si téma [předdefinované role Azure](/azure/role-based-access-control/built-in-roles).

> [!NOTE]
> Rozsah můžete nastavit na úrovni předplatného, skupiny prostředků nebo prostředku. Oprávnění jsou zděděna na nižší úrovně rozsahu. Například přidání aplikace do role čtenář pro skupinu prostředků znamená, že může číst skupinu prostředků a všechny prostředky, které obsahuje.

1. V Azure Portal vyberte úroveň rozsahu, do které chcete aplikaci přiřadit. Pokud například chcete přiřadit roli v oboru předplatného, vyhledejte a vyberte **odběry** nebo vyberte **předplatná** na domovské stránce.

   :::image type="content" source="./images/manage-payouts/search-for-subscriptions.png" alt-text="Snímek obrazovky znázorňující hledání obrazovky předplatných":::

2. Vyberte předplatné, ke kterému chcete aplikaci přiřadit.

   :::image type="content" source="./images/manage-payouts/internal-testing-subscription.png" alt-text="Snímek obrazovky s obrazovkou předplatných s příznakem interního testování nastaveným na hodnotu true":::

> [!NOTE]
> Pokud nevidíte předplatné, které hledáte, vyberte filtr globálních předplatných a ujistěte se, že pro portál je vybrané požadované předplatné.

3. Vyberte **řízení přístupu (IAM)** a pak vyberte **Přidat přiřazení role**.

4. Vyberte roli, kterou chcete aplikaci přiřadit. Pokud například chcete, aby aplikace mohla provádět akce, jako je restartování, spuštění a zastavení instancí, vyberte roli Přispěvatel. Přečtěte si další informace o [dostupných rolích](/azure/role-based-access-control/built-in-roles).

   Ve výchozím nastavení se aplikace Azure AD nezobrazí v dostupných možnostech. Pokud chcete najít svou aplikaci, vyhledejte ji a vyberte ji z výsledků. V následujícím snímku obrazovky `example-app` je aplikace AAD, kterou jste zaregistrovali.

   :::image type="content" source="./images/manage-payouts/add-role-assignment.png" alt-text="Snímek obrazovky znázorňující uživatelské rozhraní pro přidání přiřazení role pro testovací aplikaci":::

5. Vyberte **Uložit**. Pak můžete zobrazit vaši aplikaci v seznamu uživatelů s rolí pro tento obor.

   Můžete začít používat váš instanční objekt ke spouštění skriptů nebo aplikací. chcete-li spravovat oprávnění instančního objektu, přečtěte si téma stav souhlasu uživatele, kontrola oprávnění, informace o přihlášení a další informace, v [Azure Portal](https://portal.azure.com)si můžete Enterprise aplikace.

## <a name="set-up-api-permissions"></a>Nastavení oprávnění API

V této části najdete pokyny, jak nastavit požadovaná oprávnění rozhraní API. Další informace o nastavení oprávnění pro rozhraní API partnerského centra najdete v tématu [ověřování prostřednictvím rozhraní API pro partnery](/partner/develop/api-authentication).

**udělení oprávnění Graph API**

1. Otevřete [Registrace aplikací](https://go.microsoft.com/fwlink/?linkid=2083908) v Azure Portal.

2. Vyberte aplikaci nebo [vytvořte aplikaci](/azure/active-directory/develop/quickstart-register-app) , pokud ji ještě nemáte.

3. Na stránce Přehled aplikace v části **Spravovat** vyberte **oprávnění rozhraní API** a pak **přidejte oprávnění**.

4. v seznamu dostupných rozhraní api vyberte **Microsoft Graph** .

5. Vyberte **delegovaná oprávnění** a přidejte požadovaná oprávnění. Další informace najdete v tématu [Konfigurace přístupu k aplikaci](/azure/active-directory/develop/quickstart-configure-app-access-web-apis).

   :::image type="content" source="./images/manage-payouts/graph-request-api-permissions.png" alt-text="snímek obrazovky s obrazovkou oprávnění žádosti v Azure Portal s vybraným Microsoft Graph":::

**Vyjádření souhlasu rozhraní API k rozhraní API partnerského centra prostřednictvím aplikace AAD**

6. V aplikaci vyberte **oprávnění rozhraní API** a pak na obrazovce požádat API oprávnění vyberte **Přidat oprávnění** a pak **rozhraní API moje organizace používá**.

7. vyhledejte **microsoft Partner (microsoft Dev Center) API (4990cffe-04e8-4e8b-808a-1175604b879f)**.

   :::image type="content" source="./images/manage-payouts/partner-api-request-permissions.png" alt-text="Snímek obrazovky s vybranou obrazovkou oprávnění k rozhraní API s vybraným partnerem Microsoftu":::

8. Nastavte delegovaná oprávnění k **partnerskému centru**.

   :::image type="content" source="./images/manage-payouts/partner-api-request-permissions.png" alt-text="Snímek obrazovky znázorňující delegovaná oprávnění vybraná pro partnerské Centrum na obrazovce oprávnění API pro vyžádání":::

9. Udělení **souhlasu správce** pro rozhraní API.

   :::image type="content" source="./images/manage-payouts/api-permissions.png" alt-text="Snímek obrazovky s přepínačem pro souhlas správce na obrazovce oprávnění k rozhraní API":::

   Na obrazovce stavu souhlasu správce ověřte, že je povolený souhlas správce.

   :::image type="content" source="./images/manage-payouts/admin-consent-verification.png" alt-text="Snímek obrazovky se zobrazením stavu souhlasu správce":::

10. V části **ověřování** se ujistěte, že je možnost **umožnit toky veřejných klientů** nastavená na **hodnotu Ano**.

    :::image type="content" source="./images/manage-payouts/allow-public-client-flows.png" alt-text="Snímek obrazovky s ověřovací obrazovkou s povolenými toky veřejných klientů nastavenou na hodnotu Ano.":::

## <a name="run-the-sample-code-in-visual-studio"></a>Spusťte vzorový kód v Visual Studio

vzorový kód, který ukazuje, jak se dá rozhraní API použít pro platby a historii transakcí, najdete v části [Partner-Center-vyvzorkování-rozhraní api](https://github.com/microsoft/Partner-Center-Payout-APIs) GitHub úložišti.

### <a name="sample-code-notes"></a>Poznámky k ukázkovému kódu

- Konfigurace klientských tajných klíčů a certifikátů, jak je popsáno v části ověřování: v Azure Portal se nevyžadují dvě možnosti, [jak vytvořit instanční objekt](/azure/active-directory/develop/howto-create-service-principal-portal) .
- Účty s vícefaktorového ověřováním (MFA) se momentálně nepodporují a způsobí chybu.
- Rozhraní API pro výběr podporuje jenom přihlašovací údaje uživatele a hesla.

## <a name="next-steps"></a>Další kroky

- [Vytvoření aplikace Azure AD a instančního objektu s přístupem k prostředkům pomocí portálu](/azure/active-directory/develop/howto-create-service-principal-portal)
- [Registrace aplikace na platformě Microsoft Identity Platform](/graph/auth-register-app-v2)
- [Konfigurace klientské aplikace pro přístup k webovému rozhraní API](/azure/active-directory/develop/quickstart-configure-app-access-web-apis)
