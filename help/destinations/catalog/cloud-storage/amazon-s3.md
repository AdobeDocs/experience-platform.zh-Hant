---
keywords: Amazon S3;S3目的地；s3;Amazon s3
title: Amazon S3連線
description: 建立與Amazon Web Services(AWS)S3儲存的即時傳出連線，以定期從Adobe Experience Platform將CSV資料檔案匯出至您自己的S3貯體。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: a07557ec398631ece0c8af6ec7b32e0e8593e24b
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# [!DNL Amazon S3] 連接 {#s3-connection}

## 目標更改日誌 {#changelog}

>[!IMPORTANT]
>
>匯出資料集功能測試版和檔案匯出功能改善後，您現在可能會看到兩個 [!DNL Amazon S3] 目的地目錄中的卡。
>* 如果您已將檔案匯出至 **[!UICONTROL Amazon S3]** 目標，請建立新資料流到新資料流 **[!UICONTROL Amazon S3測試版]** 目的地。
>* 如果您尚未建立任何資料流至 **[!UICONTROL Amazon S3]** 目的地，請使用新 **[!UICONTROL Amazon S3測試版]** 將檔案導出到的卡 **[!UICONTROL Amazon S3]**.


![以並排檢視顯示的兩個Amazon S3目的地卡影像。](../../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

新 [!DNL Amazon S3] 目的地卡包括：

* [資料集匯出支援](/help/destinations/ui/export-datasets.md).
* 其他 [檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* 可透過 [改良的映射步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [可自訂匯出CSV資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## 總覽 {#overview}

建立與 [!DNL Amazon S3] 儲存，以定期將資料檔案從Adobe Experience Platform匯出至您自己的S3貯體。

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，如「選取設定檔屬性」畫面中所選 [目的地啟動工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以3、6、8、12或24小時為增量將檔案匯出至下游平台。 深入了解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Amazon S3設定檔匯出類型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在目標設定工作流程中，填寫下列兩節中列出的欄位。

### 驗證到目標 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA公鑰"
>abstract="或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 在下面的文檔連結中查看格式正確的鍵的示例。"

若要驗證目的地，請填寫必填欄位並選取 **[!UICONTROL 連接到目標]**.

* **[!DNL Amazon S3]存取金鑰** 和 **[!DNL Amazon S3]密鑰**:在 [!DNL Amazon S3]，產生 `access key - secret access key` 配對，以授與 [!DNL Amazon S3] 帳戶。 了解更多 [Amazon Web Services檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL 加密密鑰]**:或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 在下圖中查看格式正確的加密密鑰示例。

   ![顯示UI中格式正確之PGP金鑰的範例影像](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填寫目的地詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="貯體名稱"
>abstract="長度必須介於3到63個字元之間。 必須以字母或數字開頭和結尾。 只能包含小寫字母、數字或連字型大小(-)。 不得格式化為IP地址（例如192.100.1.1）。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="資料夾路徑"
>abstract="只能包含A-Z、a-z、0-9等字元，並可包含下列特殊字元： `/!-_.'()"^[]+$%.*"`. 若要為每個區段檔案建立資料夾，請插入巨集 `/%SEGMENT_NAME%` 或 `/%SEGMENT_ID%` 或 `/%SEGMENT_NAME%/%SEGMENT_ID%` 填入文字欄位。 宏只能插入在資料夾路徑的末尾。 在檔案中檢視巨集範例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html#use-macros" text="使用宏在儲存位置中建立資料夾"

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 貯體名稱]**:輸入 [!DNL Amazon S3] 此目的地所使用的貯體。
* **[!UICONTROL 資料夾路徑]**:輸入要承載導出檔案的目標資料夾的路徑。
* **[!UICONTROL 檔案類型]**:選取匯出的檔案應使用的格式Experience Platform。 此選項僅適用於 **[!UICONTROL Amazon S3測試版]** 目的地。 選取 [!UICONTROL CSV] 選項，您也可以 [配置檔案格式選項](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 壓縮格式]**:選擇Experience Platform應用於導出檔案的壓縮類型。 此選項僅適用於 **[!UICONTROL Amazon S3測試版]** 目的地。


>[!TIP]
>
>在連線目標工作流程中，您可以根據匯出的區段檔案，在Amazon S3儲存空間中建立自訂資料夾。 閱讀 [使用宏在儲存位置中建立資料夾](overview.md#use-macros) 的說明。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

### 必填 [!DNL Amazon S3] 權限 {#required-s3-permission}

若要成功連線並將資料匯出至 [!DNL Amazon S3] 儲存位置，為建立Identity and Access Management(IAM)用戶 [!DNL Platform] in [!DNL Amazon S3] 並指派下列動作的權限：

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## （測試版）匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需設定資料集匯出的完整資訊，請閱讀 [匯出資料集教學課程](/help/destinations/ui/export-datasets.md).

## 匯出的資料 {#exported-data}

針對 [!DNL Amazon S3] 目的地， [!DNL Platform] 在您提供的儲存位置中建立資料檔案。 如需檔案的詳細資訊，請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 在區段啟用教學課程中。
