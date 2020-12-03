---
keywords: SFTP;sftp
title: SFTP目的地
seo-title: SFTP目的地
description: 建立與SFTP伺服器的即時對外連線，以定期從Experience Platform匯出分隔資料檔案。
seo-description: 建立與SFTP伺服器的即時對外連線，以定期從Experience Platform匯出分隔資料檔案。
translation-type: tm+mt
source-git-commit: 7484e64d0d359f40ef242dfc9d2d1704018a8ed6
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# SFTP目的地

## 概述

建立與SFTP伺服器的即時對外連線，以定期從Experience Platform匯出分隔資料檔案。

## 匯出類型 {#export-type}

**基於配置檔案** -您正在導出段的所有成員，以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](../../ui/activate-destinations.md#select-attributes)。

![SFTP描述檔匯出類型](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 連接目標 {#connect-destination}

如需 [如何連線至您的雲端儲 ](./workflow.md)存目的地（包括SFTP）的指示，請參閱雲端儲存目的地工作流程。

對於SFTP目標，在「驗證」步驟的建立目標工作流中輸入以 **下資訊** :

* **主機**:SFTP儲存位置的位址
* **使用者名稱**:要登入SFTP儲存位置的使用者名稱
* **密碼**:登入SFTP儲存位置的密碼

## 匯出的資料 {#exported-data}

對於SFTP目標，即時CDP會在您提供的儲存位 `.txt` 置 `.csv` 中建立Tab分隔或檔案。 如需檔案的詳細資訊，請參閱區 [段啟動教學課程中的「電子郵件行銷目標](../../ui/activate-destinations.md#esp-and-cloud-storage) 」和「雲端儲存目標」。