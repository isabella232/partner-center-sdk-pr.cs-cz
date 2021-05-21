---
title: Schopnosti nepřímých poskytovatelů CSP v izolovaném prostoru
description: Nepřímá poskytovatelé můžou vytvořit nepřímé prodejce v izolovaném prostoru (sandbox) pro účely testování.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: bd0f38103e6b6f93ab5da386042b00801b683ccd
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2021
ms.locfileid: "110244601"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a>Funkce izolovaného prostoru nepřímých poskytovatelů CSP pro vytváření nepřímých účtů prodejců 

**Platí pro**

- Partnerské centrum

**Příslušné role**

- Nepřímý poskytovatel

Zprostředkovatelé nepřímých poskytovatelů CSP můžou vytvořit účet nepřímého prodejce CSP prostřednictvím vlastního účtu izolovaného prostoru (sandboxu) na portálu pro partnery v partnerském centru.


## <a name="prerequisites"></a>Požadavky 

Přihlašovací údaje k izolovanému prostoru nepřímých zprostředkovatelů (vrstvy 2) partnerského centra Scénář izolovaného prostoru (sandbox) podporuje ověřování jak pro samostatnou aplikaci, tak i pro přihlašovací údaje uživatele a aplikace. 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Nepřímý poskytovatel izolovaného prostoru – vytvoření nepřímého prodejce izolovaného prostoru pomocí uživatelského rozhraní partnerského centra 

 Jedná se o funkci pouze izolovaného prostoru, která umožňuje nepřímým poskytovatelům izolovaného prostoru vytvořit účet nepřímých prodejců izolovaného prostoru prostřednictvím portálu pro partnery služby.

Následující scénáře se dají nepřímým poskytovatelům provádět u nepřímých prodejců v izolovaném prostoru (sandbox) prostřednictvím uživatelského rozhraní partnerského centra: 

1. Nepřímá poskytovatelé CSP můžou vytvořit účet nepřímých prodejců CSP prostřednictvím vlastního účtu izolovaného prostoru (sandboxu) v portálu pro partnery v partnerském centru.
2. Nepřímým prodejcům CSP můžou zákazníka zobrazit nepřímými poskytovateli. 

1. Nepřímí prodejci CSP můžou spravovat účet zákazníka pomocí delegovaných oprávnění správce.

1. Nepřímá poskytovatelé CSP můžou pozvat nepřímým prodejcům CSP.
 
1. Nepřímá poskytovatelé CSP mohou odstranit účet nepřímého prodejce CSP prostřednictvím vlastního účtu izolovaného prostoru (sandbox) v portálu pro partnery.

    a.  Když nepřímý poskytovatel izolovaného prostoru odstraní relaci s nepřímým prodejcem izolovaného prostoru.

    b.  Zkontroluje, jestli má nepřímý prodejce jiné vztahy s ostatními poskytovateli. Pokud ano, bude odebrán pouze vztah s tímto konkrétním nepřímým zprostředkovatelem.

    c. Pokud se jedná o jediný vztah pro IR, bude IR odstraněn.

1. CSP Indirect Provider můžete odstranit CSP Indirect Reseller.

    a. Jedná se o funkci sandboxu, která umožňuje nepřímým poskytovatelům sandboxu odstranit nepřímé prodejce Sandboxu.
     
1. Předpoklady pro odstranění nepřímého prodejce sandboxu:

    1. Pozastavíte předplatná pro každého zákazníka nepřímého prodejce sandboxu.

    1. Odstraňte všechny zákazníky nepřímého prodejce.

1. Povolený limit 5 nepřímých prodejců sandboxu na nepřímého poskytovatele sandboxu. Po odstranění nepřímého prodejce sandboxu se kvóta resetuje.

### <a name="pre-requisites"></a>Požadavky

- Povolený limit 5 nepřímých prodejců sandboxu na nepřímého poskytovatele sandboxu. 

- Stejné ID MPN můžete použít k vytvoření několika účtů sandboxu nepřímého prodejce, pokud je země MPN ID země a země sandboxu nepřímého prodejce stejné. Pokud máte k dispozici testovací ID MPN, můžete ho použít nebo můžete získat seznam ID MPN prostřednictvím našeho [kanálu Yammeru]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ). Pokud nemáte přístup k Yammeru, Yammer vás požádá o přístup.
 
- Na nepřímého poskytovatele sandboxu je povolených jenom 75 zákazníků.

## <a name="create-csp-indirect-reseller-sandbox-account"></a>Vytvoření CSP Indirect Reseller sandboxu

1. Přihlaste se Partnerské centrum účtu sandboxu úrovně 2. 

2. V levé nabídce přejděte na Indirect Resellers (Nepřímí prodejci). 

3. Klikněte na tlačítko Add Reseller Sandbox (Přidat sandbox prodejce). 

4. Vyplňte formulář pro registraci účtu. Je to samozřejmé, ale nezapomeňte, že vytváříte účet sandboxu pro nepřímého prodejce. Tento účet se nebude prověřovat a aktivuje se ihned po dokončení registrace účtu.  

5. Po vytvoření účtu získáte na portálu přihlašovací údaje globálního správce pro účet sandboxu nepřímého prodejce. Nezapomeňte ho uložit hned, jinak se nebudete moct přihlásit jako nepřímý prodejce prodejců. 

6. Odhlaste se a znovu se přihlaste do partnerského centra pomocí nových přihlašovacích údajů pro nepřímý izolovaný prostor prodejce. Prozkoumejte možnosti, které můžete udělat jako nepřímý prodejce. Některé věci:  

    - Správa profilů  

    - Správa uživatelů a skupin 

    - Správa nepřímých zprostředkovatelů 

    - Správa zákazníků v izolovaném prostoru (CSP) 

    - Správa relací
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Nepřímý poskytovatel izolovaného prostoru – odstranění nepřímého prodejce izolovaného prostoru pomocí uživatelského rozhraní partnerského centra

 Jedná se o funkci pouze izolovaného prostoru, která umožňuje nepřímým poskytovatelům izolovaného prostoru odstranit stávající účet nepřímých prodejců izolovaného prostoru prostřednictvím portálu pro partnery. 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a>Požadavky na odstranění nepřímého prodejce izolovaného prostoru:

Existující účet izolovaného prostoru nepřímých prodejců CSP přidružený k vlastnímu účtu izolovaného poskytovatele CSP – 2.  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a>Odstranit účet izolovaného prostoru nepřímých prodejců CSP

1. Přihlaste se k partnerskému centru pomocí účtu sandboxu vrstvy 2. 

2. V nabídce vlevo přejděte na nepřímé prodejce. 

3. Klikněte na odkaz **Odstranit prodejce izolovaného prostoru** vedle nepřímým účtem izolovaného prostoru (sandbox) prodejce, který chcete odstranit. Účet izolovaného prostoru pro prodejce se trvale odstraní a nebude možné ho obnovit. 

## <a name="api-references"></a>Referenční informace k rozhraní API

- Vytvořit nepřímý prodejce 
- Odstranit nepřímý prodejce 

 

 