---
title: 將加密資料內嵌在來源UI Workspace中
description: 瞭解如何將加密資料內嵌在來源UI工作區中。
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: 9f827c1ba97fba237c216fce9c2966bcc91fd05b
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 30%

---

# 將加密資料內嵌在來源UI中

閱讀本指南，瞭解如何使用雲端儲存空間來源將加密資料擷取至Adobe Experience Platform以儲存批次資料。

## 先決條件

* 加密您的資料

## 收錄加密的資料 {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="檔案是否已加密？"
>abstract="如果您正在收錄加密的檔案，請選取此開關。"

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="選取範例檔案"
>abstract="在收錄加密的資料時，您必須收錄範例檔案才能建立對應。"

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="加密金鑰ID"
>abstract="提供與用來加密來源資料的加密金鑰對應的加密金鑰ID。"

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="簽署驗證金鑰ID"
>abstract="提供與您的已簽署加密來源資料對應的簽署驗證金鑰ID。"

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
