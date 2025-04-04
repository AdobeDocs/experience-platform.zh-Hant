---
title: Authentication
description: 瞭解如何設定Adobe Experience Platform Edge Network伺服器API的驗證。
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 7%

---

# Authentication {#authentication}

## 概觀

[!DNL Edge Network Server API]會根據事件來源和API收集網域來處理已驗證和未驗證的資料收集。

針對每個要求，[!DNL Server API]會驗證資料流[!DNL access type]設定。 使用此設定，客戶可以設定資料串流以接受已驗證的資料，或同時接受已驗證和未驗證的資料。 預設情況下，接受兩種型別的資料。

如需有關設定資料流存取型別的詳細資訊，請參閱有關如何[建立和設定資料流](../datastreams/overview.md#create)的檔案。

以下是根據資料流[!DNL Access Type]設定和收到要求的端點之行為摘要。

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| 混合（預設） | 不驗證請求 | 驗證請求 |
| 已驗證 | 驗證請求 | 驗證請求 |

來自`server.adobedc.net`上私人伺服器的API呼叫一律應經過驗證。

## 先決條件 {#prerequisites}

呼叫[!DNL Server API]之前，請確定您符合下列必要條件：

* 您擁有可存取Adobe Experience Platform的組織帳戶。
* 您的Experience Platform帳戶已針對Adobe Experience Platform API產品設定檔啟用`developer`和`user`角色。 請連絡您的[Admin Console](../access-control/home.md)管理員，為您的帳戶啟用這些角色。
* 您有Adobe ID。 如果您沒有Adobe ID，請前往[Adobe Developer Console](https://developer.adobe.com/console)並建立新帳戶。

## 收集認證 {#credentials}

若要呼叫Experience Platform API，您必須先完成[驗證教學課程](../landing/api-authentication.md)。 完成驗證教學課程，在所有Experience Platform API呼叫中提供每個必要標題的值，如下所示：

* 授權：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

Experience Platform中的資源可以隔離到特定的虛擬沙箱。 在對Experience Platform API的請求中，您可以指定將執行作業的沙箱名稱和ID。 這些是選用引數。

* x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需Experience Platform中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../sandboxes/home.md)。

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* Content-Type： `application/json`

## 設定資料集寫入許可權 {#dataset-write-permissions}

若要設定資料集寫入許可權，請前往[Admin Console](https://adminconsole.adobe.com)，找出附加至API金鑰的產品設定檔，並設定下列許可權：

* 在[!UICONTROL 沙箱]區段中，選取資料流沙箱。
* 在[!UICONTROL 資料管理]區段中，選取&#x200B;**[!UICONTROL 管理資料集]**&#x200B;許可權。

## 疑難排解授權錯誤 {#troubleshooting-authorization}

| 錯誤代碼 | 錯誤訊息 | 說明 |
| --- | --- | --- |
| `EXEG-0500-401` | 授權權杖無效 | 此錯誤訊息會在下列任一情況下顯示：  <ul><li>缺少`authorization`標頭值。</li><li>`authorization`標頭值不包含必要的`Bearer`權杖。</li><li>提供的授權權杖格式無效。</li><li>資料流需要驗證，但請求缺少必要的標頭。</li></ul> |
| `EXEG-0501-401` | 無效的使用者授權權杖 | 此錯誤訊息會在下列任一情況下顯示： <ul><li>API呼叫缺少必要的`x-user-token`標頭。</li><li>提供的使用者權杖格式無效。</li></ul> |
| `EXEG-0502-401` | 授權權杖無效 | 當提供的授權權杖具有有效格式(JWT)，但其簽章無效時，會顯示此錯誤訊息。 請檢視[驗證教學課程](../landing/api-authentication.md)，瞭解如何取得有效的JWT權杖。 |
| `EXEG-0503-401` | 授權權杖無效 | 提供的授權權杖過期時，會顯示此錯誤訊息。 請完成[驗證教學課程](../landing/api-authentication.md)以產生新的權杖。 |
| `EXEG-0504-401` | 缺少必要產品內容。 | 此錯誤訊息會在下列任一情況下顯示：  <ul><li>開發人員帳戶無法存取Adobe Experience Platform產品內容。</li><li>公司帳戶尚未取得Adobe Experience Experience Platform的許可權。</li></ul> |
| `EXEG-0505-401` | 缺少所需的授權權杖範圍 | 此錯誤僅適用於服務帳戶驗證。 當呼叫中包含的服務授權權杖屬於沒有`acp.foundation` IMS範圍存取權的服務帳戶時，便會顯示錯誤訊息。 |
| `EXEG-0506-401` | 沙箱無法供寫入 | 當開發人員帳戶沒有`WRITE`定義資料流之Experience Platform沙箱的存取權時，便會顯示此錯誤訊息。 |
