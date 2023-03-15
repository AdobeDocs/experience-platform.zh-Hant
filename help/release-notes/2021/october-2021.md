---
title: Adobe Experience Platform發行說明2021年10月
description: 2021年10月Adobe Experience Platform發行說明。
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 8%

---

# Adobe Experience Platform 發行說明

**發行日期：2021 年 10 月 27 日**

## 更新Experience Platform

更新Experience Platform。

### 使用者介面 {#ui}

使用者介面已更新，並有下列變更：

| 功能 | 說明 |
| --- | --- |
| 深色佈景主題 | 使用深色主題切換，在Platform介面的淺色主題和深色主題之間切換。 交換機位於用戶名和電子郵件下的用戶配置檔案中。 |
| 切換左側導覽 | 使用應用程式標題頂端改良的導覽切換按鈕，來顯示或隱藏顯示您的Experience Platform功能的功能表。 系統會記住您上次的選取，並只顯示您有權存取的功能。 |
| 存取可見性 | 左側導覽列只顯示您可存取的功能。 在舊版Adobe Experience Platform中，即使您無法存取無法使用的項目，也會顯示這些項目。 |

請參閱 [Platform UI指南](../../landing/ui-guide.md) 了解更多。

## 更新現有功能

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Prep]](#data-prep)
- [來源](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| `contains_key` 函數 | 此 `contains_key` 函式，可讓您檢查物件是否存在於來源中。 此函式會取代 `is_set` 函式，現已過時。 |
| 錯誤訊息 | 由 `/mappingSets/preview` 資料準備API中的端點現在與執行階段產生的錯誤訊息一致。 |

請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md) 以進一步了解此服務。

### 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

| 功能 | 說明 |
| --- | --- |
| [!DNL Amazon S3] 來源增強功能 | 您現在可以使用 `s3SessionToken` 參數來連接 [!DNL Amazon S3] 帳戶傳至Platform（使用暫時安全性憑證）。 此代號可讓您提供對 [!DNL Amazon S3] 資源給不受信任環境中的用戶。 如需詳細資訊，請參閱[[!DNL Amazon S3] 文件](../../sources/connectors/cloud-storage/s3.md#prerequisites)。 |
| [!DNL Generic REST API] （測試版） | 您現在可以建立 [!DNL Generic REST API] 源連接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) 將一般REST應用程式的資料帶入Platform。 請參閱 [[!DNL Generic REST API] 概述](../../sources/connectors/protocols/generic-rest.md) 以取得更多資訊。 |
| [!DNL Zoho CRM] （測試版） | 您現在可以建立 [!DNL Zoho CRM] 源連接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) 或 [使用者介面](../../sources/tutorials/ui/create/crm/zoho.md) 從 [!DNL Zoho CRM] 帳戶至Platform。 請參閱 [[!DNL Zoho CRM] 概述](../../sources/connectors/crm/zoho.md) 以取得更多資訊。 |

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
