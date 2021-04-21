---
keywords: Experience Platform;home；熱門主題；Blob;blob;Azure Blob;azure blob
solution: Experience Platform
title: Azure Blob來源連接器概述
topic-legacy: overview
description: 瞭解如何使用API或使用者介面將Azure Blob連接至Adobe Experience Platform。
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Azure Blob連接器

Adobe Experience Platform為AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等雲提供商提供本機連接。 您可以將這些系統中的資料導入[!DNL Platform]。

雲端儲存來源可將您自己的資料匯入[!DNL Platform]，而不需下載、格式化或上傳。 收錄的資料可格式化為XDM JSON、XDM Parce或分隔。 此程式的每個步驟都會整合至Sources工作流程中。 [!DNL Platform] 允許您從批中導入 [!DNL Azure Blob] 資料。

## IP位址允許清單

在使用來源連接器之前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

>[!IMPORTANT]
>
>[!DNL Azure Blob]源連接器當前不支援與平台的相同區域連接。 這表示如果您的Azure例項使用與平台相同的網路區域，則無法建立與平台來源的連線。 目前僅支援跨地區連線。 如需詳細資訊，請洽詢您的Adobe客戶經理。

## 檔案和目錄的命名限制

以下是您在命名雲端儲存檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以正斜線(`/`)結尾。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出：`! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元：`" \ / : | < > * ?`。
- 不允許非法的URL路徑字元。 代碼點（如`\uE000`）在NTFS檔案名中有效，但不是有效的Unicode字元。 此外，也不允許某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 有關HTTP/1.1中管理Unicode字串的規則，請參見[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許使用下列檔案名稱：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、prn, AUX, NUL, CON, CLOCK$，點字元(.)和兩個點字元(..)。

## 將[!DNL Azure Blob]連接到[!DNL Platform]

以下檔案提供如何使用API或使用者介面將Azure Blob連接至Adobe Experience Platform的資訊：

### 使用API

- [使用流程服務API建立Azure Blob來源連線](../../tutorials/api/create/cloud-storage/blob.md)
- [使用Flow Service API探索雲端儲存系統](../../tutorials/api/explore/cloud-storage.md)
- [使用Flow Service API收集雲端儲存空間資料](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立Azure Blob來源連線](../../tutorials/ui/create/cloud-storage/blob.md)
- [在UI中為雲端儲存區連線設定資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
