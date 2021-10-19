---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 資料登錄區源
topic-legacy: overview
description: 了解如何將資料登陸區連接至Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ecc9bc603bfd7b56f5f232b0d6d91eb65a901510
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform布建的儲存介面，可授予您存取安全、雲端型檔案儲存功能，將檔案匯入Platform。 您可以存取 [!DNL Data Landing Zone] 每個沙箱的容器，且所有容器的資料量總計僅限於您的Platform產品與服務授權隨附的資料總計。 Platform及其應用程式服務的所有客戶，例如 [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]，和 [!DNL Real-time Customer Data Platform] 已布建一個 [!DNL Data Landing Zone] 每個沙箱的容器。 您可以透過 [!DNL Azure Storage Explorer] 或命令列介面。

[!DNL Data Landing Zone] 支援基於SAS的身份驗證，其資料受標準保護 [!DNL Azure Blob] 儲存安全機制處於閒置狀態和在途。 基於SAS的身份驗證允許您安全地訪問 [!DNL Data Landing Zone] 容器。 訪問您的 [!DNL Data Landing Zone] 容器，這表示您不需要為網路設定任何允許清單或跨地區設定。 平台會對上傳至 [!DNL Data Landing Zone] 容器。 所有檔案會在七天後刪除。

## 檔案和目錄的命名限制

以下是在命名雲儲存檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以斜線結尾(`/`)。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元： `" \ / : | < > * ?`.
- 不允許使用非法的URL路徑字元。 程式碼點，例如 `\uE000`，但在NTFS檔案名中有效，則不是有效的Unicode字元。 此外，有些ASCII或Unicode字元，例如控制字元(例如 `0x00` to `0x1F`, `\u0081`、等)，也不允許。 如需HTTP/1.1中管理Unicode字串的規則，請參閱 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允許使用下列檔案名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、NUL、CON、CON$、點字元(............................................................................

## Connect [!DNL Data Landing Zone] to [!DNL Platform]

以下檔案提供如何從 [!DNL Data Landing Zone] 容器至Adobe Experience Platform。

### 使用API

- [建立 [!DNL Data Landing Zone] 源連接（使用流服務API）](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [使用流服務API為雲儲存源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [Connect [!DNL Data Landing Zone] 使用UI設為Platform](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [在UI中為雲儲存連線建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
