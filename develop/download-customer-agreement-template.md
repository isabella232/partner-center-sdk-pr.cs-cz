---
title: Získat odkaz ke stažení pro šablonu zákaznických smluv Microsoftu
description: Získejte odkaz ke stažení pro šablonu zákaznických smluv Microsoftu.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 8c794d264ad64a42fa6ca823ddfc3841248c01cd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766809"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Získat odkaz ke stažení pro šablonu zákaznických smluv Microsoftu

**Platí pro:**

- Partnerské centrum

Partner Center v současné době podporuje prostředek **AgreementDocument** jenom ve *veřejném cloudu Microsoftu*. Tento prostředek se nevztahuje na:

- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Tento článek popisuje, jak získat odkaz ke stažení šablony smlouvy o zákaznících Microsoftu na základě země a jazyka zákazníka.

## <a name="prerequisites"></a>Požadavky

- Pokud používáte sadu SDK partnerského centra .NET, verze 1,14 nebo novější je povinná.

- Přihlašovací údaje popsané v [partnerském centru ověřování](./partner-center-authentication.md). Tento scénář podporuje jenom ověřování aplikací a uživatelů.

- Země zákazníka, na kterou se vztahuje Šablona smlouvy o zákaznících Microsoftu.

- Jazyk, ve kterém má být lokalizovaná Šablona smlouvy Microsoft Customer Agreement

> [!IMPORTANT]
>
> - Smlouva o zákaznících Microsoftu je specifická pro danou zemi. Při žádosti o odkaz ke stažení šablony smlouvy o zákaznících Microsoftu Nezapomeňte zadat správnou zemi na základě umístění zákazníka. nebo seznam podporovaných zemí, přečtěte si [seznam podporovaných zemí a jazyků](#list-of-supported-countries-and-languages).
>
> - V některých zemích je smlouva o zákaznících Microsoftu k dispozici v několika jazycích. Pro nejlepší prostředí pro zákazníky vyberte jazyk, který nejlépe odpovídá potřebám zákazníka. Seznam podporovaných jazyků najdete v [seznamu podporovaných zemí a jazyků](#list-of-supported-countries-and-languages).
> - Tato metoda je podporována pouze se zákaznickou smlouvou Microsoftu.

## <a name="net"></a>.NET

Načtení odkazu na stažení šablony smlouvy o zákaznících Microsoftu:

1. Načtěte metadata smlouvy pro zákaznickou smlouvu Microsoftu. Musíte získat **TemplateID** smlouvy o zákaznících Microsoftu. Další informace najdete v tématu [získání metadat smlouvy pro zákaznickou smlouvu Microsoftu](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.   ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Použijte kolekci IAggregatePartner. AgreementTemplates.

3. Zavolejte metodu **ById** a určete **TemplateID** smlouvy o zákaznících Microsoftu.

4. Načte vlastnost **dokumentu** .

5. Zavolejte metodu **ByCountry** a zadejte zemi zákazníka, na kterou se vztahuje Šablona smlouvy. V případě, že metoda není zadána, je ve výchozím nastavení dotaz na hodnotu *US* . Seznam podporovaných kódů zemí najdete v [seznamu podporovaných zemí a jazyků](#list-of-supported-countries-and-languages). Tato metoda rozlišuje **velká a malá písmena**.

6. Zavolejte metodu **ByLanguage** a určete jazyk, ve kterém má být Šablona smlouvy lokalizována. Pokud není metoda zadaná nebo není pro zadanou zemi podporovaný zadaný kód země, použije se výchozí dotaz na *en-US* . Seznam podporovaných kódů jazyků najdete v [seznamu podporovaných zemí a jazyků](#list-of-supported-countries-and-languages).

7. Zavolejte metodu **Get** nebo **GetAsync** .

   ```csharp
   // IAggregatePartner partnerOperations;

   string customerCountry = "US";

   string languageForLocalization = "en-US";

   var agreementDocument = partnerOperations.   AgreementTemplates.ById   (microsoftCustomerAgreementDetails.   TemplateId).Document.ByCountry   (customerCountry).ByLanguage   (languageForLocalization).Get();
   ```

Kompletní ukázku najdete ve třídě [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [testovací aplikace konzoly](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="rest-request"></a>Žádost REST

Načtení odkazu na stažení šablony smlouvy o zákaznících Microsoftu:

1. Načtěte metadata smlouvy pro zákaznickou smlouvu Microsoftu. Musíte získat **TemplateID** smlouvy o zákaznících Microsoftu. Další informace najdete v tématu [získání metadat smlouvy pro zákaznickou smlouvu Microsoftu](get-customer-agreement-metadata.md).

2. Vytvořte žádost REST pro načtení [prostředku **AgreementDocument**](./agreement-document-resources.md). Příklad najdete v příkladu [syntaxe žádosti](#request-syntax) . Je nutné zadat následující informace:

    - **TemplateID** smlouvy o zákaznících Microsoftu.
    - Země, na kterou se vztahuje Šablona smlouvy o zákaznících Microsoftu
    - Jazyk, ve kterém má být lokalizovaná Šablona smlouvy Microsoft Customer Agreement

### <a name="request-syntax"></a>Syntaxe žádosti

Pro tento prostředek použijte následující syntaxi žádosti:

| Metoda | Identifikátor URI žádosti |
|--------|---------------------------------------------------------------------|
| GET | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreementtemplates/{Agreement-Template-ID}/Document? jazyk = {Language} &země = {Country} HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

S vaším požadavkem můžete použít následující parametry identifikátoru URI:

| Název                   | Typ   | Vyžadováno | Popis                                 |
|------------------------|--------|----------|---------------------------------------------|
| smlouva-ID šablony  | řetězec | Yes      | Jedinečný identifikátor typu smlouvy TemplateId pro smlouvu o zákaznících Microsoftu můžete získat tak, že načtěte metadata smlouvy pro zákaznickou smlouvu Microsoftu. Další informace najdete v tématu [získání metadat smlouvy pro zákaznickou smlouvu Microsoftu](./get-customer-agreement-metadata.md). Tento parametr rozlišuje **velká a malá písmena**.|
| country                | řetězec | No       | Určuje zemi, na kterou se vztahuje Šablona smlouvy. Pokud parametr není zadaný, použije se výchozí dotaz na hodnotu *US* . Seznam podporovaných kódů zemí najdete v [seznamu podporovaných zemí a jazyků](#list-of-supported-countries-and-languages).|
| language               | řetězec | No       | Určuje jazyk, ve kterém má být Šablona smlouvy lokalizována. Pokud parametr není zadaný, použije se ve výchozím nastavení dotaz na hodnotu *en-US* , nebo pokud je zadaný kód země In't podporovaný pro zadanou zemi. Seznam podporovaných kódů zemí najdete v [seznamu podporovaných zemí a jazyků](#list-of-supported-countries-and-languages).|

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí prostředek [ **AgreementDocument**](./agreement-document-resources.md) v těle odpovědi.

Prostředek má vlastnost **downloadUri** , která obsahuje řetězec adresy URL, který lze použít ke stažení šablony smlouvy. Při každém provedení dotazu se vrátí jiný odkaz. Platnost tohoto odkazu vyprší po pěti minutách.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.

Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "displayUri":"https://wopihost.int.l2o.microsoft.com/v1/officehost/agreement/files/Preview...",
    "downloadUri":"https://l2oagreementintbn2.blob.core.windows.net/agreementscontainer/Preview...",
    "language":"en-US",
    "country":"US"
}
```

## <a name="list-of-supported-countries-and-languages"></a>Seznam podporovaných zemí a jazyků

> [!IMPORTANT]
> Vlastnost Code země rozlišuje velká a malá písmena. Ujistěte se prosím, že používáte správná velká a malá písmena uvedená v následující tabulce.

| Země                   | Kód země   | Podporované kódy jazyků |
|------------------------|--------|----------|
| Ostrovy Aland | AX | en-US |
| Afghánistán | AF | en-US |
| Albánie | AL | en-US |
| Alžírsko | DZ | EN-US, fr-FR, en-US |
| Americká Samoa | AS | en-US |
| Andorra | AD | en-US |
| Angola | AO | EN-US, pt-PT |
| Anguilla | Umělá inteligence | en-US |
| Antarktida | AQ | en-US |
| Antigua a Barbuda | AG | en-US |
| Argentina | AR | EN-US, ES-ES |
| Arménie | AM | en-US |
| Aruba | AW | en-US |
| Austrálie | AU | en-US |
| Rakousko | AT | EN-US, de-DE |
| Ázerbájdžán | AZ | en-US |
| Bahamy | BS | en-US |
| Bahrajn | BH | EN-US, ar – SA |
| Bangladéš | BD | en-US |
| Barbados | BB | en-US |
| Bělorusko | BY | EN-US, ru-RU |
| Belgie | BE | EN-US, nl – NL |
| Belize | BZ | EN-US, ES-ES |
| Benin | BJ | en-US |
| Bermudy | BM | en-US |
| Bhútán | BT | en-US |
| Bolívie | BO | EN-US, ES-ES |
| Bonaire | BQ – | en-US |
| Bosna a Hercegovina | BA | en-US |
| Botswana | BW | en-US |
| Bouvetův ostrov | BV | en-US |
| Brazílie | BR | EN-US, pt-BR |
| Britské indickooceánské území | OPERACE | en-US |
| Britské Panenské ostrovy | VG | en-US |
| Brunej | BN | en-US |
| Bulharsko | BG | EN-US, BG-BG |
| Burkina Faso | BF | en-US |
| Burundi | BI | en-US |
| Côte d’Ivoire (Pobřeží slonoviny) | CI | EN-US, fr-FR |
| Cabo Verde | CV | EN-US, pt-PT |
| Kambodža | KH | en-US |
| Kamerun | CM | EN-US, fr-FR |
| Kanada | CA | EN-US, fr-FR |
| Kajmanské ostrovy | KY | EN-US, en-US |
| Středoafrická republika | CF | en-US |
| Čad | TD | en-US |
| Chile | CL | EN-US, ES-ES |
| Vánoční ostrov | CX | en-US |
| Kokosové ostrovy | CC | en-US |
| Kolumbie | CO | EN-US, ES-ES |
| Komory | KLÍČŮ | en-US |
| Konžská demokratická republika | CD | en-US |
| Kongo | CG | en-US |
| Cookovy ostrovy | CK | en-US |
| Kostarika | CR | EN-US, ES-ES |
| Chorvatsko | HR | EN-US, HR-HR |
| Curaçao | Skupina | en-US |
| Kypr | CY | en-US |
| Czechia | CZ | EN-US, cs-CZ |
| Dánsko | DK | EN-US, da-DK |
| Džibutsko | PŘEHRÁVAČE | en-US |
| Dominika | DM | en-US |
| Dominikánská republika | DO | EN-US, ES-ES |
| Ekvádor | EC | en-US |
| Egypt | EG | EN-US, ar – SA |
| Salvador | SV | EN-US, ES-ES |
| Rovníková Guinea | GQ | en-US |
| Eritrea | ER | en-US |
| Estonsko | EE | EN-US, et-EE |
| eSwatini | SZ | en-US |
| Etiopie | ET | en-US |
| Falklandské ostrovy | FK | en-US |
| Faerské ostrovy | FO | en-US |
| Fidži | FJ | en-US |
| Finsko | FI | EN-US, Fi-FI |
| Francie | FR | EN-US, fr-FR |
| Francouzská Guyana | GF | EN-US, fr-FR  |
| Francouzská Polynésie | PF | en-US |
| Francouzská jižní území | TF | en-US |
| Gabon | GA | en-US |
| Gambie | GM | en-US |
| Gruzie | GE | en-US |
| Německo | DE | EN-US, de-DE |
| Ghana | GH | en-US |
| Gibraltar | DŽI | en-US |
| Řecko | GR | EN-US, El-GR |
| Grónsko | GL | en-US |
| Grenada | GD | en-US |
| Guadeloupe | GP | en-US |
| Guam | GU | en-US |
| Guatemala | GT | EN-US, ES-ES |
| Guernsey | GG | en-US |
| Guinea | GN | en-US |
| Guinea-Bissau | GW | en-US |
| Guyana | GY | en-US |
| Haiti | HT | en-US |
| Heardův ostrov a McDonaldovy ostrovy | HM | en-US |
| Honduras | HN | EN-US, ES-ES |
| Hongkong – zvláštní administrativní oblast | HK | EN-US, zh-HK |
| Maďarsko | HU | EN-US, hu-HU |
| Island | IS | en-US |
| Indie | IN | EN-US, dobrý den |
| Indonésie | ID | EN-US, ID-ID |
| Irák | IQ | EN-US, ar – SA |
| Irsko | IE | en-US |
| Ostrov Man | IM | en-US |
| Izrael | IL | EN-US, he-IL |
| Itálie | IT | EN-US, IT |
| Jamajka | JM | en-US |
| Jan Mayen | XJ | en-US |
| Japonsko | JP | EN-US, ja-JP |
| Jersey | VARIABILNÍ | en-US |
| Jordánsko | JO | EN-US, ar – SA |
| Kazachstán | KZ | EN-US, KK-KZ |
| Keňa | KE | en-US |
| Kiribati | KI | en-US |
| Jižní Korea | KR | EN-US, ko-KR |
| Kosovo | XK | en-US |
| Kuvajt | KW | EN-US, ar – SA |
| Kyrgyzstán | KG | EN-US, ru-RU |
| Laos | LA | en-US |
| Lotyšsko | LV | EN-US, LV-LV |
| Libanon | LB | EN-US, ar – SA |
| Lesotho | LS | en-US |
| Libérie | LR | en-US |
| Libye | LY | EN-US, ar – SA |
| Lichtenštejnsko | LI | EN-US, de-DE |
| Litva | LT | EN-US, lt-LT |
| Lucembursko | LU | EN-US, fr-FR |
| Macao – zvláštní administrativní oblast | MO | EN-US, zh-HK |
| Makedonie – BRJ | MK | en-US |
| Madagaskar | MG | en-US |
| Malawi | MW | en-US |
| Malajsie | MY | EN-US, MS-MY |
| Maledivy | MV | en-US |
| Mali | ML | en-US |
| Malta | MT | en-US |
| Marshallovy ostrovy | MH | en-US |
| Martinik | MQ | en-US |
| Mauritánie | MR | en-US |
| Mauricius | SAMOHLÁSK | EN-US, ar – SA |
| Mayotte | YT | en-US |
| Mexiko | MX | EN-US, ES-ES |
| Mikronésie | FM | en-US |
| Moldavsko | MD | EN-US, RO-RO |
| Monako | MC | EN-US, fr-FR |
| Mongolsko | MN | en-US |
| Černá Hora | ME | en-US |
| Montserrat | MS | en-US |
| Maroko | MA | EN-US, fr-FR, en-US |
| Mosambik | MZ | en-US |
| Myanmar | MM | en-US |
| Namibie | Není k dispozici | en-US |
| Nauru | NR | en-US |
| Nepál | NP | en-US |
| Nizozemsko | NL | EN-US, nl – NL |
| Nová Kaledonie | NC | en-US |
| Nový Zéland | NZ | en-US |
| Nikaragua | NI | EN-US, ES-ES |
| Niger | NE | en-US |
| Nigérie | NG | en-US |
| Niue | NU | en-US |
| Norfolk | NF | en-US |
| Severní Mariany | MP | en-US |
| Norsko | NO | EN-US, NB-NO |
| Omán | OM | EN-US, ar – SA |
| Pákistán | PK | en-US |
| Palau | PW | en-US |
| Palestinská samospráva | PS | en-US |
| Panama | PA | EN-US, ES-ES |
| Papua-Nová Guinea | STRÁNKY | en-US |
| Paraguay | PY | EN-US, ES-ES |
| Peru | PE | EN-US, ES-ES |
| Filipíny | PH | en-US |
| Pitcairnovy ostrovy | PN | en-US |
| Polsko | PL | EN-US, pl-PL |
| Portugalsko | PT | EN-US, pt-PT |
| Portoriko | PR | EN-US, en-US |
| Katar | QA | EN-US, ar – SA |
| Réunion | RE | en-US |
| Rumunsko | RO | EN-US, RO-RO |
| Rusko | RU | EN-US, ru-RU |
| Rwanda | RW | EN-US, fr-FR |
| Svatý Tomáš a Princův ostrov | ST | EN-US, fr-FR |
| Saba | X | en-US |
| Saint-Barthélemy | BL | en-US |
| Svatý Kryštof a Nevis | KN | en-US |
| Svatá Lucie | LC | EN-US, en-US |
| Svatý Martin (Francie) | MF | EN-US, en-US |
| Saint Pierre a Miquelon | PM | en-US |
| Svatý Vincenc a Grenadiny | VC | en-US |
| Samoa | WS | en-US |
| San Marino | SM | en-US |
| Saúdská Arábie | SA | en-US |
| Senegal | SN | EN-US, fr-FR |
| Srbsko | RS | EN-US, SR-Latn-RS, en-US |
| Seychely | SC | en-US |
| Sierra Leone | SL | en-US |
| Singapur | SG | EN-US, zh-SG |
| Svatý Eustach | XE | en-US |
| Svatý Martin (Nizozemsko) | SX | EN-US, en-US |
| Slovensko | SK | EN-US, SK-SK |
| Slovinsko | SI | EN-US, SL-SI |
| Šalamounovy ostrovy | SB | en-US |
| Somálsko | SO | en-US |
| Jižní Afrika | ZA | en-US |
| Jižní Georgie a Jižní Sandwichovy ostrovy | GS | en-US |
| Jižní Súdán | SS | en-US |
| Španělsko | ES | EN-US, ES-ES, en-US, en-US |
| Srí Lanka | LK | en-US |
| Svatá Helena, Ascension a Tristan da Cunha | SH | en-US |
| Surinam | SR | en-US |
| Špicberky | SJ | en-US |
| Švédsko | SE | EN-US, sv-SE |
| Švýcarsko | CH | EN-US, fr-FR, en-US, en-US |
| Tchaj-wan | TW | EN-US, zh-HK |
| Tádžikistán | TJ | en-US |
| Tanzanie | TZ | en-US |
| Thajsko | TH | EN-US, th-TH |
| Timor Leste | TL | en-US |
| Togo | TG | en-US |
| Tokelau | TK | en-US |
| Tonga | TO | en-US |
| Trinidad a Tobago | TT | en-US |
| Tunisko | TN | EN-US, fr-FR, en-US |
| Turecko | TR | EN-US, tr-TR |
| Turkmenistán | TM | en-US |
| Ostrovy Turks a Caicos | TC | en-US |
| Tuvalu | TV | en-US |
| Odlehlé ostrovy USA | UM | en-US |
| Americké Panenské ostrovy | VI | en-US |
| Uganda | UG | en-US |
| Ukrajina | UA | EN-US, Spojené království – UA |
| Spojené arabské emiráty | AE | EN-US, ar – SA |
| Spojené království | GB | en-US |
| USA | USA | en-US |
| Uruguay | UY | EN-US, ES-ES |
| Uzbekistán | UZ | EN-US, ru-RU |
| Vanuatu | VU | en-US |
| Vatikán | VA | en-US |
| Venezuela | VE | EN-US, ES-ES |
| Vietnam | VN | EN-US, VI – VN |
| Wallis a Futuna | WF | en-US |
| Jemen | JE | EN-US, ar – SA |
| Zambie | ZM | en-US |
| Zimbabwe | ZW | en-US |
