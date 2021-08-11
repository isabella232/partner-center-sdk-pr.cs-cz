---
title: Vývoj pro Partnerské centrum pro národní cloudy Microsoftu
description: SDK pro Partnerské centrum rozdíly při vývoji pro Partnerské centrum pro národní cloudy Microsoftu.
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8b9b3c3b9a1a1173cf8f3e79f60e629e3d34ea13ecce2e7a2c74924bde2b7d1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994859"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Vývoj pro Partnerské centrum pro národní cloudy Microsoftu

**Platí pro:** Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Partnerské centrum obsahuje jednu sadu dokumentace k sadě SDK. Některé funkce ale nemusí být dostupné ve verzích nástroje Partnerské centrum pro národní cloudy Microsoftu.

Vývojáři musí zvážit změny sady SDK pro následující verze Partnerské centrum:

- [Partnerské centrum provozované společností 21Vianet](#partner-center-operated-by-21vianet)
- [Partnerské centrum pro Microsoft Cloud pro Německo](#partner-center-for-microsoft-cloud-germany)
- [Partnerské centrum pro Microsoft Cloud for US Government](#partner-center-for-microsoft-cloud-for-us-government)

V SDK pro Partnerské centrum článku jsou uvedené příslušné Partnerské centrum verze. Každý článek spravovaná referenční příručka uvádí také Partnerské centrum verzích v **části** Požadavky.

## <a name="partner-center-operated-by-21vianet"></a>Partnerské centrum provozované společností 21Vianet

Rozdíly mezi partnery mezi *Partnerské centrum* a Partnerské centrum provozovaných společností *21Vianet:*

- Nemůžete resetovat heslo pro uživatele zákazníka nebo úplného partnerského uživatele prostřednictvím kódu programu.

- Předplatná Azure nejsou k dispozici.

- Nemůžete spravovat licence pro uživatele zákazníka. Místo toho musí vaši zákazníci ke správě svých licencí Office 365 centrum pro správu.

- Všechny žádosti o podporu spravuje Partnerské centrum 21Vianet. Na žádosti o služby a aktualizace služeb se nevztahují.

## <a name="partner-center-for-microsoft-cloud-germany"></a>Partnerské centrum pro Microsoft Cloud pro Německo

> [!IMPORTANT]
> Na základě vývoje potřeb zákazníků se naše cloudová strategie pro Německo zaměří na doručování nových cloudových oblastí v Německu, které jsou konzistentní s naší globální cloudovou nabídkou. V souvislosti s tímto cílem už nebudeme přijímat nové zákazníky ani nasazovat nové služby z aktuálně dostupného cloudu Microsoft Cloud Germany. Stávající zákazníci mohou dál používat aktuální cloudové služby, které jsou dnes dostupné a které budeme udržovat pomocí potřebných aktualizací zabezpečení.
>
> Do budoucna mají noví zákazníci možnost používat aktuálně dostupné evropské oblasti nebo nové oblasti v Německu, jakmile budou k dispozici. Další informace najdete v článku o tom, jak [bude Microsoft poskytovat cloudových služeb z nových datacenter v Německu](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/).

Rozdíly mezi partnery mezi *Partnerské centrum* *a Partnerské centrum pro Microsoft Cloud Germany* jsou následující:

- Partneři nemůže vytvářet uživatele pro organizaci zákazníka ani přiřazovat role.
  - Partneři mohou číst pole, ale ne zapisovat ani aktualizovat.
  - Partneři musí ručně vytvořit nebo aktualizovat uživatele svých zákazníků v centru Office 365 nebo prostřednictvím Azure Portal. Viz [Azure Active Directory dokumentace k produktu](/azure/active-directory/).

- Licence pro uživatele zákazníka nemůžete spravovat pomocí rozhraní API nebo Partnerské centrum Microsoft Cloud Germany. Místo toho musíte ke správě svých licencí Office 365 centrum pro správu nebo správu licencí azure Active Directly Group (už brzy).
  - (Volitelné) Můžete použít rozhraní API služby Azure AD Graph. Viz [Přiřazení licencí uživateli.](/graph/api/user-assignlicense) Pokud Partnerské centrum Microsoft Cloud Germany, nezapomeňte místo použít koncový bod Graph pro Microsoft Cloud `https://graph.cloudapi.de` `https://graph.windows.net` Germany.

- Nemůžete resetovat heslo pro uživatele zákazníka nebo úplného partnerského uživatele prostřednictvím kódu programu. Použijte centrum Office 365 pro správu nebo Azure Portal. Viz [Resetování hesla pro uživatele v Azure Active Directory](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal). V kroku 1 se musíte přihlásit k webu Azure Portal Microsoft Cloud Germany.

- Vývojáři musí své ID aplikace zaregistrovat ručně, aby Partnerské centrum do své aplikace integrují funkce rozhraní API nebo sady SDK Partnerské centrum pro Microsoft Cloud Germany. Další informace najdete v tématu [Registrace podrobností o aplikaci pro Partnerské centrum pro národní cloud Microsoftu.](create-apps-for-partner-center-for-microsoft-national-clouds.md)

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>Partnerské centrum pro Microsoft Cloud for US Government

Rozdíly mezi partnery mezi *Partnerské centrum* *a Partnerské centrum pro Microsoft Cloud for US Government* jsou následující:

- Office 365 předplatná nejsou aktuálně dostupná pro Partnerské centrum pro Microsoft Cloud for US Government.

- Stávající partneři podporující Microsoft Cloud for US Government musí vytvořit nové účty v Partnerské centrum pro Microsoft Cloud for US Government.

- Microsoft Cloud for US Government zákazníci musí provádět transakce s jedním partnerem.
  - Vztah multichannel a multipartner a požadavek s existujícím zákazníkem v Microsoft Cloud for US Government scénářích neplatí. Toto omezení je Office 365 není aktuálně k dispozici.

- Partneři nemůže vytvářet uživatele pro organizaci zákazníka ani přiřazovat role.
  - Partneři mohou číst pole, ale ne zapisovat ani aktualizovat. Partneři musí ručně vytvořit nebo aktualizovat uživatele svých zákazníků v Azure Portal. Viz [Azure Active Directory dokumentace k produktu](/azure/active-directory/).

- Nemůžete resetovat heslo pro uživatele zákazníka nebo úplného partnerského uživatele prostřednictvím kódu programu. Použijete Azure Portal Viz [Resetování hesla pro uživatele v Azure Active Directory](/azure/active-directory/active-directory-users-reset-password-azure-portal). V kroku 1 se musíte přihlásit k Azure Portal pro Microsoft Cloud for US Government.

- Koncové body REST pro Partnerské centrum pro Microsoft Cloud for US Government jsou stejné jako pro Partnerské centrum: `https://api.partnercenter.microsoft.com` .

- Vývojáři musí své ID aplikace zaregistrovat ručně, aby Partnerské centrum do své aplikace integrují funkce rozhraní API nebo sady SDK pro Partnerské centrum pro Microsoft Cloud for US Government. Další informace najdete v tématu [Registrace podrobností o aplikaci pro Partnerské centrum pro národní cloud Microsoftu.](create-apps-for-partner-center-for-microsoft-national-clouds.md)
