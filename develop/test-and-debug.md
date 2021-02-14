---
title: Testování a ladění s izolovaným prostorem integrace
description: Naučte se používat účet izolovaného prostoru (a související tokeny) partnerského centra k testování a ladění kódu, abyste se nechtěně neúčtují nové poplatky.
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3ff4a7ec3ad984b09c60d3d820423c614fb8020d
ms.sourcegitcommit: 9f8ba784171ab4f980ed0c60ef6f2323849c4a98
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2021
ms.locfileid: "100499877"
---
# <a name="test-and-debug-with-your-partner-center-integration-sandbox-to-avoid-paying-unexpected-charges"></a>Testování a ladění pomocí izolovaného prostoru integrace partnerského centra, aby nedošlo k neočekávaným poplatkům

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Pokud chcete otestovat svůj kód, měli byste použít svůj účet integrace izolovaného prostoru (sandbox) v partnerském centru (a odpovídajících tokenech), abyste omylem neúčtovali nové poplatky, za které vaše společnost zodpovídá za placení. Další informace o tomto prostředí s testováním v produkčním prostředí (TiP) najdete v tématu [nastavení přístupu k rozhraní API v partnerském centru](set-up-api-access-in-partner-center.md).

## <a name="integration-sandbox-constraints"></a>Omezení karantény integrace

Pokud spustíte testy automatizovaného ověřování sestavení, provádíte testování v produkčním prostředí nebo provádíte Manuální testování v izolovaném prostoru (sandboxu) integrace, můžete dosáhnout maximálního limitu pro integraci izolovaného prostoru. Tato omezení jsou 75 zákazníci, 5 předplatných na zákazníka a 25 licencí na předplatné.

Limit 25 licencí znamená, že nemůžete získat nabídku v izolovaném prostoru (sandbox), která má minimální licenční požadavek, který překračuje 25 licencí. Toto omezení zahrnuje zkušební verze.

V prostředích izolovaného prostoru (sandboxu) jsou k dispozici různé soubory faktury a odsouhlasení, ale ne všechny jsou k dispozici na starších nebo moderních platformách. Ověřte následující tabulku, abyste se dozvěděli víc.

| **Soubory**                    | **K dispozici ve starší verzi** | **K dispozici v moderních** |
| ---------------------------- | ------------------------ | ------------------------ |
| Faktura v PDF                  | No                       | Yes                      |
| Soubor odsouhlasení faktury | No                       | Yes                      |
| Soubor odhadu faktury       | No                       | Yes                      |
| Denní fakturované soubor využití     | No                       | Yes                      |
| Denní nefakturovaný soubor využití   | No                       | Yes                      |


### <a name="azure-plan"></a>Plán Azure

Ve výchozím nastavení partneři nemůžou zřizovat plány Azure pomocí svých účtů izolovaného prostoru (sandboxu). Pro přístup se musí požádat o partnery, kteří k tomu potřebují, aby měli účet izolovaného prostoru (sandbox). Pokud chcete požádat o přístup, obraťte se na svého správce účet Microsoft nebo obchodní kontakt. Partneři, kteří dřív použili pro přístup ke zřízení předplatných služby Microsoft Azure (MS-AZR-0145P) ve svých účtech izolovaného prostoru (sandbox), nemusejí pro přístup znovu platit. Budou jim udělena oprávnění k automatickému zřizování plánů Azure.

Pro partnery, jejichž účty izolovaného prostoru byly schváleny pro zřizování plánů Azure, platí následující omezení:

- Každý partnerský účet izolovaného prostoru (sandbox) může mít až 10 plánů Azure napříč všemi zákazníky (bez ohledu na to, jak se plány rozdělují mezi zákazníky).

- Přímý účet pro zákazníky může vytvořit až jeden tenant Azure na každého zákazníka.

- Nepřímý poskytovatel může vytvořit až tři plány Azure na každého zákazníka (pro různé nepřímý prodejce, které jste zadali jako partnerský záznam).

- Každý plán Azure může mít až tři předplatné Azure.

- Každé předplatné Azure CSP v rámci vašeho účtu v izolovaném prostoru (sandbox) je omezeno na čtyři jádra virtuálních počítačů na datové centrum. Proto nemůžete zřídit SKU virtuálních počítačů, které vyžadují více než čtyři jádra virtuálních počítačů. Jsou vyloučeny také určité specializované SKU virtuálních počítačů, jako jsou například procesory GPU.

- Každý partnerský účet izolovaného prostoru (sandbox) má limit útraty $2000 (USD) na fakturační cyklus napříč všemi plány Azure. Jakmile partner dosáhne limitu útraty, všechny plány Azure se dočasně zablokují až do dalšího fakturačního cyklu.

### <a name="cloud-solution-provider-csp-azure-subscription-offers"></a>Nabídky předplatného Azure pro poskytovatele Cloud Solution Provider (CSP)

V účtech izolovaného prostoru (sandboxu) už nejsou dostupné nabídky předplatného Azure CSP. Patří mezi ně MS-AZR-0146P, MS-AZR-DE-0146P a MS-AZR-USGOV-0146P pro CSP Azure Subscriptions ve veřejném cloudu Microsoftu, v německém cloudu a v cloudu pro státní správu. Partneři, kteří potřebují přístup k těmto nabídkám se svým účtem izolovaného prostoru (sandbox), musí požádat o přístup. Pokud chcete požádat o přístup, prodiskutujte s vaším účet Microsoftm nebo obchodním kontaktem.

Pro partnery, jejichž účty izolovaného prostoru byly schválené pro nabídky CSP Azure pro předplatné, platí následující omezení:

- Můžete mít až 375 aktivních předplatných (75 zákazníci x 5 předplatných na každého zákazníka). Ale jenom 10 z nich může být předplatné Azure CSP.

- Když předplatné Azure CSP dosáhne $200 využití Azure, prostředky se dočasně zablokují až do dalšího fakturačního cyklu. Pořád se považuje za aktivní předplatné a počítá se do 10 aktivních limitů předplatných Azure.

- Každé předplatné Azure CSP v rámci vašeho účtu v izolovaném prostoru (sandbox) je omezeno na čtyři jádra virtuálních počítačů na datové centrum. Proto nemůžete zřídit SKU virtuálních počítačů, které vyžadují více než čtyři jádra virtuálních počítačů. Jsou vyloučeny také určité specializované SKU virtuálních počítačů, jako jsou například procesory GPU.

> [!Important]
> Všechna stávající předplatná Azure, která byla zřízena s účty izolovaného prostoru před 1. srpna 2018, již nejsou podporována a společnost Microsoft je od 16. října 2018 od 31. října. Po zrušení zřízení předplatných nebude možné je znovu povolit a přidružená data již nebudou k dispozici. Partneři, kteří mají cenná data uložená v rámci těchto předplatných, musí data zálohovat před 16. října 2018.

### <a name="azure-reserved-vm-instance"></a>Rezervovaná instance virtuálního počítače Azure

Pokud si [koupíte rezervovanou instanci virtuálního počítače Azure](purchase-azure-reservations.md) s vaším účtem izolovaného prostoru (sandbox), budete omezeni na dvě instance virtuálních počítačů na každého zákazníka. Jenom si vyberete jenom z následujících SKU produktu Azure rezervované instance virtuálního počítače:

| Název produktu  | Datum platnosti  | Název SKU                                               | Oblast [ArmRegionName] | Klíč instance [ArmSkuName] | Doba trvání | ID měřiče spotřeby       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| Řada B       | 12/1/2017 0:00  | Rezervovaná instance virtuálního počítače, Standard_B1s, KR – jih, 1 rok    | KoreaSouth             | `Standard_B1s` | `1Year`    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| Řada B       | 12/1/2017 0:00  | Rezervovaná instance virtuálního počítače, Standard_B1s, USA – východ, 1 rok     | eastus                 | `Standard_B1s` | `1Year`    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| Řada B       | 12/1/2017 0:00  | Rezervovaná instance virtuálního počítače, Standard_B1s, USA – západ 2, 1 rok   | westus2                | `Standard_B1s` | `1Year`    | 222e39f5-e99f-4fa3-a323-f46402977888 |
| Řada B       | 12/1/2017 0:00  | Rezervovaná instance virtuálního počítače, Standard_B1s, USA (střed) – sever, 1 rok    | northcentralus | `Standard_B1s` | `1Year`    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| Řada B       | 12/1/2017 0:00  | Rezervovaná instance virtuálního počítače, Standard_B1s, CA – východ, 1 rok     | CanadaEast             | `Standard_B1s` | `1Year`    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |

### <a name="subscriptions-for-commercial-marketplace-products"></a>Předplatná pro komerční produkty z webu Marketplace

V produkčním prostředí, po [Vytvoření odběru pro komerční produkty SaaS na webu Marketplace](create-subscription-azure-marketplace-products.md), je potřeba načíst přizpůsobený aktivační odkaz z partnerského centra a přejít na web vydavatele, aby se proces instalace dokončil. Fakturace předplatného se zahájí až po dokončení instalace.

V prostředí izolovaného prostoru (sandbox) CSP není k dispozici žádná integrace s nezávislými prodejci softwaru. Pokud se pokusíte načíst aktivační odkaz z partnerského centra, vrátí se fiktivní odkaz. Tento fiktivní odkaz nelze použít k dokončení procesu instalace na webu vydavatele. Pokud chcete k testování fakturace předplatných do komerčních produktů Marketplace SaaS použít účet izolovaného prostoru (sandbox), přečtěte si téma [Aktivace odběru izolovaného prostoru (sandbox) pro komerční produkty](activate-sandbox-subscription-azure-marketplace-products.md) Fakturace předplatného se začne po úspěšné aktivaci.

Pro vyčištění na konci vašeho testovacího běhu, aby bylo k dispozici místo pro další kruhové testování, přečtěte si následující články:

- [Odstranění zákaznického účet ze sandboxu pro integraci](delete-a-customer-account-from-the-integration-sandbox.md)

- [Snížení množství předplatného](change-the-quantity-of-a-subscription.md)

- [Pozastaví předplatné](suspend-a-subscription.md) , abyste ho mohli odebrat.

## <a name="best-practices-for-rest-development"></a>Osvědčené postupy pro vývoj v REST

- Použijte nástroj pro trasování sítě, abyste viděli svou žádost, odpověď a v případě, že v odpovědi došlo k chybám v kódu stavu HTTP. Další informace o zpracování chyb najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

- Pro každé volání v partnerském centru REST API použít nové ID korelace. Tento postup zajišťuje lepší protokolování a při ladění pomůže. Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

## <a name="troubleshooting-tips-for-common-rest-problems"></a>Tipy k řešení běžných potíží s rozhraním REST

- Zkontrolujte všechny vlastnosti hlaviček, včetně adresy URL a verze rozhraní API.

- Ujistěte se, že vlastnosti jsou v případě potřeby zahrnuté a správně naformátované.

- Nesprávné formátování pole je běžná chyba.

- **Značky ETag** jsou dočasné a v důsledku toho by neměly být uloženy. Když volání funkce vyžaduje **ETag**, použijte nejnovější hodnotu **ETag** tím, že znovu navrátíte prostředek. Hodnoty **ETag** by měly být zahrnuté do dvojitých uvozovek, jako je například řetězec:

   ```rest
   If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
   ```
