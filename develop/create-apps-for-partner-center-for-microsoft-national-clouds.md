---
title: Registrace podrobností o aplikaci Partnerské centrum pro národní cloud Microsoftu
description: Zjistěte, jak a proč musí vývojáři aplikací pro Partnerské centrum pro národní cloud Microsoftu registrovat podrobnosti o své aplikaci ve službě Azure AD prostřednictvím Azure Portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93d46a17bc26e9586e5e773bdf934653a571367f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973447"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a>Registrace podrobností o aplikaci Partnerské centrum pro národní cloud Microsoftu prostřednictvím Azure Portal

**Platí pro:** Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Vývojáři musí podrobnosti o své aplikaci zaregistrovat v Azure AD prostřednictvím Azure Portal. To pomáhá zajistit, že se k datům partnerů a zákazníků budou moct připojit jenom zadané aplikace.

Pro Partnerské centrum pro Microsoft Cloud for US Government v současné době musíte spravovat aplikace prostřednictvím PowerShellu. Další informace najdete v referenční [Azure PowerShell dokumentaci.](/powershell/module/Azuread/#applications)

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Při vytváření aplikace pro službu Microsoft Cloud Germany Partnerské centrum Microsoft Cloud Germany nebo pro Partnerské centrum pro Microsoft Cloud for US Government je třeba mít na paměti následující Microsoft Cloud for US Government.

## <a name="web-apps"></a>Webové aplikace

Pro webové aplikace použijte následující postupy k registraci ID vaší aplikace.

### <a name="create-or-update-web-app"></a>Vytvoření nebo aktualizace webové aplikace

1. Přejděte na [stránku Azure Portal – Registrace aplikací](https://go.microsoft.com/fwlink/?linkid=2083908) a zaregistrujte aplikaci. Přihlaste se k webu Azure Portal pomocí pracovního nebo školního účtu nebo osobního účtu Microsoft.

2. Vyberte **New registration (Nová registrace).** Další informace najdete v tématu [Rychlý start: Registrace aplikace v Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-web-app"></a>Konfigurace přístupových oprávnění rozhraní API pro webovou aplikaci

1. Zvolte aplikaci. Přejděte **Nastavení** webové aplikace.

2. V **části Přístup rozhraní API** zvolte **Požadovaná oprávnění.**

3. Další Windows Azure Active Directory:

    1. Zvolte **Windows Azure Active Directory oprávnění.**

    2. V **části Oprávnění aplikací** vyberte Číst data adresáře.

    3. Uložte oprávnění.

4. Poznamenejte si ID aplikace v **části Vlastnosti** vaší webové aplikace.

### <a name="add-a-secret-key-to-your-app"></a>Přidání tajného klíče do aplikace

1. Přejděte do **části Klíče** vaší webové aplikace.

2. Zadejte popis klíče a vyberte dobu trvání 1 nebo 2 roky podle potřeby.

3. Uložte a zkopírujte hodnotu tajného klíče. **Po opouštění této stránky se tato hodnota znovu nezobrazí.**

Z konfigurace webové aplikace byste měli mít následující podrobnosti:

- ID aplikace
- Tajný kód aplikace

### <a name="register-the-web-app-in-partner-center"></a>Registrace webové aplikace v Partnerské centrum

1. Přihlaste se k webu [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).

2. Zvolte **Řídicí** panel, zvolte **Účet Nastavení** a pak zvolte Správa **aplikací.**

3. V části **Webová aplikace** zvolte **Zaregistrovat existující aplikaci.**

4. Vyberte webovou aplikaci, kterou jste vytvořili v Azure Portal.

5. Zvolte **zaregistrovat aplikaci.**

## <a name="native-apps"></a>Nativní aplikace

Nativní aplikace nemusí být zaregistrované k Partnerské centrum. Tyto aplikace je ale potřeba nakonfigurovat tak, aby poskytovaly přístup Partnerské centrum rozhraním API.

>[!NOTE]
>Před vytvořením nativní aplikace v Azure Portal se přihlaste k Partnerské centrum pomocí přihlašovacích údajů správce z partnerského tenanta. Tím se v tenantovi vytvoří nastavení pro povolení oprávnění aplikace.

### <a name="create-native-app"></a>Vytvoření nativní aplikace

1. Přejděte na [stránku Azure Portal – Registrace aplikací](https://go.microsoft.com/fwlink/?linkid=2083908) a zaregistrujte aplikaci. Přihlaste se k webu Azure Portal pomocí pracovního nebo školního účtu nebo osobního účtu Microsoft.

2. Vyberte **New registration (Nová registrace).** Další informace najdete v tématu [Rychlý start: Registrace aplikace v Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-native-app"></a>Konfigurace přístupových oprávnění rozhraní API pro nativní aplikaci

1. Zvolte aplikaci. Přejděte na **Nastavení**.

2. V části Přístup pomocí rozhraní API zvolte **Požadovaná oprávnění.**

3. Zvolte **Windows Azure Active Directory oprávnění.** V **části Delegovaná** oprávnění vyberte tato oprávnění:

    - **Přihlášení a čtení profilu uživatele**
    - **Čtení dat z adresáře**
    - **Přístup k adresáři jako přihlášený uživatel**
    - **Čtení všech skupin**

4. Uložte oprávnění.

5. V **části Požadovaná** **oprávnění zvolte Přidat.**

6. Zvolte **Vyberte rozhraní API**.

    1. Do vyhledávacího pole zadejte **Microsoft Partnerské centrum** a vyberte ho ze seznamu výsledků.

    2. Zvolte **Vybrat**.

7. Zvolte **Vybrat oprávnění.**

    1. Vyberte **Přístupový Partnerské centrum PPE.**
    
    2. Zvolte **Vybrat**.

8. Vyberte **Hotovo**.

>[!IMPORTANT]
> Poznamenejte si ID aplikace ve vlastnostech vaší aplikace.

Není nutné registrovat nativní aplikace v Partnerské centrum, ale nativní aplikace musí být odsoulaná správcem. Poznamenejte si ID vaší nativní aplikace.
