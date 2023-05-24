---
keywords: Experience Platform；首頁；熱門主題；Adobe Experience Platform;api指南；平台API指南；平台簡介；開發人員指南
solution: Experience Platform
title: PostmanAdobe Experience Platform
description: 本文檔包含如何設定Postman環境、導入Postman集合以及每個平台服務可用集合清單的步驟。
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# PostmanAdobe Experience Platform

Postman是API開發的協作平台，允許您設定具有預設變數的環境、共用API集合、簡化CRUD請求等。 大多數平台API服務都有Postman集合，這些集合可用於幫助進行API調用。

## 如何營造PostmanExperience Platform環境

以下視頻指南概述了建立和設定您的Postman環境。 Postman環境包含對下面提供的各種集合進行API調用所需的所有標頭。 設定後，值隨時過期(如 `ACCESS_TOKEN`)可以更新環境中的當前值，並且此新值將用於所有集合。

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman收藏 {#collections}

通過訪問，可以找到包含所有可用Postman收藏的資料夾 [Experience PlatformPostman示例GitHub儲存庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)。 或者，Postman集合連結可在 [API參考文檔](https://www.adobe.com/go/platform-api-reference-en) Adobe I/O。

要下載Postman收藏，請選擇 **[!DNL Raw]** 從GitHub頁載入原始JSON檔案，使其位於新頁籤中。 然後，按一下右鍵並選擇 **[!DNL Save as]** 將檔案保存到您選擇的本地目標。

![原始JSON](./images/api-guide/raw-collection.PNG)

## 導入Postman集合 {#import}

為了利用 [Postman收藏](#collections)您需要設定環境。 完成環境設定後，選擇 **[!DNL Manage Environments]** 的子菜單。

![管理環境選擇器](./images/api-guide/environment-selector.png)

出現一個跨距，並顯示所有當前環境。 要導入集合，請選擇 **[!DNL import]** 。

![導入按鈕](./images/api-guide/import-collection.png)

系統要求您選擇要導入的檔案。 選擇要導入的Postman集合檔案。 選定後，集合將填充到「集合」(Collections)頁籤下的左滑軌中。

![填充集合](./images/api-guide/imported-collection.png)

每個集合都有不同的鍵值對，執行成功的CRUD操作可能需要這些鍵值對。 請查看服務 [API開發人員指南](api-guide.md#api-guides) 瞭解所需值、提示，並參閱示例。

要瞭解有關PostmanUI及其可用功能的更多資訊，請訪問 [Postman文檔](https://learning.postman.com/docs/getting-started/navigating-postman/)。

### 使用Postman生成訪問令牌以供非生產使用

>[!WARNING]
>
>如Identity Management服務(IMS)Postman集合中所述，表示的生成方法適合 **非生產用途**。 本地簽名從第三方主機載入JavaScript庫，遠程簽名將私鑰發送到由Adobe擁有和操作的Web服務。 雖然Adobe不儲存此私鑰，但生產密鑰不應與任何人共用。

以下視頻使用 [Identity Management服務(IMS)Postman](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) 可從公共GitHub儲存庫下載。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## 後續步驟

本文檔介紹了Postman環境、集合以及如何導入集合。 既然Postman準備好了，請 [平台入門指南](api-guide.md) 有關所需標題、示例和清單的資訊 [API指南](api-guide.md#api-guides) 可用於每個平台服務。
