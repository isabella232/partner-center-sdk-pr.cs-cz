---
title: Auditování prostředků
description: Přečtěte si Partnerské centrum auditování rozhraní API, jako je Záznam Auditu, které můžete použít k získání záznamu o Partnerské centrum aktivitě.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 50c90f7e7a5dfb274044fafab87818c7ac8428124ca9072770cc5fd9fa3806d5
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994655"
---
# <a name="auditing-resources-that-help-you-get-a-record-of-partner-center-activity"></a>Auditování prostředků, které vám pomůžou získat záznam o Partnerské centrum aktivit

S operacemi auditu můžete použít následující prostředky.

## <a name="auditrecord"></a>Záznam auditu

Představuje záznam operace prováděné partnerským uživatelem nebo aplikací.

| Vlastnost | Typ | Description |
| --- | --- | ---|
| customerId | řetězec | Řetězec ve formátu GUID, který identifikuje zákazníka. |
| customerName | řetězec | Jméno zákazníka. |
| userPrincipalName (Hlavní název uživatele) | řetězec | Hlavní název uživatele nebo identifikátor uživatele. Tato vlastnost je obvykle přihlašovací jméno uživatele v internetovém stylu ve formátu e-mailové adresy založeném na internetovém standardu RFC 822. |
| applicationId | řetězec | Řetězec, který identifikuje aplikaci, která operaci provedla. |
| resourceType | řetězec | Typ prostředku, na který se operace chovala. Možné hodnoty: `customer` , , , , , , , , `customer_user` , , `order` , , , `subscription` , `license` `third_party_add_on` `mpn_association` `transfer` `application` `application_credential` `partner_user` `partner_relationship` `partner_customer_dap` `customer_directory_role` . |
| resourceOldValue | řetězec | Stará hodnota prostředku. |
| resourceNewValue | řetězec | Nová hodnota prostředku. |
| operationType | řetězec | Typ provedené operace. Možné hodnoty: , , , , , , , , (jenom účty integrace `update_customer_qualification` `update_subscription` `upgrade_subscription` `convert_trial_subscription` `add_customer` `update_customer_billing_profile` `update_customer_partner_contract_company_name` `update_customer_spending_budget` `delete_customer` sandboxu), `remove_partner_customer_relationship` , , , `create_order` `update_order` `create_customer_user` , `delete_customer_user` `update_customer_user` `update_customer_user_licenses` `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `create_self_serve_policy` `update_self_serve_policy` `create_self_serve_policy` `delete_self_serve_policy` `remove_partner_relationship` `delete_tip_customer` `create_related_referral` `update_related_referral` `create_referral` `update_referral` `get_software_key` `get_software_download_link` `increase_spending_limit` `ready_invoice` `create_agreement` `extend_relationship` `create_transfer` `dap_admin_relationship_approved` `dap_admin_relationship_terminated` `add_user_member` `remove_user_member` . |
| operationDate (datum operace) | řetězec ve formátu data a času UTC | Datum a čas provedení operace |
| stav operace | řetězec | Stav operace, která se audituje. Možné hodnoty: `succeeded` , nebo , což `failed` `progress` znamená, že operace stále probíhá. |
| přizpůsobená data  | pole objektů | Další informace. Každý objekt obsahuje dva páry klíč-hodnota JSON: první je a řetězcová hodnota, druhý `key` je `value` a řetězcová hodnota. Počet objektů v poli závisí na typu provedené operace. |
| atributy | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat. |
