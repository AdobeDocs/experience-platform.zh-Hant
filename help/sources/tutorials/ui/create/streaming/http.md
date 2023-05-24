---
keywords: Experience Platform；首頁；熱門主題；流連接；建立流連接；ui guide;tutorial;create streaming connection;streaming ingestion;ingestion;
solution: Experience Platform
title: 使用UI建立HTTP API流連接
type: Tutorial
description: 此UI指南將幫助您使用Adobe Experience Platform建立流連接。
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 0%

---


# 建立 [!DNL HTTP API] 使用UI的流連接

本教程提供使用 [!UICONTROL 源] 工作區。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   - [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

## 建立流連接

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 **[!UICONTROL 流]** 類別，選擇 **[!UICONTROL HTTP API]** ，然後選擇 **[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/http/catalog.png)

的 **[!UICONTROL 連接HTTP API帳戶]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要使用現有帳戶，請選擇要使用建立新資料流的HTTP API帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有帳戶](../../../../images/tutorials/create/http/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供帳戶名和可選說明。 您還可以選擇提供以下配置屬性：

- **[!UICONTROL 驗證]:** 此屬性確定流連接是否需要身份驗證。 身份驗證確保從受信任的源收集資料。 如果您正在處理個人身份資訊(PII)，則應開啟此屬性。 預設情況下，此屬性處於關閉狀態。
- **[!UICONTROL XDM相容]:** 此屬性表示此流連接是否將發送與XDM架構相容的事件。 預設情況下，此屬性處於關閉狀態。

完成後，選擇 **[!UICONTROL 連接到源]** ，然後選擇 **[!UICONTROL 下一個]** 繼續。

![新帳戶](../../../../images/tutorials/create/http/new.png)

## 選擇資料

建立HTTP API連接後， **[!UICONTROL 選擇資料]** 步驟，提供用於上載和預覽資料的介面。

選擇 **[!UICONTROL 上載檔案]** 上載資料。 或者，可以將資料拖放到 [!UICONTROL 拖放檔案] 的子菜單。

![添加資料](../../../../images/tutorials/create/http/add-data.png)

上傳資料後，您可以使用介面的右側預覽檔案層次結構。 選擇 **[!UICONTROL 下一個]** 繼續。

![預覽樣本資料](../../../../images/tutorials/create/http/preview-sample-data.png)

## 將資料欄位映射到XDM架構

的 [!UICONTROL 映射] 步驟，提供將源資料映射到平台資料集的介面。

拼花檔案必須符合XDM要求，並且不要求您手動配置映射，而CSV檔案要求您顯式配置映射，但允許您選擇要映射的源資料欄位。 JSON檔案（如果標籤為XDM投訴）不需要手動配置。 但是，如果未將其標籤為符合XDM，則需要顯式配置映射。

為要接收到的入站資料選擇資料集。 可以使用現有資料集或建立新資料集。

### 建立新資料集

要建立新資料集，請選擇 **[!UICONTROL 新資料集]**。 在顯示的窗體中，提供資料集的名稱、可選說明以及目標架構。 如果選擇 [!DNL Profile]-enabled schema，您可以選擇是否也應該 [!DNL Profile] — 已啟用。

![新資料集](../../../../images/tutorials/create/http/new-dataset.png)

### 使用現有資料集

要使用現有資料集，請選擇 **[!UICONTROL 現有資料集]**。 在顯示的表單上，選擇要使用的資料集。 選擇資料集後，可以選擇該資料集是否 [!DNL Profile] — 已啟用。

![現有資料集](../../../../images/tutorials/create/http/existing-dataset.png)

### 映射標準欄位


根據您的需要，您可以選擇直接映射欄位，或使用資料準備函式轉換源資料以導出計算值或計算值。 有關使用映射器介面和計算欄位的全面步驟，請參見 [資料準備UI指南](../../../../../data-prep/ui/mapping.md)。

要添加新源欄位，請選擇 **[!UICONTROL 添加新映射]**。

![新增映射](../../../../images/tutorials/create/http/add-new-mapping.png)

出現新的源欄位和目標欄位配對。 要添加新源欄位，請選擇 [!UICONTROL 選擇源欄位] 的子菜單。

![選擇源欄位](../../../../images/tutorials/create/http/select-source-field.png)

的 [!UICONTROL 選擇屬性] 面板允許您瀏覽檔案層次結構並選擇要映射到目標XDM欄位的特定源欄位。 選擇要映射的源欄位後，選擇 **[!UICONTROL 選擇]** 繼續。

![選擇屬性](../../../../images/tutorials/create/http/select-attributes.png)

選擇源欄位後，您現在可以標識要映射到的適當目標XDM欄位。 選擇目標欄位節下的架構表徵圖。

![選擇目標域](../../../../images/tutorials/create/http/select-target-field.png)

的 [!UICONTROL 將源欄位映射到目標欄位] 的子菜單。 選擇與源欄位匹配的目標欄位，然後選擇 **[!UICONTROL 選擇]** 繼續。

![映射到目標域](../../../../images/tutorials/create/http/map-to-target-field.png)

在源欄位全部映射到其相應的目標XDM欄位後，選擇 **[!UICONTROL 下一個]**

![資料準備完成](../../../../images/tutorials/create/http/data-prep-complete.png)

## 資料流詳細資訊

的 **[!UICONTROL 資料流詳細資訊]** 的上界。 在此頁上，可以通過提供名稱和可選說明來提供建立的資料流的詳細資訊。

提供資料流的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

![資料流詳細資訊](../../../../images/tutorials/create/http/dataflow-detail.png)

## 請檢閱

的 **[!UICONTROL 審閱]** 步驟，允許您在建立資料流之前查看其詳細資訊。 詳細資訊屬於以下類別：

- **[!UICONTROL 連接]**:顯示帳戶名、源平台和源名稱。
- **[!UICONTROL 分配資料集和映射欄位]**:顯示目標資料集和資料集所遵循的模式。

確認詳細資訊正確後，選擇 **[!UICONTROL 完成]**。

![審查](../../../../images/tutorials/create/http/review.png)

## 獲取流終結點URL

建立連接後，將顯示「源詳細資訊」頁。 此頁顯示新建立的連接的詳細資訊，包括以前運行的資料流、ID和流終結點URL。

![端點](../../../../images/tutorials/create/http/endpoint.png)

## 後續步驟

按照本教程，您建立了流式HTTP連接，使您能夠使用流終結點訪問各種 [!DNL Data Ingestion] API。 有關在API中建立流連接的說明，請閱讀 [建立流連接教程](../../../api/create/streaming/http.md)。

要瞭解如何將資料流傳輸到平台，請閱讀上的教程 [流時序資料](../../../../../ingestion/tutorials/streaming-time-series-data.md) 或教程 [流記錄資料](../../../../../ingestion/tutorials/streaming-record-data.md)。
