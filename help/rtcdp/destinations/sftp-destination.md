---
keywords: SFTP;sftp
title: SFTP目的地
seo-title: SFTP目的地
description: 建立與SFTP伺服器的即時對外連線，以定期從Experience Platform匯出分隔資料檔案。
seo-description: 建立與SFTP伺服器的即時對外連線，以定期從Experience Platform匯出分隔資料檔案。
translation-type: tm+mt
source-git-commit: cbd748c1881c61f5e636567d94b68f2cf7302fa5
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# SFTP目的地

## 概述

建立與SFTP伺服器的即時對外連線，以定期從Experience Platform匯出分隔資料檔案。

若要匯出資料，請完成下列步驟：

## 連接目標 {#connect-destination}

如需 [如何連線至您的雲端儲 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)存目的地（包括SFTP）的指示，請參閱雲端儲存目的地工作流程。

對於SFTP目標，在「驗證」步驟的建立目標工作流中輸入以 **下資訊** :

* **主機**:SFTP儲存位置的位址
* **使用者名稱**:登入SFTP儲存位置的使用者名稱
* **密碼**:登入SFTP儲存位置的密碼

## 匯出的資料 {#exported-data}

對於SFTP目標，Adobe即時CDP會在您提供的儲存位置 `.txt` 中 `.csv` 建立以Tab分隔的檔案。 如需檔案的詳細資訊，請參閱區 [段啟動教學課程中的「電子郵件行銷目標](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 」和「雲端儲存目標」。