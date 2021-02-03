---
title: Prostředky vztahů
description: Popisuje prostředky vztahující se k relacím.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c5701414bd704b375dc23859b920609d5a975d9f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766710"
---
# <a name="relationships-resources"></a><span data-ttu-id="2c8d5-103">Prostředky vztahů</span><span class="sxs-lookup"><span data-stu-id="2c8d5-103">Relationships resources</span></span>

<span data-ttu-id="2c8d5-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="2c8d5-104">**Applies To**</span></span>

- <span data-ttu-id="2c8d5-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="2c8d5-105">Partner Center</span></span>

<span data-ttu-id="2c8d5-106">Popisuje prostředky vztahující se k relacím.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-106">Describes resources related to relationships.</span></span>

## <a name="partnerrelationship"></a><span data-ttu-id="2c8d5-107">PartnerRelationship</span><span class="sxs-lookup"><span data-stu-id="2c8d5-107">PartnerRelationship</span></span>

<span data-ttu-id="2c8d5-108">Představuje vztah mezi dvěma partnery.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-108">Represents a relationship between two partners.</span></span>

| <span data-ttu-id="2c8d5-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="2c8d5-109">Property</span></span>         | <span data-ttu-id="2c8d5-110">Typ</span><span class="sxs-lookup"><span data-stu-id="2c8d5-110">Type</span></span>                                                           | <span data-ttu-id="2c8d5-111">Description</span><span class="sxs-lookup"><span data-stu-id="2c8d5-111">Description</span></span>                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2c8d5-112">id</span><span class="sxs-lookup"><span data-stu-id="2c8d5-112">id</span></span>               | <span data-ttu-id="2c8d5-113">řetězec</span><span class="sxs-lookup"><span data-stu-id="2c8d5-113">string</span></span>                                                         | <span data-ttu-id="2c8d5-114">Identifikátor partnera</span><span class="sxs-lookup"><span data-stu-id="2c8d5-114">The partner identifier.</span></span> <span data-ttu-id="2c8d5-115">Identifikátor partnera určuje ID tenanta partnera, který je na straně příjemce (od) vztahu.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-115">The partner identifier specifies the tenant id of the partner who is in the recipient (from) side of the relationship.</span></span> |
| <span data-ttu-id="2c8d5-116">location</span><span class="sxs-lookup"><span data-stu-id="2c8d5-116">location</span></span>         | <span data-ttu-id="2c8d5-117">řetězec</span><span class="sxs-lookup"><span data-stu-id="2c8d5-117">string</span></span>                                                         | <span data-ttu-id="2c8d5-118">Umístění partnera.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-118">The location of the partner.</span></span>                                                                                                                   |
| <span data-ttu-id="2c8d5-119">mpnId</span><span class="sxs-lookup"><span data-stu-id="2c8d5-119">mpnId</span></span>            | <span data-ttu-id="2c8d5-120">řetězec</span><span class="sxs-lookup"><span data-stu-id="2c8d5-120">string</span></span>                                                         | <span data-ttu-id="2c8d5-121">Identifikátor Microsoft Partner Network (MPN) partnera.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-121">The Microsoft Partner Network (MPN) identifier of the partner.</span></span>                                                                                 |
| <span data-ttu-id="2c8d5-122">name</span><span class="sxs-lookup"><span data-stu-id="2c8d5-122">name</span></span>             | <span data-ttu-id="2c8d5-123">řetězec</span><span class="sxs-lookup"><span data-stu-id="2c8d5-123">string</span></span>                                                         | <span data-ttu-id="2c8d5-124">Název partnera.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-124">The name of the partner.</span></span>                                                                                                                       |
| <span data-ttu-id="2c8d5-125">Element</span><span class="sxs-lookup"><span data-stu-id="2c8d5-125">relationshipType</span></span> | <span data-ttu-id="2c8d5-126">řetězec</span><span class="sxs-lookup"><span data-stu-id="2c8d5-126">string</span></span>                                                         | <span data-ttu-id="2c8d5-127">Typ relace.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-127">The type of relationship.</span></span>                                                                                                                      |
| <span data-ttu-id="2c8d5-128">state</span><span class="sxs-lookup"><span data-stu-id="2c8d5-128">state</span></span>            | <span data-ttu-id="2c8d5-129">řetězec</span><span class="sxs-lookup"><span data-stu-id="2c8d5-129">string</span></span>                                                         | <span data-ttu-id="2c8d5-130">Stav relace (například `active` ).</span><span class="sxs-lookup"><span data-stu-id="2c8d5-130">The state of the relationship (for example `active`).</span></span>                                                                                                 |
| <span data-ttu-id="2c8d5-131">atributy</span><span class="sxs-lookup"><span data-stu-id="2c8d5-131">attributes</span></span>       | [<span data-ttu-id="2c8d5-132">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="2c8d5-132">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="2c8d5-133">Atributy metadat.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-133">The metadata attributes.</span></span>                                                                                                                       |

## <a name="relationshiprequest"></a><span data-ttu-id="2c8d5-134">RelationshipRequest</span><span class="sxs-lookup"><span data-stu-id="2c8d5-134">RelationshipRequest</span></span>

<span data-ttu-id="2c8d5-135">Poskytuje adresu URL, pomocí které může zákazník vytvořit relaci s partnerem.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-135">Provides the URL by which a customer can establish a relationship with a partner.</span></span>

| <span data-ttu-id="2c8d5-136">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="2c8d5-136">Property</span></span>   | <span data-ttu-id="2c8d5-137">Typ</span><span class="sxs-lookup"><span data-stu-id="2c8d5-137">Type</span></span>                                                           | <span data-ttu-id="2c8d5-138">Description</span><span class="sxs-lookup"><span data-stu-id="2c8d5-138">Description</span></span>                   |
|------------|----------------------------------------------------------------|-------------------------------|
| <span data-ttu-id="2c8d5-139">url</span><span class="sxs-lookup"><span data-stu-id="2c8d5-139">url</span></span>        | <span data-ttu-id="2c8d5-140">řetězec</span><span class="sxs-lookup"><span data-stu-id="2c8d5-140">string</span></span>                                                         | <span data-ttu-id="2c8d5-141">Adresa URL požadavku vztahu</span><span class="sxs-lookup"><span data-stu-id="2c8d5-141">The relationship request URL.</span></span> |
| <span data-ttu-id="2c8d5-142">atributy</span><span class="sxs-lookup"><span data-stu-id="2c8d5-142">attributes</span></span> | [<span data-ttu-id="2c8d5-143">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="2c8d5-143">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="2c8d5-144">Atributy metadat.</span><span class="sxs-lookup"><span data-stu-id="2c8d5-144">The metadata attributes.</span></span>      |
