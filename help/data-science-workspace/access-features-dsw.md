---
keywords: Experience Platform；首頁；Data Science Workspace；熱門主題；存取控制；沙箱；智慧套件；dsw功能；DSW存取；Adobe Experience Platform Intelligence；智慧；aep智慧套件
solution: Experience Platform
title: Data Science Workspace存取與功能
topic-legacy: Access and features for data science workspace
description: 以下檔案概述Data Science Workspace權限和功能存取權。
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 319cdb13c965010062aa9179b197d6f5b6a20287
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 2%

---

# Data Science Workspace存取與功能

以下檔案概述Data Science Workspace權限和功能存取權。

![DSW頁簽](./images/access/platform-tabs.png)

- **筆記型電腦：** 提供互動式開發環境([JupyterLab](./jupyterlab/overview.md))，以探索、分析和模型您的Experience Platform資料。
- **模型：** 提供用來建立、發佈和儲存進階機器學習方式和模型的工具。如需詳細資訊，請造訪[建立並發佈機器學習模型](./models-recipes/create-publish-model.md)教學課程。
- **服務：** 包含Adobe提供的服務(例如AI/ [ML服](../intelligent-services/home.md) 務)，以及您透過Data Science Workspace建立的任何自訂服務。

為什麼我只看到「服務」標籤？

- 貴組織只能使用包含Customer AI/ML服務的即時客戶資料平台(RTCDP)。

如果您看不到任何&#x200B;**Data Science**&#x200B;標籤，並想利用Data Science Workspace功能，請聯絡您的公司管理員以檢查您是否擁有Adobe Experience Platform Intelligence授權。

## Data Science Workspace封裝

Adobe Experience Platform Intelligence套件和Advanced Intelligence Pack附加元件中提供Data Science Workspace功能

下表概述了Data Science Workspace使用權限（包含和不包含Advanced Intelligence Pack附加元件）的一些主要差異：

>[!NOTE]
>
>您可以授權多個Advanced Intelligence Pack Addon，且增加的容量會新增至您的整體權益。 例如，如果您授權2個Adobe Experience Platform Advanced Intelligence Pack Addons，則您有權同時擁有20個筆記型電腦使用者。

| Data Science Workspace權限 | 僅Adobe Experience Platform Intelligence Package | Adobe Experience Platform Intelligence Plus Advanced Intelligence Pack附加元件 |
| --- | :---: | :---: |
| 支援的筆記型電腦用戶數。 | 5個同時使用者 | First Pack新增5名同時使用者，另外還有額外購買，每個套件新增10名同時使用者。 |
| 允許整合的Jupyter Notebooks進行探索性資料分析和模型編寫。 | X（支援R、Python和Scala庫） | X（添加PySpark和Spark ML庫） |
| 與查詢服務的原生整合。 在筆記型電腦中使用SQL探索和塑造資料集的功能。 | X | X |
| 存取預先建立的筆記型電腦範本，以便進行預測性分析。 | X | X |
| 使用Jupyter Notebooks手動訓練模型並對模型評分。 | X | X |
| 部署和操作模型，並能夠安排培訓和參考作業。 |  | X |
| 配方架構，可輕鬆設定、評估、訓練、評分，並將模型發佈至生產環境。 |  | X |
| UI驅動的模型實驗和評估。 |  | X |
| 延伸流模型（GPU計算）的深度學習支援。 |  | X |
| 基於Spark的分佈式計算，可針對大型資料集（10MM +列）進行訓練和評分。 |  | X |

## 存取控制

Experience Platform的存取控制是透過[Adobe Admin Console](https://adminconsole.adobe.com)管理。 此功能會運用Admin Console中的產品設定檔，將使用者與權限和沙箱連結。 有關詳細資訊，請參閱[訪問控制概述](../access-control/home.md)。

若要使用Data Science Workspace，必須啟用「管理Data Science Workspace」權限。 下表概述啟用或停用此權限的效果：

| 權限 | 啟用 | 停用 |
|---|---|---|
| 管理Data Science Workspace | 提供對Data Science Workspace中所有服務的存取。 | Data Science Workspace中所有服務的API和UI存取權限皆已停用。 禁用時，選擇&#x200B;**Notebooks**、**Models**&#x200B;和&#x200B;**Services**&#x200B;頁會被阻止。 <li>仍可透過即時客戶資料平台(RTCDP)存取&#x200B;**服務**。</li> |

## 沙箱支援

沙箱是單一Experience Platform例項中的虛擬分區。 每個Platform例項都支援多個生產沙箱和非生產沙箱，每個沙箱都會維護自己的Platform資源程式庫。 非生產沙箱可讓您測試功能、執行實驗及進行自訂設定，而不會影響生產沙箱。 如需沙箱的詳細資訊，請參閱[沙箱概述](../sandboxes/home.md)。

Data Science Workspace目前有下列沙箱限制：

- 計算資源會在生產與非生產沙箱間共用。

## 後續步驟

本檔案概述了Data Science Workspace中提供的不同存取類型和功能。

若要進一步了解Data Science Workspace，例如完整的日常工作流程，請先閱讀[Data Science Workspace逐步說明檔案](./walkthrough.md)。 如需更多一般資訊，請造訪[Data Science Workspace概述](./home.md)。
