---
title: Auditování prostředků
description: Přečtěte si o prostředcích auditování rozhraní API partnerského centra, jako je AuditRecord, které můžete použít k získání záznamu o aktivitě partnerského centra.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9d78a305c2d27dc692c609e30817b34b1f814157
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974348"
---
# <a name="auditing-resources-that-help-you-get-a-record-of-partner-center-activity"></a>Auditování prostředků, které vám pomůžou získat záznam aktivity partnerského centra

S operacemi auditu můžete použít následující prostředky.

## <a name="auditrecord"></a>AuditRecord

Představuje záznam operace prováděné partnerem uživatele nebo aplikací.

| Vlastnost | Typ | Description |
| --- | --- | ---|
| customerId | řetězec | Řetězec ve formátu GUID, který identifikuje zákazníka. |
| customerName | řetězec | Jméno zákazníka. |
| userPrincipalName (Hlavní název uživatele) | řetězec | Hlavní název uživatele nebo identifikátor uživatele Obvykle se jedná o přihlašovací jméno ve stylu Internetu pro uživatele ve formátu e-mailové adresy na základě standardu RFC 822 pro Internet. |
| applicationId | řetězec | Řetězec, který identifikuje aplikaci, která provedla operaci. |
| resourceType | řetězec | Typ prostředku, na kterém operace rozhodla. Možné hodnoty: `customer` , `customer_user` , `order` , `subscription` , `license` , `third_party_add_on` , `mpn_association` , `transfer` , `application` , `application_credential` , `partner_user` , `partner_relationship` , `partner_customer_dap` , `customer_directory_role` . |
| resourceOldValue | řetězec | Stará hodnota prostředku |
| resourceNewValue | řetězec | Nová hodnota prostředku |
| operationType | řetězec | Typ provedené operace. Možné hodnoty: `update_customer_qualification` , `update_subscription` , `upgrade_subscription` , `convert_trial_subscription` , `add_customer` , `update_customer_billing_profile` , `update_customer_partner_contract_company_name` , `update_customer_spending_budget` , `delete_customer` (pouze účty integrace izolovaného prostoru), `remove_partner_customer_relationship` , `create_order` `update_order` `create_customer_user` `delete_customer_user` `update_customer_user` `update_customer_user_licenses` `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `create_self_serve_policy` `update_self_serve_policy` `create_self_serve_policy` `delete_self_serve_policy` `remove_partner_relationship` `delete_tip_customer` `create_related_referral` `update_related_referral` `create_referral` `update_referral` `get_software_key` `get_software_download_link` `increase_spending_limit` `ready_invoice` `create_agreement` `extend_relationship` `create_transfer` `dap_admin_relationship_approved` `dap_admin_relationship_terminated` `add_user_member` `remove_user_member` ,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,. |
| operationDate | řetězec ve formátu data a času standardu UTC | Datum a čas provedení operace. |
| Stav operationstatus | řetězec | Stav auditované operace. Možné hodnoty: `succeeded` , `failed` , nebo `progress` , což znamená, že operace stále probíhá. |
| customizedData  | pole objektů | Další informace. Každý objekt obsahuje dvě páry klíč-hodnota JSON: první je `key` a hodnota řetězce, druhá je `value` a hodnota řetězce. Počet objektů v poli závisí na typu operace, která byla provedena. |
| atributy | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat. |
