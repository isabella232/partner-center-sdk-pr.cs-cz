---
title: Získání odkazu ke stažení Smlouva se zákazníkem Microsoftu šablony
description: Získejte odkaz ke stažení Smlouva se zákazníkem Microsoftu šablony.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: fccb9e3d4a837f3e8043f8c7ae1e3911d819afd7
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906523"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Získání odkazu ke stažení Smlouva se zákazníkem Microsoftu šablony

**Platí pro:** Partnerské centrum

**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Prostředek **AgreementDocument** v současné době podporuje Partnerské centrum ve veřejném cloudu Microsoftu.

Tento článek popisuje, jak získat odkaz na stažení šablony Smlouva se zákazníkem Microsoftu na základě země a jazyka zákazníka.

## <a name="prerequisites"></a>Požadavky

- Pokud používáte sadu .NET SDK Partnerské centrum, vyžaduje se verze 1.14 nebo novější.

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](./partner-center-authentication.md) Tento scénář podporuje pouze ověřování aplikací a uživatelů.

- Země zákazníka, na kterou se šablona Smlouva se zákazníkem Microsoftu vztahuje.

- Jazyk, ve kterém by Smlouva se zákazníkem Microsoftu šablony měla být lokalizována.

> [!IMPORTANT]
>
> - Tento Smlouva se zákazníkem Microsoftu je specifický pro jednotlivé země. Pokud žádáte o odkaz na stažení Smlouva se zákazníkem Microsoftu šablony, nezapomeňte zadat správnou zemi na základě polohy zákazníka. nebo seznam podporovaných zemí najdete v seznamu [podporovaných zemí a jazyků](#list-of-supported-countries-and-languages).
>
> - V některých zemích je Smlouva se zákazníkem Microsoftu k dispozici ve více jazycích. Pro co nejlepší zkušenosti zákazníků vyberte jazyk, který nejlépe odpovídá potřebám zákazníka. Seznam podporovaných jazyků najdete v seznamu [podporovaných zemí a jazyků.](#list-of-supported-countries-and-languages)
> - Tato metoda je podporována pouze s Smlouva se zákazníkem Microsoftu.

## <a name="net"></a>.NET

Načtení odkazu pro stažení Smlouva se zákazníkem Microsoftu šablony:

1. Načtěte metadata smlouvy pro Smlouva se zákazníkem Microsoftu. Je nutné získat **templateId** Smlouva se zákazníkem Microsoftu. Další informace najdete v tématu [Získání metadat smlouvy pro Smlouva se zákazníkem Microsoftu](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.   ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Použijte kolekci IAggregatePartner.AgreementTemplates.

3. Zavolejte **metodu ById** a zadejte **templateId** Smlouva se zákazníkem Microsoftu.

4. Načítá **vlastnost** Document.

5. Zavolejte **metodu ByCountry** a zadejte zemi zákazníka, na kterou se šablona smlouvy vztahuje. Pokud není zadaná metoda *,* dotaz je ve výchozím nastavení USA. Seznam podporovaných kódů zemí najdete v seznamu [podporovaných zemí](#list-of-supported-countries-and-languages)a jazyků. Tato metoda **rozlišuje velká a malá písmena.**

6. Zavolejte **metodu ByLanguage** a určete jazyk, ve které se má šablona smlouvy lokalizovat. Pokud není zadaná metoda nebo zadaný kód země není pro zadanou zemi podporovaný, dotaz je ve výchozím nastavení *en-US.* Seznam podporovaných kódů jazyků najdete v seznamu [podporovaných zemí](#list-of-supported-countries-and-languages)a jazyků.

7. Volejte **metodu Get** **nebo GetAsync.**

   ```csharp
   // IAggregatePartner partnerOperations;

   string customerCountry = "US";

   string languageForLocalization = "en-US";

   var agreementDocument = partnerOperations.   AgreementTemplates.ById   (microsoftCustomerAgreementDetails.   TemplateId).Document.ByCountry   (customerCountry).ByLanguage   (languageForLocalization).Get();
   ```

Úplnou ukázku najdete ve třídě [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [konzolové testovací aplikace.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="rest-request"></a>Požadavek REST

Načtení odkazu pro stažení Smlouva se zákazníkem Microsoftu šablony:

1. Načtěte metadata smlouvy pro Smlouva se zákazníkem Microsoftu. Je nutné získat **templateId** Smlouva se zákazníkem Microsoftu. Další informace najdete v tématu [Získání metadat smlouvy pro Smlouva se zákazníkem Microsoftu](get-customer-agreement-metadata.md).

2. Vytvořte požadavek REST pro načtení prostředku [ **AgreementDocument.**](./agreement-document-resources.md) Příklad syntaxe [požadavku.](#request-syntax) Musíte zadat následující informace:

    - TemplateId **(ID** šablony) Smlouva se zákazníkem Microsoftu.
    - Země, na kterou se šablona Smlouva se zákazníkem Microsoftu vztahuje.
    - Jazyk, ve kterém by Smlouva se zákazníkem Microsoftu šablony měla být lokalizována.

### <a name="request-syntax"></a>Syntaxe požadavku

Pro tento prostředek použijte následující syntaxi požadavku:

| Metoda | Identifikátor URI žádosti |
|--------|---------------------------------------------------------------------|
| GET | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreementtemplates/{agreement-template-id}/document?language={language}&country={country} HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

S požadavkem můžete použít následující parametry identifikátoru URI:

| Název                   | Typ   | Vyžadováno | Popis                                 |
|------------------------|--------|----------|---------------------------------------------|
| agreement-template-id  | řetězec | Yes      | Jedinečný identifikátor typu smlouvy Můžete získat templateId pro Smlouva se zákazníkem Microsoftu načtením metadat smlouvy pro Smlouva se zákazníkem Microsoftu. Další informace najdete v tématu [Získání metadat smlouvy pro Smlouva se zákazníkem Microsoftu](./get-customer-agreement-metadata.md). Tento parametr **rozlišuje velká a malá písmena.**|
| country                | řetězec | No       | Určuje zemi, na kterou se šablona smlouvy vztahuje. Pokud parametr není zadaný, výchozí hodnota dotazu je *US.* Seznam podporovaných kódů zemí najdete v seznamu [podporovaných zemí](#list-of-supported-countries-and-languages)a jazyků.|
| language               | řetězec | No       | Určuje jazyk, ve kterém se má šablona smlouvy lokalizovat. Výchozí hodnota dotazu je *en-US,* pokud není zadaný parametr nebo pokud pro zadanou zemi není podporovaný kód země zadaný v . Seznam podporovaných kódů zemí najdete v seznamu [podporovaných zemí a jazyků.](#list-of-supported-countries-and-languages)|

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

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

V případě úspěchu vrátí tato metoda v textu odpovědi prostředek [ **AgreementDocument.**](./agreement-document-resources.md)

Prostředek má vlastnost **downloadUri,** která obsahuje řetězec adresy URL, který lze použít ke stažení šablony smlouvy. Při každém dotazu se vrátí jiný odkaz. Platnost tohoto odkazu vyprší po pěti minutách.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.

K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

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
> U vlastnosti s kódem země se rozlišují malá a velká písmena. Ujistěte se, že používáte správné použití správného kaskády určeného v následující tabulce.

| Země                   | Kód země   | Podporované kódy jazyka |
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
| Bulharsko | BG | en-US, bg-BG |
| Burkina Faso | BF | en-US |
| Burundi | BI | en-US |
| Côte d’Ivoire (Pobřeží slonoviny) | CI | en-US, fr-FR |
| Cabo Verde | CV | en-US, pt-PT |
| Kambodža | KH | en-US |
| Kamerun | CM | en-US, fr-FR |
| Kanada | CA | en-US, fr-FR |
| Kajmanské ostrovy | KY | en-US, en-US |
| Středoafrická republika | CF | en-US |
| Čad | TD | en-US |
| Chile | CL | en-US, es-ES |
| Vánoční ostrov | CX | en-US |
| Kokosové ostrovy | CC | en-US |
| Kolumbie | CO | en-US, es-ES |
| Komory | Km | en-US |
| Konžská demokratická republika | CD | en-US |
| Kongo | Cg | en-US |
| Cookovy ostrovy | Ck | en-US |
| Kostarika | CR | en-US, es-ES |
| Chorvatsko | HR | en-US, hr-HR |
| Curaçao | Cw | en-US |
| Kypr | CY | en-US |
| Čeština | CZ | en-US, cs-CZ |
| Dánsko | DK | en-US, da-DK |
| Džibutsko | Dj | en-US |
| Dominika | DM | en-US |
| Dominikánská republika | DO | en-US, es-ES |
| Ekvádor | EC | en-US |
| Egypt | EG | en-US, ar-SA |
| Salvador | SV | en-US, es-ES |
| Rovníková Guinea | Gq | en-US |
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
| Indie | IN | en-US, hi-IN |
| Indonésie | ID | en-US, id-ID |
| Irák | IQ | en-US, ar-SA |
| Irsko | IE | en-US |
| Ostrov Man | IM | en-US |
| Izrael | IL | en-US, he-IL |
| Itálie | IT | en-US, it-IT |
| Jamajka | JM | en-US |
| Jan Mayen | Xj | en-US |
| Japonsko | JP | en-US, ja-JP |
| Jersey | JE (Je) | en-US |
| Jordánsko | JO | en-US, ar-SA |
| Kazachstán | KZ | en-US, kk-KZ |
| Keňa | KE | en-US |
| Kiribati | KI | en-US |
| Jižní Korea | KR | en-US, ko-KR |
| Kosovo | Xk | en-US |
| Kuvajt | KW | en-US, ar-SA |
| Kyrgyzstán | KG | en-US, ru-RU |
| Laos | LA | en-US |
| Lotyšsko | LV | en-US, lv-LV |
| Libanon | LB | en-US, ar-SA |
| Lesotho | LS | en-US |
| Libérie | LR | en-US |
| Libye | LY | en-US, ar-SA |
| Lichtenštejnsko | LI | en-US, de-DE |
| Litva | LT | en-US, lt-LT |
| Lucembursko | LU | en-US, fr-FR |
| Macao – zvláštní administrativní oblast | MO | en-US, zh-HK |
| Bývalá republika Bývalá Republika | MK | en-US |
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
| Namibie | NA | en-US |
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
