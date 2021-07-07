---
title: Úvodní příručka pro tvůrce výkladních skříní pro zákazníky CSP
description: Vytvořte online tržiště pro prodej nabídek csp (cloud solution provider) pomocí Tvůrce prodejních tržeb zákazníků CSP.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8550492c7a4201a955c7b051b453103628612f3e
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973345"
---
# <a name="csp-customer-storefront-builder-quick-start-guide"></a>Úvodní příručka pro tvůrce výkladních skříní pro zákazníky CSP

Vytvořte online tržiště pro prodej nabídek csp (cloud solution provider) pomocí Tvůrce prodejních tržeb zákazníků CSP.

## <a name="introduction-to-the-csp-customer-storefront-builder"></a>Seznámení s tvůrcem prodejníchek zákazníků CSP

CsP Customer Storefront Builder pomáhá partnerům snadno vytvořit online marketplace pro prodej nabídek CSP svým zákazníkům. Většina partnerů a malých prodejních organizací se chce místo vývoje online tržiště soustředit na prodej. Ukázková SDK pro Partnerské centrum k vytvoření a nasazení webu vyžaduje dovednosti v oblasti vývoje softwaru. S tvůrcem prodejníchek zákazníků CSP si můžete rychle a snadno vytvořit vlastní web. Můžete si také stáhnout web jako ukázkový kód nebo ho nasadit přímo do svého předplatného Azure s webem připravenou k transakci.

Tento web je plně vlastněný, podporovaný a udržovaný partnery a Microsoft z webu neshromažďuje žádná data ani telemetrii. CsP Customer Storefront Builder vytvoří web pro partnera, který je plně kompatibilní se standardem zabezpečení dat [v](https://www.pcisecuritystandards.org/) odvětví platebních karet (PCI DSS).

Kód CSP Customer Storefront Builder podléhá licenci dostupné v SDK pro Partnerské centrum [EULA.](/legal/partner-center/eula-partner-center-sdk)

>[!NOTE]
>Zodpovídáte za správu webových stránek, údržbu a případné problémy, které můžou být důsledkem vytvoření webu. Přečtěte si a pochopte výrazy v [SDK pro Partnerské centrum EULA.](/legal/partner-center/eula-partner-center-sdk)

Další informace najdete také v následujících článcích: webová prodejní skříň zákazníka [CSP](csp-customer-web-storefront.md) a [konzolová testovací aplikace](console-test-app.md).

## <a name="considerations"></a>Požadavky

Tvůrce zákaznických webových stránek CSP je určený jako rychlý způsob, jak vytvořit web. Při plánování je třeba vzít v úvahu následující aspekty:

- Po nasazení společnost Microsoft a Partnerské centrum neudrží kopii partnerského webu ani žádné informace přidané do tvůrce prodejníchek zákazníků CSP.

- Partnerské centrum partnerská předplatná Azure můžete nasadit pouze web CSP Customer Storefront.

- Po nasazení je tento web plně vlastněný a spravovaný partnerem. Microsoft nemá přístup k tomuto webu ani k žádným datům souvisejícím s webem. Partneři zodpovídají za údržbu a správu webu. Microsoft neposkytuje žádný živý web ani jinou podporu související s tvůrcem prodejních zprostředkovatelů zákazníků CSP ani žádným webem vytvořeným pomocí tvůrce zákaznického obchodu CSP.

- Partnerské centrum k tomuto webu přímo přistupovat nebo upgradovat pomocí nových nebo změněných funkcí sady SDK nebo rozhraní API. Veškeré nové funkce nebo vylepšení musí vlastnili, vyvíjet a spravovat partneři, včetně přidávání nových funkcí SDK pro Partnerské centrum rozhraní API.

- Tento Tvůrce prodejních prostorů zákazníků CSP v současné době umožňuje nakonfigurovat platbu na účet PayPal Pro/payu money (pro Indii). Pokud partneři potřebují změnit zpracovatele plateb, budou muset změnit kód tak, aby podporoval upřednostňovaný způsob platby.

- Žádné informace související s platbou přidané do Tvůrce prodejních zprostředkovatelů zákazníků CSP se neuchovávají v Partnerské centrum.

- PayPal konfigurace platby bude fungovat ve všech geografických lokalitách, kde PayPal k dispozici. PayPal dostupnost a podporu řídí výhradně PayPal a může být kdykoli ukončena pomocí PayPal.

- Konfigurace plateb za Platební karty bude v současné době fungovat pouze v Indii. Dostupnost a podpora s platbou se řídí výhradně pomocí payu a placené služby je možné kdykoli ukončit.

- Přečtěte si a pochopte výrazy v [SDK pro Partnerské centrum EULA.](/legal/partner-center/eula-partner-center-sdk)

## <a name="using-the-csp-customer-storefront-builder"></a>Použití tvůrce prodejníchek zákazníků CSP

Správci partnerů CSP na Partnerské centrum zprostředkovateli csp mohou přímo z Partnerské centrum. S minimálním úsilím je možné do tenanta partnera nasadit nový web. Po nasazení mohou partneři pomocí webu nakonfigurovat branding, nabídky a informace související s platbou a pak sdílet adresu URL webu se zákazníky.

Proces vytvoření webu s prodejními částmi je následující:

1. [Nasazení webu](#deploy)

2. [Konfigurace prodejní prodejny](#configure)

3. [Transakce ve storu](#transact)

### <a name="deploy"></a>Nasadit

Možnosti nasazení:

- Stáhněte [si Partnerské centrum kód z GitHub](https://github.com/Microsoft/Partner-Center-Storefront)
- Integrace s Azure pro nasazení nakonfigurovaného webu
- Nasazení ve stávajícím předplatném nebo přineste si vlastní předplatné

### <a name="configure"></a>Konfigurace

K přizpůsobení prodejní prodejny nejsou potřeba žádné vývojové dovednosti.

Přihlaste se pomocí svých přihlašovacích Partnerské centrum správce a nakonfigurujte:

- **Branding:** název společnosti, logo, kontakty a další.

- **Nabídky:** Zobrazení všech nabídek CSP. Můžete vybrat, které nabídky mohou vaši zákazníci zobrazit a zakoupit. Můžete také přizpůsobit informace o nabídce a přidat svou cenu.

- **PayPal platby:** přidejte informace PayPal platebního účtu. Pokud nemáte účet PayPal, můžete navštívit [https://www.paypal.com](https://www.paypal.com) a vytvořit nový účet. Tento účet se použije pro PayPal k připsaní plateb provedených zákazníky. *Microsoft neodpovídá za vztah mezi partnery a PayPal. Použití PayPal může vyžadovat, aby se partner nebo zákazníci partnera shodli na dalších podmínkách.*

- (*Pro Indii*) **Konfigurace platby pomocí platebního účtu:** Přidejte informace o platebním účtu s platbou v platbách. Pokud nemáte účet s platbou peněz, můžete navštívit [https://www.payumoney.com/](https://www.payumoney.com/) a vytvořit nový účet. Tento účet se použije pro platbu pomocí platební karty k připsaní plateb provedených zákazníky. *Microsoft neodpovídá za vztah mezi partnery a platbami. Použití placené platby může vyžadovat, aby se zákazníci partnera nebo partnera shodli na dalších podmínkách.*

### <a name="transact"></a>Transakce

- Po nasazení mohou zákazníci okamžitě nakupovat a provádět transakce.

- Zákazníci si mohou koupit přímo z partnerského portálu integrovaného s SDK pro Partnerské centrum.

#### <a name="customer-countries"></a>Země zákazníka

Zákazníci mohou patřit do těchto zemí:

| Kód země | Jméno země   |
|--------------|----------------|
| AU           | Austrálie      |
| AT           | Rakousko        |
| BE           | Belgie        |
| BG           | Bulharsko       |
| CA           | Kanada         |
| HR           | Chorvatsko        |
| CY           | Kypr         |
| CZ           | Česká republika |
| DK           | Dánsko        |
| EE           | Estonsko        |
| FI           | Finsko        |
| FR           | Francie         |
| DE           | Německo        |
| GR           | Řecko         |
| HU           | Maďarsko        |
| IS           | Island        |
| IN           | Indie          |
| IE           | Irsko        |
| IT           | Itálie          |
| JP           | Japonsko          |
| LV           | Lotyšsko         |
| LI           | Lichtenštejnsko  |
| LT           | Litva      |
| LU           | Lucembursko     |
| MT           | Malta          |
| MC           | Monako         |
| NL           | Nizozemsko    |
| NZ           | Nový Zéland    |
| NO           | Norsko         |
| PO           | Polsko         |
| PT           | Portugalsko       |
| RO           | Rumunsko        |
| SK           | Slovensko       |
| SL           | Slovinsko       |
| ES           | Španělsko          |
| SE           | Švédsko         |
| CH           | Švýcarsko    |
| GB           | Spojené království |
| USA           | USA  |

## <a name="partner-experience-scenarios"></a>Scénáře partnerských zkušeností

### <a name="deployment-scenario"></a>Scénář nasazení

Nasazení rozšířeného nebo přizpůsobeného zákaznického Prezentaceu CSP:

- Stáhněte si [vzorový kód partnerského centra prezentace](https://github.com/Microsoft/Partner-Center-Storefront) a udělejte další přizpůsobení.

- k vývoji použijte Microsoft Visual Studio 2015 (nebo novější).

- Sestavení pro další změny a vylepšení (včetně autorizací, certifikace, změn manifestu a dalších položek).

### <a name="configuration-scenario"></a>Scénář konfigurace

- Nově vytvořený web je propojený s partnerským klientem a má přístup ke všem účtům správců tohoto partnerského tenanta.

  - Partneři se můžou k tomuto novému webu přihlásit pomocí přihlašovacích údajů správce partnerského centra.

- Aplikace prezentace aktuálně podporuje francouzštinu, španělštinu, holandštinu, němčinu, japonštinu a angličtinu. (Angličtina slouží jako náhradní jazyk.)

  - Prezentace konfiguruje národní prostředí pomocí výchozího národního prostředí partnera z profilu partnera v partnerském centru. Toto národní prostředí se používá ke konfiguraci měn, formátů data a lokalizovaných nabídek v úložišti.

- partneři můžou konfigurovat branding, nabídky a PayPal nebo PayU (pro indie) platební informace.

- Partneři můžou aktualizovat název společnosti, logo společnosti, obrázek záhlaví, kontakty pro prodej a podporu a další.

- Partneři můžou zobrazit všechny dostupné nabídky CSP na základě jejich území.

  - Partneři si můžou vybrat, které nabídky chtějí zobrazovat všem svým zákazníkům.

  - Partner CSP může vybrat jednu nebo více nabídek a aktualizovat název, množství, popis funkce a cenu.
  - Cena je roční cena. Zákazníci se každoročně přihlásí.

- Partneři můžou kdykoli nakonfigurovat předem schválené transakce pro všechny aktuální a budoucí zákazníky nebo (b) konkrétní zákazníky.

  - Předběžně schválené zákazníky nemusejí platit na portálu, když přidávají nové předplatné, nakupují další licence k existujícím předplatným nebo obnoví předplatné.

  - předběžně schválené zákazníky nebudou přesměrované na PayPal ani PayU (pro indie) pro platbu během těchto transakcí.

  - Předběžně schválené transakce zákazníka umožňují partnerovi provádět online fakturaci a fakturování předem schváleným zákazníkům.

- partner CSP může zadat své PayPal informace o účtu, například PayPal ID klienta a tajný kód. Partner CSP taky může vybrat, jestli se chce testovat pomocí izolovaného prostoru nebo živého účtu.

  - Partneři můžou tyto informace najít [https://developer.paypal.com/](https://developer.paypal.com/) v nabídce **moje aplikace & přihlašovací údaje**. Tyto informace můžete získat také z aktuální aplikace nebo vytvořením nové aplikace v PayPal.
  - vytvořte nový účet PayPal, pokud ho ještě nemáte. tento účet se bude používat pro PayPal k kreditu plateb provedených zákazníky.

    - pokud chcete otevřít PayPal obchodní účet, přečtěte si téma [https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register](https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register) .

    - postup vytvoření PayPal účtu izolovaného prostoru (sandbox) najdete v tématu [https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/](https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/) .

- (V případě Indie) může partner CSP zadat své PayU informace o peněžním účtu, jako je PayU ID klienta a heslo. Partneři můžou najít další informace [https://developer.payumoney.com/](https://developer.payumoney.com/) .

  - Vytvořte nový PayU peněžní účet, pokud ho ještě nemáte. Pokud chcete otevřít účet PayU Money, navštivte [https://www.payumoney.com/merchant-account/#/](https://www.payumoney.com/merchant-account/#/) . Tento účet se bude používat pro PayU k kreditu plateb provedených zákazníky.

## <a name="customer-experience-scenarios"></a>Scénáře zákaznického prostředí

### <a name="new-customer-sign-up-scenario"></a>Scénář registrace nového zákazníka

- Ve výchozím nastavení je web veřejně dostupný a zobrazuje katalog partnerů na domovské stránce.

- Zákazníci teď můžou patřit do velkého počtu [zákaznických zemí](#customer-countries).

- Zaměřuje se na evropské země sdružení volného obchodu (ESVO), Severní Amerika, Japonsko, Indie, Austrálie a nové oblasti Zélandu.
  - Tato funkce využívá podporu regionálního ověřování v partnerském centru SDK.

- Zákazníci si můžou z katalogu vybrat nabídku k nákupu.
  - Můžou přidat své jméno zákazníka, adresu a informace související s doménou.

- zákazníci budou přesměrováni na PayPal nebo PayU (pro indie) a na možnosti rezervace. Zákazníci můžou platbu poskytnout pomocí těchto akcí:
  - svůj stávající účet PayPal nebo PayU (pro indie)
  - prostředky financování podporované v zemi PayPal nebo PayU (pro indie) Ty můžou zahrnovat kreditní karty, debetní karty a bankovní účty, jak je to možné.

- Pro tohoto zákazníka se vytvoří tenant zákazníka. Po úspěšném vytvoření objednávky tenanta se zákazníkům zobrazí podrobnosti o uživatelském účtu, heslu a předplatném.
  - Zákazníci si mohou uživatelské jméno a heslo uložit, aby zůstali přihlášeni k dalším nákupům.
  - Každé předplatné se kupuje po dobu jednoho roku a zákazníci se mohou prodloužit do 30 dnů před koncovým datem předplatného.

### <a name="view-prior-purchases-scenario"></a>Zobrazení scénáře předchozích nákupů

- Zákazník se přihlásí pomocí uživatelského jména a hesla tenanta zákazníka a přejde do části **Moje** objednávky.

- Zákazníci mohou přejít na **stránku Moje objednávky,** kde mohou zobrazit zakoupená předplatná a v případě potřeby provádět aktualizace.

- Zákazníci mohou přejít na **stránku Moje předplatná,** kde mohou zobrazit všechna předplatná (založená na licencích i na základě využití), včetně předplatných udržovaných v Partnerské centrum.

### <a name="add-licenses-to-existing-subscriptions-scenario"></a>Přidání licencí do existujícího scénáře předplatných

- V části **Moje** objednávky mohou zákazníci přidat další licence do stávajících předplatných. Zákazníci mohou přidat další licence kdykoli během jednoho roku předplatného.

- Každá přidaná licence nezmění koncové datum předplatného. Cena předplatného se ale změní v závislosti na datu, ke kterému licenci přidáte, a v místě, kde se toto datum nachází v roce. Ceny se každý den účtují podle toho, že se účtují pouze za zbývající dny v roce.

### <a name="add-more-subscriptions-scenario"></a>Přidání dalšího scénáře předplatných

- Zákazníci si mohou kdykoli koupit libovolný počet předplatných v části Přidat **předplatná** v části **Moje objednávky.**

- Zákazník může vybrat předplatné, přidat množství a zaplatit za dokončení transakce a začít předplatné okamžitě používat. Pokud je zákazník předběžně schváleným zákazníkem, je předplatné k dispozici okamžitě a faktura se zákazníkovi za platbu zasílá.

### <a name="renew-subscription-scenario"></a>Scénář prodloužení platnosti předplatného

- Zákazník může předplatné prodloužit během posledních 30 dnů před koncovým datem předplatného.

- Tato aktualizace je dostupná jenom během posledních 30 dnů.

- Pokud se předplatné během posledních 30 dnů neobnoví, odebere se ze seznamu předplatných pro tohoto tenanta zákazníka.

- Během prodloužení není možné aktualizovat množství.

### <a name="payments-scenario"></a>Scénář plateb

- Pokud správce předem schválí transakce zákazníka, pro výše uvedené scénáře se platební prostředí nebude prezentovat. Místo toho může partner odeslat fakturu za platbu předem schválenému zákazníkovi.

- U všech nových nákupů můžete přidat další licence, přidat předplatná a prodloužit jejich platnost. Zákazník může partnera zaplatit pomocí tohoto webu prostřednictvím PayPal nebo PayU (pro Indii).

- Tento web je integrovaný s PayPal nebo PayU (pro Indii) a umožňuje partnerům přijímat platby od zákazníků. PayPal účtu partnera tuto částku přičtete platební karty nebo payu (pro Indii). PayPal správu bankovních účtů v usa nebo v Indii se spravuje mimo tento web a spravuje se na PayPal.com nebo PayUmoney.com v uvedeném pořadí.

- To závisí na konfiguraci plateb pro PayPal partnery nebo pro Indii na PayPal.com nebo PayUmoney.com. Společnost Microsoft neuchová tyto informace ani skutečné platební transakce vyplývající z použití této možnosti.

### <a name="prorated-pricing-scenario"></a>Scénář s cenami naceněnou podle přímky

- Tento web podporuje ceny za vyšší ceny v případech, kdy zákazníci přidávají další licence do stávajícího předplatného.

- Platnost každého předplatného vyprší po jednom roce a po zakoupení předplatného není možné ho změnit.

- Koncové datum předplatného se nezmění přidáním dalších licencí. Zákazníkům se bude účtovat zbývající počet dnů do koncového data. Pokud jsou například první den náklady na předplatné 365 USD a další licenci přidáte ve dva den, bude cena nové licence 364 USD. Pokud o 10 dní později přidáte další licenci, bude cena 354 USD.
