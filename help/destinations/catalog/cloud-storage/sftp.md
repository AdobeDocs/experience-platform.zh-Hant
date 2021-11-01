---
keywords: SFTP;sftp
title: SFTP連線
description: 建立與SFTP伺服器的即時傳出連線，以定期從Adobe Experience Platform匯出分隔的資料檔案。
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# SFTP連線

## 總覽 {#overview}

建立與SFTP伺服器的即時傳出連線，以定期從Adobe Experience Platform匯出分隔的資料檔案。

>[!IMPORTANT]
>
> 雖然Adobe支援將資料匯出至SFTP伺服器，但建議的雲端儲存空間位置會匯出資料 [!DNL Amazon S3] 和 [!DNL Azure Blob].

## 匯出類型 {#export-type}

**設定檔**  — 您要匯出區段的所有成員，以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，如「選取屬性」畫面中所選 [目的地啟動工作流程](../../ui/activate-batch-profile-destinations.md).

![SFTP設定檔匯出類型](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 連接到目標 {#connect}

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **主機**:SFTP儲存位置的位址
* **使用者名稱**:要登入您SFTP儲存位置的使用者名稱
* **密碼**:登入您SFTP儲存位置的密碼
* **[!UICONTROL 名稱]**:輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 資料夾路徑]**:輸入要承載導出檔案的目標資料夾的路徑。

或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公開金鑰必須寫入 [!DNL Base64] 編碼字串。

## 匯出的資料 {#exported-data}

針對 [!DNL SFTP] 目的地，平台會建立 `.csv` 檔案。 如需檔案的詳細資訊，請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 在區段啟用教學課程中。

## IP位址允許清單

請參閱 [雲端儲存目的地的IP位址允許清單](ip-address-allow-list.md) 如果您需要將AdobeIP新增至允許清單。
