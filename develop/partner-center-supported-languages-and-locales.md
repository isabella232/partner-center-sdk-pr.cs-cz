---
title: Podporované jazyka a lokality pro Partnerské centrum
description: Seznam místních prostředí podporovaných v ISO2 a ISO3 pro partnerské Centrum.
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: b3a64cc6aa4b19199490dafcf15eedde12b1330a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547797"
---
# <a name="partner-center-supported-languages-and-locales"></a>Podporované jazyka a lokality pro Partnerské centrum

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Některá rozhraní API partnerského centra vyžadují hodnotu, která indikuje národní prostředí, zemi nebo oblast. Například [záhlaví REST centra pro partnery](headers.md) X-locale vyžaduje hodnotu často ve formátu "Language-Country" ("en-US" označuje "English-USA").

Ve spravovaných rozhraních API partnerského centra jsou třídy [CountryValidationRules/dotnet/API/Microsoft. Store. partnercenter. Models. CountryValidationRules. CountryValidationRules) a [OfferCategory. locale/dotnet/API/Microsoft. Store. partnercenter. Models. res. OfferCategory. locale), [ServiceRequest. CountryCode/dotnet/API/Microsoft. Store. partnercenter. Models. servicerequests. ServiceRequest. CountryCode) nebo [CustomerBillingProfile. Culture/dotnet/API/Microsoft. Store. partnercenter. Models. Customers. CustomerBillingProfile. Culture) vyžadují řetězcové hodnoty, které určují jazyk nebo zemi nebo oblast (ve formě kódu jazyka ISO2 nebo ISO3 kód země/oblasti), národní prostředí nebo jazykovou verzi (ID jazyka v kombinaci s kódem země/oblasti).

V následující tabulce jsou uvedeny kódy zemí kultury a mezinárodní normy organizace (ISO), které jsou podporovány v rozhraních API partnerského centra.

| Země/oblast                           | ISO alfa 2 kód země | ISO alfa 3 kód země | Podporované jazykové verze:                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| Afghánistán                              | AF                       | AFG                      | PS-AF/en-US                         |
| Ostrovy Aland                            | AX                       | NAŘÍZENÍ                      | sv-SE/en-US                         |
| Albánie                                  | AL                       | ALB                      | Čt-AL/en-US                         |
| Alžírsko                                  | DZ                       | DZA                      | ar-DZ/en-US                         |
| Americká Samoa                           | AS                       | ASM                      | en-US                                 |
| Andorra                                  | AD                       | A                      | CA – ES/en-US                         |
| Angola                                   | AO                       | DATEM                      | pt-PT/en-US                         |
| Anguilla                                 | Umělá inteligence                       | AIA                      | en-US                                 |
| Antarktida                               | AQ                       | ATA                      | en-US                                 |
| Antigua a Barbuda                      | AG                       | ATG                      | en-US                                 |
| Argentina                                | AR                       | ARG                      | ES-AR/en-US                         |
| Arménie                                  | AM                       | ARM                      | HY-AM/en-US                         |
| Aruba                                    | AW                       | ABW                      | nl – NL/en-US                         |
| Austrálie                                | AU                       | STŘEDNÍ                      | EN-AU/en-US                         |
| Rakousko                                  | AT                       | AUT                      | de-AT/en-US                         |
| Ázerbájdžán                               | AZ                       | AZE                      | az-Latn-AZ/en-US                    |
| Bahamy                                  | BS                       | BHS                      | en-GB/en-US                         |
| Bahrajn                                  | BH                       | BHR                      | ar – BH/en-US                         |
| Bangladéš                               | BD                       | BGD                      | BN-BD/en-US                         |
| Barbados                                 | BB                       | BRB                      | en-GB/en-US                         |
| Bělorusko                                  | BY                       | BLR                      | DO/en-US                         |
| Belgie                                  | BE                       | POPISKU                      | FR-to/nl-je/en-US                 |
| Belize                                   | BZ                       | BLZ                      | en-BZ / en-US                         |
| Benin                                    | BJ                       | Ben                      | fr-FR / en-US                         |
| Bermudy                                  | Bm                       | BMU                      | en-GB / en-US                         |
| Bhútán                                   | BT                       | Btn                      | en-US                                 |
| Bolívie                                  | BO                       | Bol                      | es-BO / en-US                         |
| Bonaire                                  | Bq                       | Bes                      | nl-NL / en-US                         |
| Bosna a Hercegovina                   | BA                       | BIH                      | bs-Latn-BA / en-US                    |
| Botswana                                 | BW                       | Bwa                      | en-GB / en-US                         |
| Bouvetův ostrov                            | Bv                       | Bvt                      | nb-NO / en-US                         |
| Brazílie                                   | BR                       | Podprsenka                      | pt-BR / en-US                         |
| Britské indickooceánské území           | Io                       | IOT                      | en-US                                 |
| Britské Panenské ostrovy                   | VG                       | Vgb                      | en-US                                 |
| Brunej                                   | BN                       | Brn                      | ms-BN / en-US                         |
| Bulharsko                                 | BG                       | Bgr                      | bg-BG / en-US                         |
| Burkina Faso                             | BF                       | Bfa                      | fr-FR / en-US                         |
| Burundi                                  | BI                       | Bdi                      | fr-FR / en-US                         |
| Cabo Verde                               | CV                       | Cpv                      | pt-CV / en-US                         |
| Kambodža                                 | KH                       | Khm                      | km-POE / en-US                         |
| Kamerun                                 | CM                       | Cmr                      | fr-FR / en-US                         |
| Kanada                                   | CA                       | Cna                      | fr-CA / en-US                         |
| Kajmanské ostrovy                           | KY                       | Cym                      | en-GB / en-US                         |
| Středoafrická republika                 | CF                       | Caf                      | fr-FR / en-US                         |
| Čad                                     | TD                       | Tcd                      | fr-FR / en-US                         |
| Chile                                    | CL                       | Chl                      | es-CL / en-US                         |
| Čína                                    | CN                       | Chn                      | zh-CN / en-US                         |
| Vánoční ostrov                         | CX                       | CXR                      | en-US                                 |
| Kokosové ostrovy                  | CC                       | CCK                      | en-US                                 |
| Kolumbie                                 | CO                       | VYLOUČIT                      | ES-CO/en-US                         |
| Komory                                  | KLÍČŮ                       | Model COM                      | fr-FR/en-US                         |
| Kongo                                    | CG                       | OZUBENÉHO kola                      | fr-FR/en-US                         |
| Konžská demokratická republika                              | CD                       | zařízení vlastněná společností (COD)                      | fr-FR/en-US                         |
| Cookovy ostrovy                             | CK                       | COK                      | en-US                                 |
| Kostarika                               | CR                       | CRI                      | ES-CR/en-US                         |
| Côte d’Ivoire (Pobřeží slonoviny)                            | CI                       | CIV                      | fr-FR/en-US                         |
| Chorvatsko                                  | HR                       | HRV                      | HR-HR/en-US                         |
| Curaçao                                  | Skupina                       | CUW                      | nl – NL/en-US                         |
| Kypr                                   | CY                       | CYP                      | El-GR/en-US                         |
| Czechia                                  | CZ                       | CZE                      | cs-CZ/EN-US                         |
| Dánsko                                  | DK                       | DNK                      | da-DK/en-US                         |
| Džibutsko                                 | PŘEHRÁVAČE                       | DJI                      | fr-FR/en-US                         |
| Dominika                                 | DM                       | DMA                      | en-US                                 |
| Dominikánská republika                       | DO                       | model DOM                      | ES-DO/en-US                         |
| Ekvádor                                  | EC                       | Cu                      | ES-ES/en-US                         |
| Egypt                                    | EG                       | EGY                      | ar – např./en-US                         |
| Salvador                              | SV                       | SLV                      | ES-SV/en-US                         |
| Rovníková Guinea                        | GQ                       | GNQ                      | ES-ES/en-US                         |
| Eritrea                                  | ER                       | ERI                      | ar-SA/en-US                         |
| Estonsko                                  | EE                       | ODHAD                      | et – EE/en-US                         |
| eSwatini                                 | SZ                       | SWZ                      | en-US                                 |
| Etiopie                                 | ET                       | ETH                      | am-ET/en-US                         |
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
| Lotyšsko                                   | LV                       | LVA                      | LV – LV/en-US                         |
| Libanon                                  | LB                       | LBN                      | ar-9,1/EN-US                         |
| Lesotho                                  | LS                       | ZÁTĚŽ                      | en-US                                 |
| Libérie                                  | LR                       | LBR                      | en-US                                 |
| Libye                                    | LY                       | LBY                      | ar-LY/en-US                         |
| Lichtenštejnsko                            | LI                       | CHÁZET                      | de-LI/en-US                         |
| Litva                                | LT                       | LTU                      | lt-LT/en-US                         |
| Lucembursko                               | LU                       | LUX                      | de-LU/fr-LU/en-US                 |
| Macao – zvláštní administrativní oblast                                | MO                       | POČÍTAČE                      | ZH-MO/en-US                         |
| Makedonie – BRJ                          | MK                       | MKD                      | MK-MK/en-US                         |
| Madagaskar                               | MG                       | MDG                      | fr-FR/en-US                         |
| Malawi                                   | MW                       | MWI                      | en-US                                 |
| Malajsie                                 | MY                       | MYS                      | EN-MY/en-US                         |
| Maledivy                                 | MV                       | MDV                      | DV-MV/en-US                         |
| Mali                                     | ML                       | MLI                      | fr-FR/en-US                         |
| Malta                                    | MT                       | MLT                      | MT-MT/en-US                         |
| Marshallovy ostrovy                         | MH                       | MHL                      | en-US                                 |
| Martinik                               | MQ                       | MTQ                      | fr-FR/en-US                         |
| Mauritánie                               | MR                       | NÁSTROJE                      | ar-SA/en-US                         |
| Mauricius                                | SAMOHLÁSK                       | MUS                      | en-GB/en-US                         |
| Mayotte                                  | YT                       | MYT                      | fr-FR/en-US                         |
| Mexiko                                   | MX                       | MEX                      | ES-MX/en-US                         |
| Mikronésie                               | FM                       | FSM                      | en-US                                 |
| Moldavsko                                  | MD                       | MDA                      | RO-RO/en-US                         |
| Monako                                   | MC                       | MCO                      | fr-MC/en-US                         |
| Mongolsko                                 | MN                       | MNG                      | MN-MN/en-US                         |
| Černá Hora                               | ME                       | MNE                      | SR-Latn-já/en-US                    |
| Montserrat                               | MS                       | VYBAVEN                      | en-US                                 |
| Maroko                                  | MA                       | MAR                      | ar-MA/en-US                         |
| Mosambik                               | MZ                       | MOZ                      | pt-PT                                 |
| Myanmar                                  | MM                       | MMR                      | en-US                                 |
| Namibie                                  | NA                       | NAM                      | en-GB/en-US                         |
| Nauru                                    | NR                       | NRU                      | en-US                                 |
| Nepál                                    | NP                       | NPL                      | Ne – NP/en-US                         |
| Nizozemské Antily                     | K                       | ANT                      | en-US                                 |
| Nizozemsko                         | NL                       | NLD                      | nl – NL/en-US                         |
| Nová Kaledonie                            | NC                       | NCL                      | fr-FR/en-US                         |
| Nový Zéland                              | NZ                       | NZL                      | EN-NZ/en-US                         |
| Nikaragua                                | NI                       | NIC                      | ES-NI/en-US                         |
| Niger                                    | NE                       | NER                      | fr-FR/en-US                         |
| Nigérie                                  | NG                       | GUTURÁLNÍ                      | ha-Latn-NG/en-US                    |
| Niue                                     | NU                       | NIU                      | en-US                                 |
| Norfolk                           | NF                       | NFK                      | en-US                                 |
| Severní Mariany                 | MP                       | MNP                      | en-US                                 |
| Norsko                                   | NO                       | NOR                      | NB-NO/en-US                         |
| Omán                                     | OM                       | OMN                      | ar-OM/en-US                         |
| Pákistán                                 | PK                       | Pack                      | Vaše PK/en-US                         |
| Palau                                    | PW                       | PLW                      | en-US                                 |
| Palestinská samospráva                    | PS                       | SBALIT                      | ar-SA/en-US                         |
| Panama                                   | PA                       | PAN                      | ES-PA/en-US                         |
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
| Srbsko                                   | RS                       | SRB                      | SR-Latn-RS/sr-Cyrl-RS/en-US       |
| Seychely                               | SC                       | SYC                      | en-US                                 |
| Sierra Leone                             | SL                       | SLE                      | en-US                                 |
| Singapur                                | SG                       | SGP                      | EN-SG/zh-SG/en-US                 |
| Svatý Eustach                           | XE                       | XSE                      | nl – NL/en-US                         |
| Svatý Martin (Nizozemsko)                             | SX                       | SXM                      | en-US                                 |
| Slovensko                                 | SK                       | SVK                      | SK-SK/en-US                         |
| Slovinsko                                 | SI                       | SVN                      | SL-SI/en-US                         |
| Šalamounovy ostrovy                          | SB                       | KLÍČOVÝCH                      | en-US                                 |
| Somálsko                                  | SO                       | SOM                      | ar-SA/en-US                         |
| Jižní Afrika                             | ZA                       | ZAF                      | EN-ZA/en-US                         |
| Jižní Georgie a Jižní Sandwichovy ostrovy | GS                       | MÉ                      | en-US                                 |
| Jižní Súdán                              | SS                       | SSD                      | en-US                                 |
| Španělsko                                    | ES                       | ŠIFROVANÉ                      | ES-ES/CA-ES/EU-ES/HK-ES/en-US |
| Srí Lanka                                | LK                       | LKA                      | si – LK/en-US                         |
| Svatá Helena, Ascension a Tristan da Cunha   | SH                       | SHN                      | en-US                                 |
| Surinam                                 | SR                       | SUR                      | nl-NL                                 |
| Špicberky                                 | SJ                       | SJM                      | NB-NO/en-US                         |
| Švédsko                                   | SE                       | SWE                      | sv-SE/en-US                         |
| Švýcarsko                              | CH                       | CYRILICE                      | de-CH/fr-CH/IT-CH/en-US         |
| Tchaj-wan                                   | TW                       | TWN                      | zh-TW/en-US                         |
| Tádžikistán                               | TJ                       | TJK                      | TG-Cyrl-TJ/en-US                    |
| Tanzanie                                 | TZ                       | TZA                      | en-GB/en-US                         |
| Thajsko                                 | TH                       | THA                      | Th-tou/en-US                         |
| Timor Leste                              | TL                       | TLS                      | pt-PT/en-US                         |
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
| Zimbabwe                                 | ZW                       | ZWE                      | EN-ZW/en-US                         |

