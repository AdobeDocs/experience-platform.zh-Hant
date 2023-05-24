---
keywords: Experience Platform；首頁；資料科學工作區；熱門主題；訪問控制；沙盒；智慧包；dsw功能；dsw訪問；Adobe Experience Platform智慧；智慧；aep智慧包
solution: Experience Platform
title: Data Science工作區訪問和功能
description: 以下文檔概述了Data Science Workspace權限和對功能的訪問。
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# Data Science工作區訪問和功能

以下文檔概述了Data Science Workspace權限和對功能的訪問。

![DSW頁籤](./images/access/platform-tabs.png)

- **筆記本：** 提供互動式開發環境([朱佩特拉布](./jupyterlab/overview.md))以瀏覽、分析和建模您的資料，以Experience Platform。
- **型號：** 提供用於建立、發佈和儲存高級機器學習配方和模型的工具。 有關詳細資訊，請訪問 [建立和發佈機器學習模型](./models-recipes/create-publish-model.md) 教程。
- **服務：** 包含Adobe提供的服務，如 [AI/ML服務](../intelligent-services/home.md) 以及您使用Data Science Workspace建立的任何自定義服務。

為什麼我只看到「服務」頁籤？

- 您的組織可能只有權獲得Adobe Real-time Customer Data Platform(Real-Time CDP)，其中包括客戶AI/ML服務。

如果您無法看到 **資料科學** 頁籤，並希望利用Data Science Workspace功能，請聯繫您的公司管理員以檢查您是否擁有Adobe Experience Platform智慧許可證。

## Data Science Workspace打包

Data Science Workspace功能可在Adobe Experience Platform智慧包和高級智慧包附件中找到

下表概述了Data Science Workspace Erviles（包含和不包含Advanced Intelligence Pack附加項）的一些主要區別：

>[!NOTE]
>
>您可以授權多個高級智慧包附加，並且增加的容量將添加到您的總體權利中。 例如，如果您授權2個Adobe Experience Platform高級智慧包地址，則您總共有20個併發筆記本用戶。

| 資料科學工作區權利 | 僅Adobe Experience Platform情報包 | Adobe Experience Platform智慧加高級智慧包附件 |
| --- | :---: | :---: |
| 支援的筆記本用戶數。 | 5個併發用戶 | 第一個包添加了5個併發用戶，另外購買的每個包添加10個併發用戶。 |
| 允許整合Jupyter筆記本進行探索性資料分析和模型創作。 | X（支援R、Python和Scala庫） | X（添加PySpark和Spark ML庫） |
| 與查詢服務的本機整合。 能夠在筆記本中使用SQL來瀏覽和塑造資料集。 | X | X |
| 訪問預構建的筆記本模板以進行預測分析。 | X | X |
| 使用Jupyter筆記本手動培訓和評分模型。 | X | X |
| 部署和操作能夠安排培訓和推薦作業的模型。 |  | X |
| 配方框架，可輕鬆配置、評估、培訓、評分並將模型發佈到生產中。 |  | X |
| UI驅動的模型實驗和評估。 |  | X |
| 對Tensorflow模型（GPU計算）的深度學習支援。 |  | X |
| 基於Spark的分佈式計算，可對大資料集（10MM +行）進行訓練和評分。 |  | X |

## 存取控制

Experience Platform的訪問控制通過 [Adobe Admin Console](https://adminconsole.adobe.com)。 此功能利用Admin Console中的產品配置檔案，將用戶與權限和沙箱連結起來。 查看 [訪問控制概述](../access-control/home.md) 的子菜單。

要使用Data Science Workspace，必須啟用「管理Data Science Workspace」權限。 下表概述了啟用或禁用此權限的效果：

| 權限 | 啟用 | 停用 |
|---|---|---|
| 管理資料科學工作區 | 提供對Data Science Workspace中所有服務的訪問。 | 禁用了對Data Science Workspace中所有服務的API和UI訪問。 禁用時，選擇 **筆記本**。 **模型**, **服務** 頁面被阻止。 <li>訪問 **服務** 仍可通過Adobe Real-time Customer Data Platform(Real-Time CDP)獲得。</li> |

## 沙盒支援

沙箱是單個Experience Platform實例中的虛擬分區。 每個平台實例支援多個生產和非生產沙盒，每個沙盒都維護自己的平台資源庫。 非生產沙箱允許您test功能、運行實驗和制定定制配置，而不影響生產沙箱。 有關沙箱的詳細資訊，請參閱 [箱概述](../sandboxes/home.md)。

目前，Data Science Workspace具有以下沙盒限制：

- 計算資源在生產和非生產沙箱之間共用。

## 後續步驟

本文檔概述了Data Science Workspace中提供的不同訪問類型和功能。

要瞭解有關Data Science Workspace（如完整的日常工作流）的更多資訊，請首先閱讀 [Data Science Workspace漫遊](./walkthrough.md) 文檔。 有關更多一般資訊，請訪問 [資料科學工作區概述](./home.md)。
