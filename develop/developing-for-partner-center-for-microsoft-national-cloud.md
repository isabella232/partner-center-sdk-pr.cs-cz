---
title: Vývoj pro partnerského centra pro národní cloudy Microsoftu
description: Rozdíly v SDK partnerského centra pro vývoj v partnerském centru pro národní cloudy Microsoftu
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d38a35fb88b4835716e429aeed731a0d55d9a669
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906465"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Vývoj pro partnerského centra pro národní cloudy Microsoftu

**Platí pro**: partnerské Centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Partnerské centrum má jednu sadu dokumentace k sadě SDK. Některé funkce ale nemusí být k dispozici ve verzích partnerského centra pro národní cloudy Microsoftu.

Vývojáři musí zvážit změny v sadě SDK pro následující verze partnerského centra:

- [Partnerské centrum provozované společností 21Vianet](#partner-center-operated-by-21vianet)
- [Partnerské centrum pro Microsoft Cloud pro Německo](#partner-center-for-microsoft-cloud-germany)
- [Partnerské centrum pro Microsoft Cloud for US Government](#partner-center-for-microsoft-cloud-for-us-government)

Každý článek o sadě SDK partnerského centra obsahuje příslušné verze partnerského centra. Každý článek spravovaných referencí obsahuje také informace o příslušných verzích partnerského centra v části **požadavky** .

## <a name="partner-center-operated-by-21vianet"></a>Partnerské centrum provozované společností 21Vianet

Mezi partnery partnerského *centra* a *partnerským centrem provozovaným společností 21Vianet* jsou rozdíly:

- Nemůžete programově resetovat heslo pro uživatele zákazníka nebo úplného partnerského uživatele.

- Odběry Azure nejsou k dispozici.

- Licence pro uživatele zákazníka nemůžete spravovat. místo toho musí vaši zákazníci spravovat své licence pomocí centra pro správu Office 365.

- Všechny žádosti o podporu se spravují prostřednictvím partnerského centra provozovaného společností 21Vianet. Žádosti o služby a aktualizace služby se nevztahují.

## <a name="partner-center-for-microsoft-cloud-germany"></a>Partnerské centrum pro Microsoft Cloud pro Německo

> [!IMPORTANT]
> Naše cloudová strategie pro Německo se na základě vývoje potřeb zákazníků zaměřuje na doručování nových oblastí cloudu v Německu, které jsou konzistentní s naší cloudovou nabídkou. S tímto zaostřením už nebudeme přijímat nové zákazníky ani nasazovat žádné nové služby z aktuálně dostupné Microsoft Cloud Německo. Stávající zákazníci můžou dál využívat aktuálně dostupné současné cloudové služby, které budeme udržovat s potřebnými aktualizacemi zabezpečení.
>
> Nové zákazníky mají možnost použít aktuálně dostupné evropské oblasti nebo nové oblasti v Německu, jakmile budou k dispozici. Další informace najdete v tématu [Microsoft pro doručování cloudových služeb z nových datových center v Německu](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/).

Mezi partnery *partnerského centra* a *partnerským centrem pro Microsoft Cloud Německo* jsou rozdíly:

- Partneři nemůžou vytvořit uživatele pro organizaci svého zákazníka nebo role přiřadit.
  - Partneři mohou číst pole, ale nemohou je zapisovat ani aktualizovat.
  - partneři musí ručně vytvořit nebo aktualizovat uživatele zákazníků v centru pro správu Office 365 nebo prostřednictvím Azure Portal. viz [dokumentace Azure Active Directory](/azure/active-directory/).

- Licence pro uživatele zákazníka nemůžete spravovat pomocí partnerského centra pro Microsoft Cloud německý portál nebo rozhraní API. místo toho je nutné ke správě licencí použít centrum pro správu Office 365 nebo službu Azure Active Group license management (již brzy).
  - (volitelné) můžete použít Graph API Azure AD. Viz [přiřazení licencí uživateli](/graph/api/user-assignlicense). u partnerského centra pro Microsoft Cloud německo nezapomeňte použít koncový bod Graph `https://graph.cloudapi.de` namísto `https://graph.windows.net` .

- Nemůžete programově resetovat heslo pro uživatele zákazníka nebo úplného partnerského uživatele. použijte centrum pro správu Office 365 nebo Azure Portal. Viz [resetování hesla pro uživatele v Azure Active Directory](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal). V kroku 1 se musíte přihlásit k Azure Portal Microsoft Cloud Německu.

- Vývojáři musí své ID aplikace zaregistrovat ručně, aby mohli integrovat funkce partnerského centra rozhraní API/sady SDK do aplikace pro partnerského centra pro Microsoft Cloud Německo. Další informace najdete v tématu [registrace podrobností aplikace pro partnerského centra pro národní Cloud společnosti Microsoft](create-apps-for-partner-center-for-microsoft-national-clouds.md).

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>Partnerské centrum pro Microsoft Cloud for US Government

mezi partnery *partnerského centra* a *partnerským centrem pro Microsoft Cloud for US Government* jsou tyto rozdíly:

- Office 365 předplatná nejsou aktuálně k dispozici pro partnerské centrum pro Microsoft Cloud for US Government.

- stávající partneři podporující Microsoft Cloud for US Government musí vytvořit nové účty v partnerském centru pro Microsoft Cloud for US Government.

- Microsoft Cloud for US Government zákazníci musí s jedním partnerem provádět transakce.
  - ve scénářích s Microsoft Cloud for US Government se nevztahují na vícekanálový a více partnerských vztahů a žádostí s existujícím zákazníkem. toto omezení je způsobeno tím, že Office 365 není aktuálně k dispozici.

- Partneři nemůžou vytvořit uživatele pro organizaci svého zákazníka nebo role přiřadit.
  - Partneři mohou číst pole, ale nemohou je zapisovat ani aktualizovat. Partneři musí ručně vytvořit nebo aktualizovat uživatele zákazníků v Azure Portal. viz [dokumentace Azure Active Directory](/azure/active-directory/).

- Nemůžete programově resetovat heslo pro uživatele zákazníka nebo úplného partnerského uživatele. Použijete Azure Portal Viz [resetování hesla pro uživatele v Azure Active Directory](/azure/active-directory/active-directory-users-reset-password-azure-portal). V kroku 1 se musíte ke službě Azure Portal přihlašovat Microsoft Cloud for US Government.

- koncové body REST pro partnerského centra pro Microsoft Cloud for US Government jsou stejné jako u partnerského centra: `https://api.partnercenter.microsoft.com` .

- Vývojáři musí své ID aplikace zaregistrovat ručně, aby mohli integrovat funkce partnerského centra rozhraní API/sady SDK do aplikace pro partnerského centra pro Microsoft Cloud for US Government. Další informace najdete v tématu [registrace podrobností aplikace pro partnerského centra pro národní Cloud společnosti Microsoft](create-apps-for-partner-center-for-microsoft-national-clouds.md).
