---
description: 瞭解在啟用以檔案為基礎的目的地資料時，如何設定檔案格式選項
title: 設定檔案型目的地的檔案格式選項
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 4dd6e8685ff5cc61342b20e971216416918b95da
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 17%

---

# 設定檔案型目的地的檔案格式選項

>[!IMPORTANT]
> 
>本檔案中說明的檔案格式選專案前僅適用於CSV檔案。

當您[連線](/help/destinations/ui/connect-destination.md)至檔案型目的地(例如[Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect)、[Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect)或[SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect))時，可以使用選項為匯出的檔案設定各種檔案格式選項。

您可以使用Experience Platform UI為匯出的檔案設定各種檔案格式選項。 您可以修改匯出檔案的幾個屬性，以符合您這端的檔案接收系統的需求，以便以最佳方式讀取和解譯從Experience Platform接收的檔案。

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## CSV檔案的檔案格式設定 {#file-configuration}

若要顯示檔案格式選項，請啟動[連線到目的地](/help/destinations/ui/connect-destination.md)工作流程。 選取&#x200B;**資料型別：區段**&#x200B;和&#x200B;**檔案型別：CSV**，以顯示匯出的`CSV`檔案可用的檔案格式設定。

>[!IMPORTANT]
>
>您連線的目的地可能沒有所有這些可用選項。 由目的地開發人員決定要在其目的地支援哪些檔案格式選項。 目的地開發人員可決定連線至目的地時可用的選項。 Experience Platform UI中的必要選項會以星號標示。
> 
>Adobe建置的雲端儲存空間目的地 — [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)、[Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md)、[Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md)、[資料登陸區域](/help/destinations/catalog/cloud-storage/data-landing-zone.md)、[Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)、[SFTP](/help/destinations/catalog/cloud-storage/sftp.md) — 目前僅支援下列六個強調的CSV選項。

![顯示部分可用檔案格式選項的影像。](../assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### 分隔字元 {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="分隔字元"
>abstract="使用此控制項為每個欄位和值設定分隔符號。查看每個選項的範例文件。"

使用此控制項為匯出的CSV檔案中的每個欄位和值設定分隔符號。 可選擇下列選項：

* 冒號`(:)`
* 逗號`(,)`
* 管道`(|)`
* 分號`(;)`
* 索引標籤`(\t)`

#### 範例

檢視以下範例，瞭解UI中每個選取專案的匯出CSV檔案內容。

* 已選取&#x200B;**[!UICONTROL 冒號`(:)`]**&#x200B;的範例輸出： `male:John:Doe`
* 選取了&#x200B;**[!UICONTROL 逗號`(,)`]**&#x200B;的範例輸出： `male,John,Doe`
* 已選取&#x200B;**[!UICONTROL 管道`(|)`]**&#x200B;的範例輸出： `male|John|Doe`
* 已選取&#x200B;**[!UICONTROL 分號`(;)`]**&#x200B;的範例輸出： `male;John;Doe`
* 已選取&#x200B;**[!UICONTROL 索引標籤`(\t)`]**&#x200B;的範例輸出： `male \t John \t Doe`

### 引號字元 {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="引號字元"
>abstract="如果要從匯出的字串中移除雙引號，請使用此選項。查看每個選項的範例文件。"

使用此選項來控制應移除雙引號還是將其保留在匯出的字串中。

可用的選項包括：

* **[!UICONTROL 空字元(\0000)]**。 使用此選項可移除匯出CSV檔案中的雙引號。
* **[!UICONTROL 雙引號(&quot;)]**。 當字串值包含分隔字元或雙引號時，請使用此選項。 此選項可協助您在匯出的CSV檔案中保留分隔符號或雙引號，以便您能夠正確識別哪個值對應到哪個欄位。

#### 範例

考慮輸入值`Anna,"Doe,John"`。

檢視以下範例，瞭解UI中每個選取專案的匯出CSV檔案內容。

* 已選取&#x200B;**[!UICONTROL Null字元(\0000)]**&#x200B;的輸出範例： `Anna,Doe,John`
* 選取&#x200B;**[!UICONTROL 雙引號(&quot;)]**&#x200B;的輸出範例： `Anna,"Doe,John"`

### 逸出字元 {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="逸出字元"
>abstract="在已引用的值中設定用於逸出引號的單一字元。查看每個選項的範例文件。"

使用此選項可設定在已引號值內逸出引號的單一字元。 例如，當字串包含在雙引號中時，此選項非常有用，因為部分字串已包含在雙引號中。 此選項會決定要用哪個字元來取代內部雙引號。 可選擇下列選項：

* 反斜線`(\)`
* 單引號`(')`

#### 範例

檢視以下範例，瞭解UI中每個選取專案的匯出CSV檔案內容。

* 選取了&#x200B;**[!UICONTROL 反斜線`(\)`]**&#x200B;的範例輸出： `"Test,\"John\",LastName"`
* 選取&#x200B;**[!UICONTROL 單引號`(')`]**&#x200B;的輸出範例： `"Test,'"John'",LastName"`

### 空值輸出 {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="空值輸出"
>abstract="使用此選項可設定空值在匯出的 CSV 檔案中的表示方式。查看每個選項的範例文件。"

使用此控制項來設定空值的字串表示法。 此選項會決定空值在匯出的CSV檔案中的表示方式。 可選擇下列選項：

* **[!UICONTROL Null （空值）]**
* **雙引號(&quot;)**&#x200B;中的空字串
* **[!UICONTROL 空字串]**

#### 範例

檢視以下範例，瞭解UI中每個選取專案的匯出CSV檔案內容。

* 已選取&#x200B;**[!UICONTROL null]**&#x200B;的範例輸出： `male,NULL,TestLastName`。 在此案例中，Experience Platform會將空白值轉換為null值。
* 已選取&#x200B;**&quot;**&#x200B;的範例輸出： `male,"",TestLastName`。 在此案例中，Experience Platform會將空白值轉換為一對雙引號。
* 已選取&#x200B;**[!UICONTROL 空字串]**&#x200B;的範例輸出： `male,,TestLastName`。 在此情況下，Experience Platform會維護空白值並依原樣匯出（不含雙引號）。

>[!TIP]
>
>以下區段中的空白值輸出與null值輸出之間的差異在於，空白值具有空白的實際值。 NULL值沒有任何值。 將空白值視為表格上的空白玻璃，將null值視為表格上沒有任何玻璃。

### Null 值輸出 {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="Null 值輸出"
>abstract="使用此控制項在匯出的檔案中設定 Null 值的字串表示方式。查看每個選項的範例文件。"

使用此控制項在匯出的檔案中設定 Null 值的字串表示方式。此選項會決定Null值在匯出的CSV檔案中的表示方式。 可選擇下列選項：

* **[!UICONTROL Null （空值）]**
* **雙引號(&quot;)**&#x200B;中的空字串
* **[!UICONTROL 空字串]**

#### 範例

檢視以下範例，瞭解UI中每個選取專案的匯出CSV檔案內容。

* 已選取&#x200B;**[!UICONTROL null]**&#x200B;的範例輸出： `male,NULL,TestLastName`。 在這種情況下，不會發生轉換，且CSV檔案包含null值。
* 已選取&#x200B;**&quot;**&#x200B;的範例輸出： `male,"",TestLastName`。 在此案例中，Experience Platform會在空字串周圍以雙引號取代null值。
* 已選取&#x200B;**[!UICONTROL 空字串]**&#x200B;的範例輸出： `male,,TestLastName`。 在這種情況下，Experience Platform會以空字串取代null值（不含雙引號）。

### 壓縮格式 {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="壓縮格式"
>abstract="設定將資料儲存到檔案時要使用的壓縮類型。支援的選項為 GZIP 和 NONE。查看每個選項的範例文件。"

設定將資料儲存到檔案時要使用的壓縮類型。支援的選項為 GZIP 和 NONE。此選項會決定是否匯出壓縮檔案。

### 編碼

*未顯示在UI熒幕擷圖中*。 指定已儲存CSV檔案的編碼（字元集）。 選項為UTF-8或UTF-16。

### 用於逸出引號的字元

*未顯示在UI熒幕擷圖中*。 此旗標可指出是否一律將包含引號的值括在引號中。

預設為逸出包含引號字元的所有值。

### 行分隔符號

*未顯示在UI熒幕擷圖中*。 定義用於寫入的線分隔符號。 長度上限為1個字元。

### 忽略前導空白字元

*未顯示在UI熒幕擷圖中*。 此旗標可指出是否應該略過匯出值的前導空格。

已選取&#x200B;**[!UICONTROL True]**&#x200B;的範例輸出： `"male","John","TestLastName"`
已選取&#x200B;**[!UICONTROL False]**&#x200B;的範例輸出： `" male","John","TestLastName"`

### 忽略結尾的空白字元

未顯示在UI熒幕擷圖中。 此旗標可指出是否應該略過匯出值的尾端空格。

已選取&#x200B;**[!UICONTROL True]**&#x200B;的範例輸出： `"male","John","TestLastName"`
已選取&#x200B;**[!UICONTROL False]**&#x200B;的範例輸出： `"male ","John","TestLastName"`

### 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何設定CSV資料檔案的檔案匯出選項，以根據下游檔案接收系統的需求量身打造檔案內容。 接下來，您可以閱讀[檔案型目的地啟用教學課程](/help/destinations/ui/activate-batch-profile-destinations.md)，以開始將檔案匯出至您偏好的雲端儲存位置。
