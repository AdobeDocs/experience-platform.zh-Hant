---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；測量；資料型別；資料型別；
solution: Experience Platform
title: 測量資料型別
description: 瞭解測量體驗資料模型(XDM)資料型別。
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 5%

---

# [!UICONTROL 量值]資料型別

[!UICONTROL Measure]是標準的Experience Data Model (XDM)資料型別，包含特定量度的具體可量化資料點。 測量由唯一識別碼和值組成。

![量值影像](../images/data-types/measure.PNG){width=500}

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `id` | 字串 | 此測量的唯一識別碼。 如果使用有損通訊通道（例如無法確保傳輸測量之行動應用程式或具有離線功能的網站）進行資料收集時，此屬性會包含使用者端產生的唯一測量識別碼。 最佳實務是維持足夠長的時間，以確保足夠的隨機性。 <br><br>如果時間戳記、裝置ID、IP、MAC位址或其他潛在的使用者識別值等資訊合併到`id`的產生中，則結果應進行雜湊處理。 這可確保值中不會編碼PII，因為目標不是識別使用者或裝置，而是及時識別特定測量。 |
| `value` | 雙精度 | 此測量可數量化的值。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
