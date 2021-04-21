---
keywords: Experience Platform；首頁；資料科學工作區；熱門主題；訪問控制；沙盒；智慧包；dsw功能；dsw訪問；Adobe Experience Platform智慧；智慧；aep智慧包
solution: Experience Platform
title: 資料科學工作區存取與功能
topic-legacy: Access and features for data science workspace
description: 以下檔案概述Data Science Workspace的權限和功能存取權。
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 3%

---

# 資料科學工作區存取與功能

以下檔案概述Data Science Workspace的權限和功能存取權。

![DSW頁籤](./images/access/platform-tabs.png)

- **筆記型電** 腦：提供互動式開發環境([JupyterLab](./jupyterlab/overview.md))，以探索、分析並建立Experience Platform資料模型。
- **模型：提** 供用來建立、發佈和儲存進階機器學習方式和模型的工具。如需詳細資訊，請造訪[建立並發佈機器學習模型](./models-recipes/create-publish-model.md)教學課程。
- **服務：** 包含Adobe提供的服務，例如智慧型 [服](../intelligent-services/home.md) 務，以及您使用Data Science Workspace建立的任何自訂服務。

為什麼我只看到「服務」標籤？

- 貴組織只能享有包含智慧型服務客戶AI的即時客戶資料平台(RTCDP)。

如果您看不到任何&#x200B;**Data Science**&#x200B;標籤，並想要使用Data Science Workspace功能，請連絡您的公司管理員以檢查您是否擁有Adobe Experience Platform情報授權。

## Adobe Experience Platform情報套件

下表概述資料科學工作區中有無「Adobe Experience Platform智慧」套件新增功能的主要差異：

>[!NOTE]
>
>您可以授權多個智慧型套件Addon，而增加的容量則會新增至您的整體權益。 例如，如果您授權2個Adobe Experience Platform智慧套件，您就有權同時擁有20個筆記型電腦使用者。

|  | [!DNL Data Science Workspace] | [!DNL Data Science Workspace] Intelligence套件附加功能 |
| --- | :---: | :---: |
| 支援的筆記本用戶數。 | 5個並行用戶 | First Pack新增5個並行使用者，而額外購買則新增10個並行使用者。 |
| 允許整合Jupyter Notebooks進行探索性資料分析和模型編寫(R、Python、Scala、PySpark) | X | X |
| 與查詢服務的原生整合。 能夠在筆記本中使用SQL來探索和塑造資料集。 | X | X |
| 存取預先建立的筆記型範本，以進行預測性分析。 | X | X |
| 使用Jupyter Notebooks手動培訓和評分模型。 | X | X |
| 部署並實施模型，並可排程培訓和推薦工作。 |  | X |
| 配方架構，可輕鬆設定、評估、訓練、分數，並將模型發佈至生產環境。 |  | X |
| UI驅動的模型實驗與評估。 |  | X |
| Tensorflow模型(GPU Compute)的深入學習支援。 |  | X |
| 基於Spark的分佈式計算，可針對大型資料集（10MM +列）進行訓練和評分。 |  | X |

## 存取控制

通過[Adobe Admin Console](https://adminconsole.adobe.com)管理Experience Platform的訪問控制。 此功能運用Admin Console中的產品設定檔，將使用者與權限和沙盒連結。 有關詳細資訊，請參閱[訪問控制概述](../access-control/home.md)。

若要使用「資料科學工作區」，必須啟用「管理資料科學工作區」權限。 下表概述啟用或停用此權限的效果：

| 權限 | 啟用 | 停用 |
|---|---|---|
| 管理資料科學工作區 | 提供資料科學工作區中所有服務的存取權。 | 資料科學工作區內所有服務的API和UI存取權已停用。 在禁用時，不能選擇&#x200B;**Notebooks**、**Models**&#x200B;和&#x200B;**Services**&#x200B;頁。 <li>**服務**&#x200B;的存取權仍可透過即時客戶資料平台(RTCDP)取得。</li> |

## 沙盒支援

沙盒是單一Experience Platform實例中的虛擬分區。 每個平台實例都支援一個生產沙盒和多個非生產沙盒，每個沙盒都維護其專屬的平台資源庫。 非生產沙盒可讓您測試功能、執行實驗並建立自訂組態，而不會影響生產沙盒。 如需沙盒的詳細資訊，請參閱[沙盒概述](../sandboxes/home.md)。

目前，Data Science Workspace有下列沙盒限制：

- 計算資源會在生產沙盒和非生產沙盒間共用。

## 後續步驟

本檔案概述資料科學工作區中可用的存取類型和功能。

若要進一步瞭解資料科學工作區，例如完整的日常工作流程，請先閱讀[資料科學工作區逐步說明檔案](./walkthrough.md)。 如需詳細資訊，請造訪[資料科學工作區概觀](./home.md)。
