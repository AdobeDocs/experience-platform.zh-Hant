---
title: 提供者類別
description: 瞭解Experience Data Model (XDM)中的Provider類別。
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 4%

---

# [!UICONTROL 提供者] 類別

在Experience Data Model (XDM)中， [!UICONTROL 提供者] class會擷取定義提供者業務實體（例如醫療保健提供者或保險提供者）的最低屬性集。

![類別結構](../images/classes/provider.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `providerName` | [[!UICONTROL 個人名稱]](../data-types/person-name.md) | 提供者的名稱。 |
| `_id` | [!UICONTROL 字串] | 記錄的唯一、系統產生的字串識別碼。 此欄位用於追蹤個別記錄的唯一性、防止資料重複，以及在下游服務中查詢該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會提供明確的值。 不過，您仍然可以視需要選擇提供自己的唯一ID值。 |
| `providerId` | [!UICONTROL 字串] | 提供者的唯一識別碼。 |

{style="table-layout:auto"}

可以使用來擴充類別 [[!UICONTROL 醫療保健提供者] 欄位群組](../field-groups/provider/healthcare-provider.md) 以說明關於醫療保健提供者的進一步詳細資訊。
