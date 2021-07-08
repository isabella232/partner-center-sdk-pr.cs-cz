---
title: Získání záznamů o využití Azure zákazníkem
description: Rozhraní API využití Azure můžete použít k získání záznamů o využití předplatného Azure zákazníka za zadané časové období.
ms.date: 04/19/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7024bc65976a9b43a62b66c529d271519181ab23
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874920"
---
# <a name="get-a-customers-utilization-records-for-azure"></a>Získání záznamů o využití Azure zákazníkem

**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Záznamy o využití předplatného Azure zákazníka můžete získat v zadaném časovém období pomocí rozhraní API využití Azure.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor předplatného.

Toto rozhraní API vrátí denní a hodinovou spotřebu nehodnoceného času pro libovolný časový rozsah. *Toto rozhraní API se ale pro plány Azure nepodporuje*. Pokud máte plán Azure, podívejte se na články [získat faktury za neúčtované řádky spotřeby](get-invoice-unbilled-consumption-lineitems.md) a místo toho [Získejte položky na řádcích spotřeby faktury](get-invoice-billed-consumption-lineitems.md) . Tyto články popisují, jak získat hodnocenou spotřebu na denní úrovni pro každý měřič na jeden prostředek. Tato spotřeba je rovnocenná datům denních zrn poskytovaných rozhraním API využití Azure. K načtení fakturovaných dat o využití budete muset použít identifikátor faktury. Nebo můžete použít aktuální a předchozí období k získání nefakturovaných odhadů využití. *Pro prostředky předplatného Azure Plan se v současné době nepodporují data s hodinovou zrnitou a libovolné filtry rozsahu kalendářních dat*.

## <a name="azure-utilization-api"></a>Rozhraní API využití Azure

Toto rozhraní API využití Azure poskytuje přístup k záznamům o využití za časové období, které představuje, kdy bylo využití oznámeno v systému fakturace. Poskytuje přístup ke stejným datům využití, která se používají k vytvoření a výpočtu souboru pro odsouhlasení. Nemá ale znalosti o logice souborů odsouhlasení systému fakturace. Neočekává se, že souhrn výsledků souborů sloučení nebude odpovídat výsledku načtenému z tohoto rozhraní API přesně za stejné časové období.

Například fakturační systém má stejná data o využití a pro určení toho, co se účtuje v souboru pro odsouhlasení, aplikují pravidla pro pozdě. Po uzavření fakturačního období bude veškeré využití až do konce dne, kdy se v souboru pro odsouhlasení zařadí fakturační období. Jakékoli pozdní využití v rámci fakturačního období, které se nahlásí během 24 hodin od konce fakturačního období, se účtuje v dalším souboru pro odsouhlasení. Pravidla pro pozdě, jak se partner účtuje, najdete v tématu [získání dat o spotřebě pro předplatné Azure](/previous-versions/azure/reference/mt219001(v=azure.100)).

Tato REST API jsou stránkovaná. Pokud je datová část odpovědi větší než jedna stránka, je nutné použít následující odkaz k získání další stránky záznamů o využití.

### <a name="scenario-partner-a-has-transferred-billing-ownership-of-azure-legacy-subscription-145p-to-partner-b"></a>Scénář: partner A převedl na partnera B vlastnictví fakturace předplatného Azure starší verze (145P).

Pokud partner přenese vlastnictví fakturace předplatného Azure staršího na jiného partnera, když nový partner rozhraní API pro přenesené předplatné zavolá, musí použít ID předplatného Commerce (které se zobrazí v účtu partnerského centra) místo ID nároku Azure. ID nároku Azure se zobrazuje pro partnera B jenom v případě, že se jedná o správce jménem (ADMINISTRATE) na Azure Portal zákazníka. 

K úspěšnému volání rozhraní API pro přenesené předplatné vyžaduje, aby nový partner používal ID předplatného Commerce.

## <a name="c"></a>C\#

Získání záznamů o využití Azure:

1. Získejte ID zákazníka a ID předplatného.

2. Voláním metody [**IAzureUtilizationCollection. Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) vrátíte [**resourcecollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) , která obsahuje záznamy o využití.

3. Získejte enumerátor záznamů využití Azure pro procházení stránek využití. Tento krok je povinný, protože kolekce prostředků je stránkovaná.

- **Ukázka**: [aplikace testů konzoly](console-test-app.md)
- **Project**: ukázky sady SDK pro partnerských Center
- **Třída**: GetAzureSubscriptionUtilization. cs

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    //
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pokud chcete získat záznamy o využití Azure, musíte nejdřív potřebovat identifikátor zákazníka a identifikátor předplatného. Potom zavolejte funkci **IAzureUtilizationCollection. Query** , která vrátí **zdrojovou** , která obsahuje záznamy o využití. Vzhledem k tomu, že je kolekce prostředků stránkovaná, musíte získat enumerátor záznamů využití Azure pro procházení stránek využití.

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1),
      new DateTime(),
      AzureUtilizationGranularity.Daily,
      true,
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator =
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    //
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pokud chcete získat záznamy o využití Azure, musíte nejdřív potřebovat identifikátor zákazníka a identifikátor předplatného. Pak zavolejte [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md). Tento příkaz vrátí všechny záznamy, které jsou k dispozici po určenou dobu.

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda | Identifikátor URI žádosti |
|------- | ----------- |
| **Čtěte** | *{baseURL}*/v1/Customers/{Customer-tenant-ID}/Subscriptions/{Subscription-ID}/utilizations/Azure? \_ čas spuštění = {start-time} &koncový \_ čas = {čas ukončení} &členitost = {členitost} &zobrazit \_ Podrobnosti = {true} |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

K získání záznamů o využití použijte následující cestu a parametry dotazu.

| Název | Typ | Vyžadováno | Popis |
| ---- | ---- | -------- | ----------- |
| Customer-tenant-ID | řetězec | Yes | Řetězec ve formátu GUID, který identifikuje zákazníka. |
| ID předplatného | řetězec | Yes | Řetězec ve formátu GUID, který identifikuje odběr. |
| start_time | řetězec ve formátu data a času UTC | Yes | Začátek časového rozsahu, který představuje, kdy bylo využití oznámeno v systému fakturace. |
| end_time | řetězec ve formátu data a času UTC | Yes | Konec časového rozsahu, který představuje, kdy bylo využití oznámeno v systému fakturace. |
| členitosti | řetězec | No | Definuje členitost agregací využití. Dostupné možnosti jsou: `daily` (výchozí) a `hourly` .
| show_details | boolean | No | Určuje, jestli se mají získat podrobnosti o využití na úrovni instance. Výchozí formát je `true`. |
| size | číslo | No | Určuje počet agregací vrácených jedním voláním rozhraní API. Výchozí hodnota je 1 000. Maximální hodnota je 1000. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádná

### <a name="request-example"></a>Příklad požadavku

Následující příklad žádosti vytvoří výsledek podobný tomu, co se soubor pro odsouhlasení zobrazí po dobu 7/2-8/1. Tyto výsledky se nemusí přesně shodovat (podrobnosti najdete v části [rozhraní API pro využití Azure](#azure-utilization-api) ).

Tento příklad žádosti vrátí data o využití uvedená v systému fakturace od 7/2 do 12:00 (UTC) a 8/2 ve 12:00 (UTC).

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí kolekci prostředků [záznamu využití Azure](azure-utilization-record-resources.md) v těle odpovědi. Pokud data o využití Azure ještě nejsou připravené v závislém systému, vrátí tato metoda stavový kód HTTP 204 s hlavičkou Retry-After.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Pomocí nástroje pro trasování sítě si přečtěte stavový kód HTTP, [typ kódu chyby](error-codes.md)a další parametry.

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&end_time=2017-07-09T00:00:00Z&granularity=Daily&show_details=True&size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```
