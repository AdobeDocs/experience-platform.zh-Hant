---
keywords: Experience Platform；首頁；熱門主題；Adobe Experience Platform;api指南；平台api指南；平台簡介；開發人員指南
solution: Experience Platform
title: Adobe Experience Platform郵遞員
topic-legacy: api guide
description: 本檔案包含說明如何設定Postman環境、匯入Postman集合，以及每個Platform服務可用集合清單的步驟。
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: a0f4e49192a54075ce7c48620c9729e61ecdfdac
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Adobe Experience Platform郵遞員

Postman是API開發的共同作業平台，可讓您使用預設變數設定環境、共用API集合、簡化CRUD要求等。 大部分的Platform API服務都有Postman集合，可用來協助進行API呼叫。

## 如何設定Postman環境以進行Experience Platform

以下影片指南概述建立和設定Postman環境。 Postman環境包含您對下方提供的各種集合進行API呼叫所需的所有標題。 設定後，每當值過期時（例如`ACCESS_TOKEN`），您就可以更新環境中的目前值，而此新值會用於所有集合。

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## 郵遞員集合 {#collections}

您可以前往[Experience PlatformPostman範例GitHub存放庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)，找到包含所有可用Postman集合的資料夾。 或者，您可以在Adobe I/O的[API參考檔案](https://www.adobe.com/go/platform-api-reference-en)中，於每個個別Swagger檔案中找到Postman收集連結。

若要下載Postman集合，請從GitHub頁面選取&#x200B;**[!DNL Raw]**，以在新索引標籤中載入原始JSON檔案。 然後，按一下右鍵並選擇&#x200B;**[!DNL Save as]**&#x200B;將檔案保存到您選擇的本地目標。

![原始JSON](./images/api-guide/raw-collection.PNG)

## 匯入Postman集合 {#import}

若要使用[Postman集合](#collections)，您需要設定一個環境。 完成環境設定後，請選取右上角的&#x200B;**[!DNL Manage Environments]**&#x200B;選取器。

![管理環境選擇器](./images/api-guide/environment-selector.png)

畫面隨即顯示彈出視窗，並顯示您目前的所有環境。 若要匯入集合，請選取&#x200B;**[!DNL import]** 。

![匯入按鈕](./images/api-guide/import-collection.png)

系統會要求您選擇要匯入的檔案。 選取要匯入的Postman集合檔案。 選取後，集合會填入「集合」標籤下的左側欄。

![填入的集合](./images/api-guide/imported-collection.png)

每個集合都有不同的機碼值組，這些組可能是執行成功CRUD作業所需的。 請參閱服務的[API開發人員指南](api-guide.md#api-guides) ，了解所需的值、秘訣，並參閱範例。

若要進一步了解Postman UI及其可用功能，請造訪[Postman檔案](https://learning.postman.com/docs/getting-started/navigating-postman/)。

### 使用Postman產生存取權杖，以供非生產使用

>[!WARNING]
>
>如Adobe I/O存取權杖產生Postman集合中所述，表示的產生方法適用於&#x200B;**非生產用途**。 本機簽署會從協力廠商主機載入JavaScript程式庫，而遠端簽署會將私密金鑰傳送至由Adobe擁有及操作的Web服務。 雖然Adobe不會儲存此私密金鑰，但生產金鑰絕不應與任何人共用。

以下影片使用[Adobe I/O存取權杖產生集合](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json)，可從公用GitHub存放庫下載。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## 後續步驟

本檔案介紹了Postman環境、集合，以及如何匯入集合。 現在您已準備好Postman了，請前往[平台快速入門手冊](api-guide.md) ，取得所需標題、範例和每個Platform服務可用之[API指南](api-guide.md#api-guides)清單的相關資訊。
