---
keywords: Experience Platform；首頁；熱門主題；Azure檔案儲存；Azure檔案儲存
solution: Experience Platform
title: Azure檔案儲存Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Azure檔案儲存體連線到Adobe Experience Platform。
exl-id: 0a5e9df6-9760-4eeb-86d5-d92d77df3d2b
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Azure檔案儲存聯結器

Adobe Experience Platform為AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等雲端提供者提供原生連線，可讓您從這些系統帶入資料。

雲端儲存空間來源可以將您自己的資料帶入[!DNL Experience Platform]，而不需要下載、格式化或上傳。 內嵌的資料可以格式化為XDM JSON、XDM Parquet或分隔。 流程的每個步驟都會整合至來源工作流程。 [!DNL Experience Platform]可讓您透過批次從[!DNL Azure File Storage]匯入資料。

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 檔案和目錄的命名限制

以下是在命名雲端儲存空間檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)結尾。 如果提供，則會自動移除。
- 必須正確逸出下列保留的URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許下列字元： `" \ / : | < > * ?`。
- 不允許非法URL路徑字元。 類似`\uE000`的程式碼點雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的規則，請參閱[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許下列檔案名稱： LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 將[!DNL Azure File Storage]連線至[!DNL Experience Platform]

以下檔案提供如何使用API或使用者介面將[!DNL Azure File Storage]連線到[!DNL Experience Platform]的資訊：

### 使用API

- [使用Flow Service API建立Azure檔案儲存基礎連線](../../tutorials/api/create/cloud-storage/azure-file-storage.md)
- [使用流量服務API探索雲端儲存空間來源的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
- [使用流量服務API為雲端儲存空間來源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立Azure檔案儲存體來源連線](../../tutorials/ui/create/cloud-storage/azure-file-storage.md)
- [在UI中為雲端儲存空間連線建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
