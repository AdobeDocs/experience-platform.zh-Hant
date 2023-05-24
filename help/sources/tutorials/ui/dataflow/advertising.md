---
keywords: Experience Platform；首頁；熱門主題；配置資料流；廣告連接器
solution: Experience Platform
title: 使用UI中的廣告源建立資料流
type: Tutorial
description: 資料流是從源資料集中檢索資料並將資料接收到平台資料集的計畫任務。 本教程提供了如何使用平台UI為廣告源建立資料流的步驟。
exl-id: 8dd1d809-e812-4a13-8831-189726b2430e
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---

# 使用UI中的廣告源建立資料流

資料流是從Adobe Experience Platform的源中檢索資料並將資料接收到資料集的調度任務。 本教程提供了如何使用平台UI為廣告源建立資料流的步驟。

>[!NOTE]
>
>為了建立資料流，您必須已經擁有具有廣告源的經過身份驗證的帳戶。 有關在UI中建立不同廣告源帳戶的教程清單，請參見 [源概述](../../../home.md#advertising)。

## 快速入門

本教程需要瞭解平台的以下元件：

* [源](../../../home.md):平台允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [[!DNL Experience Data Model (XDM)] 系統](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
* [[!DNL Data Prep]](../../../../data-prep/home.md):允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

## 添加資料

建立廣告源帳戶後， **[!UICONTROL 添加資料]** 步驟，提供介面以便您瀏覽廣告源帳戶的表層次結構。

* 介面的左半部分是瀏覽器，顯示帳戶中包含的資料表的清單。 該介面還包括一個搜索選項，允許您快速識別要使用的源資料。
* 介面的右半部分是預覽面板，允許您最多預覽100行資料。

>[!NOTE]
>
>搜索源資料選項適用於除Adobe Analytics以外的所有基於表的源。 [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]。

找到源資料後，選擇表，然後選擇 **[!UICONTROL 下一個]**。

![選擇資料](../../../images/tutorials/dataflow/table-based/select-data.png)

## 提供資料流詳細資訊

的 [!UICONTROL 資料流詳細資訊] 頁允許您選擇是使用現有資料集還是使用新資料集。 在此過程中，您還可以配置 [!UICONTROL 配置檔案資料集]。 [!UICONTROL 錯誤診斷]。 [!UICONTROL 部分攝取], [!UICONTROL 警報]。

![資料流詳細資訊](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### 使用現有資料集

要將資料插入現有資料集，請選擇 **[!UICONTROL 現有資料集]**。 可以使用 [!UICONTROL 高級搜索] 選項，或通過在下拉菜單中滾動現有資料集清單來執行此操作。 選擇資料集後，請提供資料流的名稱和說明。

![現有資料集](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### 使用新資料集

要插入新資料集，請選擇 **[!UICONTROL 新資料集]** 然後提供輸出資料集名稱和可選說明。 接下來，選擇要映射到的方案 [!UICONTROL 高級搜索] 選項，或通過在下拉菜單中滾動現有架構清單來執行。 選擇架構後，請提供資料流的名稱和說明。

![新資料集](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### 啟用 [!DNL Profile] 錯誤診斷

接下來，選擇 **[!UICONTROL 配置檔案資料集]** 切換為 [!DNL Profile]。 這允許您建立實體屬性和行為的整體視圖。 所有資料 [!DNL Profile]-enabled資料集將包含在 [!DNL Profile] 並在保存資料流時應用更改。

[!UICONTROL 錯誤診斷] 為資料流中出現的任何錯誤記錄啟用詳細的錯誤消息生成，同時 [!UICONTROL 部分攝取] 允許您接收包含錯誤的資料，最高可達您手動定義的特定閾值。 查看 [部分批處理接收概述](../../../../ingestion/batch-ingestion/partial.md) 的子菜單。

![配置檔案和錯誤](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### 啟用警報

您可以啟用警報來接收有關資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱源警報](../alerts.md)。

完成向資料流提供詳細資訊後，選擇 **[!UICONTROL 下一個]**。

![警報](../../../images/tutorials/dataflow/table-based/alerts.png)

## 將資料欄位映射到XDM架構

的 [!UICONTROL 映射] 步驟，提供一個介面，用於將源欄位從源架構映射到目標架構中相應的目標XDM欄位。

平台根據您選擇的目標架構或資料集為自動映射欄位提供智慧建議。 您可以手動調整映射規則以適合您的使用情形。 根據您的需要，您可以選擇直接映射欄位，或使用資料準備函式轉換源資料以導出計算值或計算值。 有關使用映射器介面和計算欄位的全面步驟，請參見 [資料準備UI指南](../../../../data-prep/ui/mapping.md)。

成功映射源資料後，選擇 **[!UICONTROL 下一個]**。

![映射](../../../images/tutorials/dataflow/table-based/mapping.png)

## 計畫攝取運行

的 [!UICONTROL 計畫] 步驟，允許您配置接收計畫以使用配置的映射自動接收選定的源資料。 預設情況下，計畫設定為 `Once`。 要調整攝取頻率，請選擇 **[!UICONTROL 頻率]** 然後從下拉菜單中選擇一個選項。

>[!TIP]
>
>在一次性攝取期間，間隔和回填不可見。

![調度](../../../images/tutorials/dataflow/table-based/scheduling.png)

如果你將攝入頻率設定為 `Minute`。 `Hour`。 `Day`或 `Week`，則必須設定一個間隔，以在每個接收之間建立一個設定的時間框架。 例如，接收頻率設定為 `Day` 間隔設定為 `15` 意味著資料流計畫每15天接收一次資料。

在此步驟中，您還可以 **回填** 並為資料增量接收定義一列。 回填用於接收歷史資料，而您為增量接收定義的列允許將新資料與現有資料區分。

有關計畫配置的詳細資訊，請參閱下表。

| 欄位 | 說明 |
| --- | --- |
| 頻率 | 攝入的頻率。 可選頻率包括 `Once`。 `Minute`。 `Hour`。 `Day`, `Week`。 |
| 間隔 | 設定所選頻率的間隔的整數。 間隔的值應為非零整數，並應設定為大於或等於15。 |
| 開始時間 | UTC時間戳，指示第一次攝取的時間設定為何時發生。 開始時間必須大於或等於當前UTC時間。 |
| 回填 | 一個布爾值，它確定最初接收的資料。 如果啟用回填，則在首次計畫接收期間將攝取指定路徑中的所有當前檔案。 如果禁用回填，則將只接收在第一次接收運行和開始時間之間載入的檔案。 在開始時間之前載入的檔案將不會被攝取。 |
| 載入增量資料的方式 | 具有類型、日期或時間的一組篩選源架構欄位的選項。 此欄位用於區分新資料和現有資料。 增量資料將根據選定列的時間戳進行接收。 |

![回填](../../../images/tutorials/dataflow/table-based/backfill.png)

## 查看資料流

的 **[!UICONTROL 審閱]** 步驟，允許您在建立新資料流之前查看它。 詳細資訊按以下類別分組：

* **[!UICONTROL 連接]**:顯示源類型、所選源檔案的相關路徑以及該源檔案中的列數。
* **[!UICONTROL 分配資料集和映射欄位]**:顯示源資料正被攝取到的資料集，包括該資料集所遵循的架構。
* **[!UICONTROL 計畫]**:顯示接收計畫的活動期間、頻率和間隔。

查看資料流後，選擇 **[!UICONTROL 完成]** 並為建立資料流留出一些時間。

![審查](../../../images/tutorials/dataflow/table-based/review.png)

## 監視資料流

建立資料流後，您可以監視通過它攝取的資料，以查看有關攝取率、成功和錯誤的資訊。 有關如何監視資料流的詳細資訊，請參見上的教程 [監視UI中的帳戶和資料流](../monitor.md)。

## 刪除資料流

您可以刪除不再需要或使用 **[!UICONTROL 刪除]** 函式 **[!UICONTROL 資料流]** 工作區。 有關如何刪除資料流的詳細資訊，請參見上的教程 [刪除UI中的資料流](../delete.md)。

## 後續步驟

通過遵循本教程，您已成功建立了資料流，以將廣告源中的資料帶到平台。 傳入資料現在可供下游使用 [!DNL Platform] 服務，如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]。 有關詳細資訊，請參閱以下文檔：

* [[!DNL Real-Time Customer Profile] 概覽](../../../../profile/home.md)
* [[!DNL Data Science Workspace] 概覽](../../../../data-science-workspace/home.md)


>[!WARNING]
>
> 以下視頻中顯示的平台UI已過期。 有關最新的UI螢幕截圖和功能，請參閱上面的文檔。
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)
