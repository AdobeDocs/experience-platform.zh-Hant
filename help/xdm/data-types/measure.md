---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields；模式；Schemas;measure;datatype；資料類型；
solution: Experience Platform
title: 測量資料類型
topic-legacy: overview
description: 本檔案提供測量體驗資料模型(XDM)資料類型的概述。
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 1%

---

# [!UICONTROL Measure] 資料類型

[!UICONTROL Measure] 是標準的「體驗資料模型」(XDM)資料類型，包含特定量度的具體可量化資料點。度量由唯一標識符和值組成。

<img src="../images/data-types/measure.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `id` | 字串 | 此度量的唯一識別碼。 在使用有損通訊頻道（例如行動應用程式或具有離線功能的網站）收集資料時，無法確保測量的傳輸，此屬性包含用戶端產生、採用測量的唯一ID。 最好的做法是讓這種時間足夠長，以確保足夠的隨機性。 <br><br> 如果在生成時包含時間戳、設備ID、IP、MAC地址或其他潛在用戶標識值等資訊 `id`，則應雜湊結果。這可確保PII不會編碼在值中，因為目標不是識別使用者或裝置，而是及時識別特定度量。 |
| `value` | 雙倍 | 此度量的可量化價值。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
