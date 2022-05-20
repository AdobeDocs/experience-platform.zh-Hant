---
title: Adobe Experience Platform發行說明2021年10月
description: 2021年10月為Adobe Experience Platform發佈的說明。
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 8%

---

# Adobe Experience Platform 發行說明

**發行日期：2021 年 10 月 27 日**

## 更新到Experience Platform

更新Experience Platform。

### 使用者介面 {#ui}

用戶介面已更新，更改如下：

| 功能 | 說明 |
| --- | --- |
| 深色佈景主題 | 使用「暗」主題開關在平台介面中的亮主題和暗主題之間切換。 交換機位於用戶名和電子郵件下的用戶配置檔案中。 |
| 切換左側導航 | 使用應用程式標題頂部的改進的導航切換來顯示或隱藏顯示Experience Platform功能的菜單。 系統會記住您上次選擇的內容，並只顯示您有權訪問的功能。 |
| 訪問可見性 | 左側導航欄僅顯示您可以訪問的功能。 在以前的Adobe Experience Platform版本中，即使您無法訪問不可用的項目，也是可見的。 |

查看 [平台UI指南](../../landing/ui-guide.md) 來瞭解更多資訊。

## 對現有功能的更新

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Prep]](#data-prep)
- [來源](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| `contains_key` 函數 | 的 `contains_key` 函式已引入，用於檢查源中是否存在對象。 此函式將替換 `is_set` 函式，現在已棄用。 |
| 錯誤訊息 | 返回的錯誤消息 `/mappingSets/preview` 資料準備API中的端點現在與運行時生成的錯誤消息一致。 |

查看 [[!DNL Data Prep] 概述](../../data-prep/home.md) 瞭解有關此服務的詳細資訊。

### 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

| 功能 | 說明 |
| --- | --- |
| [!DNL Amazon S3] 源增強 | 您現在可以使用 `s3SessionToken` 連接 [!DNL Amazon S3] 帳戶到平台，使用臨時安全憑據。 此令牌允許您提供對您的 [!DNL Amazon S3] 資源到不受信任環境中的用戶。 如需詳細資訊，請參閱[[!DNL Amazon S3] 文件](../../sources/connectors/cloud-storage/s3.md#prerequisites)。 |
| [!DNL Generic REST API] (Beta) | 現在可以建立 [!DNL Generic REST API] 源連接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) 將資料從通用REST應用程式帶到平台。 查看 [[!DNL Generic REST API] 概述](../../sources/connectors/protocols/generic-rest.md) 的子菜單。 |
| [!DNL Zoho CRM] (Beta) | 現在可以建立 [!DNL Zoho CRM] 源連接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) 或 [用戶介面](../../sources/tutorials/ui/create/crm/zoho.md) 從 [!DNL Zoho CRM] 帳戶到平台。 查看 [[!DNL Zoho CRM] 概述](../../sources/connectors/crm/zoho.md) 的子菜單。 |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
