---
title: 提供程式類
description: 本檔案概述Experience Data Model(XDM)中的Provider類別。
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 2%

---

# [!UICONTROL 提供者] 類

在Experience Data Model(XDM)中， [!UICONTROL 提供者] 類捕獲定義提供商業務實體（如醫療保健提供商或保險提供商）的最小屬性集。

![類結構](../images/classes/provider.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `providerName` | [[!UICONTROL 人員名稱]](../data-types/person-name.md) | 提供程式的名稱。 |
| `_id` | [!UICONTROL 字串] | 記錄的唯一、系統生成的字串標識符。 此欄位用於追蹤個別記錄的獨特性、防止資料重複，以及在下游服務中尋找該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會提供明確值。 不過，您仍可以選擇提供您自己的唯一ID值（如果您想要的話）。 |
| `providerId` | [!UICONTROL 字串] | 提供程式的唯一標識符。 |

{style="table-layout:auto"}

可使用 [[!UICONTROL 醫療保健提供商] 欄位群組](../field-groups/provider/healthcare-provider.md) 介紹有關醫療保健提供商的更多詳細資訊。
