---
keywords: Experience Platform；主題；熱門主題；HDFS;hdfs;Apache HDFS;apache hdfs
solution: Experience Platform
title: Apache HDFS源連接器概述
description: 瞭解如何使用API或用戶介面將Apache HDFS連接到Adobe Experience Platform。
exl-id: 1f156f7b-a19d-4dcf-a51d-ab6cb396d8f7
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# (Beta) [!DNL Apache] HDFS連接器

>[!NOTE]
>
>Apache HDFS連接器為beta。 查看 [源概述](../../home.md#terms-and-conditions) 的子菜單。

Adobe Experience Platform提供本地連接，如AWS, [!DNL Google Cloud Platform], [!DNL Azure]，允許您從這些系統中獲取資料。 接收的資料可以格式化為JSON、Parke或分隔。 對雲儲存提供商的支援包括 [!DNL Apache] HDFS。

## IP地址允許清單

在使用源連接器之前，必須將IP地址清單添加到允許清單。 如果無法將特定於區域的IP地址添加到允許清單，則在使用源時可能會導致錯誤或效能不佳。 查看 [IP地址允許清單](../../ip-address-allow-list.md) 的子菜單。

## 檔案和目錄的命名約束

以下是命名雲儲存檔案或目錄時必須考慮的約束條件清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以正斜槓結尾(`/`)。 如果提供，將自動刪除。
- 必須正確轉義以下保留URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用以下字元： `" \ / : | < > * ?`。
- 不允許使用非法的URL路徑字元。 代碼點類似 `\uE000`，但在NTFS檔案名中有效，則不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，如控制字元（0x00到0x1F、\u0081等）。 有關HTTP/1.1中Unicode字串的規則，請參見 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許使用下列檔案名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM9、COM9prn、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 連接 [!DNL Apache] HDFS到 [!DNL Platform]

以下文檔提供了有關如何連接的資訊 [!DNL Apache] HDFS到 [!DNL Platform] 使用API或用戶介面：

### 使用API

- [使用流服務API建立HDFS基連接](../../tutorials/api/create/cloud-storage/hdfs.md)
- [使用流服務API瀏覽雲儲存源的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服務API為雲儲存源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立Apache HDFS源連接](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [在UI中為雲儲存連接建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
