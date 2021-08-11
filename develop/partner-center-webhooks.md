---
title: Webhooky Partnerského centra
description: Webhooky umožňují partnerům registrovat se na události změny prostředků.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: cf063579b447601fa1050d6b03e0c46f6ef64abef9bb500598a047ac40ddaa1d
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997545"
---
# <a name="partner-center-webhooks"></a>Webhooky Partnerského centra

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Rozhraní API Webhooku partnerského centra umožňují partnerům registrovat se na události změny prostředků. Tyto události se doručí ve formě příspěvků HTTP na registrovanou adresu URL partnera. Aby partneři mohli získat událost z partnerského centra, bude hostovat zpětné volání, které může partnerské Centrum publikovat událost změny prostředku. Událost bude digitálně podepsaná, aby partner mohl ověřit, že byla odeslána z partnerského centra.

Partneři můžou vybírat z událostí Webhooku, jako jsou následující příklady, které jsou podporované partnerským centrem.

- **Testovací událost ("test-Created")**

    Tato událost umožňuje samoobslužné zprovoznění a testování registrace tím, že požaduje testovací událost a pak sleduje jeho průběh. Při pokusu o doručení události můžete zobrazit zprávy o chybách, které jsou přijímány od společnosti Microsoft. Toto omezení se vztahuje pouze na události "vytvořené testem". Data starší než sedm dní se vyprázdní.

- **Událost aktualizace předplatného (předplatné-Aktualizováno)**

    Tato událost se vyvolá při změně předplatného. Tyto události budou vygenerovány v případě, že dojde k vnitřní změně kromě změny prostřednictvím rozhraní API partnerského centra.

    >[!NOTE]
    >Mezi časem změny předplatného a aktivací události aktualizace předplatného dojde k prodlevě až 48 hodin.

- **Událost překročení prahové hodnoty ("usagerecords-thresholdExceeded")**

    tato událost se vyvolá v případě, že množství využití Microsoft Azure pro každého zákazníka přesáhne rozpočet výdajů na využití (jejich prahovou hodnotu). Další informace najdete v tématu [nastavení rozpočtu útraty Azure pro vaše zákazníky/partnery – Center/set-a-Azure-útraty-rozpočet-pro zákazníky).

- **Událost vytvořená odkazem (odkaz – vytvořeno)**

    Tato událost je aktivována při vytvoření odkazu.

- **Událost aktualizovaného odkazu (odkaz-Aktualizováno)**

    Tato událost je aktivována při aktualizaci odkazu.

- **Událost připravena k faktuře ("faktura-připravena")**

    Tato událost se vyvolá, když je nová faktura připravena.

Další události Webhooku se přidají pro prostředky, které se změní v systému, který partner neovládá, a provede se další aktualizace, aby se tyto události dostaly co nejblíže "reálnému času". Názory partnerů, na kterých události přidávají hodnotu do jejich podnikání, budou užitečné při určování nových událostí, které se mají přidat.

Úplný seznam událostí Webhooku podporovaných partnerským centrem najdete v tématu [události Webhooku partnerského centra](partner-center-webhook-events.md).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

## <a name="receiving-events-from-partner-center"></a>Příjem událostí z partnerského centra

Pokud chcete přijímat události z partnerského centra, musíte zveřejnit veřejně přístupný koncový bod. Vzhledem k tomu, že je tento koncový bod vystavený, musíte ověřit, jestli je komunikace z partnerského centra. Všechny události Webhooku, které jste obdrželi, jsou digitálně podepsané certifikátem, který je zřetězený do kořenového adresáře společnosti Microsoft. Bude také k dispozici odkaz na certifikát použitý k podepsání události. Tím umožníte prodloužení platnosti certifikátu, aniž byste museli službu znovu nasazovat nebo překonfigurovat. Partnerským centrem se 10 pokusí o doručení události. Pokud se událost ještě doručí po 10 pokusech, přesune se do offline fronty a žádné další pokusy se neuskuteční při doručení.

Následující ukázka ukazuje událost zveřejněnou z partnerského centra.

```http
POST /webhooks/callback
Content-Type: application/json
Authorization: Signature VOhcjRqA4f7u/4R29ohEzwRZibZdzfgG5/w4fHUnu8FHauBEVch8m2+5OgjLZRL33CIQpmqr2t0FsGF0UdmCR2OdY7rrAh/6QUW+u+jRUCV1s62M76jbVpTTGShmrANxnl8gz4LsbY260LAsDHufd6ab4oejerx1Ey9sFC+xwVTa+J4qGgeyIepeu4YCM0oB2RFS9rRB2F1s1OeAAPEhG7olp8B00Jss3PQrpLGOoAr5+fnQp8GOK8IdKF1/abUIyyvHxEjL76l7DVQN58pIJg4YC+pLs8pi6sTKvOdSVyCnjf+uYQWwmmWujSHfyU37j2Fzz16PJyWH41K8ZXJJkw==
X-MS-Certificate-Url: https://3psostorageacct.blob.core.windows.net/cert/pcnotifications-dispatch.microsoft.com.cer
X-MS-Signature-Algorithm: rsa-sha256
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 195

{
    "EventName": "test-created",
    "ResourceUri": "http://localhost:16722/v1/webhooks/registration/test",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

>[!NOTE]
>Autorizační hlavička má schéma "signatura". Toto je signatura s kódováním base64 obsahu.

## <a name="how-to-authenticate-the-callback"></a>Ověření zpětného volání

K ověření události zpětného volání přijatého z partnerského centra použijte následující postup:

1. Ověřte, zda jsou k dispozici požadovaná záhlaví (autorizace, x-MS-Certificate-URL, x-MS-Signature-Algorithm).

2. Stáhněte si certifikát použitý k podepsání obsahu (x-MS-Certificate-URL).

3. Ověřte řetěz certifikátů.

4. Ověřte "organizaci" certifikátu.

5. Přečtěte si obsah s kódováním UTF8 do vyrovnávací paměti.

6. Vytvořte poskytovatele kryptografických služeb RSA.

7. Ověřte, že data odpovídají údajům, které byly podepsány zadaným algoritmem hash (například SHA256).

8. Pokud je ověření úspěšné, zpracujte zprávu.

> [!NOTE]
> Ve výchozím nastavení se token podpisu pošle v autorizační hlavičce. Pokud jste v registraci nastavili **SignatureTokenToMsSignatureHeader** na hodnotu true, token podpisu se místo toho pošle v hlavičce x-MS-Signature.

## <a name="event-model"></a>Model událostí

Následující tabulka popisuje vlastnosti události partnerského centra.

### <a name="properties"></a>Vlastnosti

| Název                      | Description                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **EventName**             | Název události. Ve formátu {Resource} – {Action}. Například "test-Created".  |
| **ResourceUri**           | Identifikátor URI prostředku, který se změnil.                                                 |
| **ResourceName**          | Název prostředku, který se změnil.                                                |
| **AuditUrl**              | Nepovinný parametr. Identifikátor URI záznamu auditu                                                |
| **ResourceChangeUtcDate** | Datum a čas ve formátu UTC, kdy došlo ke změně prostředků.                  |

### <a name="sample"></a>Ukázka

Následující příklad ukazuje strukturu události partnerského centra.

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a>Rozhraní API Webhooku

### <a name="authentication"></a>Authentication

Všechna volání rozhraní API Webhooku se ověřují pomocí nosných tokenů v autorizační hlavičce. Získání přístupového tokenu pro přístup `https://api.partnercenter.microsoft.com` . Tento token je stejný token, který se používá pro přístup ke zbytkům rozhraní API partnerského centra.

### <a name="get-a-list-of-events"></a>Získat seznam událostí

Vrátí seznam událostí, které jsou aktuálně podporovány rozhraními API Webhooku.

### <a name="resource-url"></a>Adresa URL prostředku

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a>Příklad požadavku

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200
Status: 200
Content-Length: 183
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c0bcf3a3-46e9-48fd-8e05-f674b8fd5d66
MS-RequestId: 79419bbb-06ee-48da-8221-e09480537dfc
X-Locale: en-US

[ "subscription-updated", "test-created", "usagerecords-thresholdExceeded" ]
```

### <a name="register-to-receive-events"></a>Registrace pro příjem událostí

Zaregistruje tenanta pro příjem zadaných událostí.

#### <a name="resource-url"></a>Adresa URL prostředku

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>Příklad požadavku

```http
POST /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0e.....
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 219

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="view-a-registration"></a>Zobrazit registraci

Vrátí registraci události webhooků pro tenanta.

#### <a name="resource-url"></a>Adresa URL prostředku

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>Příklad požadavku

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200
Status: 200
Content-Length: 341
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c3b88ab0-b7bc-48d6-8c55-4ae6200f490a
MS-RequestId: ca30367d-4b24-4516-af08-74bba6dc6657
X-Locale: en-US

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="update-an-event-registration"></a>Aktualizace registrace události

Aktualizuje existující registraci události.

#### <a name="resource-url"></a>Adresa URL prostředku

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>Příklad požadavku

```http
PUT /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOR...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 258

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="send-a-test-event-to-validate-your-registration"></a>Odeslání testovací události pro ověření registrace

Vygeneruje testovací událost pro ověření registrace webhooků. Účelem tohoto testu je ověřit, že můžete přijímat události z Partnerské centrum. Data pro tyto události se odstraní sedm dní po vytvoření počáteční události. Před odesláním události ověření musíte být zaregistrovaní k události vytvoření testu pomocí registračního rozhraní API.

>[!NOTE]
>Při odesílání události ověření platí limit 2 požadavků za minutu.

#### <a name="resource-url"></a>Adresa URL prostředku

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a>Příklad požadavku

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200
Status: 200
Content-Length: 181
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 04af2aea-d413-42db-824e-f328001484d1
MS-RequestId: 2f498d5a-a6ab-468f-98d8-93c96da09051
X-Locale: en-US

{ "correlationId": "04af2aea-d413-42db-824e-f328001484d1" }
```

### <a name="verify-that-the-event-was-delivered"></a>Ověření doručení události

Vrátí aktuální stav události ověření. Toto ověření může být užitečné při řešení potíží s doručováním událostí. Odpověď obsahuje výsledek každého pokusu o doručení události.

#### <a name="resource-url"></a>Adresa URL prostředku

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a>Příklad požadavku

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200
Status: 200
Content-Length: 469
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 497e0a23-9498-4d6c-bd6a-bc4d6d0054e7
MS-RequestId: 0843bdb2-113a-4926-a51c-284aa01d722e
X-Locale: en-US

{
    "correlationId": "04af2aea-d413-42db-824e-f328001484d1",
    "partnerId": "00234d9d-8c2d-4ff5-8c18-39f8afc6f7f3",
    "status": "completed",
    "callbackUrl": "{{YourCallbackUrl}}",
    "results": [{
        "responseCode": "OK",
        "responseMessage": "",
        "systemError": false,
        "dateTimeUtc": "2017-12-08T21:39:48.2386997"
    }]
}
```

## <a name="example-for-signature-validation"></a>Příklad ověření podpisu

### <a name="sample-callback-controller-signature-aspnet"></a>Podpis kontroleru vzorového zpětného volání (ASP.NET)

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a>Ověření podpisu

Následující příklad ukazuje, jak přidat autorizační atribut do kontroleru, který přijímá zpětná volání z událostí webhooku.

``` csharp
namespace Webhooks.Security
{
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Security.Cryptography;
    using System.Security.Cryptography.X509Certificates;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Web.Http;
    using System.Web.Http.Controllers;
    using Microsoft.Partner.Logging;

    /// <summary>
    /// Signature based Authorization
    /// </summary>
    public class AuthorizeSignatureAttribute : AuthorizeAttribute
    {
        private const string MsSignatureHeader = "x-ms-signature";
        private const string CertificateUrlHeader = "x-ms-certificate-url";
        private const string SignatureAlgorithmHeader = "x-ms-signature-algorithm";
        private const string MicrosoftCorporationIssuer = "O=Microsoft Corporation";
        private const string SignatureScheme = "Signature";

        /// <inheritdoc/>
        public override async Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            ValidateAuthorizationHeaders(actionContext.Request);

            await VerifySignature(actionContext.Request);
        }

        private static async Task<string> GetContentAsync(HttpRequestMessage request)
        {
            // By default the stream can only be read once and we need to read it here so that we can hash the body to validate the signature from microsoft.
            // Load into a buffer, so that the stream can be accessed here and in the api when it binds the content to the expected model type.
            await request.Content.LoadIntoBufferAsync();

            var s = await request.Content.ReadAsStreamAsync();
            var reader = new StreamReader(s);
            var body = await reader.ReadToEndAsync();

            // set the stream position back to the beginning
            if (s.CanSeek)
            {
                s.Seek(0, SeekOrigin.Begin);
            }

            return body;
        }

        private static void ValidateAuthorizationHeaders(HttpRequestMessage request)
        {
            var authHeader = request.Headers.Authorization;
            if (string.IsNullOrWhiteSpace(authHeader?.Parameter) && string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, MsSignatureHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Authorization header missing."));
            }

            var signatureHeaderValue = GetHeaderValue(request.Headers, MsSignatureHeader);
            if (authHeader != null
                && !string.Equals(authHeader.Scheme, SignatureScheme, StringComparison.OrdinalIgnoreCase)
                && !string.IsNullOrWhiteSpace(signatureHeaderValue)
                && !signatureHeaderValue.StartsWith(SignatureScheme, StringComparison.OrdinalIgnoreCase))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Authorization scheme needs to be '{SignatureScheme}'."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, CertificateUrlHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {CertificateUrlHeader} missing."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, SignatureAlgorithmHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {SignatureAlgorithmHeader} missing."));
            }
        }

        private static string GetHeaderValue(HttpHeaders headers, string key)
        {
            headers.TryGetValues(key, out var headerValues);

            return headerValues?.FirstOrDefault();
        }

        private static async Task VerifySignature(HttpRequestMessage request)
        {
            // Get signature value from either authorization header or x-ms-signature header.
            var base64Signature = request.Headers.Authorization?.Parameter ?? GetHeaderValue(request.Headers, MsSignatureHeader).Split(' ')[1];
            var signatureAlgorithm = GetHeaderValue(request.Headers, SignatureAlgorithmHeader);
            var certificateUrl = GetHeaderValue(request.Headers, CertificateUrlHeader);
            var certificate = await GetCertificate(certificateUrl);
            var content = await GetContentAsync(request);
            var alg = signatureAlgorithm.Split('-'); // for example RSA-SHA1
            var isValid = false;

            var logger = GetLoggerIfAvailable(request);

            // Validate the certificate
            VerifyCertificate(certificate, request, logger);

            if (alg.Length == 2 && alg[0].Equals("RSA", StringComparison.OrdinalIgnoreCase))
            {
                var signature = Convert.FromBase64String(base64Signature);
                var csp = (RSACryptoServiceProvider)certificate.PublicKey.Key;

                var encoding = new UTF8Encoding();
                var data = encoding.GetBytes(content);

                var hashAlgorithm = alg[1].ToUpper();

                isValid = csp.VerifyData(data, CryptoConfig.MapNameToOID(hashAlgorithm), signature);
            }

            if (!isValid)
            {
                // log that we were not able to validate the signature
                logger?.TrackTrace(
                    "Failed to validate signature for webhook callback",
                    new Dictionary<string, string> { { "base64Signature", base64Signature }, { "certificateUrl", certificateUrl }, { "signatureAlgorithm", signatureAlgorithm }, { "content", content } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Signature verification failed"));
            }
        }

        private static ILogger GetLoggerIfAvailable(HttpRequestMessage request)
        {
            return request.GetDependencyScope().GetService(typeof(ILogger)) as ILogger;
        }

        private static async Task<X509Certificate2> GetCertificate(string certificateUrl)
        {
            byte[] certBytes;
            using (var webClient = new WebClient())
            {
                certBytes = await webClient.DownloadDataTaskAsync(certificateUrl);
            }

            return new X509Certificate2(certBytes);
        }

        private static void VerifyCertificate(X509Certificate2 certificate, HttpRequestMessage request, ILogger logger)
        {
            if (!certificate.Verify())
            {
                logger?.TrackTrace("Failed to verify certificate for webhook callback.", new Dictionary<string, string> { { "Subject", certificate.Subject }, { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Certificate verification failed."));
            }

            if (!certificate.Issuer.Contains(MicrosoftCorporationIssuer))
            {
                logger?.TrackTrace($"Certificate not issued by {MicrosoftCorporationIssuer}.", new Dictionary<string, string> { { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Certificate not issued by {MicrosoftCorporationIssuer}."));
            }
        }
    }
}
```
