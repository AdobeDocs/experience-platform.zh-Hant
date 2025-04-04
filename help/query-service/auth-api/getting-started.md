---
keywords: Experience Platform；查詢服務；IP存取控制；授權；API；快速入門
title: 資料Distiller Authorization API指南
description: 瞭解如何在Adobe Experience Platform的查詢服務中開始進行授權和IP範圍限制的安全資料存取。
role: Developer
exl-id: d93ce774-c8b2-4f15-a4d9-117d9aa5d9e7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 5%

---

# 開始使用資料Distiller Authorization API

>[!AVAILABILITY]
>
>已購買Data Distiller附加元件的客戶可使用此功能。 如需詳細資訊，請聯絡您的 Adobe 代表。

資料Distiller授權API可透過Adobe Experience Platform中的SQL介面，為組織提供更嚴格的資料存取控制。 您可以使用此API來定義IP限制、限制對指定網路的資料存取，以及增強安全性監視。

本指南概述如何設定呼叫Data Distiller Authorization API所需的授權認證和許可權。

## 快速入門 {#getting-started}

以下幾節提供有關準備所需授權值和向資料Distiller Authorization API發出第一個請求的資訊。

### 必要權限 {#required-permissions}

若要在查詢服務中啟用安全資料存取限制，您需要&#x200B;**[!UICONTROL 管理允許清單]**&#x200B;許可權。 此許可權可讓組織定義特定IP範圍（IPv4或IPv6格式），這些範圍有權透過SQL介面存取Experience Platform中的資料。 存取在沙箱層級管理，使用者可以設定核准IP位址或CIDR區塊清單，將存取限製為僅存取允許的網路。

>[!NOTE]
>
>系統管理員可以從Adobe [Admin Console](https://adminconsole.adobe.com/)設定使用者許可權。 如需詳細資訊，請參閱 [Admin Console 使用手冊](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)。

下列功能具有&#x200B;**[!UICONTROL 管理允許清單]**&#x200B;許可權：

- **定義允許的IP範圍**：只有來自這些定義範圍的IP位址或CIDR區塊才能使用SQL透過查詢服務存取Experience Platform中的資料。
- **強制IP範圍檢查**：拒絕來自允許範圍以外之IP的連線。
- **稽核和警示功能**：所有存取嘗試（包括被拒絕的連線）都會記錄為稽核事件。 這些事件可在[Adobe Experience Platform稽核記錄](../../landing/governance-privacy-security/audit-logs/overview.md)中取得，以監視潛在的安全性違規。

### 收集所需標頭的值 {#gather-values-for-required-headers}

若要呼叫Data Distiller Authorization API，您必須完成[Experience Platform API驗證教學課程](../../landing/api-authentication.md)，此教學課程會提供API呼叫中所需標頭的值。 在每個請求中包含以下標頭：

- **授權**： `Bearer {ACCESS_TOKEN}`
- **x-api-key**： `{API_KEY}`
- **x-gw-ims-org-id**： `{ORG_ID}`
- **x-sandbox-name**： `{SANDBOX_NAME}`

>[!NOTE]
>
> 如需沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

包含裝載(POST、PUT、PATCH)的所有請求也需要此標題：

- **內容型別**： `application/json`

### 後續步驟

收集到所需的許可權和標頭值後，您就可以開始為查詢服務設定IP限制。 請繼續參閱端點檔案，以取得CRUD操作的詳細範例，包括：

- API格式和範例要求/回應配對。
- 每個作業的表頭、裝載及回應代碼。

每個API呼叫範例都會示範如何格式化要求及詮釋回應，協助您在Query Service中強制安全存取資料。

如需設定及驗證IP限制的特定指示，請參閱[IP存取端點檔案](./ip-access.md)和[IP驗證端點檔案](./validate.md)。

請參閱[Data Distiller Authorization OpenAPI參考檔案](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/)，以檢視標準化、機器可讀的格式，更易於整合、測試和探索。
