---
title: SFTP目的地
seo-title: SFTP目的地
description: 建立與SFTP伺服器的即時對外連線，以定期從Experience Platform匯出分隔資料檔案。
seo-description: 建立與SFTP伺服器的即時對外連線，以定期從Experience Platform匯出分隔資料檔案。
translation-type: tm+mt
source-git-commit: 098dd31be4d6ee6971cd87bcbfe0f686e34918e1
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# SFTP目的地

## 概述

建立與SFTP伺服器的即時對外連線，以定期從Experience Platform匯出分隔資料檔案。

若要匯出資料，請完成下列步驟：

## 連接目標 {#connect-destination}

如需 [如何連線至您的雲端儲 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)存目的地（包括SFTP）的指示，請參閱雲端儲存目的地工作流程。

對於SFTP目標，在「驗證」步驟的建立目標工作流中輸入以 **下資訊** :

* **主機**: SFTP儲存位置的位址
* **使用者名稱**: 登入SFTP儲存位置的使用者名稱
* **密碼**: 登入SFTP儲存位置的密碼

## 匯出的資料 {#exported-data}

對於 [!SFTP] 目標，Adobe Real-time CDP會在您提供的儲存位置中建立以Tab `.txt` 分隔 `.csv` 的或檔案。 如需檔案的詳細資訊，請參閱區 [段啟動教學課程中的「電子郵件行銷目標](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 」和「雲端儲存目標」。