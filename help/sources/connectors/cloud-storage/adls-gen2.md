---
keywords: Experience Platform；首頁；熱門主題；Azure Data Lake Storage Gen2;ADLS-Gen2;adls gen2;ADLS Gen2
solution: Experience Platform
title: Azure資料湖儲存Gen2源連接器概述
topic-legacy: overview
description: 了解如何使用API或使用者介面將Azure Data Lake Storage Gen2連線至Adobe Experience Platform。
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: 72c3000022db68284836cc7f2248154493100913
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Azure Data Lake Storage Gen2連接器

Adobe Experience Platform為AWS等雲端提供者提供原生連線， [!DNL Google Cloud Platform]，和 [!DNL Azure]，可讓您從這些系統帶入資料。

雲端儲存來源可將您自己的資料帶入 [!DNL Platform] 而無須下載、格式化或上傳。 擷取的資料可格式化為XDM JSON、XDM Parquet或分隔字元。 流程的每個步驟都整合至來源工作流程中。 [!DNL Platform] 可讓您將資料 [!DNL Azure Data Lake Storage Gen2] (ADLS-Gen2)，通過批次。

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

>[!IMPORTANT]
>
>此 [!DNL Azure Data Lake Storage Gen2] 來源不支援與Experience Platform的相同地區連線。 如果您的Azure執行個體使用與Experience Platform相同的網路區域，則無法建立與Experience Platform來源的連線。 設定您的 [!DNL Azure Data Lake Storage Gen2] 來源。 目前僅支援跨地區連線。

## 檔案和目錄的命名限制

以下是在命名雲儲存檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以斜線結尾(`/`)。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元： `" \ / : | < > * ?`.
- 不允許使用非法的URL路徑字元。 程式碼點，例如 `\uE000`，但在NTFS檔案名中有效，則不是有效的Unicode字元。 此外，某些ASCII或Unicode字元，如控制字元（0x00到0x1F、\u0081等）也不允許使用。 如需HTTP/1.1中管理Unicode字串的規則，請參閱 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允許使用下列檔案名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、NUL、CON、CON$、點字元(............................................................................

## Connect [!DNL Azure Data Lake Storage Gen2] to [!DNL Platform]

以下檔案提供如何連線的資訊 [!DNL Azure Data Lake Storage Gen2] to [!DNL Platform] 使用API或使用者介面：

### 使用API

- [使用流量服務API建立ADLS-Gen2基本連線](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [使用流量服務API探索雲端儲存空間來源的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服務API為雲儲存源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立ADLS-Gen2來源連線](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [在UI中為雲儲存連線建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
