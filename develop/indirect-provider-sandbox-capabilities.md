---
title: Možnosti nepřímého poskytovatele CSP v sandboxu
description: Nepřímí poskytovatelé mohou pro účely testování vytvářet nepřímé prodejce v Sandboxu.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: 07608fb5f2d2a3ffc418188e0ac1ff367e3c5691aa241554a4a954de8c4f2005
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990670"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a>Možnosti sandboxu nepřímého poskytovatele CSP pro vytváření účtů nepřímých prodejců 

**Odpovídající role:** Nepřímý poskytovatel

Nepřímí poskytovatelé CSP si CSP Indirect Reseller sandboxu prostřednictvím svého vlastního účtu sandboxu vrstvy 2 na Partnerské centrum Portal.


## <a name="prerequisites"></a>Požadavky 

Partnerské centrum sandboxu nepřímého poskytovatele (vrstva 2). Scénář sandboxu podporuje ověřování pomocí samostatné aplikace i přihlašovacích údajů aplikace a uživatele. 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Nepřímý poskytovatel sandboxu – Vytvoření nepřímého prodejce sandboxu pomocí Partnerské centrum rozhraní 

 Jedná se o funkci sandboxu, která umožňuje nepřímým poskytovatelům sandboxu vytvořit účet nepřímého prodejce sandboxu prostřednictvím Partnerské centrum Portal.

Nepřímí poskytovatelé kapacity nepřímých prodejců v Sandboxu prostřednictvím uživatelského rozhraní služby Partnerské centrum scénáře: 

1. Nepřímí poskytovatelé CSP si mohou vytvořit CSP Indirect Reseller Sandbox prostřednictvím vlastního účtu sandboxu vrstvy 2 na Partnerské centrum Portal.
2. Nepřímí prodejci CSP mohou zobrazit zákazníka podle nepřímých poskytovatelů. 

1. Nepřímí prodejci CSP mohou spravovat zákaznický účet pomocí delegovaných oprávnění správce.

1. Nepřímí poskytovatelé CSP mohou pozvat nepřímé prodejce CSP.
 
1. Nepřímí poskytovatelé CSP mohou odstranit účet CSP Indirect Reseller sandboxu prostřednictvím vlastního účtu sandboxu vrstvy 2 na Partnerské centrum Portal.

    a.  Když nepřímý poskytovatel sandboxu odstraní relaci s nepřímým prodejcem sandboxu, zkontrolujte, jestli má nepřímý prodejce nějaký jiný vztah s jinými poskytovateli. Pokud ano, odebere se pouze vztah s tímto konkrétním nepřímým poskytovatelem.

    c. Pokud je to jediný vztah pro nepřímého prodejce, nepřímý prodejce se odstraní.

1. Nepřímí poskytovatelé CSP mohou odstranit CSP Indirect Reseller.

    a. Jedná se o funkci pouze sandboxu, která umožňuje nepřímým poskytovatelům sandboxu odstranit nepřímé prodejce sandboxu.
     
1. Předpoklady pro odstranění nepřímého prodejce sandboxu:

    1. Pozastavíte předplatná pro každého zákazníka nepřímého prodejce sandboxu.

    1. Odstraňte všechny zákazníky nepřímého prodejce.

1. Povolený limit pěti nepřímých prodejců sandboxu na nepřímého poskytovatele sandboxu. Po odstranění nepřímého prodejce sandboxu se kvóta resetuje.

### <a name="pre-requisites"></a>Požadavky

- Povolený limit pěti nepřímých prodejců sandboxu na nepřímého poskytovatele sandboxu. 

- Stejné ID MPN můžete použít k vytvoření několika účtů sandboxu nepřímého prodejce, pokud je země MPN ID země a země sandboxu nepřímého prodejce stejné. Pokud máte k dispozici testovací ID MPN, můžete ho použít nebo můžete získat seznam ID MPN prostřednictvím našeho [Yammer kanálu]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ). Pokud nemáte přístup k Yammer, Yammer požádat o přístup.
 
- Na nepřímého poskytovatele sandboxu je povolených jenom 75 zákazníků.

## <a name="create-csp-indirect-reseller-sandbox-account"></a>Vytvoření CSP Indirect Reseller sandboxu

1. Přihlaste se Partnerské centrum účtu sandboxu vrstvy 2. 

2. V nabídce vlevo přejděte na Indirect Resellers (Nepřímí prodejci). 

3. Vyberte tlačítko **Add Reseller Sandbox (Přidat sandbox prodejce).** 

4. Vyplňte formulář pro registraci účtu. Je to samozřejmé, ale nezapomeňte, že vytváříte účet sandboxu pro nepřímého prodejce. Tento účet se nebude prověřovat a aktivuje se ihned po dokončení registrace účtu.  

5. Po vytvoření účtu získáte na portálu přihlašovací údaje globálního správce pro účet sandboxu nepřímého prodejce. Nezapomeňte ho uložit okamžitě, jinak se nebudete moct přihlásit jako sandbox nepřímého prodejce. 

6. Odhlásit se a znovu se přihlásit Partnerské centrum pomocí nových přihlašovacích údajů pro Sandbox nepřímého prodejce. Prozkoumejte možnosti, které můžete dělat jako nepřímý prodejce. Tady jsou některé věci:  

    - Správa profilů  

    - Správa uživatelů a skupin 

    - Správa nepřímých poskytovatelů 

    - Správa zákazníků csp sandboxu 

    - Správa relací
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Nepřímý poskytovatel sandboxu – Odstranění nepřímého prodejce sandboxu pomocí Partnerské centrum rozhraní

 Jedná se o funkci sandboxu, která umožňuje nepřímým poskytovatelům sandboxu odstranit existující účet nepřímého prodejce sandboxu přes Partnerské centrum Portal. 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a>Předpoklady pro odstranění nepřímého prodejce sandboxu:

Existující účet CSP Indirect Reseller Sandbox přidružený k vašemu vlastnímu účtu CSP Indirect Provider Tier-2 Sandbox.  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a>Odstranění CSP Indirect Reseller sandboxu

1. Přihlaste se Partnerské centrum účtu sandboxu úrovně 2. 

2. V nabídce vlevo přejděte na Indirect Resellers (Nepřímí prodejci). 

3. Vyberte odkaz **Delete Reseller Sandbox (Odstranit sandbox prodejce)** vedle účtu sandboxu nepřímého prodejce, který chcete odstranit. Účet sandboxu nepřímého prodejce se trvale odstraní a není možné ho obnovit. 

## <a name="api-references"></a>Referenční informace k rozhraní API

- Vytvoření nepřímého prodejce 
- Odstranění nepřímého prodejce 

 

 