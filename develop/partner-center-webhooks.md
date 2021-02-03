---
title: Webhooky Partnerského centra
description: Webhooky umožňují partnerům registrovat se na události změny prostředků.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 8225623ade7e922ac23ebf0ed9215686b0601244
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766826"
---
# <a name="partner-center-webhooks"></a><span data-ttu-id="753ab-103">Webhooky Partnerského centra</span><span class="sxs-lookup"><span data-stu-id="753ab-103">Partner Center webhooks</span></span>

<span data-ttu-id="753ab-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="753ab-104">**Applies To**</span></span>

- <span data-ttu-id="753ab-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="753ab-105">Partner Center</span></span>
- <span data-ttu-id="753ab-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="753ab-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="753ab-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="753ab-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="753ab-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="753ab-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="753ab-109">Rozhraní API Webhooku partnerského centra umožňují partnerům registrovat se na události změny prostředků.</span><span class="sxs-lookup"><span data-stu-id="753ab-109">The Partner Center Webhook APIs allow partners to register for resource change events.</span></span> <span data-ttu-id="753ab-110">Tyto události se doručí ve formě příspěvků HTTP na registrovanou adresu URL partnera.</span><span class="sxs-lookup"><span data-stu-id="753ab-110">These events are delivered in the form of HTTP POSTs to the partner's registered URL.</span></span> <span data-ttu-id="753ab-111">Aby partneři mohli získat událost z partnerského centra, bude hostovat zpětné volání, které může partnerské Centrum publikovat událost změny prostředku.</span><span class="sxs-lookup"><span data-stu-id="753ab-111">To receive an event from Partner Center, partners will host a callback where Partner Center can POST the resource change event.</span></span> <span data-ttu-id="753ab-112">Událost bude digitálně podepsaná, aby partner mohl ověřit, že byla odeslána z partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="753ab-112">The event will be digitally signed so that the partner can verify that it was sent from Partner Center.</span></span>

<span data-ttu-id="753ab-113">Partneři můžou vybírat z událostí Webhooku, jako jsou následující příklady, které jsou podporované partnerským centrem.</span><span class="sxs-lookup"><span data-stu-id="753ab-113">Partners can select from Webhook events, like the following examples, that are supported by Partner Center.</span></span>

- <span data-ttu-id="753ab-114">**Testovací událost ("test-Created")**</span><span class="sxs-lookup"><span data-stu-id="753ab-114">**Test Event ("test-created")**</span></span>

    <span data-ttu-id="753ab-115">Tato událost umožňuje samoobslužné zprovoznění a testování registrace tím, že požaduje testovací událost a pak sleduje jeho průběh.</span><span class="sxs-lookup"><span data-stu-id="753ab-115">This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress.</span></span> <span data-ttu-id="753ab-116">Při pokusu o doručení události můžete zobrazit zprávy o chybách, které jsou přijímány od společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="753ab-116">You can see the failure messages that are being received from Microsoft while trying to deliver the event.</span></span> <span data-ttu-id="753ab-117">Toto omezení se vztahuje pouze na události "vytvořené testem".</span><span class="sxs-lookup"><span data-stu-id="753ab-117">This restriction only applies to "test-created" events.</span></span> <span data-ttu-id="753ab-118">Data starší než sedm dní se vyprázdní.</span><span class="sxs-lookup"><span data-stu-id="753ab-118">Data older than seven days will be purged.</span></span>

- <span data-ttu-id="753ab-119">**Událost aktualizace předplatného (předplatné-Aktualizováno)**</span><span class="sxs-lookup"><span data-stu-id="753ab-119">**Subscription Updated Event ("subscription-updated")**</span></span>

    <span data-ttu-id="753ab-120">Tato událost se vyvolá při změně předplatného.</span><span class="sxs-lookup"><span data-stu-id="753ab-120">This event is raised when the subscription changes.</span></span> <span data-ttu-id="753ab-121">Tyto události budou vygenerovány v případě, že dojde k vnitřní změně kromě změny prostřednictvím rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="753ab-121">These events will be generated when there is an internal change in addition to when changes are made through the Partner Center API.</span></span>

    >[!NOTE]
    ><span data-ttu-id="753ab-122">Mezi časem změny předplatného a aktivací události aktualizace předplatného dojde k prodlevě až 48 hodin.</span><span class="sxs-lookup"><span data-stu-id="753ab-122">There is a delay of up to 48 hours between the time a subscription changes and when the Subscription Updated event is triggered.</span></span>

- <span data-ttu-id="753ab-123">**Událost překročení prahové hodnoty ("usagerecords-thresholdExceeded")**</span><span class="sxs-lookup"><span data-stu-id="753ab-123">**Threshold Exceeded Event ("usagerecords-thresholdExceeded")**</span></span>

    <span data-ttu-id="753ab-124">Tato událost se vyvolá v případě, že množství využití Microsoft Azure pro každého zákazníka přesáhne rozpočet výdajů na využití (jejich prahovou hodnotu).</span><span class="sxs-lookup"><span data-stu-id="753ab-124">This event is raised when the amount of Microsoft Azure usage for any customer exceeds their usage spending budget (their threshold).</span></span> <span data-ttu-id="753ab-125">Další informace najdete v tématu [nastavení rozpočtu útraty Azure pro vaše zákazníky/partnery – Center/set-a-Azure-útraty-rozpočet-pro zákazníky).</span><span class="sxs-lookup"><span data-stu-id="753ab-125">For more information, see  [Set an Azure spending budget for your customers/partner-center/set-an-azure-spending-budget-for-your-customers).</span></span>

- <span data-ttu-id="753ab-126">**Událost vytvořená odkazem (odkaz – vytvořeno)**</span><span class="sxs-lookup"><span data-stu-id="753ab-126">**Referral Created Event ("referral-created")**</span></span>

    <span data-ttu-id="753ab-127">Tato událost je aktivována při vytvoření odkazu.</span><span class="sxs-lookup"><span data-stu-id="753ab-127">This event is raised when the referral is created.</span></span>

- <span data-ttu-id="753ab-128">**Událost aktualizovaného odkazu (odkaz-Aktualizováno)**</span><span class="sxs-lookup"><span data-stu-id="753ab-128">**Referral Updated Event ("referral-updated")**</span></span>

    <span data-ttu-id="753ab-129">Tato událost je aktivována při aktualizaci odkazu.</span><span class="sxs-lookup"><span data-stu-id="753ab-129">This event is raised when the referral is updated.</span></span>

- <span data-ttu-id="753ab-130">**Událost připravena k faktuře ("faktura-připravena")**</span><span class="sxs-lookup"><span data-stu-id="753ab-130">**Invoice Ready Event ("invoice-ready")**</span></span>

    <span data-ttu-id="753ab-131">Tato událost se vyvolá, když je nová faktura připravena.</span><span class="sxs-lookup"><span data-stu-id="753ab-131">This event is raised when the new invoice is ready.</span></span>

<span data-ttu-id="753ab-132">Další události Webhooku se přidají pro prostředky, které se změní v systému, který partner neovládá, a provede se další aktualizace, aby se tyto události dostaly co nejblíže "reálnému času".</span><span class="sxs-lookup"><span data-stu-id="753ab-132">Future Webhook events will be added for resources that change in the system that the partner isn't in control of, and further updates will be made to get those events as close to "real time" as possible.</span></span> <span data-ttu-id="753ab-133">Názory partnerů, na kterých události přidávají hodnotu do jejich podnikání, budou užitečné při určování nových událostí, které se mají přidat.</span><span class="sxs-lookup"><span data-stu-id="753ab-133">Feedback from Partners on which events add value to their business will be useful in determining what new events to add.</span></span>

<span data-ttu-id="753ab-134">Úplný seznam událostí Webhooku podporovaných partnerským centrem najdete v tématu [události Webhooku partnerského centra](partner-center-webhook-events.md).</span><span class="sxs-lookup"><span data-stu-id="753ab-134">For a complete list of Webhook events supported by Partner Center, see [Partner Center webhook events](partner-center-webhook-events.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="753ab-135">Požadavky</span><span class="sxs-lookup"><span data-stu-id="753ab-135">Prerequisites</span></span>

- <span data-ttu-id="753ab-136">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="753ab-136">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="753ab-137">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="753ab-137">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="receiving-events-from-partner-center"></a><span data-ttu-id="753ab-138">Příjem událostí z partnerského centra</span><span class="sxs-lookup"><span data-stu-id="753ab-138">Receiving events from Partner Center</span></span>

<span data-ttu-id="753ab-139">Pokud chcete přijímat události z partnerského centra, musíte zveřejnit veřejně přístupný koncový bod.</span><span class="sxs-lookup"><span data-stu-id="753ab-139">To receive events from Partner Center, you must expose a publicly accessible endpoint.</span></span> <span data-ttu-id="753ab-140">Vzhledem k tomu, že je tento koncový bod vystavený, musíte ověřit, jestli je komunikace z partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="753ab-140">Because this endpoint is exposed, you must validate that the communication is from Partner Center.</span></span> <span data-ttu-id="753ab-141">Všechny události Webhooku, které jste obdrželi, jsou digitálně podepsané certifikátem, který je zřetězený do kořenového adresáře společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="753ab-141">All Webhook events that you receive are digitally signed with a certificate that chains to the Microsoft Root.</span></span> <span data-ttu-id="753ab-142">Bude také k dispozici odkaz na certifikát použitý k podepsání události.</span><span class="sxs-lookup"><span data-stu-id="753ab-142">A link to the certificate used to sign the event will also be provided.</span></span> <span data-ttu-id="753ab-143">Tím umožníte prodloužení platnosti certifikátu, aniž byste museli službu znovu nasazovat nebo překonfigurovat.</span><span class="sxs-lookup"><span data-stu-id="753ab-143">This will allow the certificate to be renewed without you having to redeploy or reconfigure your service.</span></span> <span data-ttu-id="753ab-144">Partnerským centrem se 10 pokusí o doručení události.</span><span class="sxs-lookup"><span data-stu-id="753ab-144">Partner Center will make 10 attempts to deliver the event.</span></span> <span data-ttu-id="753ab-145">Pokud se událost ještě doručí po 10 pokusech, přesune se do offline fronty a žádné další pokusy se neuskuteční při doručení.</span><span class="sxs-lookup"><span data-stu-id="753ab-145">If the event is still not delivered after 10 attempts, it will be moved into an offline queue and no further attempts will be made at delivery.</span></span>

<span data-ttu-id="753ab-146">Následující ukázka ukazuje událost zveřejněnou z partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="753ab-146">The following sample shows an event posted from Partner Center.</span></span>

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
><span data-ttu-id="753ab-147">Autorizační hlavička má schéma "signatura".</span><span class="sxs-lookup"><span data-stu-id="753ab-147">The Authorization header has a scheme of "Signature".</span></span> <span data-ttu-id="753ab-148">Toto je signatura s kódováním base64 obsahu.</span><span class="sxs-lookup"><span data-stu-id="753ab-148">This is a base64 encoded signature of the content.</span></span>

## <a name="how-to-authenticate-the-callback"></a><span data-ttu-id="753ab-149">Ověření zpětného volání</span><span class="sxs-lookup"><span data-stu-id="753ab-149">How to authenticate the callback</span></span>

<span data-ttu-id="753ab-150">K ověření události zpětného volání přijatého z partnerského centra použijte následující postup:</span><span class="sxs-lookup"><span data-stu-id="753ab-150">To authenticate the callback event received from Partner Center, follow these steps:</span></span>

1. <span data-ttu-id="753ab-151">Ověřte, zda jsou k dispozici požadovaná záhlaví (autorizace, x-MS-Certificate-URL, x-MS-Signature-Algorithm).</span><span class="sxs-lookup"><span data-stu-id="753ab-151">Verify the required headers are present (Authorization, x-ms-certificate-url, x-ms-signature-algorithm).</span></span>

2. <span data-ttu-id="753ab-152">Stáhněte si certifikát použitý k podepsání obsahu (x-MS-Certificate-URL).</span><span class="sxs-lookup"><span data-stu-id="753ab-152">Download the certificate used to sign the content (x-ms-certificate-url).</span></span>

3. <span data-ttu-id="753ab-153">Ověřte řetěz certifikátů.</span><span class="sxs-lookup"><span data-stu-id="753ab-153">Verify the Certificate Chain.</span></span>

4. <span data-ttu-id="753ab-154">Ověřte "organizaci" certifikátu.</span><span class="sxs-lookup"><span data-stu-id="753ab-154">Verify the "Organization" of the certificate.</span></span>

5. <span data-ttu-id="753ab-155">Přečtěte si obsah s kódováním UTF8 do vyrovnávací paměti.</span><span class="sxs-lookup"><span data-stu-id="753ab-155">Read the content with UTF8 encoding into a buffer.</span></span>

6. <span data-ttu-id="753ab-156">Vytvořte poskytovatele kryptografických služeb RSA.</span><span class="sxs-lookup"><span data-stu-id="753ab-156">Create an RSA Crypto Provider.</span></span>

7. <span data-ttu-id="753ab-157">Ověřte, že data odpovídají údajům, které byly podepsány zadaným algoritmem hash (například SHA256).</span><span class="sxs-lookup"><span data-stu-id="753ab-157">Verify the data matches what was signed with the specified hash algorithm (for example SHA256).</span></span>

8. <span data-ttu-id="753ab-158">Pokud je ověření úspěšné, zpracujte zprávu.</span><span class="sxs-lookup"><span data-stu-id="753ab-158">If the verification succeeds, process the message.</span></span>

> [!NOTE]
> <span data-ttu-id="753ab-159">Ve výchozím nastavení se token podpisu pošle v autorizační hlavičce.</span><span class="sxs-lookup"><span data-stu-id="753ab-159">By default, the signature token will be sent in an Authorization header.</span></span> <span data-ttu-id="753ab-160">Pokud jste v registraci nastavili **SignatureTokenToMsSignatureHeader** na hodnotu true, token podpisu se místo toho pošle v hlavičce x-MS-Signature.</span><span class="sxs-lookup"><span data-stu-id="753ab-160">If you set **SignatureTokenToMsSignatureHeader** to true in your registration, the signature token will be sent in the x-ms-signature header instead.</span></span>

## <a name="event-model"></a><span data-ttu-id="753ab-161">Model událostí</span><span class="sxs-lookup"><span data-stu-id="753ab-161">Event model</span></span>

<span data-ttu-id="753ab-162">Následující tabulka popisuje vlastnosti události partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="753ab-162">The following table describes the properties of a Partner Center event.</span></span>

### <a name="properties"></a><span data-ttu-id="753ab-163">Vlastnosti</span><span class="sxs-lookup"><span data-stu-id="753ab-163">Properties</span></span>

| <span data-ttu-id="753ab-164">Název</span><span class="sxs-lookup"><span data-stu-id="753ab-164">Name</span></span>                      | <span data-ttu-id="753ab-165">Description</span><span class="sxs-lookup"><span data-stu-id="753ab-165">Description</span></span>                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="753ab-166">**EventName**</span><span class="sxs-lookup"><span data-stu-id="753ab-166">**EventName**</span></span>             | <span data-ttu-id="753ab-167">Název události.</span><span class="sxs-lookup"><span data-stu-id="753ab-167">The name of the event.</span></span> <span data-ttu-id="753ab-168">Ve formátu {Resource} – {Action}.</span><span class="sxs-lookup"><span data-stu-id="753ab-168">In the form {resource}-{action}.</span></span> <span data-ttu-id="753ab-169">Například "test-Created".</span><span class="sxs-lookup"><span data-stu-id="753ab-169">For example, "test-created".</span></span>  |
| <span data-ttu-id="753ab-170">**ResourceUri**</span><span class="sxs-lookup"><span data-stu-id="753ab-170">**ResourceUri**</span></span>           | <span data-ttu-id="753ab-171">Identifikátor URI prostředku, který se změnil.</span><span class="sxs-lookup"><span data-stu-id="753ab-171">The URI of the resource that changed.</span></span>                                                 |
| <span data-ttu-id="753ab-172">**ResourceName**</span><span class="sxs-lookup"><span data-stu-id="753ab-172">**ResourceName**</span></span>          | <span data-ttu-id="753ab-173">Název prostředku, který se změnil.</span><span class="sxs-lookup"><span data-stu-id="753ab-173">The name of the resource that changed.</span></span>                                                |
| <span data-ttu-id="753ab-174">**AuditUrl**</span><span class="sxs-lookup"><span data-stu-id="753ab-174">**AuditUrl**</span></span>              | <span data-ttu-id="753ab-175">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="753ab-175">Optional.</span></span> <span data-ttu-id="753ab-176">Identifikátor URI záznamu auditu</span><span class="sxs-lookup"><span data-stu-id="753ab-176">The URI of the Audit record.</span></span>                                                |
| <span data-ttu-id="753ab-177">**ResourceChangeUtcDate**</span><span class="sxs-lookup"><span data-stu-id="753ab-177">**ResourceChangeUtcDate**</span></span> | <span data-ttu-id="753ab-178">Datum a čas ve formátu UTC, kdy došlo ke změně prostředků.</span><span class="sxs-lookup"><span data-stu-id="753ab-178">The date and time, in UTC format, when the resource change occurred.</span></span>                  |

### <a name="sample"></a><span data-ttu-id="753ab-179">Ukázka</span><span class="sxs-lookup"><span data-stu-id="753ab-179">Sample</span></span>

<span data-ttu-id="753ab-180">Následující příklad ukazuje strukturu události partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="753ab-180">The following sample shows the structure of a Partner Center event.</span></span>

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a><span data-ttu-id="753ab-181">Rozhraní API Webhooku</span><span class="sxs-lookup"><span data-stu-id="753ab-181">Webhook APIs</span></span>

### <a name="authentication"></a><span data-ttu-id="753ab-182">Authentication</span><span class="sxs-lookup"><span data-stu-id="753ab-182">Authentication</span></span>

<span data-ttu-id="753ab-183">Všechna volání rozhraní API Webhooku se ověřují pomocí nosných tokenů v autorizační hlavičce.</span><span class="sxs-lookup"><span data-stu-id="753ab-183">All calls to the Webhook APIs are authenticated using the Bearer token in the Authorization Header.</span></span> <span data-ttu-id="753ab-184">Získání přístupového tokenu pro přístup `https://api.partnercenter.microsoft.com` .</span><span class="sxs-lookup"><span data-stu-id="753ab-184">Acquire an access token to access `https://api.partnercenter.microsoft.com`.</span></span> <span data-ttu-id="753ab-185">Tento token je stejný token, který se používá pro přístup ke zbytkům rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="753ab-185">This token is the same token that is used to access the rest of the Partner Center APIs.</span></span>

### <a name="get-a-list-of-events"></a><span data-ttu-id="753ab-186">Získat seznam událostí</span><span class="sxs-lookup"><span data-stu-id="753ab-186">Get a list of events</span></span>

<span data-ttu-id="753ab-187">Vrátí seznam událostí, které jsou aktuálně podporovány rozhraními API Webhooku.</span><span class="sxs-lookup"><span data-stu-id="753ab-187">Returns a list of the events that are currently supported by the Webhook APIs.</span></span>

### <a name="resource-url"></a><span data-ttu-id="753ab-188">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="753ab-188">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a><span data-ttu-id="753ab-189">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="753ab-189">Request example</span></span>

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="753ab-190">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="753ab-190">Response example</span></span>

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

### <a name="register-to-receive-events"></a><span data-ttu-id="753ab-191">Registrace pro příjem událostí</span><span class="sxs-lookup"><span data-stu-id="753ab-191">Register to receive events</span></span>

<span data-ttu-id="753ab-192">Zaregistruje tenanta pro příjem zadaných událostí.</span><span class="sxs-lookup"><span data-stu-id="753ab-192">Registers a tenant to receive the specified events.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="753ab-193">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="753ab-193">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="753ab-194">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="753ab-194">Request example</span></span>

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

### <a name="response-example"></a><span data-ttu-id="753ab-195">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="753ab-195">Response example</span></span>

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

### <a name="view-a-registration"></a><span data-ttu-id="753ab-196">Zobrazit registraci</span><span class="sxs-lookup"><span data-stu-id="753ab-196">View a registration</span></span>

<span data-ttu-id="753ab-197">Vrátí registraci události webhooků pro tenanta.</span><span class="sxs-lookup"><span data-stu-id="753ab-197">Returns the Webhooks event registration for a tenant.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="753ab-198">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="753ab-198">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="753ab-199">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="753ab-199">Request example</span></span>

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="753ab-200">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="753ab-200">Response example</span></span>

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

### <a name="update-an-event-registration"></a><span data-ttu-id="753ab-201">Aktualizace registrace události</span><span class="sxs-lookup"><span data-stu-id="753ab-201">Update an event registration</span></span>

<span data-ttu-id="753ab-202">Aktualizuje existující registraci události.</span><span class="sxs-lookup"><span data-stu-id="753ab-202">Updates an existing event registration.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="753ab-203">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="753ab-203">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="753ab-204">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="753ab-204">Request example</span></span>

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

### <a name="response-example"></a><span data-ttu-id="753ab-205">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="753ab-205">Response example</span></span>

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

### <a name="send-a-test-event-to-validate-your-registration"></a><span data-ttu-id="753ab-206">Odeslat testovací událost pro ověření vaší registrace</span><span class="sxs-lookup"><span data-stu-id="753ab-206">Send a test event to validate your registration</span></span>

<span data-ttu-id="753ab-207">Vygeneruje testovací událost pro ověření registrace webhooků.</span><span class="sxs-lookup"><span data-stu-id="753ab-207">Generates a test event to validate the Webhooks registration.</span></span> <span data-ttu-id="753ab-208">Tento test je určen k ověření, že můžete přijímat události z partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="753ab-208">This test is intended to validate that you can receive events from Partner Center.</span></span> <span data-ttu-id="753ab-209">Data pro tyto události budou odstraněna sedm dní od vytvoření počáteční události.</span><span class="sxs-lookup"><span data-stu-id="753ab-209">Data for these events will be deleted seven days after the initial event is created.</span></span> <span data-ttu-id="753ab-210">Před odesláním události ověření musíte být registrováni pro událost vytvářenou pomocí registračního rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="753ab-210">You must be registered for the "test-created" event, using the registration API, before sending a validation event.</span></span>

>[!NOTE]
><span data-ttu-id="753ab-211">Při odesílání události ověření existuje omezení počtu 2 požadavků za minutu.</span><span class="sxs-lookup"><span data-stu-id="753ab-211">There is a throttle limit of 2 requests per minute when posting a validation event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="753ab-212">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="753ab-212">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a><span data-ttu-id="753ab-213">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="753ab-213">Request example</span></span>

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a><span data-ttu-id="753ab-214">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="753ab-214">Response example</span></span>

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

### <a name="verify-that-the-event-was-delivered"></a><span data-ttu-id="753ab-215">Ověření doručení události</span><span class="sxs-lookup"><span data-stu-id="753ab-215">Verify that the event was delivered</span></span>

<span data-ttu-id="753ab-216">Vrátí aktuální stav události ověření.</span><span class="sxs-lookup"><span data-stu-id="753ab-216">Returns the current state of the validation event.</span></span> <span data-ttu-id="753ab-217">Toto ověření může být užitečné při řešení problémů s doručováním událostí.</span><span class="sxs-lookup"><span data-stu-id="753ab-217">This verification can be helpful for troubleshooting event delivery issues.</span></span> <span data-ttu-id="753ab-218">Odpověď obsahuje výsledek pro každý pokus, který je proveden pro doručení události.</span><span class="sxs-lookup"><span data-stu-id="753ab-218">The Response contains a result for each attempt that is made to deliver the event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="753ab-219">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="753ab-219">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a><span data-ttu-id="753ab-220">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="753ab-220">Request example</span></span>

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="753ab-221">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="753ab-221">Response example</span></span>

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

## <a name="example-for-signature-validation"></a><span data-ttu-id="753ab-222">Příklad pro ověřování podpisů</span><span class="sxs-lookup"><span data-stu-id="753ab-222">Example for Signature Validation</span></span>

### <a name="sample-callback-controller-signature-aspnet"></a><span data-ttu-id="753ab-223">Ukázkový podpis kontroleru zpětného volání (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="753ab-223">Sample Callback Controller signature (ASP.NET)</span></span>

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a><span data-ttu-id="753ab-224">Ověření podpisu</span><span class="sxs-lookup"><span data-stu-id="753ab-224">Signature Validation</span></span>

<span data-ttu-id="753ab-225">Následující příklad ukazuje, jak přidat autorizační atribut do kontroleru, který přijímá zpětná volání z událostí Webhooku.</span><span class="sxs-lookup"><span data-stu-id="753ab-225">The following example shows how to add an Authorization Attribute to the controller that is receiving callbacks from Webhook events.</span></span>

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
