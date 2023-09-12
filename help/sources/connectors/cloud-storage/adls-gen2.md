---
title: Azure Data Lake Storage Gen2來源聯結器概觀
description: 瞭解如何使用API或使用者介面將Azure Data Lake Storage Gen2連線至Adobe Experience Platform。
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: f879f2a627e55db96a89796b9f3308744bf93f67
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Azure Data Lake Storage Gen2聯結器

Adobe Experience Platform為AWS等雲端服務供應商提供原生連線， [!DNL Google Cloud Platform]、和 [!DNL Azure]，可讓您從這些系統帶入資料。

雲端儲存空間來源可將您自己的資料帶入Experience Platform，無需下載、格式化或上傳。 內嵌的資料可以格式化為XDM JSON、XDM Parquet或分隔。 流程的每個步驟都會整合至來源工作流程。 Experience Platform可讓您從匯入資料 [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2)。

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

>[!IMPORTANT]
>
>此 [!DNL Azure Data Lake Storage Gen2] 來源不支援與Experience Platform的相同區域連線。 如果您的Azure執行個體使用與Experience Platform相同的網路區域，則無法建立與Experience Platform來源的連線。 設定時，請勿使用Azure美國東部2、Azure西歐和Azure澳洲東部區域 [!DNL Azure Data Lake Storage Gen2] 來源。 目前僅支援跨區域連線。

## 檔案和目錄的命名限制

以下是在命名雲端儲存空間檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元： `" \ / : | < > * ?`.
- 不允許非法URL路徑字元。 程式碼點數如下 `\uE000`雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的管理規則，請參閱 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允許下列檔案名稱： LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 連線 [!DNL Azure Data Lake Storage Gen2] 至Experience Platform

>[!NOTE]
>
>用於建立 [!DNL Azure Data Lake Storage Gen2] 帳戶應至少具有 **儲存Blob資料Reader** 從存取控制(IAM)指派的角色

以下檔案提供有關如何連線的資訊 [!DNL Azure Data Lake Storage Gen2] 若要使用API或使用者介面Experience Platform：

### 使用API

- [建立 [!DNL Azure Data Lake Storage Gen2] 使用流量服務API的基礎連線](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [使用流量服務API探索雲端儲存空間來源的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
- [使用流量服務API為雲端儲存空間來源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [建立 [!DNL Azure Data Lake Storage Gen2] ui中的來源連線](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [在UI中為雲端儲存空間連線建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
