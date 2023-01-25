---
description: 了解如何在將資料啟用至以檔案為基礎的目的地時設定檔案格式選項
title: （測試版）為檔案式目的地設定檔案格式選項
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 14ce4a11f53ef24b3008b3f775cc926d05ea8f8e
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 1%

---

# （測試版）為檔案式目的地設定檔案格式選項

>[!IMPORTANT]
>
>此 **[!UICONTROL 檔案格式選項]** Adobe Experience Platform中的功能目前仍在測試中。 檔案和功能可能會有所變更。
>請連絡您的Adobe代表以取得此功能的存取權。
> 
>本檔案中所述的檔案格式選項目前僅適用於CSV檔案。

為導出的檔案配置各種檔案格式選項的選項在您 [connect](/help/destinations/ui/connect-destination.md) 到基於檔案的目標，例如 [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect)，或 [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

您可以使用Experience PlatformUI，為匯出的檔案配置各種檔案格式選項。 您可以修改導出檔案的多個屬性，以匹配您所在的檔案接收系統的要求，以便以最佳方式讀取和解釋從Experience Platform接收的檔案。

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## 檔案格式設定 {#file-configuration}

要顯示檔案格式選項，請啟動 [連接到目的地](/help/destinations/ui/connect-destination.md) 工作流程。 選擇 **資料類型：區段** 和 **檔案類型：CSV** 顯示可用於導出的 `CSV` 檔案。

>[!IMPORTANT]
>
>您要連接的目的地可能沒有所有這些選項可用。 目的地開發人員可自行決定要在目的地支援哪些檔案格式選項。 目的地開發人員可決定連線至目的地時可用的選項。 必要選項在Experience PlatformUI中以星號標示。
> 
>新的雲端儲存空間目的地 —  [(Beta)Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [（測試版）Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta)Azure資料湖儲存Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [（測試版）資料登陸區](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [（測試版）Google雲端儲存空間](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [（測試版）SFTP](/help/destinations/catalog/cloud-storage/sftp.md)  — 目前僅支援下方強調顯示的六個CSV選項。

![顯示一些可用檔案格式選項的影像。](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### 分隔字元 {#delimiter}

為每個欄位和值設定分隔符號。 可選擇下列選項：

* 冒號 `(:)`
* 逗號 `(,)`
* 直立線符號 `(|)`
* 分號 `(;)`
* Tab 鍵 `(\\t)`

### 引號字元

設定用於逸出引號值的單一字元，其中分隔符可以是值的一部分。

### 逸出字元

在已引號的值內設定用於逸出引號的單字元。

### 空值輸出

設定空值的字串表示。

### Null值輸出

在導出的檔案中設定空值的字串表示。

輸出範例，包含 **[!UICONTROL null]** 已選取： `male,NULL,TestLastName`
輸出範例，包含 **&quot;** 已選取： `male,"",TestLastName`
輸出範例，包含 **[!UICONTROL 空字串]** 已選取： `male,,TestLastName`

### 壓縮格式

設定將資料保存到檔案時要使用的壓縮編解碼器。 支援的選項為GZIP和NONE。

### 編碼

*未顯示在UI螢幕截圖中*. 指定儲存之CSV檔案的編碼（字元集）。 選項為UTF-8或UTF-16。

### Char以逸出引號

*未顯示在UI螢幕截圖中*. 指示是否應始終將包含引號的值括在引號中的標誌。

預設值是逸出包含引號字元的所有值。

### 行分隔符

*未顯示在UI螢幕截圖中*. 定義應用於寫入的行分隔符。 長度上限為1個字元。

### 忽略前導空白字元

*未顯示在UI螢幕截圖中*. 此旗標可指出是否應略過匯出值的前導空白字元。

輸出範例，包含 **[!UICONTROL True]** 已選取： `"male","John","TestLastName"`
輸出範例，包含 **[!UICONTROL False]** 已選取： `" male","John","TestLastName"`

### 忽略尾隨空格

未顯示在UI螢幕截圖中。 指出是否應忽略匯出值的尾隨空格的標幟。

輸出範例，包含 **[!UICONTROL True]** 已選取： `"male","John","TestLastName"`
輸出範例，包含 **[!UICONTROL False]** 已選取： `"male ","John","TestLastName"`

### 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何設定CSV資料檔案的檔案匯出選項，以根據下游檔案接收系統的需求量身打造檔案內容。 接下來，您可以閱讀 [檔案型目的地啟用教學課程](/help/destinations/ui/activate-batch-profile-destinations.md) 若要開始將檔案匯出至您偏好的雲端儲存空間位置。
