---
title: 驗證
description: 瞭解如何設定Adobe Experience Platform Edge Network Server API的驗證。
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 1%

---

# 驗證 {#authentication}

## 概觀

此 [!DNL Edge Network Server API] 會根據事件來源和API收集網域來處理已驗證和未驗證的資料收集。

對於每個請求， [!DNL Server API] 驗證資料流 [!DNL access type] 設定。 使用此設定，客戶可以設定資料串流以接受已驗證的資料，或同時接受已驗證和未驗證的資料。 預設情況下，接受兩種型別的資料。

如需設定資料流存取型別的詳細資訊，請參閱如何設定的檔案。 [建立和設定資料串流](../datastreams/overview.md#create).

以下是根據資料流的行為摘要 [!DNL Access Type] 設定和收到請求的端點。

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| 混合（預設） | 不驗證請求 | 驗證請求 |
| 已驗證 | 驗證請求 | 驗證請求 |

來自上私人伺服器的API呼叫 `server.adobedc.net` 應該一律經過驗證。

## 先決條件 {#prerequisites}

呼叫 [!DNL Server API]，確定您符合下列先決條件：

* 您擁有可存取Adobe Experience Platform的組織帳戶。
* 您的Experience Platform帳戶具有 `developer` 和 `user` Adobe Experience Platform API產品設定檔啟用的角色。 連絡您的 [Admin Console](../access-control/home.md) 管理員為您的帳戶啟用這些角色。
* 您有Adobe ID。 如果您沒有Adobe ID，請前往 [Adobe Developer Console](https://developer.adobe.com/console) 並建立新帳戶。

## 收集認證 {#credentials}

若要呼叫Platform API，您必須先完成 [驗證教學課程](../landing/api-authentication.md). 完成驗證教學課程，在所有Experience Platform API呼叫中提供每個必要標題的值，如下所示：

* 授權：持有人 `{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

Experience Platform中的資源可以隔離到特定的虛擬沙箱。 在對Platform API的請求中，您可以指定將執行作業的沙箱名稱和ID。 這些是選用引數。

* x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需Experience Platform中沙箱的詳細資訊，請參閱 [沙箱概述檔案](../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* Content-Type： `application/json`

## 設定資料集寫入許可權 {#dataset-write-permissions}

若要設定資料集寫入許可權，請前往 [Admin Console](https://adminconsole.adobe.com)，找到附加至API金鑰的產品設定檔，並設定下列許可權：

* 在 [!UICONTROL 沙箱] 區段，選取資料流沙箱。
* 在 [!UICONTROL 資料管理] 區段，選取 **[!UICONTROL 管理資料集]** 許可權。

## 疑難排解授權錯誤 {#troubleshooting-authorization}

| 錯誤代碼 | 錯誤訊息 | 說明 |
| --- | --- | --- |
| `EXEG-0500-401` | 無效的授權權杖 | 此錯誤訊息會在下列任一情況下顯示：  <ul><li>此 `authorization` 缺少標頭值。</li><li>此 `authorization` 標頭值未包含必要的 `Bearer` Token。</li><li>提供的授權權杖格式無效。</li><li>資料流需要驗證，但請求缺少必要的標頭。</li></ul> |
| `EXEG-0501-401` | 無效的使用者授權權杖 | 此錯誤訊息會在下列任一情況下顯示： <ul><li>API呼叫缺少必要的 `x-user-token` 標頭。</li><li>提供的使用者權杖格式無效。</li></ul> |
| `EXEG-0502-401` | 無效的授權權杖 | 當提供的授權權杖具有有效格式(JWT)，但其簽章無效時，會顯示此錯誤訊息。 檢查 [驗證教學課程](../landing/api-authentication.md) 以瞭解如何取得有效的JWT權杖。 |
| `EXEG-0503-401` | 無效的授權權杖 | 提供的授權權杖過期時，會顯示此錯誤訊息。 瀏覽 [驗證教學課程](../landing/api-authentication.md) 以產生新的Token。 |
| `EXEG-0504-401` | 缺少必要的產品內容 | 此錯誤訊息會在下列任一情況下顯示：  <ul><li>開發人員帳戶無法存取Adobe Experience Platform產品內容。</li><li>公司帳戶尚無權使用AdobeExperience Platform。</li></ul> |
| `EXEG-0505-401` | 缺少必要的授權權杖範圍 | 此錯誤僅適用於服務帳戶驗證。 當呼叫中包含的服務授權權杖屬於無權存取的服務帳戶時，便會顯示錯誤訊息 `acp.foundation` IMS範圍。 |
| `EXEG-0506-401` | 沙箱無法供寫入 | 當開發人員帳戶沒有 `WRITE` 存取定義資料流的Experience Platform沙箱。 |
