---
keywords: Azure Blob;Blob目的地；s3;Azure Blob目的地
title: Azure Blob連接
description: 建立與Azure Blob儲存的即時傳出連線，以定期從Adobe Experience Platform匯出CSV資料檔案。
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# [!DNL Azure Blob] 連接

## 總覽 {#overview}

[!DNL Azure Blob] (下稱 [!DNL Blob])是Microsoft的雲端物件儲存解決方案。 本教學課程提供建立 [!DNL Blob] 目的地使用 [!DNL Platform] 使用者介面。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-time Customer Profile]](../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效 [!DNL Blob] 目的地，您可以略過本檔案的其餘部分，並繼續進行有關 [將區段啟用至您的目的地](../../ui/activate-batch-profile-destinations.md).

## 支援的檔案格式 {#file-formats}

[!DNL Experience Platform] 支援以下要匯出至的檔案格式 [!DNL Blob]:

* 分隔字元分隔值(DSV):目前，對DSV格式化資料檔案的支援僅限於逗號分隔值。 今後將提供對一般DSV檔案的支援。

## 連接到目標 {#connect}

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 連線字串]**:存取Blob儲存中的資料時需要連線字串。 此 [!DNL Blob] 連線字串模式的開頭為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * 如需有關設定 [!DNL Blob] 連接字串，請參閱 [為Azure儲存帳戶配置連接字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) 在Microsoft檔案中。

* 或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公開金鑰必須寫入 [!DNL Base64] 編碼字串。
* **[!UICONTROL 名稱]**:輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 資料夾路徑]**:輸入要承載導出檔案的目標資料夾的路徑。
* **[!UICONTROL 容器]**:輸入 [!DNL Azure Blob Storage] 供此目的地使用的容器。

或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公開金鑰必須寫入 [!DNL Base64] 編碼字串。

## 啟用此目的地的區段 {#activate}

請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。
