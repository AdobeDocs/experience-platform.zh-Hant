---
title: Amazon S3目的地
seo-title: Amazon S3目的地
description: 建立Amazon Web Services(AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。
seo-description: 建立Amazon Web Services(AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# [!DNL Amazon S3] 目的地

## 概述

建立與 [!DNL Amazon Web Services] (AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。

## 連接目標 {#connect-destination}

如需如 [何連線至您的雲端儲 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)存目的地的指示，請參閱雲端儲存目的地工作流程，包括 [!DNL Amazon S3]:

對於目 [!DNL Amazon S3] 標，請在建立目標工作流中輸入以下資訊：

* **[!DNL Amazon S3]訪問密鑰和[!DNL Amazon S3]密鑰&#x200B;**: 在中[!DNL Amazon S3]，生成訪問密鑰——秘密訪問密鑰對，以授予Adobe即時CDP對您帳戶的訪[!DNL Amazon S3]問權。



>[!IMPORTANT]
>
>Adobe Real-time CDP需要對 `write` 將要傳送匯出檔案的儲存貯體物件的權限。
