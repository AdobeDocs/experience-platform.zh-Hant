---
keywords: SFTP;sftp
title: SFTP目的地
seo-title: SFTP目的地
description: 建立與SFTP伺服器的即時對外連線，以定期從Experience Platform匯出分隔資料檔案。
seo-description: 建立與SFTP伺服器的即時對外連線，以定期從Experience Platform匯出分隔資料檔案。
translation-type: tm+mt
source-git-commit: d0a04c61bfe4024a2bb45ea7babab9073fcd6c22
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# SFTP目的地

## 概述

建立與SFTP伺服器的即時對外連線，以定期從Experience Platform匯出分隔資料檔案。

## 匯出類型 {#export-type}

**描述檔匯出** -您要匯出區段的所有成員，以及所要的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](/help/rtcdp/destinations/activate-destinations.md#select-attributes)。

![SFTP描述檔匯出類型](/help/rtcdp/destinations/assets/sftp-export-type.png)

## 連接目標 {#connect-destination}

如需 [如何連線至您的雲端儲 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)存目的地（包括SFTP）的指示，請參閱雲端儲存目的地工作流程。

對於SFTP目標，在「驗證」步驟的建立目標工作流中輸入以 **下資訊** :

* **主機**:SFTP儲存位置的位址
* **使用者名稱**:登入SFTP儲存位置的使用者名稱
* **密碼**:登入SFTP儲存位置的密碼

## 匯出的資料 {#exported-data}

對於SFTP目標，Adobe即時CDP會在您提供的儲存位置 `.txt` 中 `.csv` 建立以Tab分隔的檔案。 如需檔案的詳細資訊，請參閱區 [段啟動教學課程中的「電子郵件行銷目標](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 」和「雲端儲存目標」。