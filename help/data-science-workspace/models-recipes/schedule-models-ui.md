---
keywords: Experience Platform;安排模型;數據科學工作環境;熱門話題;時程表評分;排程培訓
solution: Experience Platform
title: 在数据科學工作環境 UI中計劃模型
type: Tutorial
description: Adobe Experience Platform數據科學工作環境允許在機器學習服務上設置計劃的評分和培訓運行。 自動執行培訓和評分過程可以通過跟上數據中的模式來幫助隨著時間的推移保持和提高服務的效率。
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# 在数据科學工作環境 UI中計劃模型

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

Adobe Experience Platform [!DNL Data Science Workspace]可讓您在機器學習服務上設定排程的評分和訓練執行。 自動化訓練和評分程式，可隨時掌握資料中的模式，協助維持及改善服務效率。

此教學課程會透過[!UICONTROL 服務庫]，逐步說明在現有服務上設定訓練和評分排程的步驟。 它分為下列主要區段：

- [設定排程評分](#configure-scheduled-scoring)
- [設定排程訓練](#configure-scheduled-training)

## 快速入門

要完成此教學課程，您必須有權訪問 [!DNL Experience Platform]。 如果您無權存取 中的 [!DNL Experience Platform]組織，請在繼續操作前與系統管理員聯繫。

此教學課程需要現有服務。 如果沒有可訪問的服務，可以按照將模型發佈為服務[&#128279;](./publish-model-service-ui.md)教學課程創建一個。

## 設定排程評分 {#configure-scheduled-scoring}

模型評分可以設定為依排程進行的自動化程式。 建立服務後，您可以依照以下步驟設定並套用評分排程：

在Adobe Experience Platform中，選取位於左側導覽欄中的&#x200B;**[!UICONTROL 服務]**&#x200B;索引標籤以存取&#x200B;**[!DNL Service Gallery]**。 尋找您想要排程評分回合的服務，並選取&#x200B;**[!UICONTROL 開啟]**&#x200B;以檢視其&#x200B;**[!UICONTROL 總覽]**&#x200B;頁面。

![](../images/models-recipes/schedule/select_service.png)

「總覽」頁面會顯示服務的評分資訊。 選取&#x200B;**[!UICONTROL 更新排程]**&#x200B;連結以設定評分排程。

![](../images/models-recipes/schedule/update_scoring.png)

設定評分排程的頻率、開始日期、結束日期、輸入資料集和輸出資料集。 在您滿意組態之後，請選取&#x200B;**[!UICONTROL 建立]**&#x200B;以更新服務的評分排程。

![](../images/models-recipes/schedule/set_scoring_schedule.png)

您更新的評分排程會顯示在服務的&#x200B;**[!UICONTROL 總覽]**&#x200B;頁面中。

![](../images/models-recipes/schedule/scoring_set.png)

## 設定計劃培訓 {#configure-scheduled-training}

配置在服務上運行的計劃培訓可確保機器學習模型更新為最新的數據模式。 每當計劃的培訓運行完成時，生成的經過訓練的模型將用於為服務提供支援，直到下一次計劃的培訓運行。

創建服務后，可以追隨以下步驟來配置和應用培訓計劃：

在Adobe Experience Platform中，選取位於左側導覽欄中的&#x200B;**[!UICONTROL 服務]**&#x200B;索引標籤，以存取&#x200B;**[!UICONTROL 服務庫]**。 尋找您想要排程訓練執行的服務，並選取&#x200B;**[!UICONTROL 開啟]**&#x200B;以檢視其&#x200B;**[!UICONTROL 概觀]**&#x200B;頁面。

![](../images/models-recipes/schedule/select_service.png)

「概觀」頁面會顯示服務的訓練資訊。 選取&#x200B;**[!UICONTROL 更新排程]**&#x200B;連結以設定訓練排程。

![](../images/models-recipes/schedule/update_training.png)

設定用於訓練排程的頻率、開始日期、結束日期和輸入資料集。 在您滿意組態之後，請選取&#x200B;**[!UICONTROL 建立]**&#x200B;以更新服務的訓練排程。

![](../images/models-recipes/schedule/set_training_schedule.png)

您更新的訓練排程會顯示在服務的&#x200B;**[!UICONTROL 總覽]**&#x200B;頁面中。

![](../images/models-recipes/schedule/training_set.png)

## 後續步驟

按照此教學課程操作，您已成功計劃了服務上的自動培訓和評分運行，並完成了 [!DNL Data Science Workspace] 教學課程 UI 工作流程。 如果尚未執行此操作，請考慮 [重新啟動教學課程](./create-retails-sales-dataset.md) 並追隨 API 工作流程以創建、訓練、評分和發佈模型。
