---
title: 將加密資料內嵌在來源UI Workspace中
description: 瞭解如何將加密資料內嵌在來源UI工作區中。
badge: Beta
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: b4545943abbb68d36a64935feb4466d075331504
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 15%

---

# 將加密資料內嵌在來源UI中

>[!AVAILABILITY]
>
>來源UI中加密資料擷取的支援為測試版，可能不適用於您的組織。 功能和檔案可能會有所變更。

您可以使用雲端儲存批次來源將加密的資料檔案和資料夾擷取到Adobe Experience Platform。 透過加密的資料擷取，您可以運用非對稱的加密機制，將批次資料安全地傳輸至Experience Platform。 目前，支援的非對稱加密機製為PGP和GPG。

此功能可用於下列來源：

* [Amazon S3]
* [Azure Blob]
* [Azure Data Lake Storage Gen2]
* [Azure檔案儲存體]
* [資料登陸區域]
* [FTP]
* [Google雲端儲存空間]
* [HDFS]
* [Oracle物件存放區]
* [SFTP]

閱讀本指南，瞭解如何使用UI將加密資料與雲端儲存批次來源一起內嵌。

## 快速入門

在UI中使用加密的資料擷取之前，先瞭解下列Experience Platform功能和概念會很有幫助：

* [來源](../../home.md)：在Experience Platform中使用來源，從Adobe應用程式或協力廠商資料來源擷取資料。
* [資料流](../../../dataflows/home.md)：資料流是跨Experience Platform行動資料的資料作業的表示法。 您可以使用來源工作區建立資料流程，將指定來源的資料擷取至Experience Platform。
* [沙箱](../../../sandboxes/home.md)：在Experience Platform中使用沙箱，在您的Experience Platform執行個體之間建立虛擬分割區，並建立專用於開發或生產的環境。

### 高階大綱

1. 使用Experience PlatformUI中的來源工作區來建立加密金鑰組。 或者，您也可以建立簽署驗證金鑰組，為您的加密資料提供額外的安全層。
2. 使用公開金鑰加密資料。
3. 將加密的資料放入您的雲端儲存提供者。 在此步驟中，您也必須確定您有範例檔案，可作為將來源資料對應至體驗資料模型(XDM)結構描述的參考。
4. 透過建立來源連線來內嵌加密的資料以Experience Platform。
5. 在建立來源連線時，請提供與您用來加密資料的公開金鑰對應的金鑰ID。 如果您也使用簽署驗證金鑰配對機制，則您也必須提供對應至加密資料的簽署驗證金鑰ID。
6. 繼續進行資料流建立步驟。

## 建立加密金鑰對 {#create-an-encryption-key-pair}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="加密金鑰 ID"
>abstract="提供加密金鑰 ID，且此 ID 必須與用來加密來源資料的加密金鑰對應。"

* 在Platform UI中，導覽至來源工作區，然後從頂端標題中選取[!UICONTROL 金鑰組]。
* 系統會將您帶到一個頁面，其中顯示貴組織中現有加密金鑰組的清單。 此頁面提供指定金鑰的標題、ID、型別、加密演演算法、到期日和狀態的資訊。 若要建立新的金鑰組，請選取&#x200B;**[!UICONTROL 建立金鑰]**。
* 接著，選擇您要建立的金鑰型別。 若要建立加密金鑰，請選取&#x200B;**[!UICONTROL 加密金鑰]**，然後提供您加密金鑰的標題和複雜密碼。 複雜密碼是加密金鑰的額外保護層。 建立後，Experience Platform會將複雜密碼與公開金鑰儲存在不同的安全儲存庫中。 您必須提供非空白字串作為複雜密碼。

### 建立簽章驗證金鑰 {#create-a-sign-verification-key}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="簽章驗證金鑰 ID"
>abstract="提供與您已簽署的加密來源資料對應的簽章驗證金鑰 ID。"

## 收錄加密的資料 {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="檔案是否已加密？"
>abstract="如果您正在收錄加密的檔案，請選取此開關。"

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="選取範例檔案"
>abstract="在收錄加密的資料時，您必須收錄範例檔案才能建立對應。"


<!-- 
## Outline

Sections:

* Create public key
* Create customer key
* Create sources flow to ingest encrypted data
  * File ingestion
  * Folder ingestion
* Updated encrypted flow

* Select [!UICONTROL Key Pairs] from the header in the sources UI workspace.
  * You are taken to the [!UICONTROL Key Pairs] page:
    * Select **[!UICONTROL Encryption key]** for list of key pairs that you have created and managed.
    * Select **[!UICONTROL Customer key]** for a list of key pairs that your customers have created and managed.
* Key Pair functions:
  * Select **[!UICONTROL Key details]** to view key details.
  * Select **[!UICONTROL Delete]** to delete.
* Select [!UICONTROL Create key] to create either an encryption key or a customer key

## Questions and clarifications

* Public key vs. customer key
* Verify E2E:
  * Create keys (encryption key or customer key)
  * Use these keys to encrypt your data
  * Place your encrypted data in your cloud storage (Amazon S3 or Google Cloud Storage)
  * Ingest that encrypted data to Experience Platform by creating a source connection
    * Select the encrypted source data
    * Enable "Is the file encrypted"
    * Select/upload sample file for mapping
    * Use the encryption key name that corresponds with the key used to encrypt the source data
      * If the data was encrypted using customer key, provide the sign verification key.
  * Proceed with source connection creation flow -->
