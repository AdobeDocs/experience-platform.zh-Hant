---
keywords: Experience Platform;home；熱門主題；FTP;ftp;
solution: Experience Platform
title: FTP來源連接器概述
topic: 概述
description: 瞭解如何使用API或使用者介面將FTP伺服器連線至Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: 7fc99214272d2ce743b3666826c66f5d65e4d2ca
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# （測試版）FTP連接器

>[!NOTE]
>
>FTP連接器處於測試階段。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../home.md#terms-and-conditions)。

Adobe Experience Platform為AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等雲提供商提供了本機連接，使您能夠從這些系統中獲取資料。

雲端儲存來源可將您自己的資料匯入[!DNL Platform]，而不需下載、格式化或上傳。 收錄的資料可格式化為XDM JSON、XDM Parce或分隔。 此程式的每個步驟都會整合至Sources工作流程中。 [!DNL Platform] 可讓您透過批次從FTP或SFTP伺服器匯入資料。

>[!IMPORTANT]
>
>當使用FTP來源連接器建立資料流時，強烈建議您設定一次性擷取排程，因為FTP伺服器中遇到的增量更新問題仍未解決。

## IP位址允許清單

在使用來源連接器之前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 檔案和目錄的命名限制

以下是您在命名雲端儲存檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以正斜線(`/`)結尾。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出：`! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元：`" \ / : | < > * ?`。
- 不允許非法的URL路徑字元。 代碼點（如`\uE000`）在NTFS檔案名中有效，但不是有效的Unicode字元。 此外，也不允許某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 有關HTTP/1.1中管理Unicode字串的規則，請參見[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許使用下列檔案名稱：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、prn, AUX, NUL, CON, CLOCK$，點字元(.)和兩個點字元(..)。

## 將FTP連接至[!DNL Platform]

以下檔案提供如何使用API或使用者介面將FTP伺服器連線至[!DNL Platform]的資訊：

### 使用API

- [使用流程服務API建立FTP來源連線](../../tutorials/api/create/cloud-storage/ftp.md)
- [使用Flow Service API探索雲端儲存系統](../../tutorials/api/explore/cloud-storage.md)
- [使用Flow Service API收集雲端儲存空間資料](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立FTP來源連線](../../tutorials/ui/create/cloud-storage/ftp.md)
- [在UI中為雲端儲存區連線設定資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)