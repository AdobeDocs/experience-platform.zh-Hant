---
keywords: Experience Platform；首頁；熱門主題；FTP;FTP;
solution: Experience Platform
title: FTP來源連接器概觀
topic-legacy: overview
description: 了解如何使用API或使用者介面將FTP伺服器連線至Adobe Experience Platform。
exl-id: a6186fad-8a7b-4103-80c7-a522ff69fe9e
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# (Beta)FTP連接器

>[!NOTE]
>
>FTP連接器為測試版。 有關使用測試版標籤連接器的詳細資訊，請參閱[來源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform為AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等雲提供商提供本機連接，允許您從這些系統中帶來資料。

雲端儲存來源可將您自己的資料帶入[!DNL Platform]，而無需下載、格式化或上傳。 擷取的資料可格式化為XDM JSON、XDM Parquet或分隔字元。 流程的每個步驟都整合至來源工作流程中。 [!DNL Platform] 可讓您透過批次從FTP或SFTP伺服器匯入資料。

>[!IMPORTANT]
>
>使用FTP來源連接器建立資料流時，強烈建議設定一次性擷取排程，因為FTP伺服器內發生的增量更新延遲問題。

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 檔案和目錄的命名限制

以下是在命名雲儲存檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以斜線(`/`)結尾。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出：`! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元：`" \ / : | < > * ?`。
- 不允許使用非法的URL路徑字元。 代碼點（如`\uE000`）在NTFS檔案名中有效，但不是有效的Unicode字元。 此外，某些ASCII或Unicode字元，如控制字元（0x00到0x1F、\u0081等）也不允許使用。 有關HTTP/1.1中管理Unicode字串的規則，請參閱[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許使用下列檔案名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、NUL、CON、CON$、點字元(............................................................................

## 將FTP連接到[!DNL Platform]

以下檔案提供如何使用API或使用者介面將FTP伺服器連線至[!DNL Platform]的資訊：

### 使用API

- [使用流量服務API建立FTP基礎連線](../../tutorials/api/create/cloud-storage/ftp.md)
- [使用流量服務API探索雲端儲存空間來源的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服務API為雲儲存源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立FTP來源連線](../../tutorials/ui/create/cloud-storage/ftp.md)
- [在UI中為雲儲存連線建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
