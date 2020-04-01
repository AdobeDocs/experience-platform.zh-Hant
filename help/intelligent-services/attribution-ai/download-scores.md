---
keywords: Experience Platform;attribution ai;access scores;popular topics
solution: Experience Platform
title: 在Attribution AI中存取分數
topic: Accessing scores
translation-type: tm+mt
source-git-commit: 689b4c7a96856e1167ee435a6740fed006136256

---


# 在Attribution AI中存取分數

>[!IMPORTANT] 如需大量匯出資料之原始分數下載的詳細資訊，請連絡attributionai-support@adobe.com。

存取歸因AI的分數是透過Snowflake完成。 目前，您需要以電子郵件寄送Adobe支援，來信請寄至attributionai-support@adobe.com，以設定並接收Snowflake的讀者帳戶認證。

在Adobe支援處理您的要求後，您會收到Snowflake讀者帳戶的URL，以及下列相應的認證：

- 雪花URL
- 使用者名稱
- 密碼

>[!NOTE] Reader帳戶是使用支援JDBC連接器的SQL客戶端、工作表和BI解決方案查詢資料。

一旦擁有認證和URL，您就可以查詢模型表格（其原始格式。.）、依觸點日期匯總或轉換日期。

## 在雪花中尋找您的圖式

使用提供的憑據，登錄到Snowflake。 按一下左 **上方主導覽中的** 「工作表」標籤，然後導覽至左側面板中的資料庫目錄。

![工作表與導覽](./images/download-scores/edited_snowflake_1.png)

接著，按 **一下畫面右上角的** 「選取架構」。 在出現的快顯視窗中，確認您已選取正確的資料庫。 接著，按一下「 *結構* 」下拉式清單，並選取其中一個列出的結構。 您可以直接從所選方案下列出的分數表中查詢。

![查找架構](./images/download-scores/edited_snowflake_2.png)

## 下載原始分數

如需Raw分數下載的詳細資訊，請聯絡attributionai-support@adobe.com。

## 將PowerBI連接到雪花（可選）

您的Snowflake憑據可用於設定PowerBI案頭資料庫和Snowflake資料庫之間的連接。

首先，在「服 *務器* 」框下，鍵入Snowflake URL。 接著，在 *Warehouse*&#x200B;下，輸入&quot;XSMALL&quot;。 然後，輸入您的使用者名稱和密碼。

![POWERBI範例](./images/download-scores/powerbi-snowflake.png)

建立連線後，請選取您的Snowflake資料庫，然後選取適當的架構。 您現在可以載入所有表格。

在您選取結構後，就會出現包含您歸因分數的表格。

| 表格 | 說明 |
| ----- | ----------- |
| APP_{APP_ID} | 原始歸因分數。 |
| APP_{APP_ID}_BY_CONV_DATE | 在轉換日期層級匯總原始歸因分數。 |
| APP_{APP_ID}_BY_TP_DATE | 在觸點日期層級匯總原始歸因分數。 |

## 後續步驟

本檔案概述查詢Attribution AI資料和存取分數所需的步驟。 您現在可以繼續瀏覽其他 [智慧型服務](../home.md) 和參考線。