---
keywords: Experience Platform；首頁；熱門主題；Adobe Experience Platform；api指南；平台api指南；平台簡介；開發人員指南
solution: Experience Platform
title: Adobe Experience Platform中的Postman
description: 本檔案包含概述如何設定Postman環境、匯入Postman集合的步驟，以及每個Platform服務的可用集合清單。
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Adobe Experience Platform中的Postman

Postman是API開發的共同作業平台，可讓您使用預設變數設定環境、共用API集合、簡化CRUD請求等。 大部分的Platform API服務都有Postman集合，可用來協助進行API呼叫。

## 如何設定Postman環境以進行Experience Platform

下列影片指南會概述如何建立和設定Postman環境。 Postman環境包含您對下面提供的各種集合進行API呼叫所需的所有必要標頭。 設定完成後，每當值過期（例如`ACCESS_TOKEN`）時，您都可以更新環境中目前的值，此新值將用於所有集合。

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman集合 {#collections}

造訪[Experience Platform的Postman範例GitHub存放庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)，即可找到包含所有可用Postman集合的資料夾。 或者，您也可以在Adobe I/O上的[API參考檔案](https://www.adobe.com/go/platform-api-reference-en)的每個個別Swagger檔案中找到Postman集合連結。

若要下載Postman集合，請從GitHub頁面選取「**[!DNL Raw]**」，在新索引標籤中載入原始JSON檔案。 然後，按一下滑鼠右鍵並選取&#x200B;**[!DNL Save as]**，以將檔案儲存至您選擇的本機目的地。

![原始JSON](./images/api-guide/raw-collection.PNG)

## 匯入Postman集合 {#import}

若要使用[Postman集合](#collections)，您必須設定環境。 完成環境設定後，請選取右上角的&#x200B;**[!DNL Manage Environments]**&#x200B;選取器。

![管理環境選擇器](./images/api-guide/environment-selector.png)

彈出視窗隨即出現，並顯示您所有目前的環境。 若要匯入集合，請選取「**[!DNL import]**」。

![匯入按鈕](./images/api-guide/import-collection.png)

系統會要求您選擇要匯入的檔案。 選取您要匯入的Postman集合檔案。 選取後，集合會填入左側邊欄的集合標籤下。

![已填入集合](./images/api-guide/imported-collection.png)

每個集合都有不同的機碼值組，這些組是執行成功CRUD作業所必需的。 請檢閱服務的[API開發人員指南](api-guide.md#api-guides)，瞭解必要的值、秘訣並檢視範例。

若要進一步瞭解Postman UI及其可用功能，請瀏覽[Postman檔案](https://learning.postman.com/docs/getting-started/navigating-postman/)。

### 使用Postman產生存取權杖以用於非生產用途

>[!WARNING]
>
>如Identity Management Service (IMS) Postman集合中所述，所代表的產生方法適用於&#x200B;**非生產使用**。 本機簽署會從協力廠商主機載入JavaScript程式庫，而遠端簽署會將私密金鑰傳送至Adobe擁有並操作的Web服務。 雖然Adobe不會儲存此私密金鑰，但生產金鑰絕不可與任何人共用。

以下影片使用[Identity Management Service (IMS) Postman集合](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json)，該集合可從公用GitHub存放庫下載。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## 後續步驟

本檔案介紹Postman環境、系列以及如何匯入系列。 現在您已準備好Postman，請造訪[平台快速入門手冊](api-guide.md)，取得每個平台服務可用的必要標題、範例和[API指南](api-guide.md#api-guides)清單的相關資訊。
