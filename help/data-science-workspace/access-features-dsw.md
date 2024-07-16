---
keywords: Experience Platform；首頁；資料科學Workspace；熱門主題；存取控制；沙箱；情報套件；dsw功能；dsw存取；Adobe Experience Platform Intelligence；情報；aep intelligence套件
solution: Experience Platform
title: 資料科學Workspace存取與功能
description: 以下檔案概述資料科學Workspace許可權和功能的存取權。
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# 資料科學Workspace存取與功能

以下檔案概述資料科學Workspace許可權和功能的存取權。

![DSW標籤](./images/access/platform-tabs.png)

- **筆記型電腦：**&#x200B;提供互動式開發環境([JupyterLab](./jupyterlab/overview.md))，以探索、分析您的資料，並在Experience Platform上建立模型。
- **模型：**&#x200B;提供用來建立、發佈和儲存進階機器學習配方和模型的工具。 如需詳細資訊，請造訪[建立和發佈機器學習模型](./models-recipes/create-publish-model.md)教學課程。
- **服務：**&#x200B;包含Adobe提供的服務（例如[AI/ML服務](../intelligent-services/home.md)）以及您使用Data Science Workspace建立的任何自訂服務。

為什麼我只看到「服務」標籤？

- 您的組織可能僅有權使用Adobe Real-time Customer Data Platform (Real-Time CDP)，其中包括Customer AI/ML服務。

如果您無法看到任何&#x200B;**資料科學**&#x200B;標籤，但想要使用資料科學Workspace功能，請聯絡公司管理員，檢查您是否擁有Adobe Experience Platform Intelligence授權。

## 資料科學Workspace封裝

資料科學Workspace功能可在Adobe Experience Platform Intelligence套件和進階Intelligence Pack附加元件中取得

下表概述資料科學Workspace許可權的部分主要差異，包含與不包含Advanced Intelligence Pack附加元件：

>[!NOTE]
>
>您可以授權一個以上的Advanced Intelligence Pack附加元件，增加的容量會新增至您的整體權益。 例如，如果您授權2個Adobe Experience Platform Advanced Intelligence Pack附加元件，則可同時有20個Notebook使用者。

| 資料科學Workspace權益 | 僅限Adobe Experience Platform Intelligence套件 | Adobe Experience Platform Intelligence加上Advanced Intelligence Pack附加元件 |
| --- | :---: | :---: |
| 支援的Notebook使用者數目。 | 5位同時使用者 | 第一個套件會新增5個同時使用者，而額外的購買會為每個套件新增10個同時使用者。 |
| 允許整合的Jupyter Notebooks進行探索性資料分析和模型製作。 | X （支援R、Python和Scala程式庫） | X （新增PySpark和Spark ML程式庫） |
| 與查詢服務的原生整合。 能夠使用SQL在筆記型電腦中探索及塑造資料集。 | X | X |
| 存取預先建立的筆記型電腦範本，以進行預測性分析。 | X | X |
| 使用Jupyter Notebooks手動訓練模型並為其評分。 | X | X |
| 部署模型並使其可操作化，能夠排程培訓和推斷工作。 | | X |
| 配方架構，可輕鬆設定、評估、訓練、計分並將模型發佈至生產環境。 |  | X |
| UI導向模型實驗與評估。 | | X |
| Tensorflow模型（GPU運算）的深度學習支援。 | | X |
| 以Spark為基礎的分散式計算，可針對大型資料集（10MM +列）進行訓練和評分。 | | X |

## 存取控制

Experience Platform的存取控制是透過[Adobe Admin Console](https://adminconsole.adobe.com)管理。 此功能運用Admin Console中的產品設定檔，將使用者與許可權和沙箱連結。 如需詳細資訊，請參閱[存取控制總覽](../access-control/home.md)。

若要使用資料科學Workspace，「管理資料科學Workspace」許可權必須啟用。 下表概述啟用或停用此許可權的效果：

| 權限 | 啟用 | 停用 |
|---|---|---|
| 管理資料科學Workspace | 提供資料科學Workspace中所有服務的存取權。 | 已停用對Data Science Workspace中所有服務的API和UI存取。 停用時，無法選取&#x200B;**筆記本**、**模型**&#x200B;和&#x200B;**服務**&#x200B;頁面。 <li>仍可透過Adobe Real-time Customer Data Platform (Real-Time CDP)存取&#x200B;**服務**。</li> |

## 沙箱支援

沙箱是單一Experience Platform執行個體中的虛擬分割區。 每個Platform執行個體支援多個生產和非生產沙箱，每個沙箱都維護自己的Platform資源庫。 非生產沙箱可讓您測試功能、執行實驗並進行自訂設定，而不會影響您的生產沙箱。 如需沙箱的詳細資訊，請參閱[沙箱概觀](../sandboxes/home.md)。

目前，Data Science Workspace有下列沙箱限制：

- 運算資源會在生產和非生產沙箱之間共用。

## 後續步驟

本檔案概述資料科學Workspace中可用的各種存取型別和功能。

若要進一步瞭解Data Science Workspace，例如完整的日常工作流程，請先閱讀[Data Science Workspace逐步說明](./walkthrough.md)檔案。 如需更多一般資訊，請造訪[資料科學Workspace概觀](./home.md)。
