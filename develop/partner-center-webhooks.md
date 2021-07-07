---
title: Webhooky Partnerského centra
description: Webhooky umožňují partnerům registrovat události změny prostředků.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 74d5981436ba29ea4f6f93a5693ec6da82777eb4
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547729"
---
# <a name="partner-center-webhooks"></a><span data-ttu-id="bcc79-103">Webhooky Partnerského centra</span><span class="sxs-lookup"><span data-stu-id="bcc79-103">Partner Center webhooks</span></span>

<span data-ttu-id="bcc79-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="bcc79-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bcc79-105">Rozhraní API Partnerské centrum webhooku umožňují partnerům registrovat události změny prostředků.</span><span class="sxs-lookup"><span data-stu-id="bcc79-105">The Partner Center Webhook APIs allow partners to register for resource change events.</span></span> <span data-ttu-id="bcc79-106">Tyto události se doručí do registrované adresy URL partnera ve formě požadavků HTTP.</span><span class="sxs-lookup"><span data-stu-id="bcc79-106">These events are delivered in the form of HTTP POSTs to the partner's registered URL.</span></span> <span data-ttu-id="bcc79-107">Aby partneři mohli přijímat události Partnerské centrum, budou hostovat zpětné volání, Partnerské centrum může událost změny prostředku POST.</span><span class="sxs-lookup"><span data-stu-id="bcc79-107">To receive an event from Partner Center, partners will host a callback where Partner Center can POST the resource change event.</span></span> <span data-ttu-id="bcc79-108">Událost bude digitálně podepsaná, aby partner mohl ověřit, že se odeslala z Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="bcc79-108">The event will be digitally signed so that the partner can verify that it was sent from Partner Center.</span></span>

<span data-ttu-id="bcc79-109">Partneři si mohou vybrat z událostí webhooku, jako jsou následující příklady, které podporuje Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="bcc79-109">Partners can select from Webhook events, like the following examples, that are supported by Partner Center.</span></span>

- <span data-ttu-id="bcc79-110">**Testovací událost ("test-created")**</span><span class="sxs-lookup"><span data-stu-id="bcc79-110">**Test Event ("test-created")**</span></span>

    <span data-ttu-id="bcc79-111">Tato událost vám umožní registraci sama onboardovat a otestovat tak, že si vyžádáte testovací událost a pak budete sledovat její průběh.</span><span class="sxs-lookup"><span data-stu-id="bcc79-111">This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress.</span></span> <span data-ttu-id="bcc79-112">Uvidíte zprávy o selhání, které microsoft přijímá při pokusu o doručení události.</span><span class="sxs-lookup"><span data-stu-id="bcc79-112">You can see the failure messages that are being received from Microsoft while trying to deliver the event.</span></span> <span data-ttu-id="bcc79-113">Toto omezení se vztahuje pouze na události vytvořené testem.</span><span class="sxs-lookup"><span data-stu-id="bcc79-113">This restriction only applies to "test-created" events.</span></span> <span data-ttu-id="bcc79-114">Data starší než sedm dnů se vyprázdní.</span><span class="sxs-lookup"><span data-stu-id="bcc79-114">Data older than seven days will be purged.</span></span>

- <span data-ttu-id="bcc79-115">**Událost aktualizace předplatného (aktualizace předplatného)**</span><span class="sxs-lookup"><span data-stu-id="bcc79-115">**Subscription Updated Event ("subscription-updated")**</span></span>

    <span data-ttu-id="bcc79-116">Tato událost se vyvolala při změně předplatného.</span><span class="sxs-lookup"><span data-stu-id="bcc79-116">This event is raised when the subscription changes.</span></span> <span data-ttu-id="bcc79-117">Tyto události se vygenerují v případě, že dojde k interní změně kromě toho, že se změny provádí prostřednictvím Partnerské centrum API.</span><span class="sxs-lookup"><span data-stu-id="bcc79-117">These events will be generated when there is an internal change in addition to when changes are made through the Partner Center API.</span></span>

    >[!NOTE]
    ><span data-ttu-id="bcc79-118">Mezi změnou předplatného a aktivací události Aktualizace předplatného je zpoždění až 48 hodin.</span><span class="sxs-lookup"><span data-stu-id="bcc79-118">There is a delay of up to 48 hours between the time a subscription changes and when the Subscription Updated event is triggered.</span></span>

- <span data-ttu-id="bcc79-119">**Událost překročení prahové hodnoty (usagerecords-thresholdExceeded)**</span><span class="sxs-lookup"><span data-stu-id="bcc79-119">**Threshold Exceeded Event ("usagerecords-thresholdExceeded")**</span></span>

    <span data-ttu-id="bcc79-120">Tato událost se nastane, když výše Microsoft Azure využití u všech zákazníků překročí rozpočet útraty za využití (jejich prahovou hodnotu).</span><span class="sxs-lookup"><span data-stu-id="bcc79-120">This event is raised when the amount of Microsoft Azure usage for any customer exceeds their usage spending budget (their threshold).</span></span> <span data-ttu-id="bcc79-121">Další informace najdete v tématu [Nastavení rozpočtu útraty Azure pro zákazníky/partnerské centrum/set-an-azure-spending-budget-for-your-customers).</span><span class="sxs-lookup"><span data-stu-id="bcc79-121">For more information, see  [Set an Azure spending budget for your customers/partner-center/set-an-azure-spending-budget-for-your-customers).</span></span>

- <span data-ttu-id="bcc79-122">**Událost vytvoření referenčního seznamu ("vytvoření referenčního seznamu")**</span><span class="sxs-lookup"><span data-stu-id="bcc79-122">**Referral Created Event ("referral-created")**</span></span>

    <span data-ttu-id="bcc79-123">Tato událost se vyvolala při vytvoření referenčního odkazu.</span><span class="sxs-lookup"><span data-stu-id="bcc79-123">This event is raised when the referral is created.</span></span>

- <span data-ttu-id="bcc79-124">**Aktualizovaná událost referenčního seznamu (aktualizace referenčních seznamu)**</span><span class="sxs-lookup"><span data-stu-id="bcc79-124">**Referral Updated Event ("referral-updated")**</span></span>

    <span data-ttu-id="bcc79-125">Tato událost se vyvolala při aktualizaci referenčního odkazu.</span><span class="sxs-lookup"><span data-stu-id="bcc79-125">This event is raised when the referral is updated.</span></span>

- <span data-ttu-id="bcc79-126">**Událost připravenou na fakturu (připravenou k fakturaci)**</span><span class="sxs-lookup"><span data-stu-id="bcc79-126">**Invoice Ready Event ("invoice-ready")**</span></span>

    <span data-ttu-id="bcc79-127">Tato událost se vyvolala, když je nová faktura připravená.</span><span class="sxs-lookup"><span data-stu-id="bcc79-127">This event is raised when the new invoice is ready.</span></span>

<span data-ttu-id="bcc79-128">Budoucí události webhooku budou přidány pro prostředky, které se mění v systému, nad který partner nemá kontrolu, a budou provedeny další aktualizace, aby se tyto události dostaly co nejvíce do "v reálném čase".</span><span class="sxs-lookup"><span data-stu-id="bcc79-128">Future Webhook events will be added for resources that change in the system that the partner isn't in control of, and further updates will be made to get those events as close to "real time" as possible.</span></span> <span data-ttu-id="bcc79-129">Názory partnerů na to, které události přidávají do své firmy přidanou hodnotu, budou užitečné při určování nových událostí, které se mají přidat.</span><span class="sxs-lookup"><span data-stu-id="bcc79-129">Feedback from Partners on which events add value to their business will be useful in determining what new events to add.</span></span>

<span data-ttu-id="bcc79-130">Úplný seznam událostí webhooku podporovaných webhookem podporovaných Partnerské centrum najdete [v Partnerské centrum událostí webhooku.](partner-center-webhook-events.md)</span><span class="sxs-lookup"><span data-stu-id="bcc79-130">For a complete list of Webhook events supported by Partner Center, see [Partner Center webhook events](partner-center-webhook-events.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bcc79-131">Požadavky</span><span class="sxs-lookup"><span data-stu-id="bcc79-131">Prerequisites</span></span>

- <span data-ttu-id="bcc79-132">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="bcc79-132">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bcc79-133">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="bcc79-133">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="receiving-events-from-partner-center"></a><span data-ttu-id="bcc79-134">Příjem událostí z Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="bcc79-134">Receiving events from Partner Center</span></span>

<span data-ttu-id="bcc79-135">Pokud chcete přijímat události Partnerské centrum, musíte zveřejnit veřejně přístupný koncový bod.</span><span class="sxs-lookup"><span data-stu-id="bcc79-135">To receive events from Partner Center, you must expose a publicly accessible endpoint.</span></span> <span data-ttu-id="bcc79-136">Vzhledem k tomu, že je tento koncový bod vystavený, musíte ověřit, že komunikace pochází z Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="bcc79-136">Because this endpoint is exposed, you must validate that the communication is from Partner Center.</span></span> <span data-ttu-id="bcc79-137">Všechny události webhooku, které obdržíte, jsou digitálně podepsané certifikátem, který se zřetězuje s kořenem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="bcc79-137">All Webhook events that you receive are digitally signed with a certificate that chains to the Microsoft Root.</span></span> <span data-ttu-id="bcc79-138">Bude také poskytnut odkaz na certifikát použitý k podepsání události.</span><span class="sxs-lookup"><span data-stu-id="bcc79-138">A link to the certificate used to sign the event will also be provided.</span></span> <span data-ttu-id="bcc79-139">To umožní obnovení certifikátu bez nutnosti opětovného nasazení nebo překonfigurování služby.</span><span class="sxs-lookup"><span data-stu-id="bcc79-139">This will allow the certificate to be renewed without you having to redeploy or reconfigure your service.</span></span> <span data-ttu-id="bcc79-140">Partnerské centrum 10 pokusů o doručení události.</span><span class="sxs-lookup"><span data-stu-id="bcc79-140">Partner Center will make 10 attempts to deliver the event.</span></span> <span data-ttu-id="bcc79-141">Pokud se událost ani po 10 pokusech doručí, přesune se do offline fronty a žádné další pokusy nebudou provedeny při doručení.</span><span class="sxs-lookup"><span data-stu-id="bcc79-141">If the event is still not delivered after 10 attempts, it will be moved into an offline queue and no further attempts will be made at delivery.</span></span>

<span data-ttu-id="bcc79-142">Následující příklad ukazuje událost z webu Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="bcc79-142">The following sample shows an event posted from Partner Center.</span></span>

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
><span data-ttu-id="bcc79-143">Autorizační hlavička má schéma Podpis.</span><span class="sxs-lookup"><span data-stu-id="bcc79-143">The Authorization header has a scheme of "Signature".</span></span> <span data-ttu-id="bcc79-144">Jedná se o signaturu obsahu s kódováním Base64.</span><span class="sxs-lookup"><span data-stu-id="bcc79-144">This is a base64 encoded signature of the content.</span></span>

## <a name="how-to-authenticate-the-callback"></a><span data-ttu-id="bcc79-145">Ověření zpětného volání</span><span class="sxs-lookup"><span data-stu-id="bcc79-145">How to authenticate the callback</span></span>

<span data-ttu-id="bcc79-146">Pokud chcete ověřit událost zpětného volání přijatou z Partnerské centrum, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="bcc79-146">To authenticate the callback event received from Partner Center, follow these steps:</span></span>

1. <span data-ttu-id="bcc79-147">Ověřte, že jsou k dispozici požadované hlavičky (Authorization, x-ms-certificate-url, x-ms-signature-algorithm).</span><span class="sxs-lookup"><span data-stu-id="bcc79-147">Verify the required headers are present (Authorization, x-ms-certificate-url, x-ms-signature-algorithm).</span></span>

2. <span data-ttu-id="bcc79-148">Stáhněte si certifikát použitý k podepsání obsahu (x-ms-certificate-url).</span><span class="sxs-lookup"><span data-stu-id="bcc79-148">Download the certificate used to sign the content (x-ms-certificate-url).</span></span>

3. <span data-ttu-id="bcc79-149">Ověřte řetěz certifikátů.</span><span class="sxs-lookup"><span data-stu-id="bcc79-149">Verify the Certificate Chain.</span></span>

4. <span data-ttu-id="bcc79-150">Ověřte organizaci certifikátu.</span><span class="sxs-lookup"><span data-stu-id="bcc79-150">Verify the "Organization" of the certificate.</span></span>

5. <span data-ttu-id="bcc79-151">Načtěte obsah s kódováním UTF8 do vyrovnávací paměti.</span><span class="sxs-lookup"><span data-stu-id="bcc79-151">Read the content with UTF8 encoding into a buffer.</span></span>

6. <span data-ttu-id="bcc79-152">Vytvořte zprostředkovatele kryptografických služeb RSA.</span><span class="sxs-lookup"><span data-stu-id="bcc79-152">Create an RSA Crypto Provider.</span></span>

7. <span data-ttu-id="bcc79-153">Ověřte, že data odpovídají tomu, co bylo podepsáno zadaným hashovacím algoritmem (například SHA256).</span><span class="sxs-lookup"><span data-stu-id="bcc79-153">Verify the data matches what was signed with the specified hash algorithm (for example SHA256).</span></span>

8. <span data-ttu-id="bcc79-154">Pokud ověření proběhne úspěšně, zpracujte zprávu.</span><span class="sxs-lookup"><span data-stu-id="bcc79-154">If the verification succeeds, process the message.</span></span>

> [!NOTE]
> <span data-ttu-id="bcc79-155">Ve výchozím nastavení se token podpisu odesílá v autorizační hlavičce.</span><span class="sxs-lookup"><span data-stu-id="bcc79-155">By default, the signature token will be sent in an Authorization header.</span></span> <span data-ttu-id="bcc79-156">Pokud ve své registraci nastavíte **SignatureTokenToMsSignatureHeader** na true, token podpisu se místo toho odesílá v hlavičce x-ms-signature.</span><span class="sxs-lookup"><span data-stu-id="bcc79-156">If you set **SignatureTokenToMsSignatureHeader** to true in your registration, the signature token will be sent in the x-ms-signature header instead.</span></span>

## <a name="event-model"></a><span data-ttu-id="bcc79-157">Model událostí</span><span class="sxs-lookup"><span data-stu-id="bcc79-157">Event model</span></span>

<span data-ttu-id="bcc79-158">Následující tabulka popisuje vlastnosti události Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="bcc79-158">The following table describes the properties of a Partner Center event.</span></span>

### <a name="properties"></a><span data-ttu-id="bcc79-159">Vlastnosti</span><span class="sxs-lookup"><span data-stu-id="bcc79-159">Properties</span></span>

| <span data-ttu-id="bcc79-160">Název</span><span class="sxs-lookup"><span data-stu-id="bcc79-160">Name</span></span>                      | <span data-ttu-id="bcc79-161">Description</span><span class="sxs-lookup"><span data-stu-id="bcc79-161">Description</span></span>                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="bcc79-162">**EventName**</span><span class="sxs-lookup"><span data-stu-id="bcc79-162">**EventName**</span></span>             | <span data-ttu-id="bcc79-163">Název události.</span><span class="sxs-lookup"><span data-stu-id="bcc79-163">The name of the event.</span></span> <span data-ttu-id="bcc79-164">Ve tvaru {resource}-{action}.</span><span class="sxs-lookup"><span data-stu-id="bcc79-164">In the form {resource}-{action}.</span></span> <span data-ttu-id="bcc79-165">Například "test-created".</span><span class="sxs-lookup"><span data-stu-id="bcc79-165">For example, "test-created".</span></span>  |
| <span data-ttu-id="bcc79-166">**Identifikátor URI prostředku**</span><span class="sxs-lookup"><span data-stu-id="bcc79-166">**ResourceUri**</span></span>           | <span data-ttu-id="bcc79-167">Identifikátor URI prostředku, který se změnil.</span><span class="sxs-lookup"><span data-stu-id="bcc79-167">The URI of the resource that changed.</span></span>                                                 |
| <span data-ttu-id="bcc79-168">**Název prostředku**</span><span class="sxs-lookup"><span data-stu-id="bcc79-168">**ResourceName**</span></span>          | <span data-ttu-id="bcc79-169">Název prostředku, který se změnil.</span><span class="sxs-lookup"><span data-stu-id="bcc79-169">The name of the resource that changed.</span></span>                                                |
| <span data-ttu-id="bcc79-170">**AuditUrl**</span><span class="sxs-lookup"><span data-stu-id="bcc79-170">**AuditUrl**</span></span>              | <span data-ttu-id="bcc79-171">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="bcc79-171">Optional.</span></span> <span data-ttu-id="bcc79-172">Identifikátor URI záznamu Auditu.</span><span class="sxs-lookup"><span data-stu-id="bcc79-172">The URI of the Audit record.</span></span>                                                |
| <span data-ttu-id="bcc79-173">**ResourceChangeUtcDate**</span><span class="sxs-lookup"><span data-stu-id="bcc79-173">**ResourceChangeUtcDate**</span></span> | <span data-ttu-id="bcc79-174">Datum a čas ve formátu UTC, kdy došlo ke změně prostředku</span><span class="sxs-lookup"><span data-stu-id="bcc79-174">The date and time, in UTC format, when the resource change occurred.</span></span>                  |

### <a name="sample"></a><span data-ttu-id="bcc79-175">Ukázka</span><span class="sxs-lookup"><span data-stu-id="bcc79-175">Sample</span></span>

<span data-ttu-id="bcc79-176">Následující příklad ukazuje strukturu události Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="bcc79-176">The following sample shows the structure of a Partner Center event.</span></span>

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a><span data-ttu-id="bcc79-177">Rozhraní API webhooků</span><span class="sxs-lookup"><span data-stu-id="bcc79-177">Webhook APIs</span></span>

### <a name="authentication"></a><span data-ttu-id="bcc79-178">Authentication</span><span class="sxs-lookup"><span data-stu-id="bcc79-178">Authentication</span></span>

<span data-ttu-id="bcc79-179">Všechna volání rozhraní API webhooku se ověřují pomocí tokenu Bearer v autorizační hlavičce.</span><span class="sxs-lookup"><span data-stu-id="bcc79-179">All calls to the Webhook APIs are authenticated using the Bearer token in the Authorization Header.</span></span> <span data-ttu-id="bcc79-180">Získání přístupového tokenu pro přístup k `https://api.partnercenter.microsoft.com` .</span><span class="sxs-lookup"><span data-stu-id="bcc79-180">Acquire an access token to access `https://api.partnercenter.microsoft.com`.</span></span> <span data-ttu-id="bcc79-181">Tento token je stejný token, který se používá pro přístup ke zbývajícím Partnerské centrum API.</span><span class="sxs-lookup"><span data-stu-id="bcc79-181">This token is the same token that is used to access the rest of the Partner Center APIs.</span></span>

### <a name="get-a-list-of-events"></a><span data-ttu-id="bcc79-182">Získání seznamu událostí</span><span class="sxs-lookup"><span data-stu-id="bcc79-182">Get a list of events</span></span>

<span data-ttu-id="bcc79-183">Vrátí seznam událostí, které jsou aktuálně podporovány rozhraními API webhooku.</span><span class="sxs-lookup"><span data-stu-id="bcc79-183">Returns a list of the events that are currently supported by the Webhook APIs.</span></span>

### <a name="resource-url"></a><span data-ttu-id="bcc79-184">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="bcc79-184">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a><span data-ttu-id="bcc79-185">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="bcc79-185">Request example</span></span>

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="bcc79-186">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="bcc79-186">Response example</span></span>

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

### <a name="register-to-receive-events"></a><span data-ttu-id="bcc79-187">Registrace pro příjem událostí</span><span class="sxs-lookup"><span data-stu-id="bcc79-187">Register to receive events</span></span>

<span data-ttu-id="bcc79-188">Zaregistruje tenanta pro příjem zadaných událostí.</span><span class="sxs-lookup"><span data-stu-id="bcc79-188">Registers a tenant to receive the specified events.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="bcc79-189">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="bcc79-189">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="bcc79-190">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="bcc79-190">Request example</span></span>

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

### <a name="response-example"></a><span data-ttu-id="bcc79-191">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="bcc79-191">Response example</span></span>

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

### <a name="view-a-registration"></a><span data-ttu-id="bcc79-192">Zobrazení registrace</span><span class="sxs-lookup"><span data-stu-id="bcc79-192">View a registration</span></span>

<span data-ttu-id="bcc79-193">Vrátí registraci události webhooků pro tenanta.</span><span class="sxs-lookup"><span data-stu-id="bcc79-193">Returns the Webhooks event registration for a tenant.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="bcc79-194">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="bcc79-194">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="bcc79-195">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="bcc79-195">Request example</span></span>

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="bcc79-196">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="bcc79-196">Response example</span></span>

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

### <a name="update-an-event-registration"></a><span data-ttu-id="bcc79-197">Aktualizace registrace události</span><span class="sxs-lookup"><span data-stu-id="bcc79-197">Update an event registration</span></span>

<span data-ttu-id="bcc79-198">Aktualizuje existující registraci události.</span><span class="sxs-lookup"><span data-stu-id="bcc79-198">Updates an existing event registration.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="bcc79-199">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="bcc79-199">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="bcc79-200">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="bcc79-200">Request example</span></span>

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

### <a name="response-example"></a><span data-ttu-id="bcc79-201">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="bcc79-201">Response example</span></span>

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

### <a name="send-a-test-event-to-validate-your-registration"></a><span data-ttu-id="bcc79-202">Odeslat testovací událost pro ověření vaší registrace</span><span class="sxs-lookup"><span data-stu-id="bcc79-202">Send a test event to validate your registration</span></span>

<span data-ttu-id="bcc79-203">Vygeneruje testovací událost pro ověření registrace webhooků.</span><span class="sxs-lookup"><span data-stu-id="bcc79-203">Generates a test event to validate the Webhooks registration.</span></span> <span data-ttu-id="bcc79-204">Tento test je určen k ověření, že můžete přijímat události z partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="bcc79-204">This test is intended to validate that you can receive events from Partner Center.</span></span> <span data-ttu-id="bcc79-205">Data pro tyto události budou odstraněna sedm dní od vytvoření počáteční události.</span><span class="sxs-lookup"><span data-stu-id="bcc79-205">Data for these events will be deleted seven days after the initial event is created.</span></span> <span data-ttu-id="bcc79-206">Před odesláním události ověření musíte být registrováni pro událost vytvářenou pomocí registračního rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="bcc79-206">You must be registered for the "test-created" event, using the registration API, before sending a validation event.</span></span>

>[!NOTE]
><span data-ttu-id="bcc79-207">Při odesílání události ověření existuje omezení počtu 2 požadavků za minutu.</span><span class="sxs-lookup"><span data-stu-id="bcc79-207">There is a throttle limit of 2 requests per minute when posting a validation event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="bcc79-208">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="bcc79-208">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a><span data-ttu-id="bcc79-209">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="bcc79-209">Request example</span></span>

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a><span data-ttu-id="bcc79-210">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="bcc79-210">Response example</span></span>

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

### <a name="verify-that-the-event-was-delivered"></a><span data-ttu-id="bcc79-211">Ověření doručení události</span><span class="sxs-lookup"><span data-stu-id="bcc79-211">Verify that the event was delivered</span></span>

<span data-ttu-id="bcc79-212">Vrátí aktuální stav události ověření.</span><span class="sxs-lookup"><span data-stu-id="bcc79-212">Returns the current state of the validation event.</span></span> <span data-ttu-id="bcc79-213">Toto ověření může být užitečné při řešení problémů s doručováním událostí.</span><span class="sxs-lookup"><span data-stu-id="bcc79-213">This verification can be helpful for troubleshooting event delivery issues.</span></span> <span data-ttu-id="bcc79-214">Odpověď obsahuje výsledek pro každý pokus, který je proveden pro doručení události.</span><span class="sxs-lookup"><span data-stu-id="bcc79-214">The Response contains a result for each attempt that is made to deliver the event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="bcc79-215">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="bcc79-215">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a><span data-ttu-id="bcc79-216">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="bcc79-216">Request example</span></span>

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="bcc79-217">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="bcc79-217">Response example</span></span>

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

## <a name="example-for-signature-validation"></a><span data-ttu-id="bcc79-218">Příklad pro ověřování podpisů</span><span class="sxs-lookup"><span data-stu-id="bcc79-218">Example for Signature Validation</span></span>

### <a name="sample-callback-controller-signature-aspnet"></a><span data-ttu-id="bcc79-219">Ukázkový podpis kontroleru zpětného volání (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="bcc79-219">Sample Callback Controller signature (ASP.NET)</span></span>

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a><span data-ttu-id="bcc79-220">Ověření podpisu</span><span class="sxs-lookup"><span data-stu-id="bcc79-220">Signature Validation</span></span>

<span data-ttu-id="bcc79-221">Následující příklad ukazuje, jak přidat autorizační atribut do kontroleru, který přijímá zpětná volání z událostí Webhooku.</span><span class="sxs-lookup"><span data-stu-id="bcc79-221">The following example shows how to add an Authorization Attribute to the controller that is receiving callbacks from Webhook events.</span></span>

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
