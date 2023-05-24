---
title: 驗證
description: 瞭解如何配置Adobe Experience Platform邊緣網路伺服器API的身份驗證。
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# 驗證 {#authentication}

## 總覽

的 [!DNL Edge Network Server API] 根據事件源和API收集域處理經過驗證和未經驗證的資料收集。

對於每個請求， [!DNL Server API] 驗證資料流 [!DNL access type] 的子菜單。 使用此設定，客戶可以配置資料流以接受經過驗證的資料，或者接受經過驗證的資料和未經驗證的資料。 預設情況下，兩種類型的資料都被接受。

有關配置資料流訪問類型的詳細資訊，請參閱有關如何配置資料流訪問類型的文檔 [建立和配置資料流](../edge/datastreams/overview.md#create)。

下面是基於資料流的行為摘要 [!DNL Access Type] 配置和接收請求的終結點。

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| 混合（預設） | 不驗證請求 | 驗證請求 |
| 已驗證 | 驗證請求 | 驗證請求 |

來自上的專用伺服器的API調用 `server.adobedc.net` 應該始終經過認證。

## 先決條件 {#prerequisites}

在您呼叫 [!DNL Server API]，確保滿足以下先決條件：

* 您有一個組織帳戶，可以訪問Adobe Experience Platform。
* 您的Experience Platform帳戶 `developer` 和 `user` 為Adobe Experience PlatformAPI產品配置檔案啟用的角色。 聯繫您 [Admin Console](../access-control/home.md) 管理員，以為您的帳戶啟用這些角色。
* 你有個Adobe ID。 如果你沒有Adobe ID，去 [Adobe Developer控制台](https://developer.adobe.com/console) 並建立新帳戶。

## 收集憑據 {#credentials}

要調用平台API，必須先完成 [驗證教程](../landing/api-authentication.md)。 完成Experience Platform教程將提供所有驗證API調用中每個必需標頭的值，如下所示：

* 授權：持 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的資源可以隔離到特定的虛擬沙箱。 在對平台API的請求中，可以指定操作將在其中進行的沙盒的名稱和ID。 這些是可選參數。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關Experience Platform中沙箱的詳細資訊，請參見 [沙盒概述文檔](../sandboxes/home.md)。

所有包含負載(POST、PUT、PATCH)的請求都需要附加的媒體類型報頭：

* Content-Type: `application/json`

## 配置資料集寫入權限 {#dataset-write-permissions}

要配置資料集寫入權限，請轉到 [Admin Console](https://adminconsole.adobe.com)，找到附加到API鍵的產品配置檔案，並設定以下權限：

* 在 [!UICONTROL 沙箱] ，選擇資料流沙盒。
* 在 [!UICONTROL 資料管理] 的 **[!UICONTROL 管理資料集]** 權限。

## 疑難解答授權錯誤 {#troubleshooting-authorization}

| 錯誤代碼 | 錯誤訊息 | 說明 |
| --- | --- | --- |
| `EXEG-0500-401` | 授權令牌無效 | 出現以下任何情況時都會顯示此錯誤消息：  <ul><li>的 `authorization` 缺少標頭值。</li><li>的 `authorization` 標頭值不包括所需值 `Bearer` 標籤。</li><li>提供的授權令牌的格式無效。</li><li>資料流需要驗證，但請求缺少必需的標頭。</li></ul> |
| `EXEG-0501-401` | 無效的用戶授權令牌 | 出現以下任何情況時都會顯示此錯誤消息： <ul><li>API調用缺少所需 `x-user-token` 標題。</li><li>提供的用戶令牌的格式無效。</li></ul> |
| `EXEG-0502-401` | 授權令牌無效 | 當提供的授權令牌具有有效格式(JWT)，但其簽名無效時，將顯示此錯誤消息。 檢查 [驗證教程](../landing/api-authentication.md) 瞭解如何獲取有效的JWT令牌。 |
| `EXEG-0503-401` | 授權令牌無效 | 提供的授權令牌過期時顯示此錯誤消息。 通過 [驗證教程](../landing/api-authentication.md) 生成新標籤。 |
| `EXEG-0504-401` | 缺少必需的產品上下文 | 出現以下任何情況時都會顯示此錯誤消息：  <ul><li>開發人員帳戶無權訪問Adobe Experience Platform產品上下文。</li><li>公司帳戶尚無權使用Adobe經驗平台。</li></ul> |
| `EXEG-0505-401` | 缺少所需的授權令牌作用域 | 此錯誤僅適用於服務帳戶身份驗證。 當包括在呼叫中的服務授權令牌屬於沒有訪問該服務的服務帳戶時，顯示錯誤消息 `acp.foundation` IMS範圍。 |
| `EXEG-0506-401` | 無法訪問沙盒進行寫入 | 當開發人員帳戶沒有 `WRITE` 訪問定義資料流的Experience Platform沙盒。 |
