---
keywords: Experience Platform；首頁；熱門主題；Oracle對象儲存；oracle對象儲存
solution: Experience Platform
title: Oracle對象儲存源連接器概述
description: 瞭解如何使用API或用戶介面將Oracle對象儲存連接到Adobe Experience Platform。
exl-id: 5e8b85c8-9f01-49a6-9556-7b9c7518fb4b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Oracle對象儲存連接器

Adobe Experience Platform提供本地連接，如AWS, [!DNL Google Cloud Platform]，允許您將這些系統中的資料帶到平台中，以用於下游服務和目標。

雲儲存源可以將資料帶入平台，而無需下載、格式化或上載。 所攝取的資料可以格式化為XDM JSON、XDM Parke或分隔。 流程的每個步驟都整合到源工作流中。 平台允許您從 [!DNL Oracle Object Storage] 批處理。

## IP地址允許清單

在使用源連接器之前，必須將IP地址清單添加到允許清單。 如果無法將特定於區域的IP地址添加到允許清單，則在使用源時可能會導致錯誤或效能不佳。 查看 [IP地址允許清單](../../ip-address-allow-list.md) 的子菜單。

## 檔案和目錄的命名約束

以下是命名雲儲存檔案或目錄時必須考慮的約束條件清單：

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以正斜槓結尾(`/`)。 如果提供，將自動刪除。
- 必須正確轉義以下保留URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用以下字元： `" \ / : | < > * ?`。
- 不允許使用非法的URL路徑字元。 代碼點類似 `\uE000`，但在NTFS檔案名中有效，則不是有效的Unicode字元。 此外，還不允許使用某些ASCII或Unicode字元，如控制字元（0x00到0x1F、\u0081等）。 有關HTTP/1.1中Unicode字串的規則，請參見 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許使用下列檔案名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM9、COM9prn、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 連接 [!DNL Oracle Object Storage] 到平台

以下文檔提供了有關如何使用API或用戶介面將Oracle對象儲存連接到Adobe Experience Platform的資訊：

### 使用API

- [使用流服務API建立Oracle對象儲存基連接](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [使用流服務API瀏覽雲儲存源的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服務API為雲儲存源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立Oracle對象儲存源連接](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [在UI中為雲儲存連接建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
