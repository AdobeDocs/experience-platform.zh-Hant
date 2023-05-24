---
keywords: Experience Platform；首頁；熱門主題；源；連接器；源連接器；市場活動；市場活動管理服務
title: 使用平台UI建立Adobe Campaign Managed Cloud Services源連接
description: 瞭解如何使用平台UI將Adobe Experience Platform與Adobe Campaign Managed Cloud Services連接。
exl-id: 067ed558-b239-4845-8c85-3bf9b1d4caed
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 6%

---

# 使用平台UI建立Adobe Campaign Managed Cloud Services源連接

本教程提供建立源連接以將您的Adobe Campaign Managed Cloud Services資料帶到Adobe Experience Platform的步驟。

## 快速入門

本指南要求對以下Experience Platform元件進行工作理解：

* [源](../../../../home.md):平台允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [沙箱](../../../../../sandboxes/home.md):平台提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 將Adobe Campaign Managed Cloud Services連接到平台

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 還可以使用搜索欄縮小顯示的源。

在 **[!UICONTROL Adobe應用程式]** 類別，選擇 **[!UICONTROL Adobe Campaign Managed Cloud Services]** ，然後選擇 **[!UICONTROL 添加資料]**。

![顯示Adobe Campaign Managed Cloud Services卡的源目錄。](../../../../images/tutorials/create/campaign/catalog.png)

### 選擇資料 {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="Adobe Campaign 環境執行個體"
>abstract="您要使用的 Adobe Campaign 環境的名稱。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="目標對應"
>abstract="目標對應指 Campaign 用於傳遞訊息的技術物件，並包含傳送傳遞所需的所有技術設定 (地址、電話號碼、選擇加入指標、額外的識別碼……)。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="方案名稱"
>abstract="Adobe Campaign 資料庫中定義的實體的名稱。"
>text="Learn more in documentation"

的 [!UICONTROL 選擇資料] 步驟，為您提供配置 [!UICONTROL Adobe Campaign實例]。 [!UICONTROL 目標映射], [!UICONTROL 架構名稱]。

| 屬性 | 說明 |
| --- | --- |
| Adobe Campaign實例 | 您正在使用的Adobe Campaign環境實例的名稱。 |
| 目標對應 | 市場活動用於傳遞消息的技術對象，並包含發送交貨所需的所有技術設定。 |
| 方案名稱 | 要引入平台的架構實體的名稱。 選項包括「傳遞日誌」和「跟蹤日誌」。 |

![一個介面，您可以在其中配置Adobe Campaign實例、目標映射和架構名稱。](../../../../images/tutorials/create/campaign/select-data.png)

一旦您為市場活動實例、目標映射和方案名稱提供了值，螢幕將更新以顯示方案以及示例資料集的預覽。 完成後，選擇 **[!UICONTROL 下一個]**。

![模式層次的預覽以及資料集的示例](../../../../images/tutorials/create/campaign/preview.png)

### 使用現有資料集

的 [!UICONTROL 資料流詳細資訊] 頁允許您選擇是使用現有資料集還是為資料流配置新資料集。

要使用現有資料集，請選擇 **[!UICONTROL 現有資料集]**。 可以使用 [!UICONTROL 高級搜索] 選項，或通過在下拉菜單中滾動現有資料集清單來執行此操作。

選擇資料集後，請為資料流提供名稱和可選說明。

![顯示現有資料集選項的介面。](../../../../images/tutorials/create/campaign/existing-dataset.png)

### 使用新資料集

要使用新資料集，請選擇 **[!UICONTROL 新資料集]** 然後提供輸出資料集名稱和可選說明。 接下來，選擇要映射到的方案 [!UICONTROL 高級搜索] 選項，或通過在下拉菜單中滾動現有架構清單來執行。 完成後，選擇 **[!UICONTROL 下一個]**。

![顯示新資料集選項的介面。](../../../../images/tutorials/create/campaign/new-dataset.png)

### 啟用警報

您可以啟用警報來接收有關資料流狀態的通知。 從清單中選擇警報以訂閱和接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱源警報](../../alerts.md)。

完成向資料流提供詳細資訊後，選擇 **[!UICONTROL 下一個]**。

![可以為資料流啟用的不同警報類型的選擇。](../../../../images/tutorials/create/campaign/alerts.png)

### 將資料欄位映射到XDM架構

的 [!UICONTROL 映射] 步驟，提供一個介面，用於將源欄位從源架構映射到目標架構中相應的目標XDM欄位。

平台根據您選擇的目標架構或資料集為自動映射欄位提供智慧建議。 您可以手動調整映射規則以適合您的使用情形。 根據您的需要，您可以選擇直接映射欄位，或使用資料準備函式轉換源資料以導出計算值或計算值。 有關使用映射器介面和計算欄位的全面步驟，請參見 [資料準備UI指南](../../../../../data-prep/ui/mapping.md)。

>[!IMPORTANT]
>
>將源欄位映射到目標XDM欄位時，必須確保將指定的主標識欄位映射到相應的目標XDM欄位。

成功映射源資料後，選擇 **[!UICONTROL 下一個]**。

![一個映射樹，其中四個源資料欄位映射到其相應的XDM模式欄位。](../../../../images/tutorials/create/campaign/mapping.png)

### 查看資料流

的 **[!UICONTROL 審閱]** 步驟，允許您在建立新資料流之前查看它。 詳細資訊按以下類別分組：

* **[!UICONTROL 連接]**:顯示源類型、所選源檔案的相關路徑以及該源檔案中的列數。
* **[!UICONTROL 分配資料集和映射欄位]**:顯示源資料正被攝取到的資料集，包括該資料集所遵循的架構。

查看資料流後，選擇 **[!UICONTROL 完成]** 並為建立資料流留出一些時間。

![顯示連接和資料集資訊的審閱頁。](../../../../images/tutorials/create/campaign/review.png)

### 監視您的資料集活動

建立資料流後，您可以監視通過它攝取的資料，以查看有關攝取的速率以及成功和失敗批處理的資訊。

要開始查看資料集活動，請選擇 **[!UICONTROL 資料流]** 在源目錄中。

![選擇了資料流標題頁籤的源目錄頁。](../../../../images/tutorials/create/campaign/dataflows.png)

接下來，從顯示的資料流清單中選擇目標資料集。

![已選擇Adobe Campaign傳遞日誌目標資料集的現有資料流清單。](../../../../images/tutorials/create/campaign/target-dataset.png)

此時將顯示資料集活動頁。 從此處，您可以看到有關資料流效能的資訊，包括接收率、成功批處理和失敗批處理。

此頁還提供了一個介面，用於更新資料流的元資料描述、啟用部分接收和錯誤診斷，以及向資料集添加新資料。

![具有表示所選資料集的攝取速率的圖形的介面。](../../../../images/tutorials/create/campaign/dataset-activity.png)

## 後續步驟

通過遵循本教程，您已成功建立了一個資料流，以將Campaign v8交付日誌和跟蹤日誌資料帶到平台。 現在，下游平台服務(如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]。 有關詳細資訊，請參閱以下文檔：

* [[!DNL Real-Time Customer Profile] 概覽](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] 概覽](../../../../../data-science-workspace/home.md)
