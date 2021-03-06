---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；測量；資料類型；資料類型；
solution: Experience Platform
title: 測量資料類型
topic-legacy: overview
description: 本檔案概述測量體驗資料模型(XDM)資料類型。
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---

#  測量資料類型

 測量是標準的體驗資料模型(XDM)資料類型，包含特定量度的具體可量化資料點。度量由唯一標識符和值組成。

<img src="../images/data-types/measure.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `id` | 字串 | 此度量的唯一標識符。 在使用有損通信通道（如移動應用或具有離線功能的網站）收集資料時，如果無法確保測量的傳輸，則此屬性包含由客戶端生成、所採取測量的唯一ID。 最好讓這一時間足夠長，以確保足夠的隨機性。 <br><br> 如果在產生時納入時間戳、裝置ID、IP、MAC位址或其他潛在使用者識別值等資訊，則 `id`應雜湊結果。這可確保值中不會有PII編碼，因為目標不是要識別使用者或裝置，而是要及時識別特定測量。 |
| `value` | 雙倍 | 此度量的可量化值。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
