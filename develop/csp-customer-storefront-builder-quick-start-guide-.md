---
title: Úvodní příručka pro tvůrce výkladních skříní pro zákazníky CSP
description: Vytvořte online tržiště pro prodej nabídek poskytovatele Cloud Solution Provider (CSP) pomocí Tvůrce prezentace Customer CSP.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 83ae0c789f95485ec3eb272434e57421a8f93fb6
ms.sourcegitcommit: 970031473b2e8cd3d08c6c097949c057a51df3ef
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505318"
---
# <a name="csp-customer-storefront-builder-quick-start-guide"></a>Úvodní příručka pro tvůrce výkladních skříní pro zákazníky CSP

**Platí pro:**

- Partnerské centrum

Vytvořte online tržiště pro prodej nabídek poskytovatele Cloud Solution Provider (CSP) pomocí Tvůrce prezentace Customer CSP.

## <a name="introduction-to-the-csp-customer-storefront-builder"></a>Úvod do Tvůrce prezentace Customer CSP

Customer prezentace Builder pro poskytovatele CSP pomáhá partnerům snadno vytvořit online tržiště, které svým zákazníkům prodávají nabídky CSP. Většina partnerů a organizací malých prodejců se chce soustředit na prodej místo vývoje online webu Marketplace. Ukázková aplikace partnerského centra SDK vyžaduje pro vytvoření a nasazení webu dovednosti s vývojem softwaru. Pomocí Tvůrce prezentace Customer CSP můžete snadno a rychle vytvořit vlastní web. Můžete si také stáhnout web jako vzorový kód nebo ho nasadit přímo do předplatného Azure s připraveným na web v jazyce Transact.

Tento web je plně vlastněn, podporován a udržován partnery a společnost Microsoft neshromažďuje žádná data ani telemetrie z webu. Tvůrce prezentace Customer CSP vytvoří web pro partnera, který plně dodržuje [standard zabezpečení dat v odvětví platebních karet](https://www.pcisecuritystandards.org/) (PCI DSS).

Kód tvůrce prezentace pro poskytovatele CSP podléhá licenci dostupné v [smlouvě EULA partnerského centra SDK](/legal/partner-center/eula-partner-center-sdk).

>[!NOTE]
>Zodpovídáte za správu webu prezentace, údržbu a všechny problémy, které by mohly nastat při vytváření webů. Přečtěte si podmínky v tématu [smlouva EULA partnerského centra SDK](/legal/partner-center/eula-partner-center-sdk)a porozumět jim.

Další informace najdete také v následujících článcích: [poskytovatel CSP web prezentace](csp-customer-web-storefront.md) a [testovací aplikace konzoly](console-test-app.md).

## <a name="considerations"></a>Požadavky

Customer prezentace Builder pro poskytovatele CSP je určený jako rychlý způsob, jak vytvořit web. Při plánování mějte na paměti následující skutečnosti:

- Po nasazení neudržuje Microsoft a partnerská centra kopii webu partnera ani žádné informace přidané do Tvůrce prezentace Customer CSP.

- Partnerské centrum může nasadit web prezentace Customer CSP jenom na předplatná Azure partnera.

- Tento web je po nasazení plně vlastněn a spravován partnerem. Společnost Microsoft nemá k tomuto webu přístup ani žádná data související s webem. Partner zodpovídá za údržbu a správu webu. Microsoft neposkytuje žádný živý web ani jinou podporu, která se vztahuje k tvůrci prezentace (Customer Provider Provider) nebo libovolnému webu vytvořenému pomocí Tvůrce prezentace Customer pro poskytovatele kryptografických služeb.

- Partnerské centrum nemůže získat přímý přístup k tomuto webu nebo ho upgradovat pomocí nových nebo změněných funkcí sady SDK nebo rozhraní API. Všechny nové funkce nebo vylepšení musí být vlastněné, vyvinuté a spravované partnery, včetně přidání nových funkcí SDK pro partnerských Center nebo funkcí rozhraní API.

- Tento prezentace tvůrce pro poskytovatele CSP v současné době poskytuje možnost konfigurovat platbu na účet služby PayPal pro/PayU Money (pro Indie). Pokud partneři potřebují změnit platební procesor, bude muset změnit kód tak, aby podporoval preferovaný způsob platby.

- Jakékoli informace související s platbami, které jsou přidané v Tvůrci prezentace Customer CSP, se v partnerském centru neukládají ani neuchovávají.

- Konfigurace plateb PayPal bude fungovat v jakýchkoli geografických oblastech, kde je PayPal k dispozici. Dostupnost a podpora služby PayPal se řídí výhradně pomocí služby PayPal a může je kdykoli ukončit služba PayPal.

- Konfigurace platby PayU bude v současnosti fungovat jenom v Indii. Dostupnost a podpora PayU se řídí výhradně PayU a může být kdykoli ukončená PayU.

- Přečtěte si podmínky v tématu [smlouva EULA partnerského centra SDK](/legal/partner-center/eula-partner-center-sdk)a porozumět jim.

## <a name="using-the-csp-customer-storefront-builder"></a>Pomocí Tvůrce prezentace Customer CSP

Správci CSP v partnerském centru můžou nasazovat prezentace zákazníka poskytovatele CSP přímo z partnerského centra. S minimálním úsilím se dá na tenanta partnera nasadit nový web. Po nasazení můžou partneři používat web ke konfiguraci brandingu, nabídek a informací souvisejících s platbami a pak sdílet adresu URL webu se zákazníky.

Proces vytvoření webu prezentace je následující:

1. [Nasazení webu](#deploy)

2. [Konfigurace prezentace](#configure)

3. [Transact na prezentace](#transact)

### <a name="deploy"></a>Nasadit

Možnosti nasazení:

- Stažení [ukázkového kódu prezentace partnerského centra](https://github.com/Microsoft/Partner-Center-Storefront) z GitHubu
- Integrace s Azure za účelem nasazení nakonfigurovaného webu
- Nasaďte v existujícím předplatném nebo využijte vlastní předplatné.

### <a name="configure"></a>Konfigurace

K přizpůsobení prezentace se nevyžadují žádné znalosti vývoje.

Přihlaste se pomocí přihlašovacích údajů správce partnerského centra ke konfiguraci:

- **Branding**: název společnosti, logo, kontakty a další.

- **Nabídky**: Zobrazit všechny nabídky CSP. Můžete vybrat, které nabídky můžou vaši zákazníci zobrazit a koupit. Můžete také přizpůsobit informace o nabídce a přidat svou cenu.

- **Konfigurace platby PayPal**: přidejte informace o platebním účtu PayPal. Pokud nemáte účet PayPal, můžete navštívit [https://www.paypal.com](https://www.paypal.com) a vytvořit nový účet. Tento účet se bude používat pro služby PayPal k kreditu plateb provedených zákazníky. *Společnost Microsoft není zodpovědná za vztah mezi partnery a PayPal. Používání služby PayPal může vyžadovat, aby si zákazníci partnera nebo partnera souhlasili s dalšími podmínkami.*

- (*Pro Indie*) **Konfigurace platby PayU**: přidejte informace o platebním účtu PayU pro peníze. Pokud nemáte peněžní účet PayU, můžete navštívit [https://www.payumoney.com/](https://www.payumoney.com/) a vytvořit nový účet. Tento účet se bude používat pro PayU k kreditu plateb provedených zákazníky. *Společnost Microsoft není zodpovědná za vztah mezi partnery a PayU. Použití PayU může vyžadovat, aby si zákazníci partnera nebo partnera souhlasili s dalšími podmínkami.*

### <a name="transact"></a>Transakce

- Po nasazení si zákazníci můžou hned koupit a provádět transakce.

- Zákazníci si můžou koupit přímo z portálu pro partnery, který je integrovaný do sady partner Center SDK.

#### <a name="customer-countries"></a>Země zákazníka

Zákazníci můžou patřit do těchto zemí:

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

- K vývoji použijte Microsoft Visual Studio 2015 (nebo novější).

- Sestavení pro další změny a vylepšení (včetně autorizací, certifikace, změn manifestu a dalších položek).

### <a name="configuration-scenario"></a>Scénář konfigurace

- Nově vytvořený web je propojený s partnerským klientem a má přístup ke všem účtům správců tohoto partnerského tenanta.

  - Partneři se můžou k tomuto novému webu přihlásit pomocí přihlašovacích údajů správce partnerského centra.

- Aplikace prezentace aktuálně podporuje francouzštinu, španělštinu, holandštinu, němčinu, japonštinu a angličtinu. (Angličtina slouží jako náhradní jazyk.)

  - Prezentace konfiguruje národní prostředí pomocí výchozího národního prostředí partnera z profilu partnera v partnerském centru. Toto národní prostředí se používá ke konfiguraci měn, formátů data a lokalizovaných nabídek v úložišti.

- Partneři můžou konfigurovat branding, nabídky a PayPal nebo PayU (pro Indie) platební informace.

- Partneři můžou aktualizovat název společnosti, logo společnosti, obrázek záhlaví, kontakty pro prodej a podporu a další.

- Partneři můžou zobrazit všechny dostupné nabídky CSP na základě jejich území.

  - Partneři si můžou vybrat, které nabídky chtějí zobrazovat všem svým zákazníkům.

  - Partner CSP může vybrat jednu nebo více nabídek a aktualizovat název, množství, popis funkce a cenu.
  - Cena je roční cena. Zákazníci se každoročně přihlásí.

- Partneři můžou kdykoli nakonfigurovat předem schválené transakce pro všechny aktuální a budoucí zákazníky nebo (b) konkrétní zákazníky.

  - Předběžně schválené zákazníky nemusejí platit na portálu, když přidávají nové předplatné, nakupují další licence k existujícím předplatným nebo obnoví předplatné.

  - Předběžně schválené zákazníky nebudou přesměrováni na PayPal nebo PayU (pro Indie) pro platbu během těchto transakcí.

  - Předběžně schválené transakce zákazníka umožňují partnerovi provádět online fakturaci a fakturování předem schváleným zákazníkům.

- Partner CSP může zadat své informace o svém účtu PayPal, jako je třeba ID klienta PayPal a tajný kód. Partner CSP taky může vybrat, jestli se chce testovat pomocí izolovaného prostoru nebo živého účtu.

  - Partneři můžou tyto informace najít [https://developer.paypal.com/](https://developer.paypal.com/) v nabídce **moje aplikace & přihlašovací údaje**. Tyto informace můžete získat také z aktuální aplikace nebo vytvořením nové aplikace v PayPal.
  - Vytvořte nový účet PayPal, pokud ho ještě nemáte. Tento účet se bude používat pro služby PayPal k kreditu plateb provedených zákazníky.

    - Pokud chcete otevřít obchodní účet PayPal, přečtěte si téma [https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register](https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register) .

    - Pokud chcete vytvořit účet v izolovaném prostoru služby PayPal, podívejte se na [https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/](https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/) .

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

- Zákazníci budou přesměrováni na možnosti rezervace služby PayPal nebo PayU (pro Indie). Zákazníci můžou platbu poskytnout pomocí těchto akcí:
  - Svůj stávající účet PayPal nebo PayU (pro Indie)
  - Nástroje pro financování, které v zemi podporuje PayPal nebo PayU (pro Indie) Ty můžou zahrnovat kreditní karty, debetní karty a bankovní účty, jak je to možné.

- Pro tohoto zákazníka se vytvoří tenant zákazníka. Po úspěšném vytvoření objednávky tenanta se zákazníkům zobrazí podrobnosti o uživatelském účtu, heslu a předplatném.
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

- Pro všechny nové nákupy můžete přidat další licence, přidat odběry a prodloužit platnost. Zákazník může prostřednictvím tohoto webu zaplatit partnera prostřednictvím služby PayPal nebo PayU (pro Indie).

- Tento web je integrovaný v rámci služby PayPal nebo PayU (pro Indie) a umožňuje partnerům přijímat platby od svých zákazníků. V rámci služby PayPal nebo PayU (pro Indie) se tato částka v účtu partnera vyčerpá. Správa bankovních účtů v PayPal nebo PayU (pro Indie) je mimo tento web a je spravovaná na PayPal.com nebo PayUmoney.com v uvedeném pořadí.

- To závisí na partnerech, které konfigurují svou konfiguraci platby orPayU PayPal (pro Indie) na PayPal.com nebo PayUmoney.com. Společnost Microsoft tyto informace neuloží ani skutečné platební transakce vyplývající z použití této možnosti.

### <a name="prorated-pricing-scenario"></a>Scénář poměrné ceny

- Tento web podporuje poměrné ceny v případech, kdy zákazníci přidávají více licencí do stávajícího předplatného.

- Platnost každého předplatného vyprší po jednom roce a po zakoupení předplatného se nedá změnit.

- Koncové datum předplatného se nemění přidáním dalších licencí. Zákazníkům se bude účtovat zbývající počet dní až do koncového data. Například pokud je 1. den v rámci předplatného je $365 a do dvou dnů přidáte další licenci, bude cena za novou licenci $364. Pokud později přidáte licenci po dobu 10 dnů, bude cena $354.
