---
title: 驗證
description: 了解如何設定Adobe Experience Platform Edge Network Server API的驗證。
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# 驗證 {#authentication}

## 總覽

此 [!DNL Edge Network Server API] 會根據事件來源和API收集網域，處理已驗證和未驗證的資料收集。

對於每個請求， [!DNL Server API] 驗證資料流 [!DNL access type] 設定。 使用此設定，客戶可以設定資料流以接受已驗證資料，或同時接受已驗證和未驗證的資料。 預設會接受這兩種資料類型。

如需設定資料流存取類型的詳細資訊，請參閱如何設定的檔案 [建立和設定資料流](../edge/datastreams/overview.md#create).

以下是根據資料流的行為摘要 [!DNL Access Type] 設定和接收請求的端點。

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| 混合（預設） | 不驗證請求 | 驗證請求 |
| 已驗證 | 驗證請求 | 驗證請求 |

來自上私人伺服器的API呼叫 `server.adobedc.net` 應一律驗證。

## 先決條件 {#prerequisites}

在您可以呼叫 [!DNL Server API]，請確定您符合下列必要條件：

* 您有可存取Adobe Experience Platform的組織帳戶。
* 您的Experience Platform帳戶具有 `developer` 和 `user` 為Adobe Experience Platform API產品設定檔啟用的角色。 請連絡您的 [Admin Console](../access-control/home.md) 管理員來為您的帳戶啟用這些角色。
* 你有Adobe ID。 如果您沒有Adobe ID，請前往 [Adobe Developer Console](https://developer.adobe.com/console) 並建立新帳戶。

## 收集憑據 {#credentials}

若要呼叫Platform API，您必須先完成 [驗證教學課程](../landing/api-authentication.md). 完成驗證教學課程後，所有Experience PlatformAPI呼叫中每個必要標題的值都會顯示，如下所示：

* 授權：承載 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的資源可以隔離至特定的虛擬沙箱。 在向Platform API提出的請求中，您可以指定要執行操作之沙箱的名稱和ID。 這些是選用參數。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需Experience Platform中沙箱的詳細資訊，請參閱 [沙箱概述檔案](../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* Content-Type: `application/json`

## 設定資料集寫入權限 {#dataset-write-permissions}

若要設定資料集寫入權限，請前往 [Admin Console](https://adminconsole.adobe.com)，找出附加至您API金鑰的產品設定檔，並設定下列權限：

* 在 [!UICONTROL 沙箱] 區段，選取datastream沙箱。
* 在 [!UICONTROL 資料管理] 區段，選取 **[!UICONTROL 管理資料集]** 權限。

## 疑難排解授權錯誤 {#troubleshooting-authorization}

| 錯誤代碼 | 錯誤訊息 | 說明 |
| --- | --- | --- |
| `EXEG-0500-401` | 授權令牌無效 | 出現下列任何情況時，都會顯示此錯誤訊息：  <ul><li>此 `authorization` 缺少標題值。</li><li>此 `authorization` 標題值不包含必要 `Bearer` 代號。</li><li>提供的授權Token格式無效。</li><li>資料流需要驗證，但請求缺少必要的標頭。</li></ul> |
| `EXEG-0501-401` | 用戶授權令牌無效 | 出現下列任何情況時，都會顯示此錯誤訊息： <ul><li>API呼叫缺少必要 `x-user-token` 頁首。</li><li>提供的用戶令牌的格式無效。</li></ul> |
| `EXEG-0502-401` | 授權令牌無效 | 當提供的授權Token具有有效格式(JWT)，但其簽名無效時，將顯示此錯誤消息。 檢查 [驗證教學課程](../landing/api-authentication.md) 了解如何取得有效的JWT代號。 |
| `EXEG-0503-401` | 授權令牌無效 | 提供的授權Token過期時，會顯示此錯誤訊息。 瀏覽 [驗證教學課程](../landing/api-authentication.md) 來產生新代號。 |
| `EXEG-0504-401` | 缺少必需的產品上下文 | 出現下列任何情況時，都會顯示此錯誤訊息：  <ul><li>開發人員帳戶無法存取Adobe Experience Platform產品內容。</li><li>公司帳戶尚無權使用AdobeExperience Platform。</li></ul> |
| `EXEG-0505-401` | 缺少所需的授權令牌作用域 | 此錯誤僅適用於服務帳戶驗證。 當呼叫中包含的服務授權Token屬於沒有存取權的服務帳戶時，會顯示錯誤訊息 `acp.foundation` IMS範圍。 |
| `EXEG-0506-401` | 無法寫入的沙箱 | 當開發人員帳戶沒有 `WRITE` 存取定義資料流的Experience Platform沙箱。 |
