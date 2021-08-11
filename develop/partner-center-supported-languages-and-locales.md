---
title: Podporované jazyka a lokality pro Partnerské centrum
description: Seznam podporovaných národní prostředí ISO2 a ISO3 pro Partnerské centrum.
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 6f2e1d50fa0f2ace2e94f4dbb5681e2164241ee57a85249136a55fce20893fbb
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997579"
---
# <a name="partner-center-supported-languages-and-locales"></a>Podporované jazyka a lokality pro Partnerské centrum

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Některá Partnerské centrum API vyžadují hodnotu označující národní prostředí, zemi nebo oblast. Například hlavička [Partnerské centrum REST](headers.md) vyžaduje hodnotu často ve formátu "language-country" ("en-US" označuje "angličtina – USA").

V rozhraních PARTNERSKÉ CENTRUM spravovaných rozhraními API třída [CountryValidationRules/dotnet/api/microsoft.store.partnercenter.models.countryvalidationrules.countryvalidationrules) a třída [OfferCategory.Locale/dotnet/api/microsoft.store.partnercenter.models.offers.offercategory.locale), [ServiceRequest.CountryCode/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.countrycode) nebo vlastnosti [CustomerBillingProfile.Culture/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile.culture) vyžadují řetězcové hodnoty, které označují jazyk nebo zemi/oblast (ve formátu kódu jazyka ISO2 nebo kódu ISO3 země/oblasti), národní prostředí, nebo jazykovou verzi (ID jazyka kombinované s kódem země/oblasti).

Následující tabulka uvádí jazykové verze a kódy zemí ORGANIZACE ISO (International Standards Organization), které jsou podporované v Partnerské centrum API.

| Země/oblast                           | ISO Alpha 2 Country Code | ISO Alpha 3 Country Code | Podporované jazykové verze                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| Afghánistán                              | AF                       | AFG                      | ps-AF / en-US                         |
| Ålandské ostrovy                            | Ax                       | Ala                      | sv-SE / en-US                         |
| Albánie                                  | AL                       | PŘESTOŽE                      | sq-AL / en-US                         |
| Alžírsko                                  | DZ                       | Dza                      | ar- NEE/ en-US                         |
| Americká Samoa                           | AS                       | ASM                      | en-US                                 |
| Andorra                                  | AD                       | A                      | ca-ES / en-US                         |
| Angola                                   | AO                       | AGO (PŘED)                      | pt-PT / en-US                         |
| Anguilla                                 | Umělá inteligence                       | Aia                      | en-US                                 |
| Antarktida                               | Aq                       | Ata                      | en-US                                 |
| Antigua a Barbuda                      | AG                       | ATG                      | en-US                                 |
| Argentina                                | AR                       | Arg                      | es-AR / en-US                         |
| Arménie                                  | AM                       | ARM                      | hy-AM / en-US                         |
| Aruba                                    | Aw                       | ABW                      | nl-NL / en-US                         |
| Austrálie                                | AU                       | Aus                      | en-AU / en-US                         |
| Rakousko                                  | AT                       | AUT                      | de-AT / en-US                         |
| Ázerbájdžán                               | AZ                       | AZE                      | az-Latn-AZ / en-US                    |
| Bahamy                                  | BS                       | Bhs                      | en-GB / en-US                         |
| Bahrajn                                  | BH                       | Bhr                      | ar-POE / en-US                         |
| Bangladéš                               | BD                       | Bgd                      | bn-BD / en-US                         |
| Barbados                                 | BB                       | Brb                      | en-GB / en-US                         |
| Bělorusko                                  | BY                       | BLR                      | be-BY / en-US                         |
| Belgie                                  | BE                       | Bel                      | fr-BE / nl-BE / en-US                 |
| Belize                                   | BZ                       | BLZ                      | EN-BZ/en-US                         |
| Benin                                    | BJ                       | BEN                      | fr-FR/en-US                         |
| Bermudy                                  | BM                       | BMU                      | en-GB/en-US                         |
| Bhútán                                   | BT                       | BTN                      | en-US                                 |
| Bolívie                                  | BO                       | KNIHÁCH online                      | ES-BO/en-US                         |
| Bonaire                                  | BQ –                       | BES                      | nl – NL/en-US                         |
| Bosna a Hercegovina                   | BA                       | BOSNĚ                      | BS – Latn-BA/en-US                    |
| Botswana                                 | BW                       | BWA                      | en-GB/en-US                         |
| Bouvetův ostrov                            | BV                       | BVT                      | NB-NO/en-US                         |
| Brazílie                                   | BR                       | BRA                      | pt-BR/en-US                         |
| Britské indickooceánské území           | OPERACE                       | IOT                      | en-US                                 |
| Britské Panenské ostrovy                   | VG                       | VGB                      | en-US                                 |
| Brunej                                   | BN                       | BRN                      | MS-BN/en-US                         |
| Bulharsko                                 | BG                       | BGR                      | BG-BG/en-US                         |
| Burkina Faso                             | BF                       | BFA                      | fr-FR/en-US                         |
| Burundi                                  | BI                       | BDI                      | fr-FR/en-US                         |
| Cabo Verde                               | CV                       | CPV                      | PT – CV/en-US                         |
| Kambodža                                 | KH                       | KHM                      | km – KH/en-US                         |
| Kamerun                                 | CM                       | CMR                      | fr-FR/en-US                         |
| Kanada                                   | CA                       | NEMŮŽE                      | fr – CA/en-US                         |
| Kajmanské ostrovy                           | KY                       | CYM                      | en-GB/en-US                         |
| Středoafrická republika                 | CF                       | CAF                      | fr-FR/en-US                         |
| Čad                                     | TD                       | TCD                      | fr-FR/en-US                         |
| Chile                                    | CL                       | CHL                      | ES-CL/en-US                         |
| Čína                                    | CN                       | CHN                      | zh-CN/en-US                         |
| Vánoční ostrov                         | CX                       | CXR                      | en-US                                 |
| Kokosové ostrovy                  | CC                       | Cck                      | en-US                                 |
| Kolumbie                                 | CO                       | Col                      | es-CO / en-US                         |
| Komory                                  | Km                       | Model COM                      | fr-FR / en-US                         |
| Kongo                                    | Cg                       | Ozubená                      | fr-FR / en-US                         |
| Konžská demokratická republika                              | CD                       | zařízení vlastněná společností (COD)                      | fr-FR / en-US                         |
| Cookovy ostrovy                             | Ck                       | COK                      | en-US                                 |
| Kostarika                               | CR                       | Cri                      | es-CR / en-US                         |
| Côte d’Ivoire (Pobřeží slonoviny)                            | CI                       | Civ                      | fr-FR / en-US                         |
| Chorvatsko                                  | HR                       | HRV                      | hr-HR / en-US                         |
| Curaçao                                  | Cw                       | Nácesí                      | nl-NL / en-US                         |
| Kypr                                   | CY                       | Cyp                      | el-GR / en-US                         |
| Čeština                                  | CZ                       | Cze                      | cs-CZ / en-US                         |
| Dánsko                                  | DK                       | Dnk                      | da-DK / en-US                         |
| Džibutsko                                 | Dj                       | Dji                      | fr-FR / en-US                         |
| Dominika                                 | DM                       | DMA                      | en-US                                 |
| Dominikánská republika                       | DO                       | model DOM                      | es-DO / en-US                         |
| Ekvádor                                  | EC                       | Ecu                      | es-EC / en-US                         |
| Egypt                                    | EG                       | EGY                      | ar-EG / en-US                         |
| Salvador                              | SV                       | Slv                      | es-SV / en-US                         |
| Rovníková Guinea                        | Gq                       | GNQ                      | es-ES / en-US                         |
| Eritrea                                  | ER                       | Eri                      | ar-SA / en-US                         |
| Estonsko                                  | EE                       | Est                      | et-EE / en-US                         |
| eSwa entita                                 | SZ                       | SWZ                      | en-US                                 |
| Etiopie                                 | ET                       | Eth                      | am-ET / en-US                         |
| Falklandské ostrovy                         | FK                       | FLK                      | en-US                                 |
| Faerské ostrovy                            | FO                       | STEJNÉ                      | FO-FO/en-US                         |
| Fidži                                     | FJ                       | FJI                      | en-GB/en-US                         |
| Finsko                                  | FI                       | FIN                      | Fi-FI/sv-FI/en-US                 |
| Francie                                   | FR                       | FRA                      | fr-FR/en-US                         |
| Francouzská Guyana                            | GF                       | GUF                      | fr-FR/en-US                         |
| Francouzská Polynésie                         | PF                       | PYF                      | fr-FR/en-US                         |
| Francouzská jižní území              | TF                       | ATF                      | fr-FR/en-US                         |
| Gabon                                    | GA                       | GAB                      | fr-FR/en-US                         |
| Gambie                                   | GM                       | GMB                      | en-US                                 |
| Gruzie                                  | GE                       | GEOGRAFICKY                      | ka – GE/en-US                         |
| Německo                                  | DE                       | DEU                      | de-DE/EN-US                         |
| Ghana                                    | GH                       | GHA                      | en-GB/en-US                         |
| Gibraltar                                | DŽI                       | GIB                      | en-US                                 |
| Řecko                                   | GR                       | GRC                      | El-GR/en-US                         |
| Grónsko                                | GL                       | GRL                      | da-DK/en-US                         |
| Grenada                                  | GD                       | GRD                      | en-US                                 |
| Guadeloupe                               | GP                       | VRSTVĚ                      | fr-FR/en-US                         |
| Guam                                     | GU                       | Arabská                      | en-US                                 |
| Guatemala                                | GT                       | GTM                      | ES-GT/en-US                         |
| Guernsey                                 | GG                       | GGY                      | en-US                                 |
| Guinea                                   | GN                       | GIN                      | fr-FR/en-US                         |
| Guinea-Bissau                            | GW                       | GNB                      | pt-PT/en-US                         |
| Guyana                                   | GY                       | GUY                      | en-US                                 |
| Haiti                                    | HT                       | HTI                      | fr-FR/en-US                         |
| Heardův ostrov a McDonaldovy ostrovy        | HM                       | HMD                      | en-US                                 |
| Honduras                                 | HN                       | HND                      | ES-HN/en-US                         |
| Hongkong – zvláštní administrativní oblast                            | HK                       | HKG                      | zh-HK/en-US                         |
| Maďarsko                                  | HU                       | HUN                      | hu – HU/en-US                         |
| Island                                  | IS                       | Vrátí                      | je-IS/en-US                         |
| Indie                                    | IN                       | IND                      | en-IN/Hi-IN/en-US                 |
| Indonésie                                | ID                       | IDN                      | ID-ID/en-US                         |
| Irák                                     | IQ                       | POŽADAVKU                      | ar – SWEETIQ/en-US                         |
| Irsko                                  | IE                       | IRL                      | EN-IE/en-US                         |
| Ostrov Man                              | IM                       | IMN                      | en-US                                 |
| Izrael                                   | IL                       | ISR                      | He-IL/en-US                         |
| Itálie                                    | IT                       | ITA                      | IT – IT/en-US                         |
| Jamajka                                  | JM                       | DŽEM                      | EN-JM/en-US                         |
| Jan Mayen                                | XJ                       | XJA                      | NB-NO/en-US                         |
| Japonsko                                    | JP                       | JPN                      | ja-JP/en-US                         |
| Jersey                                   | VARIABILNÍ                       | JEY                      | en-US                                 |
| Jordánsko                                   | JO                       | JOR                      | ar – JO/en-US                         |
| Kazachstán                               | KZ                       | KAZ                      | KK-KZ/en-US                         |
| Keňa                                    | KE                       | KEN                      | SW – KE/en-US                         |
| Kiribati                                 | KI                       | KIR                      | en-US                                 |
| Jižní Korea                                    | KR                       | KOR                      | ko-KR/en-US                         |
| Kosovo                                   | XK                       | XKS                      | en-US                                 |
| Kuvajt                                   | KW                       | KWT                      | ar – KW/en-US                         |
| Kyrgyzstán                               | KG                       | KGZ                      | ky-KG/en-US                         |
| Laos                                     | LA                       | LAOSKÝ                      | Lo – LA/en-US                         |
| Lotyšsko                                   | LV                       | LVA                      | lv-LV / en-US                         |
| Libanon                                  | LB                       | LBN                      | ar-LB / en-US                         |
| Lesotho                                  | LS                       | Lso                      | en-US                                 |
| Libérie                                  | LR                       | LBR                      | en-US                                 |
| Libye                                    | LY                       | Lby                      | ar-LY / en-US                         |
| Lichtenštejnsko                            | LI                       | Lež                      | de-LI / en-US                         |
| Litva                                | LT                       | Ltu                      | lt-LT / en-US                         |
| Lucembursko                               | LU                       | Lux                      | de-LU / fr-LU / en-US                 |
| Macao – zvláštní administrativní oblast                                | MO                       | Mac                      | zh-MO / en-US                         |
| Bývalá republika Bývalá Republika                          | MK                       | Mkd                      | mk-MK / en-US                         |
| Madagaskar                               | MG                       | MDG                      | fr-FR / en-US                         |
| Malawi                                   | MW                       | MWI                      | en-US                                 |
| Malajsie                                 | MY                       | MYS                      | en-MY / en-US                         |
| Maledivy                                 | MV                       | MDV                      | dv-MV / en-US                         |
| Mali                                     | ML                       | Mli                      | fr-FR / en-US                         |
| Malta                                    | MT                       | Mlt                      | mt-MT / en-US                         |
| Marshallovy ostrovy                         | MH                       | MHL                      | en-US                                 |
| Martinik                               | MQ                       | MTQ                      | fr-FR / en-US                         |
| Mauritánie                               | MR                       | Mrt                      | ar-SA / en-US                         |
| Mauricius                                | Mu                       | MUS                      | en-GB / en-US                         |
| Mayotte                                  | YT                       | MYT                      | fr-FR / en-US                         |
| Mexiko                                   | MX                       | Mex                      | es-MX / en-US                         |
| Mikronésie                               | FM                       | Fsm                      | en-US                                 |
| Moldavsko                                  | MD                       | Mda                      | ro-RO / en-US                         |
| Monako                                   | MC                       | Mco                      | fr-MC / en-US                         |
| Mongolsko                                 | MN                       | Mng                      | mn-MN / en-US                         |
| Černá Hora                               | ME                       | Měnová zařízení                      | sr-Latn-ME / en-US                    |
| Montserrat                               | MS                       | Msr                      | en-US                                 |
| Maroko                                  | MA                       | MAR                      | ar-MA / en-US                         |
| Mosambik                               | MZ                       | Moz                      | pt-PT                                 |
| Myanmar                                  | MM                       | Mmr                      | en-US                                 |
| Namibie                                  | NA                       | Nam                      | en-GB / en-US                         |
| Nauru                                    | NR                       | NRU                      | en-US                                 |
| Nepál                                    | NP                       | Npl                      | ne-NP / en-US                         |
| Nizozemské Antily                     | An                       | Ant                      | en-US                                 |
| Nizozemsko,                         | NL                       | NLD                      | nl-NL / en-US                         |
| Nová Kaledonie                            | NC                       | NCL                      | fr-FR / en-US                         |
| Nový Zéland                              | NZ                       | NZL                      | en-NZ / en-US                         |
| Nikaragua                                | NI                       | NIC                      | es-NI / en-US                         |
| Niger                                    | NE                       | Ner                      | fr-FR / en-US                         |
| Nigérie                                  | NG                       | Vzp                      | ha-Latn-NG / en-US                    |
| Niue                                     | NU                       | Niu                      | en-US                                 |
| Norfolk                           | Nf                       | NFK                      | en-US                                 |
| Severní Mariany                 | MP                       | MNP                      | en-US                                 |
| Norsko                                   | NO                       | NOR                      | nb-NO / en-US                         |
| Omán                                     | OM                       | OMN                      | ar-OM / en-US                         |
| Pákistán                                 | PK                       | PAK                      | your-PK / en-US                         |
| Palau                                    | PW                       | PLW                      | en-US                                 |
| Palestinská samospráva                    | PS                       | Pse                      | ar-SA / en-US                         |
| Panama                                   | PA                       | PAN                      | es-PA / en-US                         |
| Papua-Nová Guinea                         | Str                       | PNG                      | en-US                                 |
| Paraguay                                 | PY                       | Slídit                      | es-PY / en-US                         |
| Peru                                     | PE                       | PER                      | es-PE / en-US                         |
| Filipíny                              | PH                       | Phl                      | en-PH / en-US                         |
| Pitcairnovy ostrovy                         | Pn                       | Pcn                      | en-US                                 |
| Polsko                                   | PL                       | Pol                      | pl-PL / en-US                         |
| Portugalsko                                 | PT                       | Prt                      | pt-PT / en-US                         |
| Portoriko                              | PR                       | Pri                      | es-PR / en-US                         |
| Katar                                    | QA                       | QAT                      | ar-QA / en-US                         |
| Réunion                                  | RE                       | Reu                      | fr-FR / en-US                         |
| Rumunsko                                  | RO                       | Rou                      | ro-RO / en-US                         |
| Rusko                                   | RU                       | RUS                      | ru-RU / en-US                         |
| Rwanda                                   | RW                       | Rwa                      | rw-RW / en-US                         |
| Saba                                     | Xs                       | XSA                      | nl-NL / en-US                         |
| Svatý Kryštof a Nevis                    | KN                       | Kna                      | en-GB / en-US                         |
| Svatá Lucie                              | Lc                       | Lca                      | en-US                                 |
| Svatý Martin (Francie)                             | Mf                       | Maf                      | fr-FR / en-US                         |
| Saint Pierre a Miquelon                | PM                       | Spm                      | fr-FR / en-US                         |
| Svatý Vincenc a Grenadiny         | VC                       | Vct                      | en-US                                 |
| Saint-Barthélemy                         | BL                       | Blm                      | fr-FR / en-US                         |
| Samoa                                    | WS                       | Wsm                      | en-US                                 |
| San Marino                               | Sm                       | Smr                      | it-IT / en-US                         |
| Sâo Tomé a Můžetencipe                    | ST                       | Stp                      | pt-PT / en-US                         |
| Saúdská Arábie                             | SA                       | Sau                      | ar-SA / en-US                         |
| Senegal                                  | SN                       | Senátor                      | wo-SN / en-US                         |
| Srbsko                                   | RS                       | Srb                      | sr-Latn-RS / sr-Cyrl-RS / en-US       |
| Seychely                               | SC                       | SYC                      | en-US                                 |
| Sierra Leone                             | SL                       | Sle                      | en-US                                 |
| Singapur                                | SG                       | Sgp                      | en-SG / zh-SG / en-US                 |
| Svatý Eustach                           | Xe                       | XSE                      | nl-NL / en-US                         |
| Svatý Martin (Nizozemsko)                             | Sx                       | Sxm                      | en-US                                 |
| Slovensko                                 | SK                       | Svk                      | sk-SK / en-US                         |
| Slovinsko                                 | SI                       | Svn                      | sl-SI / en-US                         |
| Šalamounovy ostrovy                          | Sb                       | Slb                      | en-US                                 |
| Somálsko                                  | SO                       | Som                      | ar-SA / en-US                         |
| Jižní Afrika                             | ZA                       | ZAF                      | en-ZA / en-US                         |
| Jižní Georgie a Jižní Sandwichovy ostrovy | Gs                       | Sgs                      | en-US                                 |
| Jižní Súdán                              | SS                       | SSD                      | en-US                                 |
| Španělsko                                    | ES                       | Esp                      | es-ES / ca-ES / eu-ES / gl-ES / en-US |
| Srí Lanka                                | LK                       | ZAK                      | si-LK / en-US                         |
| St Kaň, Ascension, Tristan da Çha   | SH                       | Shn                      | en-US                                 |
| Surinam                                 | SR                       | Sur                      | nl-NL                                 |
| Špicberky                                 | Sj                       | SJM                      | nb-NO / en-US                         |
| Švédsko                                   | SE                       | Swe                      | sv-SE / en-US                         |
| Švýcarsko                              | CH                       | Che                      | de-CH / fr-CH / it-CH / en-US         |
| Tchaj-wan                                   | TW                       | TWN                      | zh-TW / en-US                         |
| Tádžikistán                               | Tj., tj.                       | TJK                      | tg-Cyrl-TJ / en-US                    |
| Tanzanie                                 | TZ                       | TZA                      | en-GB / en-US                         |
| Thajsko                                 | TH                       | Tha                      | th-TH / en-US                         |
| Timor Leste                              | TL                       | TLS                      | pt-PT / en-US                         |
| Togo                                     | TG                       | Tgo                      | fr-FR / en-US                         |
| Tokelau                                  | Tk                       | TKL                      | en-US                                 |
| Tonga                                    | TO                       | Ton                      | en-US                                 |
| Trinidad a Tobago                      | TT                       | Tto                      | en-TT / en-US                         |
| Tunisko                                  | TN                       | TUN (Vyladit)                      | ar-TN / en-US                         |
| Turecko                                   | TR                       | Tur                      | tr-TR / en-US                         |
| Turkmenistán                             | TM                       | TKM                      | tk-TM / en-US                         |
| Ostrovy Turks a Caicos                 | TC                       | Tca                      | en-US                                 |
| Tuvalu                                   | TV                       | TUV                      | en-US                                 |
| Uganda                                   | UG                       | Uga                      | en-GB / en-US                         |
| Ukrajina                                  | UA                       | Ukr                      | uk-UA / en-US                         |
| Spojené arabské emiráty                     | AE                       | Jsou                      | ar-AE / en-US                         |
| Spojené království                           | GB                       | Gbr                      | en-GB / en-US                         |
| Odlené ostrovy USA                    | UM                       | Umi                      | en-US                                 |
| Americké Panenské ostrovy                      | VI                       | VIR (Vir)                      | en-US                                 |
| USA                            | USA                       | USA                      | en-US / es-US                         |
| Uruguay                                  | UY                       | Ury                      | es-UY / en-US                         |
| Uzbekistán                               | UZ                       | UZB                      | uz-Latn-UZ / en-US                    |
| Vanuatu                                  | Vu                       | Vut                      | en-US                                 |
| Vatikán                             | VA                       | Dph                      | it-IT / en-US                         |
| Venezuela                                | VE                       | VEN                      | es-VE / en-US                         |
| Vietnam                                  | VN                       | Vnm                      | vi-VN / en-US                         |
| Wallis a Futuna                        | WF                       | WLF                      | fr-FR / en-US                         |
| Jemen                                    | YE (Ye)                       | YEM                      | ar-YE / en-US                         |
| Zambie                                   | ZM                       | ZMB                      | en-GB / en-US                         |
| Zimbabwe                                 | ZW                       | ZWE                      | en-ZW / en-US                         |

