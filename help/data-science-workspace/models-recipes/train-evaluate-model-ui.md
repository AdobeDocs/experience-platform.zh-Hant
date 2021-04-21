---
keywords: Experience Platform；訓練和評估；資料科學工作區；熱門主題；建立模型；建立培訓運行
solution: Experience Platform
title: 在資料科學工作區UI中訓練和評估模型
topic-legacy: tutorial
type: Tutorial
description: 在Adobe Experience Platform資料科學工作區中，機器學習模型是通過結合適合模型意圖的現有配方來建立的。 然後，對模型進行訓練和評估，通過微調其相關的超參數來優化其操作效率和效能。 方式可重複使用，這表示您可以使用單一方式，針對特定目的建立並量身打造多個模型。
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 1%

---

# 在資料科學工作區UI中訓練和評估模型

在Adobe Experience Platform資料科學工作區中，機器學習模型是通過結合適合模型意圖的現有配方來建立的。 然後，對模型進行訓練和評估，通過微調其相關的超參數來優化其操作效率和效能。 方式可重複使用，這表示您可以使用單一方式，針對特定目的建立並量身打造多個模型。

本教學課程將逐步介紹建立、訓練和評估模型的步驟。

## 快速入門

要完成本教學課程，您必須具有[!DNL Experience Platform]的存取權。 如果您沒有[!DNL Experience Platform]中IMS組織的存取權，請在繼續之前先與系統管理員聯絡。

本教學課程需要現有的配方。 如果您沒有配方，請依照UI](./import-packaged-recipe-ui.md)教學課程中的[匯入封裝配方，然後再繼續。

## 建立模型

在Experience Platform中，選擇位於左側導航中的&#x200B;**[!UICONTROL Models]**&#x200B;頁籤，然後選擇瀏覽頁籤以查看現有模型。 選擇頁面右上角的&#x200B;**[!UICONTROL Create Model]**&#x200B;以開始建立模型。

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

瀏覽現有配方的清單，查找並選擇用於建立模型的配方，然後選擇&#x200B;**[!UICONTROL Next]**。
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

選擇適當的輸入資料集，然後選擇&#x200B;**[!UICONTROL Next]**。 這將設定模型的預設輸入訓練資料集。
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

為「模型」(Model)提供名稱並查看預設「模型」(Model)配置。 在「配方」建立過程中，通過按兩下配置值來應用預設配置，複查和修改配置值。

若要提供新的組態，請選取&#x200B;**[!UICONTROL Upload New Config]**，並將包含「模型」組態的JSON檔案拖曳至瀏覽器視窗。 選擇&#x200B;**[!UICONTROL Finish]**&#x200B;以建立模型。

>[!NOTE]
>
>配置是獨特的，且特定於其預定配方，這表示「零售銷售配方」的配置將不適用於「產品Recommendations配方」。 有關零售銷售方式配置的清單，請參閱[reference](#reference)部分。

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## 建立訓練執行

在Experience Platform中，選擇位於左側導航中的&#x200B;**[!UICONTROL Models]**&#x200B;頁籤，然後選擇瀏覽頁籤以查看現有模型。 查找並選擇附加到要培訓的模型名稱的超連結。

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

所有現有培訓執行都會列出其目前的培訓狀態。 對於使用[!DNL Data Science Workspace]使用者介面建立的模型，會自動產生訓練執行，並使用預設組態和輸入訓練資料集來執行。

選擇「模型概述」頁面右上角的&#x200B;**[!UICONTROL Train]**，以建立新的訓練執行。

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

為培訓運行選擇培訓輸入資料集，然後選擇&#x200B;**[!UICONTROL Next]**。

![](../images/models-recipes/train-evaluate-ui/training_input.png)

如圖所示，建立模型期間提供的預設配置，請按兩下這些值，以相應地更改和修改這些配置。 選擇&#x200B;**[!UICONTROL Finish]**&#x200B;以建立並執行培訓運行。

>[!NOTE]
>
>配置是獨特的，且特定於其預定配方，這表示「零售銷售配方」的配置將不適用於「產品Recommendations配方」。 有關零售銷售方式配置的清單，請參閱[reference](#reference)部分。

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## 評估模型

在Experience Platform中，選擇位於左側導航中的&#x200B;**[!UICONTROL Models]**&#x200B;頁籤，然後選擇瀏覽頁籤以查看現有模型。 查找並選擇附加到要評估的模型名稱的超連結。

![選取模型](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

所有現有培訓執行都會列出其目前的培訓狀態。 在完成多個培訓執行後，您可以在模型評估圖表中比較不同培訓執行的評估度量。 使用圖形上方的下拉式清單選取評估度量。

「平均絕對百分比錯誤(MAPE)」量度將正確性表示為錯誤的百分比。 這用於識別效能最佳的實驗。 MAPE越低越好。

![培訓執行概觀](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

「精確度」度量描述相關例項與擷取的&#x200B;*例項總數之比例。*&#x200B;精確度可以看作是隨機選擇的結果正確的概率。

![執行多個執行](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

選取特定的訓練執行會開啟評估頁面，提供該執行的詳細資訊。 這可在執行完成之前完成。 在評估頁面上，您可以看到其他評估度量、設定參數和訓練執行專屬的視覺化。

![預覽記錄](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

您也可以下載活動記錄檔，以檢視執行的詳細資訊。 對於失敗的執行，記錄檔特別有用，以檢視出錯之處。

![活動日誌](../images/models-recipes/train-evaluate-ui/activity_logs.png)

超參數無法訓練，模型必須通過測試不同的超參陣列合來優化。 重複此模型訓練和評估流程，直到您到達最佳模型。

## 後續步驟

本教學課程將引導您在[!DNL Data Science Workspace]中建立、訓練和評估模型。 到達最佳化模型後，您就可以使用經過訓練的模型，依照UI](./score-model-ui.md)教學課程中的[對模型評分來產生見解。

## 參考 {#reference}

### 零售銷售方式配置

超參數決定模型的訓練行為，修改超參數將影響模型的準確性和精度：

| 超參數 | 說明 | 建議範圍 |
--- | --- | ---
| learning_rate | 學習率會透過learning_rate縮減每棵樹的貢獻。 learning_rate和n_meativers之間存在取捨。 | 0.1 | [2 - 10] /估計數 |
| n_mediators | 要執行的升級階段數。 漸層增強功能對過度調整相當穩健，因此，大量的漸層增強功能通常能產生較佳的效能。 | 100 | 100 - 1000 |
| max_depth | 個別回歸估計的最大深度。 最大深度限制樹中的節點數。 調整此參數以獲得最佳效能；最佳值取決於輸入變數的互動。 | 3 | 4 - 10 |

其他參數確定模型的技術屬性：

| 參數鍵 | 類型 | 說明 |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | 字串 | 逗號分隔的輸入模式屬性清單。 |
| `ACP_DSW_TARGET_FEATURES` | 字串 | 逗號分隔的輸出模式屬性清單。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布林值 | 確定輸入和輸出特徵是否可修改 |
| `tenantId` | 字串 | 此ID可確保您建立的資源具有正確的命名空間，並且包含在IMS組織中。 [請依照此處的](../../xdm/api/getting-started.md#know-your-tenant_id) 步驟尋找您的租用戶ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字串 | 用於訓練模型的輸入模式。 |
| `evaluation.labelColumn` | 字串 | 評估視覺化的欄標籤。 |
| `evaluation.metrics` | 字串 | 用於評估模型的評估度量的逗號分隔清單。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字串 | 用於計分模型的輸出方案。 |
