---
title: Testování a ladění s integračním sandboxem
description: Zjistěte, jak pomocí účtu sandboxu Partnerské centrum integrace (a souvisejících tokenů) otestovat a ladit kód, aby se vám nechtěně nenabídly nové poplatky.
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7a9d7755cd9f493f44f9a7bbf613e0f80cf7b4ac
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530102"
---
# <a name="test-and-debug-with-your-partner-center-integration-sandbox-to-avoid-paying-unexpected-charges"></a>Testování a ladění s Partnerské centrum integration sandboxu, abyste se vyhnuli neočekávaným poplatkům

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

K otestování kódu byste měli použít svůj účet sandboxu pro integraci v Partnerské centrum (a odpovídající tokeny), aby se vám nechtěně neplatily nové poplatky, za které zodpovídá vaše společnost. Další informace o tomto prostředí TiP (test-in-production) najdete v tématu Nastavení přístupu k rozhraní [API v Partnerské centrum](set-up-api-access-in-partner-center.md).

## <a name="integration-sandbox-constraints"></a>Omezení sandboxu integrace

Pokud spustíte automatizované ověřovací testy sestavení, provedete testování v produkčním prostředí nebo provedete ruční testování v sandboxu integrace, můžete dosáhnout maximálních limitů pro sandbox integrace. Tato omezení jsou 75 zákazníků, 5 předplatných na zákazníka a 25 licencí na předplatné.

Limit 25 licencí znamená, že v sandboxu nemůžete získat nabídku, která má minimální požadavek na licenci, který překračuje 25 licencí. Toto omezení zahrnuje zkušební verze.

V prostředích sandboxu jsou k dispozici různé soubory faktur a odsouhlasení, ale ne všechny jsou k dispozici na starších nebo moderních platformách. Další informace najdete v následující tabulce.

| **Soubory**                    | **K dispozici ve starší verzi** | **K dispozici v moderním** |
| ---------------------------- | ------------------------ | ------------------------ |
| Faktura v PDF                  | No                       | Yes                      |
| Soubor s vyrovnáním faktur | No                       | Yes                      |
| Soubor s odhadem faktury       | No                       | Yes                      |
| Soubor s denním fakturovaným využitím     | No                       | Yes                      |
| Soubor s denním nefakfaktem využití   | No                       | Yes                      |


### <a name="azure-plan"></a>Plán Azure

Ve výchozím nastavení nemůžou partneři zřizovat plány Azure s využitím svých účtů sandboxu. Partneři, kteří to potřebují udělat s využitím svého účtu sandboxu, musí požádat o přístup. Pokud chcete požádat o přístup, obraťte se na účet Microsoft nebo obchodní kontakt. Partneři, kteří dříve požádali o přístup ke zřízení předplatných Microsoft Azure (MS-AZR-0145P) ve svých účtech sandboxu, nemusí znovu zažádat o přístup. Bude jim udělen přístup k automatickému zřizování plánů Azure.

Pro partnery, jejichž účty sandboxu byly schváleny ke zřizování plánů Azure, platí následující omezení:

- Každý partnerský účet sandboxu může mít až 10 plánů Azure napříč všemi tenanty zákazníků (bez ohledu na to, jak se plány distribuují mezi zákazníky).

- Partner s přímým vyúčtováním může vytvořit až jeden plán Azure na tenanta zákazníka.

- Nepřímý poskytovatel může vytvořit až tři plány Azure na tenanta zákazníka (pro různé nepřímé prodejce zadané jako Partner-of-Record).

- Každý plán Azure může mít až tři předplatná Azure.

- Každé předplatné Azure CSP v rámci vašeho účtu sandboxu je omezené na čtyři jádra virtuálních počítačů na jedno datové centrum. Proto nemůžete zřídit skladové hodnoty virtuálních počítače, které vyžadují více než čtyři jádra virtuálního počítače. Vyloučené jsou také některé specializované skladové hodnoty virtuálních počítače, jako jsou jádra GPU.

- Každý partnerský účet sandboxu má limit útraty 2 000 USD na fakturační cyklus ve všech plánech Azure. Jakmile partner dosáhne limitu výdaje, všechny plány Azure budou dočasně zakázané až do dalšího fakturačního období.

### <a name="cloud-solution-provider-csp-azure-subscription-offers"></a>Cloud Solution Provider předplatného Azure (CSP)

Nabídky předplatného Azure CSP už nejsou pro účty sandboxu ve výchozím nastavení dostupné. Patří mezi ně MS-AZR-0146P, MS-AZR-DE-0146P a MS-AZR-USGOV-0146P pro předplatná Azure CSP ve veřejném cloudu Microsoftu, německém cloudu a cloudu pro státní správu. Partneři, kteří potřebují přístup k těmto nabídekm pomocí svého účtu sandboxu, musí požádat o přístup. Pokud chcete požádat o přístup, proberte to se svým účet Microsoft nebo obchodním kontaktem.

Pro partnery, jejichž účty sandboxu byly schváleny pro nabídky předplatného Azure CSP, platí následující omezení:

- Můžete mít maximálně 375 aktivních předplatných (75 zákazníků × 5 předplatných na zákazníka). Pouze 10 z těchto předplatných však může být předplatná Azure CSP.

- Když předplatné Azure CSP dosáhne 200 USD využití Azure, jeho prostředky se dočasně deaktivují až do dalšího fakturačního období. Stále se považuje za aktivní předplatné a počítá se do limitu 10 aktivních předplatných Azure.

- Každé předplatné Azure CSP v rámci vašeho účtu sandboxu je omezené na čtyři jádra virtuálních počítačů na jedno datové centrum. Proto nemůžete zřídit skladové hodnoty virtuálních počítače, které vyžadují více než čtyři jádra virtuálního počítače. Vyloučené jsou také některé specializované skladové hodnoty virtuálních počítače, jako jsou jádra GPU.

> [!Important]
> Všechna stávající předplatná Azure CSP zřízená s účty sandboxu před 1. srpnem 2018 už nejsou podporovaná a Microsoft ji od 16. října 2018 z zřízení zrušte. Po rušení zřízení předplatných už není možné je znovu povolit a přidružená data už nejsou dostupná. Partneři, kteří mají v těchto předplatných uložená cenná data, musí data před 16. říjnem 2018 zálohovat.

### <a name="azure-reserved-vm-instance"></a>Rezervovaná instance virtuálního počítače Azure

Pokud kupujete [rezervovanou instanci virtuálního](purchase-azure-reservations.md) počítače Azure s vaším účtem sandboxu, jste omezeni na dvě instance virtuálních počítače na zákazníka. Také jste omezeni na výběr pouze z následujících SKU produktů rezervovaných instancí virtuálních počítače Azure:

| Název produktu  | Datum platnosti  | Název SKU                                               | Oblast [ArmRegionName] | Klíč instance [ArmSkuName] | Doba trvání | ID měřiče Consumption       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| Řada B       | 12/1/2017 0:00  | Rezervovaná instance virtuálního počítače, Standard_B1s, Korea – jih, 1 rok    | KoreaSouth             | `Standard_B1s` | `1Year`    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| Řada B       | 12/1/2017 0:00  | Rezervovaná instance virtuálního počítače, Standard_B1s, USA – východ, 1 rok     | eastus                 | `Standard_B1s` | `1Year`    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| Řada B       | 12/1/2017 0:00  | Rezervovaná instance virtuálního počítače, Standard_B1s, USA – západ 2, 1 rok   | westus2                | `Standard_B1s` | `1Year`    | 222e39f5-e99f-4fa3-a323-f46402977888 |
| Řada B       | 12/1/2017 0:00  | Rezervovaná instance virtuálního počítače, Standard_B1s, USA (střed) – sever, 1 rok    | northcentralus | `Standard_B1s` | `1Year`    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| Řada B       | 12/1/2017 0:00  | Rezervovaná instance virtuálního počítače, Standard_B1s, CA – východ, 1 rok     | Kanada – východ             | `Standard_B1s` | `1Year`    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |

### <a name="subscriptions-for-commercial-marketplace-products"></a>Předplatná pro produkty komerčního marketplace

Po vytvoření předplatného produktů [SaaS](create-subscription-azure-marketplace-products.md)na komerčním marketplace musíte v produkčním prostředí načíst individuální aktivační odkaz ze služby Partnerské centrum a navštívit web vydavatele a dokončit proces nastavení. Fakturace předplatného začne až po dokončení nastavení.

V prostředí sandboxu CSP neexistuje žádná integrace s isvédy. Pokud se pokusíte načíst aktivační odkaz z Partnerské centrum, vrátí se fiktivní odkaz. Tento fiktivní odkaz nelze použít k dokončení procesu instalace na webu vydavatele. Pokud chcete účet sandboxu pro integraci použít k otestování fakturace předplatných na komerčním marketplace produktů SaaS, podívejte se místo toho na aktivaci [předplatného sandboxu pro produkty komerčního marketplace.](activate-sandbox-subscription-azure-marketplace-products.md) Fakturace předplatného začne po úspěšné aktivaci.

Pokud chcete na konci testovacího běhu vyčistit prostor pro další kolo testování, podívejte se na následující články:

- [Odstranění zákaznického účet ze sandboxu pro integraci](delete-a-customer-account-from-the-integration-sandbox.md)

- [Snížení množství předplatného](change-the-quantity-of-a-subscription.md)

- [Pozastavit předplatné,](suspend-a-subscription.md) abyste ho mohli odebrat.

## <a name="best-practices-for-rest-development"></a>Osvědčené postupy pro vývoj REST

- Použijte nástroj pro trasování sítě, abyste viděli svůj požadavek, odpověď a případné chyby ve stavovém kódu HTTP v odpovědi. Další informace o zpracování chyb najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

- Pro každé volání metody použijte nové ID korelace Partnerské centrum REST API. Tento postup zajišťuje lepší protokolování a pomůže vám při ladění. Další informace najdete v Partnerské centrum [REST.](headers.md)

## <a name="troubleshooting-tips-for-common-rest-problems"></a>Tipy k řešení běžných potíží s rozhraním REST

- Zkontrolujte všechny vlastnosti hlavičky, včetně adresy URL a verze rozhraní API.

- V případě potřeby se ujistěte, že jsou zahrnuté vlastnosti a že jsou správně naformátované.

- Nesprávné formátování pole je běžnou chybou.

- **ETagy** jsou dočasné a proto by se neměly ukládat. Pokud volání funkce vyžaduje **ETagy,** použijte nejnovější hodnotu **ETags** tím, že prostředek znovu získáte. **Hodnoty Značek ETag** by měly být zahrnuty do dvojitých uvozovek, jako je řetězec:

   ```rest
   If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
   ```
