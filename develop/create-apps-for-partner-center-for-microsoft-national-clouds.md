---
title: Registrace podrobností o aplikaci pro partnerského centra pro národní Cloud Microsoftu
description: Přečtěte si, jak a proč můžou vývojáři aplikací pro partnerské Centrum pro národní Cloud od Microsoftu zaregistrovat podrobnosti o své aplikaci pomocí služby Azure AD prostřednictvím Azure Portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 887cb71c752ac5d9c61398536711545c19cc7600
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/07/2020
ms.locfileid: "97767132"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a>Zaregistrujte podrobnosti o aplikaci pro partnerského centra pro národní Cloud Microsoftu prostřednictvím Azure Portal

**Platí pro:**

- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Vývojáři musí zaregistrovat podrobnosti o své aplikaci pomocí služby Azure AD prostřednictvím Azure Portal. To pomáhá zajistit, že se k partnerům a zákaznickým datům budou moci připojit pouze konkrétní aplikace.

Pro partnerského centra Microsoft Cloud pro státní správu USA je aktuálně nutné spravovat aplikace prostřednictvím PowerShellu. Další informace najdete v [dokumentaci Azure PowerShell reference](/powershell/module/Azuread/#applications).

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pamatujte na následující další požadavky, když vytvoříte aplikaci pro partnerského centra pro Microsoft Cloud Německo nebo partnerské Centrum pro Microsoft Cloud pro státní správu USA.

## <a name="web-apps"></a>Webové aplikace

Pro webové aplikace použijte následující postupy k registraci ID aplikace.

### <a name="create-or-update-web-app"></a>Vytvořit nebo aktualizovat webovou aplikaci

1. Pro registraci aplikace přejděte na stránku [Azure Portal-registrace aplikací](https://go.microsoft.com/fwlink/?linkid=2083908) . Přihlaste se k webu Azure Portal pomocí pracovního nebo školního účtu nebo osobního účtu Microsoft.

2. Vyberte **Nová registrace**. Další informace najdete v tématu [rychlý Start: registrace aplikace s platformou Microsoft Identity](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-web-app"></a>Konfigurace přístupových oprávnění k rozhraní API pro webovou aplikaci

1. Zvolte aplikaci. Přejít na **Nastavení** webové aplikace

2. V části **přístup k rozhraní API** vyberte **požadovaná oprávnění** .

3. Oprávnění pro Windows Azure Active Directory:

    1. Vyberte možnost **Windows Azure Active Directory oprávnění**.

    2. V **oprávnění aplikace** vyberte číst data adresáře.

    3. Uložte oprávnění.

4. Poznamenejte si ID aplikace v části **vlastnosti** vaší webové aplikace.

### <a name="add-a-secret-key-to-your-app"></a>Přidání tajného klíče do aplikace

1. Přejít do části **klíče** ve vaší webové aplikaci.

2. Zadejte popis klíče a vyberte dobu trvání 1 nebo 2 roky, jak potřebujete.

3. Uložte a zkopírujte hodnotu tajného klíče. **Tato hodnota se po opuštění této stránky znovu nezobrazí.**

Z konfigurace webové aplikace byste měli mít následující podrobnosti:

- ID aplikace
- Tajný kód aplikace

### <a name="register-the-web-app-in-partner-center"></a>Registrace webové aplikace v partnerském centru

1. Přihlaste se k [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) .

2. Zvolte **řídicí panel**, vyberte **Nastavení účtu** a pak zvolte **Správa aplikací**.

3. V části **Webová aplikace** vyberte **zaregistrovat existující aplikaci**.

4. Vyberte webovou aplikaci, kterou jste vytvořili v Azure Portal.

5. Vyberte možnost **zaregistrovat aplikaci**.

## <a name="native-apps"></a>Nativní aplikace

Nativní aplikace nemusí být zaregistrované v partnerském centru. Tyto aplikace je ale potřeba nakonfigurovat tak, aby poskytovaly přístup k rozhraním API partnerského centra.

>[!NOTE]
>Před vytvořením nativní aplikace v Azure Portal se přihlaste do partnerského centra pomocí pověření uživatele správce z partnerského tenanta. Tím se vytvoří nastavení v tenantovi, aby se povolila oprávnění aplikace.

### <a name="create-native-app"></a>Vytvořit nativní aplikaci

1. Pro registraci aplikace přejděte na stránku [Azure Portal-registrace aplikací](https://go.microsoft.com/fwlink/?linkid=2083908) . Přihlaste se k webu Azure Portal pomocí pracovního nebo školního účtu nebo osobního účtu Microsoft.

2. Vyberte **Nová registrace**. Další informace najdete v tématu [rychlý Start: registrace aplikace s platformou Microsoft Identity](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-native-app"></a>Konfigurace přístupových oprávnění k rozhraní API pro nativní aplikaci

1. Zvolte aplikaci. Přejít na **Nastavení**.

2. V možnosti přístup přes rozhraní API vyberte **požadovaná oprávnění**.

3. Vyberte možnost **Windows Azure Active Directory oprávnění**. V **delegovaných oprávněních** vyberte Tato oprávnění:

    - **Přihlášení a čtení profilu uživatele**
    - **Čtení dat z adresáře**
    - **Přístup k adresáři jako přihlášený uživatel**
    - **Číst všechny skupiny**

4. Uložte oprávnění.

5. V **požadovaném oprávnění** vyberte **Přidat** .

6. Zvolte **Vyberte rozhraní API**.

    1. Do vyhledávacího pole zadejte **Microsoft Partner Center** a vyberte ho ze seznamu výsledků.

    2. Zvolte **Vybrat**.

7. Zvolte **možnost vybrat oprávnění**.

    1. Vyberte **OOP Access partner Center**.
    
    2. Zvolte **Vybrat**.

8. Vyberte **Hotovo**.

>[!IMPORTANT]
> Poznamenejte si ID aplikace ve vlastnostech vaší aplikace.

V partnerském centru nemusíte registrovat nativní aplikace, ale je potřeba, aby byla v nativní aplikaci souhlas správce. Poznamenejte si ID aplikace vaší nativní aplikace.
