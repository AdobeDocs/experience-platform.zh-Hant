---
keywords: SFTP;sftp
title: SFTP連線
description: 建立與SFTP伺服器的即時傳出連線，以定期從Adobe Experience Platform匯出分隔的資料檔案。
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: b7392596c7ed96032dc8ad6bb8e423640f562394
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# SFTP連線

## 概覽 {#overview}

建立與SFTP伺服器的即時傳出連線，以定期從Adobe Experience Platform匯出分隔的資料檔案。

>[!IMPORTANT]
>
> 雖然Adobe支援將資料匯出至SFTP伺服器，但要匯出資料的建議雲端儲存空間為[!DNL Amazon S3]和[!DNL Azure Blob]。

## 匯出類型 {#export-type}

**以設定檔為基礎**  — 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，從目的地啟用工作流程的「選取屬性」畫面 [中選取](../../ui/activate-batch-profile-destinations.md)。

![SFTP設定檔匯出類型](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **主機**:SFTP儲存位置的位址
* **使用者名稱**:要登入您SFTP儲存位置的使用者名稱
* **密碼**:登入您SFTP儲存位置的密碼
* **[!UICONTROL 名稱]**:輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 資料夾路徑]**:輸入要承載導出檔案的目標資料夾的路徑。

或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公開金鑰必須寫入為[!DNL Base64]編碼字串。

## 匯出的資料 {#exported-data}

對於[!DNL SFTP]目的地，Platform會在您提供的儲存位置中建立以Tab分隔的`.csv`檔案。 如需檔案的詳細資訊，請參閱區段啟用教學課程中的[啟動對象資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md)。

## IP位址允許清單

如果您需要將AdobeIP新增至允許清單，請參閱雲端儲存目標的[IP位址允許清單](ip-address-allow-list.md)。
