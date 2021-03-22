---
keywords: SFTP;sftp
title: SFTP連線
description: 建立與SFTP伺服器的即時對外連線，以定期從Adobe Experience Platform匯出分隔資料檔案。
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# SFTP連線

## 概述 {#overview}

建立與SFTP伺服器的即時對外連線，以定期從Adobe Experience Platform匯出分隔資料檔案。

>[!IMPORTANT]
>
> 雖然Adobe支援將資料匯出至SFTP伺服器，但建議的雲端儲存位置會是[!DNL Amazon S3]和[!DNL Azure Blob]。

## 導出類型{#export-type}

**基於描述檔** -您要匯出區段的所有成員，以及所要的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](../../ui/activate-destinations.md#select-attributes)。

![SFTP描述檔匯出類型](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 連接目標{#connect-destination}

請參閱[雲端儲存目標工作流程](./workflow.md)，以取得如何連線至您的雲端儲存目標（包括SFTP）的指示。

對於SFTP目標，請在&#x200B;**驗證**&#x200B;步驟的建立目標工作流中輸入以下資訊：

* **主機**:SFTP儲存位置的位址
* **使用者名稱**:要登入SFTP儲存位置的使用者名稱
* **密碼**:登入SFTP儲存位置的密碼

## 導出資料{#exported-data}

對於SFTP目標，平台會在您提供的儲存位置中建立以Tab分隔的`.txt`或`.csv`檔案。 如需檔案的詳細資訊，請參閱區段啟動教學課程中的[電子郵件行銷目標和雲端儲存目標](../../ui/activate-destinations.md#esp-and-cloud-storage)。

## IP位址允許清單

如果您需要將AdobeIP新增至允許清單，請參閱雲端儲存空間目標的[IP位址允許清單。](./ip-address-allow-list.md)