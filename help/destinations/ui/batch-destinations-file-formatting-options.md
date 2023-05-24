---
description: 瞭解如何在將資料激活到基於檔案的目標時配置檔案格式選項
title: （測試版）為基於檔案的目標配置檔案格式選項
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: b1e9b781f3b78a22b8b977fe08712d2926254e8c
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 19%

---

# （測試版）為基於檔案的目標配置檔案格式選項

>[!IMPORTANT]
>
>的 **[!UICONTROL 檔案格式選項]** 功能目前位於Adobe Experience Platform的Beta版。 文檔和功能可能會更改。
>請與Adobe代表聯繫以訪問此功能。
> 
>本文檔中描述的檔案格式選項當前僅可用於CSV檔案。

當您 [連接](/help/destinations/ui/connect-destination.md) 到基於檔案的目標，如 [AmazonS3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect)。 [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect)或 [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect)。

可以使用Experience PlatformUI為導出的檔案配置各種檔案格式選項。 您可以修改導出檔案的幾個屬性以滿足您一側的檔案接收系統的要求，以便以最佳方式讀取和解釋從Experience Platform接收的檔案。

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## CSV檔案的檔案格式配置 {#file-configuration}

要顯示檔案格式選項，請啟動 [連接到目標](/help/destinations/ui/connect-destination.md) 工作流。 選擇 **資料類型：段** 和 **檔案類型：CSV** 顯示可用於導出的 `CSV` 的子菜單。

>[!IMPORTANT]
>
>您連接到的目標可能沒有所有這些選項可用。 由目標開發人員確定他們希望在其目標中支援哪些檔案格式選項。 目標開發人員可以確定在連接到目標時可用的選項。 在Experience PlatformUI中，必需的選項標有星號。
> 
>新的雲儲存目標 —  [(β)AmazonS3](/help/destinations/catalog/cloud-storage/amazon-s3.md)。 [（測試版）Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md)。 [(Beta)Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md)。 [(Beta)資料登錄區](/help/destinations/catalog/cloud-storage/data-landing-zone.md)。 [（測試版）Google雲儲存](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)。 [(Beta)SFTP](/help/destinations/catalog/cloud-storage/sftp.md)  — 當前僅支援下面突出顯示的六個CSV選項。

![顯示某些可用檔案格式選項的影像。](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### 分隔字元 {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="分隔字元"
>abstract="使用此控制項為每個欄位和值設定分隔符號。查看每個選項的範例文件。"

使用此控制項可為導出的CSV檔案中的每個欄位和值設定分隔符。 可選擇下列選項：

* 冒號 `(:)`
* 逗號 `(,)`
* 直立線符號 `(|)`
* 分號 `(;)`
* Tab 鍵 `(\t)`

#### 範例

查看導出的CSV檔案中內容的下面示例，以及UI中的每個選擇。

* 輸出示例 **[!UICONTROL 冒號`(:)`]** 選定： `male:John:Doe`
* 輸出示例 **[!UICONTROL 逗號`(,)`]** 選定： `male,John,Doe`
* 輸出示例 **[!UICONTROL 管道`(|)`]** 選定： `male|John|Doe`
* 輸出示例 **[!UICONTROL 分號`(;)`]** 選定： `male;John;Doe`
* 輸出示例 **[!UICONTROL 頁籤`(\t)`]** 選定： `male \t John \t Doe`

### 引號字元 {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="引號字元"
>abstract="如果要從匯出的字串中移除雙引號，請使用此選項。查看每個選項的範例文件。"

如果要從匯出的字串中移除雙引號，請使用此選項。可選擇下列選項：

* **[!UICONTROL 空字元(\000)]**。 使用此選項可從導出的CSV檔案中刪除雙引號。
* **[!UICONTROL 雙引號(&quot;)]**。 使用此選項可在導出的CSV檔案中保留雙引號。

#### 範例

在UI中查看導出的CSV檔案中內容的下面示例以及每個選擇。

* 輸出示例 **[!UICONTROL 空字元(\000)]** 選定： `Test,John,LastName`
* 輸出示例 **[!UICONTROL 雙引號(&quot;)]** 選定： `"Test","John","LastName"`

### 逸出字元 {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="逸出字元"
>abstract="在已引用的值中設定用於逸出引號的單一字元。查看每個選項的範例文件。"

使用此選項可設定一個字元，用於在已引用的值內轉義引號。 例如，如果字串用雙引號括起來，而字串的一部分已用雙引號括起來，則此選項非常有用。 此選項確定用哪個字元替換內部雙引號。 可選擇下列選項：

* 反斜線 `(\)`
* 單報價 `(')`

#### 範例

在UI中查看導出的CSV檔案中內容的下面示例以及每個選擇。

* 輸出示例 **[!UICONTROL 反斜線`(\)`]** 選定： `"Test,\"John\",LastName"`
* 輸出示例 **[!UICONTROL 單報價`(')`]** 選定： `"Test,'"John'",LastName"`

### 空值輸出 {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="空值輸出"
>abstract="使用此選項可設定空值在匯出的 CSV 檔案中的表示方式。查看每個選項的範例文件。"

使用此控制項設定空值的字串表示形式。 此選項確定在導出的CSV檔案中如何表示空值。 可選擇下列選項：

* **[!UICONTROL null]**
* **&quot;**
* **[!UICONTROL 空字串]**

#### 範例

在UI中查看導出的CSV檔案中內容的下面示例以及每個選擇。

* 輸出示例 **[!UICONTROL 空]** 選定： `male,NULL,TestLastName`。 在這種情況下，Experience Platform會將空值轉換為空值。
* 輸出示例 **&quot;** 選定： `male,"",TestLastName`。 在這種情況下，Experience Platform會將空值轉換為一對雙引號。
* 輸出示例 **[!UICONTROL 空字串]** 選定： `male,,TestLastName`。 在這種情況下，Experience Platform會保留空值，並按原樣導出它（不帶雙引號）。

>[!TIP]
>
>空值輸出與下節中空值輸出之間的差異在於空值的實際值為空。 NULL值根本沒有任何值。 將空值視為案頭上的空玻璃，將空值視為案頭上根本沒有玻璃。

### Null 值輸出 {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="Null 值輸出"
>abstract="使用此控制項在匯出的檔案中設定 Null 值的字串表示方式。查看每個選項的範例文件。"

使用此控制項在匯出的檔案中設定 Null 值的字串表示方式。此選項確定在導出的CSV檔案中如何表示空值。 可選擇下列選項：

* **[!UICONTROL null]**
* **&quot;&quot;**
* **[!UICONTROL 空字串]**

#### 範例

在UI中查看導出的CSV檔案中內容的下面示例以及每個選擇。

* 輸出示例 **[!UICONTROL 空]** 選定： `male,NULL,TestLastName`。 在這種情況下，不會進行轉換，CSV檔案包含空值。
* 輸出示例 **&quot;** 選定： `male,"",TestLastName`。 在這種情況下，Experience Platform將空值替換為空字串周圍的雙引號。
* 輸出示例 **[!UICONTROL 空字串]** 選定： `male,,TestLastName`。 在這種情況下，Experience Platform用空字串（不帶雙引號）替換空值。

### 壓縮格式 {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="壓縮格式"
>abstract="設定將資料儲存到檔案時要使用的壓縮類型。支援的選項為 GZIP 和 NONE。查看每個選項的範例文件。"

設定將資料儲存到檔案時要使用的壓縮類型。支援的選項為 GZIP 和 NONE。此選項確定是否導出壓縮檔案。

### 編碼

*未顯示在UI螢幕快照中*。 指定已保存CSV檔案的編碼（字元集）。 選項為UTF-8或UTF-16。

### 要轉義引號的字元

*未顯示在UI螢幕快照中*。 指示是否始終應將包含引號的值括在引號中的標誌。

預設值是轉義包含引號字元的所有值。

### 行分隔符

*未顯示在UI螢幕快照中*。 定義應用於寫入的行分隔符。 最大長度為1個字元。

### 忽略前導空格

*未顯示在UI螢幕快照中*。 應跳過一個標誌，指示是否從要導出的值中引導空格。

輸出示例 **[!UICONTROL 真]** 選定： `"male","John","TestLastName"`
輸出示例 **[!UICONTROL 假]** 選定： `" male","John","TestLastName"`

### 忽略尾隨空格

未顯示在UI螢幕快照中。 應跳過一個標誌，指示是否從正在導出的值中跳過尾隨空格。

輸出示例 **[!UICONTROL 真]** 選定： `"male","John","TestLastName"`
輸出示例 **[!UICONTROL 假]** 選定： `"male ","John","TestLastName"`

### 後續步驟 {#next-steps}

閱讀本文檔後，您現在知道如何為CSV資料檔案配置檔案導出選項，以便根據下游檔案接收系統的要求定制檔案內容。 接下來，你可以 [基於檔案的目標激活教程](/help/destinations/ui/activate-batch-profile-destinations.md) 開始將檔案導出到首選雲儲存位置。
