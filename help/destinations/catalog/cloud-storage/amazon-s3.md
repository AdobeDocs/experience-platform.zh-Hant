---
title: Amazon S3連線
description: 建立與您的Amazon Web Services (AWS) S3儲存區的即時輸出連線，以定期從Adobe Experience Platform將CSV資料檔案匯出至您自己的S3貯體。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 8771aa0df001e8ef81d4ad712f4d1f9661b405b2
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 17%

---

# [!DNL Amazon S3] 連線 {#s3-connection}

## 目的地變更記錄檔 {#changelog}

+++ 檢視變更記錄檔


| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2024 年 1 月 | 功能和檔案更新 | Amazon S3目的地聯結器現在支援新的假定角色驗證型別。 如需詳細資訊，請參閱 [驗證區段](#assumed-role-authentication). |
| 2023 年 7 月 | 功能和檔案更新 | 2023年7月Experience Platform發行版本中， [!DNL Amazon S3] 目的地提供新功能，如下所示： <br><ul><li>[資料集匯出支援](/help/destinations/ui/export-datasets.md)</li><li>其他[檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)。</li><li>能夠透過[改善的對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)，在您匯出的檔案內設定自訂檔案標頭。</li><li>[能夠自訂匯出的CSV資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## 連線至您的 [!DNL Amazon S3] 透過API或UI儲存 {#connect-api-or-ui}

* 若要連線至您的 [!DNL Amazon S3] 使用Platform使用者介面的儲存位置，請閱讀章節 [連線到目的地](#connect) 和 [啟用此目的地的對象](#activate) 底下。
* 若要連線至您的 [!DNL Amazon S3] 以程式設計方式儲存位置，請閱讀 [使用流量服務API教學課程，將對象啟用至檔案型目的地](../../api/activate-segments-file-based-destinations.md).

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如 [目的地啟用工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Amazon S3以設定檔為基礎的匯出型別，在UU中強調顯示。](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需如何設定資料集匯出的完整資訊，請閱讀教學課程：

* 操作說明 [使用Platform使用者介面匯出資料集](/help/destinations/ui/export-datasets.md).
* 操作說明 [使用流量服務API以程式設計方式匯出資料集](/help/destinations/api/export-datasets.md).

## 匯出資料的檔案格式 {#file-format}

匯出時 *對象資料*，平台會建立 `.csv`， `parquet`，或 `.json` 檔案中所指定的儲存位置。 如需檔案的詳細資訊，請參閱 [支援的匯出檔案格式](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) 區段建立模型。

匯出時 *資料集*，平台會建立 `.parquet` 或 `.json` 檔案中所指定的儲存位置。 如需檔案的詳細資訊，請參閱 [驗證資料集匯出成功](../../ui/export-datasets.md#verify) 區段的資料。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA 公開金鑰"
>abstract="或者，您可以附加 RSA 格式的公開金鑰以對匯出的檔案進行加密。透過下面的文件連結檢視格式正確的金鑰範例。"

若要向目的地進行驗證，請填寫必填欄位並選取 **[!UICONTROL 連線到目的地]**. Amazon S3目的地支援兩種驗證方法：

* 存取金鑰和機密金鑰驗證
* 假定角色驗證

#### 存取金鑰和機密金鑰驗證

當您想要輸入Amazon S3存取金鑰和秘密金鑰，以允許Experience Platform將資料匯出至Amazon S3屬性時，請使用此驗證方法。

![選取存取金鑰和機密金鑰驗證時必填欄位的影像。](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]存取金鑰** 和 **[!DNL Amazon S3]秘密金鑰**：在 [!DNL Amazon S3]，產生 `access key - secret access key` 配對，授予Platform存取權給您的 [!DNL Amazon S3] 帳戶。 進一步瞭解 [Amazon Web Services檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL 加密金鑰]**：您可以選擇附加RSA格式的公開金鑰，為匯出的檔案新增加密。 在下圖中檢視格式正確的加密金鑰範例。

  ![此影像顯示UI中格式正確的PGP金鑰範例。](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### 假定角色 {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="假定角色驗證"
>abstract="如果您不想與 Adobe 共用帳戶金鑰和祕密金鑰，請使用此驗證類型。否則，Experience Platform 會使用基於角色的存取連線到您的 Amazon S3 位置。貼上您在 AWS 中為 Adobe 使用者建立之角色的 ARN。該模式類似於 `arn:aws:iam::800873819705:role/destinations-role-customer` "

![選取假定的角色驗證時必填欄位的影像。](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

如果您不想與 Adobe 共用帳戶金鑰和祕密金鑰，請使用此驗證類型。Experience Platform會改用角色型存取來連線至您的Amazon S3位置。

為此，您需要在AWS主控台中建立一個Adobe的假設使用者， [許可權必要許可權](#required-s3-permission) 以寫入您的Amazon S3貯體。 建立 **[!UICONTROL 受信任的實體]** 在AWS中透過Adobe帳戶 **[!UICONTROL 670664943635]**. 如需詳細資訊，請參閱 [有關建立角色的AWS檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).

* **[!DNL Role]**：貼上您在AWS中為Adobe使用者建立之角色的ARN。 模式類似於 `arn:aws:iam::800873819705:role/destinations-role-customer`.
* **[!UICONTROL 加密金鑰]**：您可以選擇附加RSA格式的公開金鑰，為匯出的檔案新增加密。 在下圖中檢視格式正確的加密金鑰範例。

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="貯體名稱"
>abstract="長度必須介於 3 到 63 個字元之間。開頭和結尾必須是字母或數字。必須僅包含小寫字母、數字或連字號 (-)。不得格式化為 IP 位址 (例如，192.100.1.1)。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="檔案夾路徑"
>abstract="必須僅包含字元 A-Z、a-z、0-9，並且可以包含以下特殊字元：`/!-_.'()"^[]+$%.*"`。若要為每個對象檔案建立一個檔案夾，請將巨集 `/%SEGMENT_NAME%` 或 `/%SEGMENT_ID%` 或 `/%SEGMENT_NAME%/%SEGMENT_ID%` 插入文字欄位。只能將巨集插入檔案夾路徑的末尾。檢視文件中的巨集範例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=zh-Hant#use-macros" text="使用巨集在您的儲存位置建立檔案夾"

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**：輸入此目的地的說明。
* **[!UICONTROL 貯體名稱]**：輸入 [!DNL Amazon S3] 要由此目的地使用的貯體。
* **[!UICONTROL 資料夾路徑]**：輸入將託管已匯出檔案之目的地資料夾的路徑。
* **[!UICONTROL 檔案型別]**：選取Experience Platform應用於匯出檔案的格式。 選取 [!UICONTROL CSV] 選項，您也可以 [設定檔案格式選項](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 壓縮格式]**：選取Experience Platform應用於匯出檔案的壓縮型別。
* **[!UICONTROL 包含資訊清單檔案]**：如果您希望匯出專案包含資訊清單JSON檔案，且檔案中包含有關匯出位置、匯出大小等資訊，請開啟此選項。 資訊清單的命名格式為 `manifest-<<destinationId>>-<<dataflowRunId>>.json`. 檢視 [範例資訊清單檔案](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). 資訊清單檔案包含下列欄位：
   * `flowRunId`：此 [資料流執行](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 產生匯出的檔案。
   * `scheduledTime`：檔案匯出的時間(UTC)。
   * `exportResults.sinkPath`：儲存已匯出檔案所在儲存位置的路徑。
   * `exportResults.name`：匯出的檔案名稱。
   * `size`：匯出的檔案大小，以位元組為單位。

>[!TIP]
>
>在連線目標工作流程中，您可以根據匯出的受眾檔案，在Amazon S3儲存空間中建立自訂資料夾。 讀取 [使用巨集在您的儲存位置中建立資料夾](overview.md#use-macros) 以取得指示。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

### 必填 [!DNL Amazon S3] 許可權 {#required-s3-permission}

若要成功連線並匯出資料至 [!DNL Amazon S3] 儲存位置，建立「識別與存取管理」(IAM)使用者 [!DNL Platform] 在 [!DNL Amazon S3] 並為以下動作指派許可權：

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

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

另請參閱 [啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用此目的地對象的指示。

## 驗證資料匯出成功 {#exported-data}

若要確認資料是否已成功匯出，請檢查 [!DNL Amazon S3] 儲存，並確認匯出的檔案包含預期的設定檔母體。

## IP位址允許清單 {#ip-address-allow-list}

請參閱 [IP位址允許清單](ip-address-allow-list.md) 文章(如果您需要將AdobeIP新增至允許清單)。