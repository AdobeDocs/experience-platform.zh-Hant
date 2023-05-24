---
keywords: Experience Platform；主題；熱門主題；模式；模式；XDM；欄位；模式；模式；度量；資料類型；資料類型；資料類型；
solution: Experience Platform
title: 度量資料類型
description: 本文檔概述了度量體驗資料模型(XDM)資料類型。
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 1%

---

# [!UICONTROL 度量] 資料類型

[!UICONTROL 度量] 是標準的體驗資料模型(XDM)資料類型，它包含特定度量的具體可量化資料點。 度量由唯一標識符和值組成。

<img src="../images/data-types/measure.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `id` | 字串 | 此度量的唯一標識符。 在使用有損通信通道（如移動應用或具有離線功能的網站）收集資料的情況下，如果無法確保測量的傳輸，則此屬性包含客戶端生成的所採用測量的唯一ID。 最佳做法是，讓這一時間足夠長，以確保足夠的隨機性。 <br><br> 如果在生成時包含諸如時間戳、設備ID、IP、MAC地址或其他潛在用戶標識值之類的資訊 `id`，應對結果進行散列。 這可確保在值中不編碼PII，因為目標不是標識用戶或設備，而是及時確定特定度量。 |
| `value` | 雙倍 | 此度量的可量化值。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
