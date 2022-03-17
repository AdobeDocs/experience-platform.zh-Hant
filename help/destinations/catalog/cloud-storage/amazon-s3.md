---
keywords: AmazonS3;S3目標；s3;amazon s3
title: AmazonS3連接
description: 建立到Amazon Web Services(AWS)S3儲存的即時出站連接，以定期將CSV資料檔案從Adobe Experience Platform導出到您自己的S3儲存桶中。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 691e3181e05a24b6bb0ebbe8e0f797a2b4c572d2
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# [!DNL Amazon S3] 連接 {#s3-connection}

## 總覽 {#overview}

建立到的即時出站連接 [!DNL Amazon Web Services] (AWS)S3儲存，定期將CSV資料檔案從Adobe Experience Platform導出到您自己的S3儲存桶中。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 批]** | 批處理目標將檔案以3、6、8、12或24小時的增量導出到下游平台。 閱讀有關 [基於批檔案的目標](/help/destinations/destination-types.md#file-based)。 |

{style=&quot;table-layout:auto&quot;}

![AmazonS3基於配置檔案的導出類型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 連接到目標 {#connect}

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="儲存段名稱"
>abstract="長度必須介於3到63個字元之間。 必須以字母或數字開頭和結尾。 只能包含小寫字母、數字或連字元(-)。 不能將格式設定為IP地址(例如，192.100.1.1)。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="資料夾路徑"
>abstract="只能包含字元A-Z、a-z、0-9，並且可以包含以下特殊字元： `/!-_.'()"^[]+$%.*"`。 要按段檔案建立資料夾，請將宏/%SEGMENT_NAME%或/%SEGMENT_ID%或/%SEGMENT_NAME%/%SEGMENT_ID%插入文本欄位。 宏只能插入資料夾路徑的末尾。 查看文檔中的宏示例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#use-macros" text="使用宏在儲存位置中建立資料夾"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA公鑰"
>abstract="或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 公鑰必須寫為Base64編碼字串。"

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **[!DNL Amazon S3]訪問密鑰** 和 **[!DNL Amazon S3]密鑰**:在 [!DNL Amazon S3]，生成 `access key - secret access key` 對以授予您的平台訪問權 [!DNL Amazon S3] 帳戶。 在 [Amazon Web Services文檔](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。
* **[!UICONTROL 名稱]**:輸入一個名稱，以幫助您標識此目標。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 儲存段名稱]**:輸入 [!DNL Amazon S3] 該目標使用的儲存桶。
* **[!UICONTROL 資料夾路徑]**:輸入將承載導出檔案的目標資料夾的路徑。

或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公鑰必須寫為 [!DNL Base64] 編碼字串。

>[!TIP]
>
>在連接目標工作流中，您可以在每個導出的段檔案的AmazonS3儲存中建立一個自定義資料夾。 閱讀 [使用宏在儲存位置中建立資料夾](overview.md#use-macros) 的雙曲餘切值。

### 必需 [!DNL Amazon S3] 權限 {#required-s3-permission}

要成功將資料連接和導出到 [!DNL Amazon S3] 建立Identity and Access Management(IAM)用戶 [!DNL Platform] 在 [!DNL Amazon S3] 並為以下操作分配權限：

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

## 將段激活到此目標 {#activate}

請參閱 [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md) 有關激活此目標受眾段的說明。

## 導出的資料 {#exported-data}

對於 [!DNL Amazon S3] 目的地， [!DNL Platform] 建立 `.csv` 檔案。 有關檔案的詳細資訊，請參見 [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md) 在段激活教程中。
