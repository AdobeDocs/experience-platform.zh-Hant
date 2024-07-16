---
keywords: Experience Platform；為模型評分；資料科學Workspace；熱門主題；ui；評分回合；評分結果
solution: Experience Platform
title: 在資料科學Workspace UI中為模型評分
type: Tutorial
description: Adobe Experience Platform Data Science Workspace中的評分可透過將輸入資料饋送至現有的已訓練模型來達成。 評分結果會儲存於指定的輸出資料集，並可作為新批次檢視。
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---

# 在資料科學Workspace UI中為模型評分

將輸入資料饋送至現有的已訓練模型，即可在Adobe Experience Platform [!DNL Data Science Workspace]中取得評分。 評分結果會儲存於指定的輸出資料集，並可作為新批次檢視。

本教學課程示範在[!DNL Data Science Workspace]使用者介面中為模型評分所需的步驟。

## 快速入門

若要完成本教學課程，您必須有[!DNL Experience Platform]的存取權。 如果您沒有[!DNL Experience Platform]中組織的存取權，請在繼續之前與您的系統管理員交談。

本教學課程需要經過訓練的模型。 如果您沒有經過訓練的模型，請遵循[訓練並在UI](./train-evaluate-model-ui.md)教學課程中評估模型，然後再繼續。

## 建立新的評分回合

評分回合是使用來自先前完成並評估的訓練回合的最佳化設定來建立。 模型的最佳設定集，通常由檢閱訓練回合評估量度來決定。

尋找最佳訓練回合，以使用其設定進行評分。 然後，透過選取附加至其名稱的超連結來開啟所需的訓練回合。

![選取訓練回合](../images/models-recipes/score/select-run.png)

從訓練回合&#x200B;**[!UICONTROL 評估]**&#x200B;索引標籤，選取畫面右上角的&#x200B;**[!UICONTROL 分數]**。 新的評分工作流程隨即開始。

![](../images/models-recipes/score/training_run_overview.png)

選取輸入評分資料集，然後選取&#x200B;**[!UICONTROL 下一步]**。

![](../images/models-recipes/score/scoring_input.png)

選取輸出評分資料集，這是儲存評分結果的專用輸出資料集。 確認您的選取範圍並選取&#x200B;**[!UICONTROL 下一步]**。

![](../images/models-recipes/score/scoring_results.png)

工作流程的最後一步會提示您設定評分回合。 模型會將這些設定用於評分回合。
請注意，您無法移除在建立模型期間所設定的繼承引數。 您可以編輯或回覆非繼承的引數，方法是按兩下值或選取回覆圖示，同時將滑鼠游標停留在專案上。

![組態](../images/models-recipes/score/configuration.png)

檢閱並確認評分設定，並選取&#x200B;**[!UICONTROL 完成]**&#x200B;以建立並執行評分回合。 您被導向到&#x200B;**[!UICONTROL 評分回合]**&#x200B;索引標籤，並顯示狀態為&#x200B;**[!UICONTROL 擱置中]**&#x200B;的新評分回合。

![評分回合索引標籤](../images/models-recipes/score/scoring_runs_tab.png)

評分回合可以以下列其中一種狀態顯示：
- 待處理
- 完成
- 失敗
- 執行中

狀態會自動更新。 如果狀態為&#x200B;**[!UICONTROL Complete]**&#x200B;或&#x200B;**[!UICONTROL Failed]**，則繼續下一步。

## 檢視評分結果

若要檢視評分結果，請從選取訓練回合開始。

![選取訓練回合](../images/models-recipes/score/select-run.png)

您被重新導向到訓練回合&#x200B;**[!UICONTROL 評估]**&#x200B;頁面。 在訓練回合評估頁面頂端附近，選取&#x200B;**[!UICONTROL 評分回合]**&#x200B;索引標籤，以檢視現有評分回合清單。

![評估頁面](../images/models-recipes/score/view_scoring_runs.png)

接著，選取評分回合以檢視回合詳細資料。

![執行詳細資料](../images/models-recipes/score/view_details.png)

如果選取的評分回合具有「完成」或「失敗」狀態，就可使用&#x200B;**[!UICONTROL 檢視活動記錄]**&#x200B;連結。 如果評分回合失敗，執行記錄檔可提供有用的資訊來判斷失敗的原因。 若要下載執行記錄，請選取&#x200B;**[!UICONTROL 檢視活動記錄]**。

![選取檢視記錄](../images/models-recipes/score/view_logs.png)

**[!UICONTROL 檢視活動記錄]**&#x200B;彈出視窗會出現。 選取URL以自動下載關聯的記錄檔。

![](../images/models-recipes/score/activity_logs.png)

您也可選擇選取&#x200B;**[!UICONTROL 預覽評分結果資料集]**，以檢視您的評分結果。

![選取預覽結果](../images/models-recipes/score/view_results.png)

提供輸出資料集的預覽。

![預覽結果](../images/models-recipes/score/preview_results.png)

若要取得完整的評分結果集，請選取右側欄中的&#x200B;**[!UICONTROL 評分結果資料集]**&#x200B;連結。

## 後續步驟

本教學課程將逐步引導您完成在[!DNL Data Science Workspace]中使用經過訓練的模型來評分資料的步驟。 請依照有關[在UI](./publish-model-service-ui.md)中發佈模型即服務的教學課程，讓您組織內的使用者透過提供對機器學習服務的輕鬆存取來評分資料。
