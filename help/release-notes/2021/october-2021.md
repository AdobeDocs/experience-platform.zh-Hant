---
title: Adobe Experience Platform發行說明2021年10月
description: Adobe Experience Platform 2021 年 10 月版本注意事項。
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 24%

---

# Adobe Experience Platform 發行說明

**發行日期： 2021年10月27日**

## Experience Platform的更新

Experience Platform的更新。

### 使用者介面 {#ui}

使用者介面已更新，其中包含下列變更：

| 功能 | 說明 |
| --- | --- |
| 深色主題 | 在Platform介面中，使用深色佈景主題切換開關，在淺色和深色佈景主題之間切換。 交換器位於使用者名稱和電子郵件下的使用者設定檔中。 |
| 切換左側導覽 | 使用改善的應用程式標題頂端的導覽切換按鈕，可顯示或隱藏顯示Experience Platform功能的功能表。 系統會記住您最後的選擇，並僅顯示您有權存取的功能。 |
| 存取可見性 | 左側導覽列僅顯示您可以存取的功能。 在舊版Adobe Experience Platform中，即使您無法存取，也會顯示無法使用的專案。 |

請參閱[平台UI指南](../../landing/ui-guide.md)以深入瞭解。

## 現有功能的更新

Adobe Experience Platform 現有功能的更新：

- [[!DNL Data Prep]](#data-prep)
- [來源](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| `contains_key`函式 | 已引入`contains_key`函式，可讓您檢查來源中是否存在物件。 此函式取代`is_set`函式，該函式現已棄用。 |
| 錯誤訊息 | 資料準備API中`/mappingSets/preview`端點傳回的錯誤訊息現在與執行階段產生的錯誤訊息一致。 |

請參閱[[!DNL Data Prep] 總覽](../../data-prep/home.md)以進一步瞭解此服務。

### 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

| 功能 | 說明 |
| --- | --- |
| [!DNL Amazon S3]個來源增強功能 | 您現在可以使用`s3SessionToken`引數，使用暫時性安全性認證將您的[!DNL Amazon S3]帳戶連線至Platform。 此Token可讓您向不受信任環境中的使用者提供對您[!DNL Amazon S3]資源的短期暫時存取權。 如需詳細資訊，請參閱[[!DNL Amazon S3] 文件](../../sources/connectors/cloud-storage/s3.md#prerequisites)。 |
| [!DNL Generic REST API] (Beta) | 您現在可以使用[[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md)建立[!DNL Generic REST API]來源連線，將一般REST應用程式的資料帶入Platform。 如需詳細資訊，請參閱[[!DNL Generic REST API] 概觀](../../sources/connectors/protocols/generic-rest.md)。 |
| [!DNL Zoho CRM] (Beta) | 您現在可以使用[[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md)或[使用者介面](../../sources/tutorials/ui/create/crm/zoho.md)建立[!DNL Zoho CRM]來源連線，將您的[!DNL Zoho CRM]帳戶中的資料帶到Platform。 如需詳細資訊，請參閱[[!DNL Zoho CRM] 概觀](../../sources/connectors/crm/zoho.md)。 |

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
