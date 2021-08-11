---
title: Přidání ověřené domény pro zákazníka
description: Zjistěte, jak přidat ověřenou doménu do seznamu schválených domén pro zákazníka v Partnerské centrum. Proveďte to pomocí Partnerské centrum rozhraní API a rozhraní REST API.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 570008c955ce3242b02c1df4c87df52aea3627abb6c86a069cc7c4c0d1d6f799
ms.sourcegitcommit: ac8f5f8bedaddba5110dd4e562fbd9a2b24837df
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/08/2021
ms.locfileid: "116885573"
---
# <a name="add-a-verified-domain-to-the-list-of-approved-domains-for-an-existing-customer"></a>Přidání ověřené domény do seznamu schválených domén pro existujícího zákazníka 

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Postup přidání ověřené domény do seznamu schválených domén pro existujícího zákazníka

## <a name="prerequisites"></a>Požadavky

- Musíte být partner, který je doménový registrátor.

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="adding-a-verified-domain"></a>Přidání ověřené domény

Pokud jste partner, který je doménový registrátor, můžete pomocí tohoto rozhraní API odeslat nový prostředek domény do seznamu domén `verifieddomain` stávajícího zákazníka. [](#domain) Pokud to chcete provést, identifikujte zákazníka pomocí jeho CustomerTenantId. Zadejte hodnotu vlastnosti VerifiedDomainName. Předejte [prostředek domény](#domain) v požadavku s požadovanými vlastnostmi Name, Capability, AuthenticationType, Status a VerificationMethod. Pokud chcete určit, že nová doména je federovaná doména, nastavte vlastnost AuthenticationType v prostředku [Doména](#domain) na a do požadavku zahržte prostředek [](#domain) `Federated` [DomainFederationSettings.](#domain-federation-settings) Pokud je metoda úspěšná, odpověď bude obsahovat [prostředek domény](#domain) pro novou ověřenou doménu.

### <a name="custom-verified-domains"></a>Vlastní ověřené domény

Když přidáváte vlastní ověřenou doménu, která není zaregistrovaná v **doméně onmicrosoft.com**, musíte vlastnost [CustomerUser.immutableId](user-resources.md#customeruser) nastavit na jedinečnou hodnotu ID zákazníka, pro který doménu přidáváte. Tento jedinečný identifikátor je vyžadován během procesu ověřování při ověřování domény. Další informace o uživatelských účtech zákazníků najdete v tématu [Vytvoření uživatelských účtů pro zákazníka.](create-user-accounts-for-a-customer.md)

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda | Identifikátor URI žádosti                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Pomocí následujícího parametru dotazu zadejte zákazníka, pro který přidáváte ověřenou doménu.

| Název                   | Typ     | Vyžadováno | Popis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | guid | Y        | Hodnota je identifikátor GUID naformátovaný **jako CustomerTenantId,** který umožňuje zadat zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje požadované vlastnosti v textu požadavku.

| Název                                                  | Typ   | Vyžadováno                                      | Popis                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | řetězec | Yes                                           | Ověřený název domény. |
| [Doména](#domain)                                     | object | Yes                                           | Obsahuje informace o doméně. |
| [Nastavení domainFederationSettings](#domain-federation-settings) | object | Ano (pokud AuthenticationType = `Federated` )     | Nastavení federace domény, které se má použít, pokud je doména `Federated` doména, a ne `Managed` doména. |

### <a name="domain"></a>Doména

Tato tabulka popisuje požadované a volitelné **vlastnosti domény** v textu požadavku.

| Název               | Typ                                     | Vyžadováno | Popis                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authenticationtype                                    | řetězec           | Yes      | Definuje, jestli je doména `Managed` doména, nebo `Federated` doména. Podporované hodnoty: `Managed` , `Federated` .|
| Schopnost                                            | řetězec           | Yes      | Určuje schopnost domény. Například, `Email`.                  |
| IsDefault (Výchozí)                                             | Logická hodnota s možnou hodnotou null | No       | Určuje, jestli je doména výchozí doménou pro tenanta. Podporované hodnoty: `True` `False` , , `Null` .        |
| IsInitial                                             | Logická hodnota s možnou hodnotou null | No       | Určuje, jestli je doména počáteční doménou. Podporované hodnoty: `True` `False` , , `Null` .                       |
| Name                                                  | řetězec           | Yes      | Název domény.                                                          |
| RootDomain                                            | řetězec           | No       | Název kořenové domény.                                              |
| Status                                                | řetězec           | Yes      | Stav domény. Například, `Verified`. Podporované hodnoty:  `Unverified` `Verified` , , `PendingDeletion` .                               |
| Metoda ověřování                                    | řetězec           | Yes      | Typ metody ověření domény. Podporované hodnoty: `None` `DnsRecord` , , `Email` .                                    |

### <a name="domain-federation-settings"></a>Nastavení federace domény

Tato tabulka popisuje požadované a volitelné **vlastnosti DomainFederationSettings** v textu požadavku.

| Název   | Typ   | Vyžadováno | Popis                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | řetězec           | No      | Přihlašovací identifikátor URI používaný bohatými klienty. Tato vlastnost je adresa URL ověřování STS partnera. |
| Metoda DefaultInteractiveAuthenticationMethod | řetězec           | No      | Označuje výchozí metodu ověřování, která se má použít, když aplikace vyžaduje, aby uživatel měl interaktivní přihlášení. |
| FederationBrandName                    | řetězec           | No      | Název značky federace.        |
| Identifikátor IssuerUri                              | řetězec           | Yes     | Název vystavitele certifikátů.                        |
| LogOffUri                              | řetězec           | Yes     | Identifikátor URI odhlášení. Tato vlastnost popisuje identifikátor URI pro odhlášení federované domény.        |
| MetadataExchangeUri                    | řetězec           | No      | Adresa URL, která určuje koncový bod výměny metadat používaný k ověřování z bohatých klientských aplikací. |
| NextSigningCertificate                 | řetězec           | No      | Certifikát, který služba AD FS V2 STS použije pro nadcházející budoucnost k podepisu deklarací identity. Tato vlastnost je reprezentace certifikátu v kódování Base64. |
| OpenIdConnectDiscoveryEndpoint         | řetězec           | No      | OpenID Připojení koncového bodu zjišťování federovaných služby IDP STS. |
| PassiveLogOnUri                        | řetězec           | Yes     | Přihlašovací identifikátor URI používaný staršími pasivními klienty. Tato vlastnost je adresa pro odesílání federovaných požadavků na přihlášení. |
| PreferredAuthenticationProtocol        | řetězec           | Yes     | Formát ověřovacího tokenu. Například, `WsFed`. Podporované hodnoty: `WsFed` , `Samlp` |
| PromptLoginBehavior                    | řetězec           | Yes     | Typ chování při přihlášení výzvy.  Například, `TranslateToFreshPasswordAuth`. Podporované hodnoty: `TranslateToFreshPasswordAuth` , `NativeSupport` , `Disabled` |
| SigningCertificate                     | řetězec           | Yes     | Certifikát, který služba AD FS V2 STS aktuálně používá k podepisu deklarací identity. Tato vlastnost je reprezentace certifikátu v kódování Base64. |
| SigningCertificateUpdateStatus         | řetězec           | No      | Určuje stav aktualizace podpisového certifikátu. |
| SigningCertificateUpdateStatus         | Logická hodnota s možnou hodnotou null | No      | Určuje, jestli dp STS podporuje MFA. Podporované hodnoty: `True` `False` , , `Null` .|

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
    "VerifiedDomainName": "Example.com",
    "Domain": {
        "AuthenticationType": "Federated",
        "Capability": "Email",
        "IsDefault": Null,
        "IsInitial": Null,
        "Name": "Example.com",
        "RootDomain": null,
        "Status": "Verified",
        "VerificationMethod": "None"
    },
    "DomainFederationSettings": {
        "ActiveLogOnUri": "https://sts.microsoftonline.com/FederationPassive/",
        "DefaultInteractiveAuthenticationMethod": "http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password",
        "FederationBrandName": "FederationBrandName",
        "IssuerUri": "Example.com",
        "LogOffUri": "https://sts.microsoftonline.com/FederationPassive/",
        "MetadataExchangeUri": null,
        "NextSigningCertificate": null,
        "OpenIdConnectDiscoveryEndpoint": "https://sts.contoso.com/adfs/.well-known/openid-configuration",
        "PassiveLogOnUri": "https://sts.microsoftonline.com/Trust/2005/UsernameMixed",
        "PreferredAuthenticationProtocol": "WsFed",
        "PromptLoginBehavior": "TranslateToFreshPasswordAuth",
        "SigningCertificate": <Certificate Signature goes here>,
        "SigningCertificateUpdateStatus": null,
        "SupportsMfa": true
    }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu toto rozhraní API vrátí [prostředek](#domain) domény pro novou ověřenou doménu.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 201 Created
Content-Length: 206
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "authenticationType": "federated",
    "capability": "email",
    "isDefault": false,
    "isInitial": false,
    "name": "Example.com",
    "status": "verified",
    "verificationMethod": "dns_record"
}
```
