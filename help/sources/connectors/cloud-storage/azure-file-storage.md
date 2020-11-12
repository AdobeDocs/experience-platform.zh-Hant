---
keywords: Experience Platform;home;popular topics;Azure File Storage;azure file storage
solution: Experience Platform
title: Azure檔案儲存連接器
topic: overview
description: 以下檔案提供如何使用API或使用者介面將Azure檔案儲存連接至平台的資訊。
translation-type: tm+mt
source-git-commit: e0a0b7fc28b8cc85c5140d3840e06e5c7078c307
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---


# （測試版）Azure檔案儲存連接器

>[!NOTE]
>
>Azure檔案儲存連接器正在測試中。 如需使用 [測試版標籤連接器的詳細資訊](../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform為AWS等雲端提供商提供原生連接 [!DNL Google Cloud Platform]功能 [!DNL Azure]，讓您能夠從這些系統中取得資料。

雲端儲存來源可將您自己的資料匯入 [!DNL Platform] 其中，而不需下載、格式化或上傳。 收錄的資料可格式化為XDM JSON、XDM鑲木地板或分隔字元。 此程式的每個步驟都會整合至Sources工作流程中。 [!DNL Platform] 允許您從批中導入 [!DNL Azure File Storage] 資料。

## IP位址允許清單

在使用來源連接器之前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細 [資訊，請參閱](../../ip-address-allow-list.md) 「IP位址允許清單」頁面。

## 檔案和目錄的命名限制

以下是您在命名雲端儲存檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以斜線(`/`)結尾。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出： `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- 不允許使用下列字元： `" \ / : | < > * ?`.
- 不允許非法的URL路徑字元。 代碼點（如） `\uE000`在NTFS檔案名中有效時，是無效的Unicode字元。 此外，也不允許某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 有關HTTP/1.1中管理Unicode字串的規則，請參見 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許使用下列檔案名稱：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、prn, AUX, NUL, CON, CLOCK$，點字元(.)和兩個點字元(..)。

## 連線 [!DNL Azure File Storage] 至 [!DNL Platform]

以下檔案提供如何連線至使用API [!DNL Azure File Storage] 或使 [!DNL Platform] 用者介面的資訊：

### 使用API

- [使用流程服務API建立Azure檔案儲存連接器](../../tutorials/api/create/cloud-storage/azure-file-storage.md)
- [使用Flow Service API探索雲端儲存系統](../../tutorials/api/explore/cloud-storage.md)
- [使用Flow Service API收集雲端儲存空間資料](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立Azure檔案儲存來源連接器](../../tutorials/ui/create/cloud-storage/azure-file-storage.md)
- [在UI中為雲端儲存連接器設定資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)