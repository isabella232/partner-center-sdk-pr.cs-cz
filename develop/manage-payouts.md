---
title: Správa výplat pomocí rozhraní API pro výplaty
description: Zjistěte, jak pomocí rozhraní API Partnerské centrum payout service získat přístup k datům o platbě.
ms.date: 06/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: jasongroce
ms.author: sabaja
ms.openlocfilehash: b9bdc6da64a79f4f35466fb62662b086a8e1ab3cadc99c7ca685303752f9d166
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996288"
---
# <a name="manage-payouts-using-the-payout-service-api"></a>Správa výplat pomocí rozhraní API pro výplaty

Tento článek vysvětluje, jak můžete získat přístup k datům o platbách prostřednictvím rozhraní API služby platba místo Partnerské centrum uživatelského rozhraní. Tato rozhraní API poskytují programový způsob, jak poskytovat funkce [Export dat](https://partner.microsoft.com/dashboard/payouts/reports/incentiveexport) v Partnerské centrum.

## <a name="available-apis"></a>Dostupná rozhraní API

Všechna dostupná rozhraní API najdete na adrese [Partner Payouts](/rest/api/partner-center/partner-payouts).

## <a name="prerequisites"></a>Požadavky

- [Zaregistrujte aplikaci v AAD nebo Microsoft Identity](/graph/auth-register-app-v2) v Azure Portal a přidejte do aplikace příslušné vlastníky a role.
- Nainstalujte [Visual Studio](https://visualstudio.microsoft.com/downloads/).

## <a name="register-an-application-with-the-microsoft-identity-platform"></a>Registrace aplikace na platformě Microsoft Identity Platform

Služba [Microsoft identity platform](/azure/active-directory/develop/v2-overview) pomáhá vytvářet aplikace, ke které se uživatelé a zákazníci mohou přihlašovat pomocí svých identit Microsoftu nebo účtů na sociálních sítích, a poskytovat autorizovaný přístup k vlastním rozhraním API nebo rozhraním API Microsoftu, jako je microsoft Graph.

1. Přihlaste se k webu [Azure Portal](https://portal.azure.com/) pomocí pracovního nebo školního účtu nebo osobního účtu Microsoft.

   Pokud váš účet poskytuje přístup k více než jednomu tenantovi, vyberte svůj účet v pravém horním rohu a nastavte relaci portálu na správného tenanta Azure AD.

2. V levém navigačním podokně vyberte službu Azure Active Directory, pak **klikněte na Registrace aplikací** a pak na Nová **registrace.** Zobrazí **se stránka Zaregistrovat** aplikaci.

   :::image type="content" source="./images/manage-payouts/new-app-registration.png" alt-text="Snímek obrazovky s obrazovkou Zaregistrovat aplikaci v Azure Portal":::

3. Zadejte registrační informace vaší aplikace:

   - Název: Zadejte smysluplný název aplikace, který se zobrazí uživatelům aplikace.
   - Podporované typy účtů: Vyberte, které účty bude vaše aplikace podporovat.

    | **Podporované typy účtu**                             | **Popis**                                                                                            |
    |---------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
    | Pouze účty v tomto organizačním adresáři          | Tuto možnost vyberte, pokud vytváříte obchodní aplikaci. Tato možnost není dostupná, pokud neregistrujete aplikaci v adresáři. Tato možnost se mapuje pouze na účty Azure AD s jedním tenantem.  Tato možnost je výchozí, pokud neregistrujete aplikaci mimo adresář. V případech, kdy je aplikace zaregistrovaná mimo adresář, jsou výchozí možností účty Azure AD s více tenanty a osobní účty Microsoft.             |
    | Účty v libovolném organizačním adresáři                | Tuto možnost vyberte, pokud chcete cílit na všechny zákazníky z řad firem a vzdělávacích institucí.  Tato možnost se mapuje pouze na účty Azure AD s více tenanty. Pokud jste při registraci aplikace použili možnost s účty Azure AD pouze s jedním tenantem, v okně Ověřování ji můžete převést na účet Azure AD s více tenanty a zpět na účet Azure AD s jedním tenantem.                                                                                                                                                  |
    | Účty v libovolném organizačním adresáři a osobní účty Microsoft | Tuto možnost vyberte, pokud chcete cílit na co nejširší okruh zákazníků. Tato možnost se mapuje na účty Azure AD s více tenanty a osobní účty Microsoft.  Pokud jste aplikaci zaregistrovali jako účty Azure AD s více tenanty a osobní účty Microsoft, nemůžete tento výběr změnit v uživatelském rozhraní. Místo toho musíte ke změně podporovaných typů účtu použít editor manifestu aplikace.                                                                          |

   - *(volitelné)* Identifikátor URI pro přesměrování: Vyberte typ aplikace, kterou sestavíte, webový nebo veřejný klient (mobilní & desktop) a pak zadejte identifikátor URI přesměrování (nebo adresu URL odpovědi) pro vaši aplikaci. (Adresa URL pro přesměrování je místo, kam se po ověření uživatele bude odeslat ověřovací odpověď.) 

      V případě webových aplikací zadejte základní adresu URL vaší aplikace. Například `http://localhost:31544` může být adresa URL pro webovou aplikaci spuštěnou na místním počítači. Uživatelé by se pomocí této adresy URL přihlašovali k webové klientské aplikaci.
      V případě veřejných klientských aplikací zadejte identifikátor URI, který Azure AD použije k vrácení odpovědí týkajících se tokenu. Zadejte konkrétní hodnotu pro vaši aplikaci, například `myapp://auth`.

4. Vyberte **Zaregistrovat**. Azure AD přiřadí vaší aplikaci jedinečné ID aplikace (klienta) a načte se stránka přehledu aplikace.

   :::image type="content" source="./images/manage-payouts/register-an-application.png" alt-text="<alternativního textu>":::

5. Pokud chcete do své aplikace přidat možnosti, můžete vybrat další možnosti konfigurace, včetně brandingu, certifikátů a tajných kódů, oprávnění rozhraní API a dalších možností.

## <a name="platform-specific-properties"></a>Vlastnosti specifické pro platformu

Následující tabulka uvádí vlastnosti, které je potřeba nakonfigurovat a kopírovat pro různé druhy aplikací. **Přiřazeno** znamená, že byste měli použít hodnotu přiřazenou službou Azure AD.

| Typ aplikace              | Platforma | ID aplikace (klienta) | Tajný klíč klienta | Identifikátor URI nebo adresa URL přesměrování | Implicitní Flow                                                         |
|-----------------------|----------|-------------------------|---------------|------------------|-----------------------------------------------------------------------|
| Nativní/mobilní         | Nativní   | Přiřazené                | No            | Přiřazené         | No                                                                    |
| Webová aplikace               | Web      | Přiřazené                | Yes           | Yes              | Volitelné Open ID Připojení middleware ve výchozím nastavení používá hybridní tok (Ano) |
| Jedno stránková aplikace (SPA) | Web      | Přiřazené                | Yes           | Yes              | Ano, SSP používají Open ID Připojení implicitní Flow                            |
| Služba/démon        | Web      | Přiřazené                | Yes           | Yes              | No                                                                    |

## <a name="create-a-service-principal"></a>Vytvoření instančního objektu

Pokud chcete získat přístup k prostředkům ve vašem předplatném, musíte aplikaci přiřadit roli. Pomoc s rozhodováním, která role nabízí pro aplikaci správné oprávnění, najdete v tématu [Předdefinované role Azure.](/azure/role-based-access-control/built-in-roles)

> [!NOTE]
> Rozsah můžete nastavit na úrovni předplatného, skupiny prostředků nebo prostředku. Oprávnění se dědí do nižších úrovní oboru. Například přidání aplikace do role Čtenář pro skupinu prostředků znamená, že může číst skupinu prostředků a všechny prostředky, které obsahuje.

1. V Azure Portal vyberte úroveň oboru, ke které chcete aplikaci přiřadit. Pokud například chcete přiřadit roli v oboru předplatného, vyhledejte a vyberte **Předplatná** nebo **vyberte** Předplatná na domovské stránce.

   :::image type="content" source="./images/manage-payouts/search-for-subscriptions.png" alt-text="Snímek obrazovky znázorňující hledání na obrazovce Předplatná":::

2. Vyberte předplatné, ke které chcete aplikaci přiřadit.

   :::image type="content" source="./images/manage-payouts/internal-testing-subscription.png" alt-text="Snímek obrazovky Předplatná s příznakem Interní testování nastaveným na true":::

> [!NOTE]
> Pokud nevidíte předplatné, které hledáte, vyberte filtr globálních předplatných a ujistěte se, že je pro portál vybrané předplatné, které chcete.

3. Vyberte **Řízení přístupu (IAM)** a pak vyberte **Přidat přiřazení role.**

4. Vyberte roli, kterou chcete přiřadit k aplikaci. Pokud například chcete aplikaci povolit provádění akcí, jako je restartování, spuštění a zastavení instancí, vyberte roli Přispěvatel. Přečtěte si další informace [o dostupných rolích.](/azure/role-based-access-control/built-in-roles)

   Ve výchozím nastavení se aplikace Azure AD v dostupných možnostech nezobrazují. Pokud chcete najít aplikaci, vyhledejte název a ve výsledcích ji vyberte. Na následujícím snímku obrazovky `example-app` je aplikace AAD, kterou jste zaregistrovali.

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
