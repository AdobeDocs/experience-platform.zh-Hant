---
keywords: Experience Platform;home；熱門主題；串流連接；建立流連接；ui指南；教學課程；建立流連接；流攝取；攝取；
solution: Experience Platform
title: 使用UI建立串流連線
topic: tutorial
type: Tutorial
description: 本UI指南將協助您使用Adobe Experience Platform建立串流連線。
translation-type: tm+mt
source-git-commit: a4019227abaddd9dbe143899d273580ebf21849e
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---


# 使用UI建立串流連線

本UI指南將協助您使用Adobe Experience Platform建立串流連線。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   - [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

## 建立串流連線

登入[!DNL Experience Platform] UI後，從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示多種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL Streaming]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL HTTP API]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL Add data]**&#x200B;以建立新的HTTP串流連接器。

![](../../../../images/tutorials/create/http/catalog.png)

此時將顯示&#x200B;**[!UICONTROL 連接HTTP API帳戶]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新憑據，請選擇&#x200B;**[!UICONTROL 新建帳戶]**。 在出現的輸入表單上，提供帳戶名稱和選擇性說明。 您也可以選擇提供下列配置屬性：

- **[!UICONTROL 驗證]:** 此屬性決定串流連線是否需要驗證。驗證可確保從受信任的來源收集資料。 如果您正在處理個人識別資訊(PII)，應開啟此屬性。 依預設，此屬性會關閉。
- **[!UICONTROL XDM模式相容性]:** 此屬性表示此流連接是否將發送與XDM模式相容的事件。依預設，此屬性會開啟。

完成後，選擇&#x200B;**[!UICONTROL 連接到源]** ，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![](../../../../images/tutorials/create/http/new-account.png)

### 現有帳戶

若要使用現有憑證進行連線，請選取您要使用的HTTP API連線，然後選取「下一步」以繼續。****

![](../../../../images/tutorials/create/http/existing-account.png)

## 選擇資料

建立HTTP API連線後，會出現「選取資料&#x200B;]**」步驟，提供介面以選擇要連線的資料集。**[!UICONTROL &#x200B;您可以選擇建立新資料集或連線至現有資料集。

### 建立新資料集

要建立新資料集，請選擇&#x200B;**[!UICONTROL 新建資料集]**。 在顯示的表單上，提供資料集的名稱、選用說明以及目標架構。 如果您選擇啟用描述檔的架構，您可以選擇資料集是否也應啟用描述檔。

![](../../../../images/tutorials/create/http/new-dataset.png)

### 使用現有資料集

若要使用現有資料集，請選取&#x200B;**[!UICONTROL 現有資料集]**。 在顯示的表格上，選取您要使用的資料集。 選擇資料集後，您可以選擇是否應啟用資料集。

![](../../../../images/tutorials/create/http/existing-dataset.png)

## 資料流詳細資訊

將顯示&#x200B;**[!UICONTROL 資料流詳細資訊]**&#x200B;步驟。 在此頁中，可以通過指定名稱和可選說明來提供建立的資料流的詳細資訊。

提供資料流的詳細資訊後，選擇&#x200B;**[!UICONTROL Next]**。

![](../../../../images/tutorials/create/http/dataflow-detail.png)

## 評論

出現&#x200B;**[!UICONTROL 查看]**&#x200B;步驟，允許您在建立資料流之前查看其詳細資訊。 詳細資訊分為下列類別：

- **[!UICONTROL 連接]**:顯示帳戶名稱、來源平台和來源名稱。
- **[!UICONTROL 指派資料集和地圖欄位]**:顯示目標資料集和資料集所遵守的模式。

確認詳細資訊正確後，選擇&#x200B;**[!UICONTROL 完成]**。

![](../../../../images/tutorials/create/http/review.png)

## 取得串流端點URL

在建立連線後，會顯示來源詳細資料頁面。 此頁顯示新建立的連接的詳細資訊，包括以前運行的資料流、ID和流端點URL。

![](../../../../images/tutorials/create/http/get-streaming-url.png)

## 後續步驟

在本教學課程中，您已建立串流HTTP連線，讓您使用串流端點來存取各種[!DNL Data Ingestion] API。 有關在API中建立流連接的說明，請閱讀[建立流連接教程](../../../api/create/streaming/http.md)。

要瞭解如何將資料串流至平台，請閱讀有關[串流時間系列資料](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教學課程，或有關[串流記錄資料](../../../../../ingestion/tutorials/streaming-record-data.md)的教學課程。
