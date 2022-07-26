---
title: 提供程式類
description: 本文檔概述了「體驗資料模型」(XDM)中的Provider類。
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 4%

---

# [!UICONTROL 提供程式] 類

在經驗資料模型(XDM)中， [!UICONTROL 提供程式] 類捕獲定義提供商業務實體（如醫療保健提供商或保險提供商）的最小屬性集。

![類結構](../images/classes/provider.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `providerName` | [[!UICONTROL 人員姓名]](../data-types/person-name.md) | 提供程式的名稱。 |
| `_id` | [!UICONTROL 字串] | 記錄的唯一系統生成的字串標識符。 此欄位用於跟蹤單個記錄的唯一性、防止重複資料以及在下游服務中查找該記錄。<br><br>由於此欄位是系統生成的，因此在資料接收期間不會提供顯式值。 但是，如果您願意，您仍然可以選擇提供您自己的唯一ID值。 |
| `providerId` | [!UICONTROL 字串] | 提供程式的唯一標識符。 |

{style=&quot;table-layout:auto&quot;}

類可與 [[!UICONTROL 醫療保健提供商] 欄位組](../field-groups/provider/healthcare-provider.md) 以詳細描述有關醫療保健提供商的詳細資訊。
