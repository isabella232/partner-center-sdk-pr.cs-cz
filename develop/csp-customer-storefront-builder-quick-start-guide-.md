---
title: Úvodní příručka pro tvůrce výkladních skříní pro zákazníky CSP
description: Vytvořte online tržiště pro prodej nabídek csp (cloud solution provider) pomocí Tvůrce prodejních tržeb zákazníků CSP.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 69fe30b61d7260e4c3365d2486cec5ffadd2a3fbb39bb50158a44d8716ff2d71
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995216"
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

## <a name="partner-experience-scenarios"></a>Scénáře partnerského prostředí

### <a name="deployment-scenario"></a>Scénář nasazení

Nasazení vylepšené nebo přizpůsobené prodejní prodejny zákazníků CSP:

- Stáhněte si [Partnerské centrum kódu ve storu](https://github.com/Microsoft/Partner-Center-Storefront) a proveďte další úpravy.

- K Microsoft Visual Studio použijte nástroj 2015 (nebo novější).

- Sestavení pro další změny a vylepšení (včetně autorizací, certifikací, změn manifestu a dalších položek)

### <a name="configuration-scenario"></a>Scénář konfigurace

- Nově vytvořený web je propojený s partnerským tenantem a má přístup ke všem účtům správce tohoto partnerského tenanta.

  - Partneři se k tomuto novému webu mohou přihlásit pomocí svých přihlašovacích Partnerské centrum správce.

- Aplikace pro prodejní prodejny v současné době podporuje francouzštinu, španělštinu, nizozemštinu, němčinu, japonštinu a angličtinu. (Angličtina slouží jako záložní jazyk.)

  - Prodejní skříň nakonfiguruje národní prostředí pomocí výchozího národního prostředí partnera z profilu partnera v Partnerské centrum. Toto národní prostředí slouží ke konfiguraci měn, formátů dat a lokalizovaných nabídek v úložišti.

- Partneři mohou konfigurovat branding, nabídky a PayPal platební údaje nebo platební údaje pro Platby (pro Indii).

- Partneři mohou aktualizovat název společnosti, logo společnosti, obrázek záhlaví, kontakty pro prodej a podporu a další.

- Partneři uvidí všechny dostupné nabídky CSP na základě jejich teritoria.

  - Partneři si mohou vybrat, které nabídky chtějí zobrazit všem svým zákazníkům.

  - Partner CSP může vybrat jednu nebo více nabídek a aktualizovat název, množství, popis funkce a cenu.
  - Cena je roční cena. Zákazníci se předplatí ročně.

- Partneři mohou kdykoli nakonfigurovat předběžně schválené transakce pro (a) všechny aktuální a budoucí zákazníky NEBO (b) konkrétní zákazníky.

  - Předschválení zákazníci nemusí platit na portálu, když přidávají nová předplatná, kupují další licence ke stávajícím předplatným nebo prodlužují platnost předplatného.

  - Předschválení zákazníci nebudou během těchto transakcí přesměrováni PayPal ani na platby za platby (pro Indii).

  - Předem schválené transakce zákazníků umožňují partnerovi provádět offline fakturaci a fakturaci svým předběžně schváleným zákazníkům.

- Partner CSP může zadat informace o PayPal účtu, jako je PayPal ID klienta a tajný klíč. Partner CSP si také může vybrat, jestli chce testovat pomocí sandboxu nebo živého účtu.

  - Partneři najdou tyto informace v [https://developer.paypal.com/](https://developer.paypal.com/) části Moje aplikace & přihlašovací **údaje.** Tyto informace můžete získat také z aktuální aplikace nebo vytvořením nové aplikace v PayPal.
  - Vytvořte nový PayPal, pokud ho ještě nemáte. Tento účet se použije pro PayPal k připsaní plateb provedených zákazníky.

    - Pokud chcete otevřít PayPal obchodní účet, podívejte se na . [https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register](https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register)

    - Pokud chcete vytvořit PayPal sandboxu, podívejte se na [https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/](https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/) .

- (Pro Indii) Partner CSP může zadat informace o účtu s platbou, jako je ID klienta s platbou a heslo. Další informace o produktu najdete u [https://developer.payumoney.com/](https://developer.payumoney.com/) partnerů.

  - Vytvořte nový účet s platbou, pokud ho ještě nemáte. Pokud chcete otevřít účet s platbou peněz, přejděte na [https://www.payumoney.com/merchant-account/#/](https://www.payumoney.com/merchant-account/#/) . Tento účet se použije pro platbu pomocí platební karty k připsaní plateb provedených zákazníky.

## <a name="customer-experience-scenarios"></a>Scénáře s prostředím pro zákazníky

### <a name="new-customer-sign-up-scenario"></a>Scénář registrace nového zákazníka

- Ve výchozím nastavení je web veřejně dostupný a zobrazuje katalog partnera na domovské stránce.

- Zákazníci teď mohou patřit do velkého počtu [zákaznických zemí](#customer-countries).

- Zaměřuje se na země Evropské asociace volného obchodu (EFTA), Severní Amerika, Japonsko, Indie, Austrálie a Novozélandské oblasti.
  - Tato funkce využívá podporu regionální autorizace v SDK pro Partnerské centrum.

- Zákazníci si mohou vybrat nabídku z katalogu a koupit ji.
  - Mohou přidat jméno zákazníka, adresu a informace související s doménou.

- Zákazníci budou přesměrováni na pokladnu PayPal nebo payu (pro Indii). Zákazníci mohou poskytnout platbu pomocí těchto služeb:
  - Jejich stávající PayPal nebo účet PayU (pro Indii)
  - Nástroje pro financování podporované v jejich zemi PayPal nebo PayU (pro Indii). Ty mohou zahrnovat kreditní karty, debetní karty a bankovní účty.

- Pro tohoto zákazníka se vytvoří tenant zákazníka. Po úspěšném vytvoření objednávky tenanta se zákazníkům zobrazí uživatelské jméno, heslo a podrobnosti předplatného.
  - Zákazníci si můžou uživatelské jméno a heslo uložit, aby se mohli zůstat přihlášeni k dalším nákupům.
  - Každé předplatné se koupí za rok a zákazníci se můžou prodloužit na 30 dní před datem ukončení předplatného.

### <a name="view-prior-purchases-scenario"></a>Zobrazit scénář předchozích nákupů

- Zákazník se přihlásí pomocí uživatelského jména a hesla tenanta zákazníka a přejde do oddílu **Moje objednávky** .

- Zákazníci můžou přejít na stránku **Moje objednávky** , kde můžou zobrazit koupená předplatná a v případě potřeby aktualizovat aktualizace.

- Zákazníci můžou přejít na stránku **Moje předplatná** , kde můžou zobrazit všechna předplatná (založená na licencích i na základě využití), včetně těch, které se udržují v partnerském centru.

### <a name="add-licenses-to-existing-subscriptions-scenario"></a>Přidání licencí do existujícího scénáře předplatných

- V části **Moje objednávky** můžou zákazníci přidávat další licence k existujícím předplatným. Zákazníci můžou přidat další licence kdykoli během roku předplatného.

- Každá přidaná licence nemění koncové datum předplatného. Cena předplatného se ale změní na základě data, na které jste licenci přidali, a tam, kde je toto datum v roce. Ceny se účtují poměrně denně, a to jenom za zbývající dny v roce.

### <a name="add-more-subscriptions-scenario"></a>Přidání dalších scénářů předplatného

- Zákazníci si můžou kdykoliv koupit libovolný počet předplatných v části **Přidat předplatná** v části **Moje objednávky**.

- Zákazník může vybrat předplatné, přidat množství a zaplatit za dokončení transakce a hned začít předplatné začít používat. Pokud je zákazník předem schváleným zákazníkem, předplatné je možné okamžitě použít a faktury zákazníkovi se pošle platba.

### <a name="renew-subscription-scenario"></a>Scénář obnovení předplatného

- Zákazník může předplatné obnovit během posledních 30 dnů před datem ukončení předplatného.

- To je dostupné jenom za posledních 30 dní.

- Pokud nedojde k obnovení za posledních 30 dní, předplatné se odebere ze seznamu předplatných pro tohoto tenanta zákazníka.

- Během obnovování nelze aktualizovat množství.

### <a name="payments-scenario"></a>Scénář plateb

- Pokud je zákazník předběžně schválený pro transakce správcem, platební prostředí se nezobrazuje pro výše uvedené scénáře. Místo toho může partner odeslat fakturu pro platbu předem schválenému zákazníkovi.

- Pro všechny nové nákupy můžete přidat další licence, přidat odběry a prodloužit platnost. zákazník může zaplatit partnera pomocí tohoto webu prostřednictvím PayPal nebo PayU (pro indie).

- tento web je integrovaný s PayPal nebo PayU (pro indie) a umožňuje partnerům přijímat platby od svých zákazníků. PayPal nebo PayU (pro indie) dal tuto částku v účtu partnera. správa bankovních účtů PayPal nebo PayU (pro indie) je mimo tento web a je spravovaná na PayPal. com nebo PayUmoney.com.

- tato konfigurace je závislá na partnerech konfigurujících konfiguraci plateb PayPal orPayU (pro indie) na PayPal. com nebo PayUmoney.com. Společnost Microsoft tyto informace neuloží ani skutečné platební transakce vyplývající z použití této možnosti.

### <a name="prorated-pricing-scenario"></a>Scénář poměrné ceny

- Tento web podporuje poměrné ceny v případech, kdy zákazníci přidávají více licencí do stávajícího předplatného.

- Platnost každého předplatného vyprší po jednom roce a po zakoupení předplatného se nedá změnit.

- Koncové datum předplatného se nemění přidáním dalších licencí. Zákazníkům se bude účtovat zbývající počet dní až do koncového data. Například pokud je 1. den v rámci předplatného je $365 a do dvou dnů přidáte další licenci, bude cena za novou licenci $364. Pokud později přidáte licenci po dobu 10 dnů, bude cena $354.
