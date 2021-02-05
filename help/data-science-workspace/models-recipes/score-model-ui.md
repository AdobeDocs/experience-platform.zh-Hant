---
keywords: Experience Platform；為模型評分；Data Science Workspace；熱門主題；ui；評分運行；評分結果
solution: Experience Platform
title: 在資料科學工作區UI中為模型評分
topic: tutorial
type: Tutorial
description: '在Adobe Experience Platform Data Science Workspace中，將輸入資料輸入現有的訓練模型，即可獲得分數。 然後，將計分結果儲存並作為新批在指定的輸出資料集中查看。 '
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# 在資料科學工作區UI中為模型評分

在Adobe Experience Platform中，將輸入資料輸入現有的訓練模型，即可達到[!DNL Data Science Workspace]的評分。 然後，將計分結果儲存並作為新批在指定的輸出資料集中查看。

本教學課程示範在[!DNL Data Science Workspace]使用者介面中為模型評分所需的步驟。

## 快速入門

要完成本教學課程，您必須具有[!DNL Experience Platform]的存取權。 如果您沒有[!DNL Experience Platform]中IMS組織的存取權，請在繼續之前先與系統管理員聯絡。

本教學課程需要經過訓練的模型。 如果您沒有經過訓練的模型，請依照[訓練，並在UI](./train-evaluate-model-ui.md)教學課程中評估模型，然後再繼續。

## 建立新的計分執行

使用從先前完成和評估的培訓運行中優化的配置建立計分運行。 模型的一組最佳組態通常是透過檢閱訓練執行評估度量來決定。

1. 尋找最佳的訓練執行，以使用其設定進行計分。 按一下所要的「訓練」執行名稱，以開啟它。

2. 在「培訓執行&#x200B;**[!UICONTROL 評估]**」標籤中，按一下畫面右上角的&#x200B;**[!UICONTROL 分數]**&#x200B;按鈕。 這將啟動新的&#x200B;**執行計分**工作流。
   ![](../images/models-recipes/score/training_run_overview.png)

3. 選取輸入計分資料集，然後按一下「下一步」。****
   ![](../images/models-recipes/score/scoring_input.png)

4. 選擇輸出計分資料集，這是儲存計分結果的專用輸出資料集。 確認您的選擇，然後按一下「下一步」。****
   ![](../images/models-recipes/score/scoring_results.png)

5. 工作流程的最後一個步驟會提示您設定計分執行。 這些配置由模型用於計分運行。
請注意，您將無法移除在「模型」建立過程中設定的繼承參數。 您可以編輯或還原未繼承的參數，方法是按兩下該值，或在將滑鼠懸停在條目上時按一下還原表徵圖。
   ![](../images/models-recipes/score/configuration.png)
檢閱並確認計分設定，然後按一 ****  下「完成」以建立並執行計分執行。系統會將您導向至「計分執行&#x200B;****」標籤，而新的計分執行會顯示狀態。
   ![](../images/models-recipes/score/scoring_runs_tab.png)
計分執行將顯示下列四種狀態之一：暫掛、完成、失敗或正在運行，並且會自動更新。如果狀態為「已完成」或「失敗」，請繼續下一步。

## 檢視計分結果

1. 尋找用於計分執行的訓練執行，然後按一下名稱以檢視其&#x200B;**[!UICONTROL 評估]**&#x200B;頁面。

2. 在訓練執行評估頁面的頂端，按一下「計分執行&#x200B;****」標籤，以檢視現有計分執行的清單。 按一下計分清單，在右欄中檢視其詳細資訊。
   ![](../images/models-recipes/score/view_details.png)

3. 如果所選計分運行的狀態為「完成」或「失敗」，則右列中的&#x200B;**[!UICONTROL 查看活動日誌]**連結將處於活動狀態。 按一下連結可查看或下載執行日誌。 如果計分運行失敗，執行日誌可以在確定失敗原因時提供有用資訊。
   ![](../images/models-recipes/score/activity_logs.png)

4. 按一下右欄中的「預覽計分結果資料集&#x200B;]**」連結。**[!UICONTROL 您將可從計分執行中預覽輸出資料集。
   ![](../images/models-recipes/score/preview_results.png)

5. 如需完整的計分結果集，請按一下右欄中的&#x200B;**[!UICONTROL 計分結果資料集]**&#x200B;連結。

## 後續步驟

本教學課程將逐步引導您使用[!DNL Data Science Workspace]中經過訓練的模型來分數資料。 依照[在UI](./publish-model-service-ui.md)中發佈模型為服務的教學課程，讓組織內的使用者可輕鬆存取機器學習服務，以便對資料評分。
