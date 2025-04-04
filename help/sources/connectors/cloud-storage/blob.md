---
keywords: Experience Platform；首頁；熱門主題；Blob；Blob；Azure Blob；Azure Blob
solution: Experience Platform
title: Azure Blob Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Azure Blob連線至Adobe Experience Platform。
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Azure Blob聯結器

Adobe Experience Platform為AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等雲端提供者提供原生連線。 您可以將資料從這些系統帶入[!DNL Experience Platform]。

雲端儲存空間來源可以將您自己的資料帶入[!DNL Experience Platform]，而不需要下載、格式化或上傳。 內嵌的資料可以格式化為XDM JSON、XDM Parquet或分隔。 流程的每個步驟都會整合至來源工作流程。 [!DNL Experience Platform]可讓您透過批次從[!DNL Azure Blob]匯入資料。

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

>[!IMPORTANT]
>
>[!DNL Azure Blob]來源不支援與Experience Platform的相同區域連線。 如果您的[!DNL Azure]執行個體使用與Experience Platform相同的網路區域，則無法建立與Experience Platform來源的連線。 目前僅支援跨區域連線。

## 檔案和目錄的命名限制

以下是在命名雲端儲存空間檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)結尾。 如果提供，則會自動移除。
- 必須正確逸出下列保留的URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許下列字元： `" \ / : | < > * ?`。
- 不允許非法URL路徑字元。 類似`\uE000`的程式碼點雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的規則，請參閱[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許下列檔案名稱： LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 將[!DNL Azure Blob]連線至[!DNL Experience Platform]

以下檔案提供如何使用API或使用者介面將Azure Blob連線至Adobe Experience Platform的資訊：

### 使用API

- [使用流程服務API建立Azure Blob基本連線](../../tutorials/api/create/cloud-storage/blob.md)
- [使用流量服務API探索雲端儲存空間來源的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
- [使用流量服務API為雲端儲存空間來源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在使用者介面中建立Azure Blob來源連線](../../tutorials/ui/create/cloud-storage/blob.md)
- [在UI中為雲端儲存空間連線建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
