---
title: Amazon S3目的地
seo-title: Amazon S3目的地
description: 建立Amazon Web Services(AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。
seo-description: 建立Amazon Web Services(AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。
translation-type: tm+mt
source-git-commit: f3c6c27b7ad07ada0df18aabe0e8503253b38342

---


# Amazon S3目的地

## 概述

建立Amazon Web Services(AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。

## 連接目標 {#connect-destination}

如需如 [何連線至您的雲端儲 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)存目的地（包括Amazon S3）的指示，請參閱雲端儲存目的地工作流程。

對於Amazon S3目標，請在建立目標工作流中輸入以下資訊：

* **Amazon S3訪問密鑰和Amazon S3密鑰**:在Amazon S3中，產生存取金鑰——機密存取金鑰對，以授與Amazon S3帳戶的Adobe即時CDP存取權。



>[!IMPORTANT]
>
>Adobe Real-time CDP需要對 `write` 將要傳送匯出檔案的儲存貯體物件的權限。
