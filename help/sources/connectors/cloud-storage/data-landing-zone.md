---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 資料登錄區源
topic-legacy: overview
description: 了解如何將資料登陸區連接至Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] 是Adobe Experience Platform [!DNL Azure Blob] 所布建的儲存介面，可讓您存取安全、雲端型的檔案儲存功能，將檔案匯入Platform。您可以存取每個沙箱一個[!DNL Data Landing Zone]容器，且所有容器的資料量總計僅限於您的Platform Produces and Services授權隨附的資料總計。 Platform及其應用程式服務（例如[!DNL Customer Journey Analytics]、[!DNL Journey Orchestration]、[!DNL Intelligent Services]和[!DNL Real-time Customer Data Platform]）的所有客戶，都會為每個沙箱布建一個[!DNL Data Landing Zone]容器。 您可以透過[!DNL Azure Storage Explorer]或命令列介面，將檔案讀取及寫入容器。

[!DNL Data Landing Zone] 支援基於SAS的身份驗證，其資料受靜態和在 [!DNL Azure Blob] 途的標準儲存安全機制保護。基於SAS的身份驗證允許通過公共Internet連接安全地訪問您的[!DNL Data Landing Zone]容器。 訪問[!DNL Data Landing Zone]容器不需要任何網路更改，這意味著您不需要為網路配置任何允許清單或跨區域設定。 平台會對上傳至[!DNL Data Landing Zone]容器的所有檔案執行嚴格的七天存留時間(TTL)。 所有檔案會在七天後刪除。

## 檔案和目錄的命名限制

以下是在命名雲儲存檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以斜線(`/`)結尾。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出：`! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元：`" \ / : | < > * ?`。
- 不允許使用非法的URL路徑字元。 代碼點（如`\uE000`）在NTFS檔案名中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（例如`0x00`至`0x1F`、`\u0081`等）。 有關HTTP/1.1中管理Unicode字串的規則，請參閱[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許使用下列檔案名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、NUL、CON、CON$、點字元(............................................................................

## 將[!DNL Data Landing Zone]連接到[!DNL Platform]

以下檔案提供如何使用API或使用者介面，將資料從[!DNL Data Landing Zone]容器帶入Adobe Experience Platform的資訊。

### 使用API

- [使用流服務API建立 [!DNL Data Landing Zone] 源連接](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [使用流服務API為雲儲存源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [使用UI連線 [!DNL Data Landing Zone] 至Platform](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [在UI中為雲儲存連線建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
