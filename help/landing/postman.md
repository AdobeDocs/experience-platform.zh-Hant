---
keywords: Experience Platform；首頁；熱門主題；Adobe Experience Platform;api指南；平台api指南；平台簡介；開發人員指南
solution: Experience Platform
title: Adobe Experience Platform郵遞員
topic-legacy: api guide
description: 本檔案包含如何設定郵遞員環境、匯入郵遞員系列以及每個平台服務可用系列清單的步驟。
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Adobe Experience Platform郵遞員

Postman是API開發的協作平台，可讓您使用預設變數來設定環境、共用API集合、簡化CRUD要求等。 大部分的平台API服務都有郵遞員系列，可用來協助進行API呼叫。

## 如何建立郵遞員Experience Platform環境

以下視頻指南概述了建立和設定郵遞員環境。 郵遞員環境包含您對下列各種系列進行API呼叫所需的所有標題。 設定後，只要值過期（例如`ACCESS_TOKEN`），您就可以更新環境中的目前值，而此新值會用於所有系列。

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## 郵遞員系列{#collections}

您可以訪問[Experience Platform郵遞員示例GitHub儲存庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)，找到包含所有可用郵遞員集的資料夾。 或者，在Adobe I/O的[API參考檔案](http://www.adobe.com/go/platform-api-reference-en)中，可在每個Swagger檔案中找到Postman收集連結。

若要下載Postman系列，請從GitHub頁面選擇&#x200B;**[!DNL Raw]**，將原始JSON檔案載入新標籤。 然後，按一下右鍵並選擇&#x200B;**[!DNL Save as]**&#x200B;將檔案保存到您選擇的本地目標。

![原始JSON](./images/api-guide/raw-collection.PNG)

## 匯入郵遞員系列{#import}

要利用[Postman集合](#collections)，您需要設定環境。 完成環境設定後，請選擇右上角的&#x200B;**[!DNL Manage Environments]**&#x200B;選擇器。

![管理環境選擇器](./images/api-guide/environment-selector.png)

出現快顯視窗，並顯示您目前的所有環境。 若要匯入系列，請選取&#x200B;**[!DNL import]**。

![導入按鈕](./images/api-guide/import-collection.png)

系統會要求您選擇要匯入的檔案。 選擇您要匯入的Postman系列檔案。 選取後，系列會填入「系列」索引標籤下方的左側導軌中。

![填入的系列](./images/api-guide/imported-collection.png)

每個系列都有不同的索引鍵值配對，執行成功的CRUD作業可能需要這些配對。 請參閱服務的[API開發人員指南](api-guide.md#api-guides)，以瞭解所需值、提示，並參閱範例。

若要進一步瞭解郵遞員使用者介面及其可用功能，請造訪[郵遞員檔案](https://learning.postman.com/docs/getting-started/navigating-postman/)。

### 使用Postman產生存取Token以供非生產使用

>[!WARNING]
>
>如Adobe I/O訪問令牌生成Postman集合中所述，表示的生成方法適合於&#x200B;**非生產用途**。 本端簽署會從協力廠商主機載入JavaScript程式庫，而遠端簽署會將私密金鑰傳送至由Adobe所擁有和運作的web service。 雖然Adobe不儲存此私密金鑰，但生產金鑰絕不應與任何人共用。

以下視訊使用[Adobe I/O存取Token產生系列](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json)，可從公用GitHub儲存庫下載。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## 後續步驟

本檔案介紹郵遞員環境、系列，以及如何匯入系列。 現在您已準備好Postman，請造訪[平台快速入門手冊](api-guide.md)，以取得必要標題、範例的相關資訊，以及每個平台服務可用的[API指南](api-guide.md#api-guides)清單。
