---
keywords: Experience Platform；首頁；熱門主題；Google雲端儲存空間；google雲端儲存空間
solution: Experience Platform
title: Google雲端儲存來源連接器概觀
topic: 概述
description: 瞭解如何使用API或使用者介面將Google雲端儲存空間連線至Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: 7fc99214272d2ce743b3666826c66f5d65e4d2ca
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---


# Google雲端儲存空間連接器

Adobe Experience Platform為AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等雲提供商提供了本機連接，使您能夠從這些系統中獲取資料。

雲端儲存來源可將您自己的資料匯入平台，而不需下載、格式化或上傳。 收錄的資料可以格式化為符合「體驗資料模型」(XDM)的JSON或Parce，或以分隔格式。 流程的每個步驟都整合在來源工作流程中。 平台允許您從[!DNL Google Cloud Storage]通過批導入資料。

## IP位址允許清單

在使用來源連接器之前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 連接[!DNL Google Cloud Storage]帳戶的先決條件設定

為了連接到平台，您必須首先啟用[!DNL Google Cloud Storage]帳戶的互操作性。 要訪問互操作性設定，請開啟[!DNL Google Cloud Platform]並從導航面板的&#x200B;**[!UICONTROL Cloud Storage]**&#x200B;選項中選擇&#x200B;**[!UICONTROL Settings]**。

![](../../images/tutorials/create/google-cloud-storage/nav.png)

此時將顯示&#x200B;**[!UICONTROL Settings]**&#x200B;頁。 從這裡，您可以看到有關[!DNL Google]專案ID的資訊，以及有關[!DNL Google Cloud Storage]帳戶的詳細資訊。 要訪問互操作性設定，請從頂部標題中選擇&#x200B;**[!UICONTROL Interoperability]**。

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

**[!UICONTROL Interoperability]**&#x200B;頁包含有關驗證、訪問密鑰和與服務帳戶關聯的預設項目的資訊。 要為服務帳戶生成新的訪問密鑰ID和秘密訪問密鑰，請選擇&#x200B;**[!UICONTROL Create a Key for a Service Account]**。

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新產生的存取金鑰ID和機密存取金鑰，將您的[!DNL Google Cloud Storage]帳戶連接至平台。

## 檔案和目錄的命名限制

以下是您在命名雲端儲存檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以正斜線(`/`)結尾。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出：`! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元：`" \ / : | < > * ?`。
- 不允許非法的URL路徑字元。 代碼點（如`\uE000`）在NTFS檔案名中有效，但不是有效的Unicode字元。 此外，也不允許某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 有關HTTP/1.1中管理Unicode字串的規則，請參見[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許使用下列檔案名稱：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、prn, AUX, NUL, CON, CLOCK$，點字元(.)和兩個點字元(..)。

## 將[!DNL Google Cloud Storage]連接到平台

以下檔案提供如何使用API或使用者介面將[!DNL Google Cloud Storage]連線至平台的資訊：

### 使用API

- [使用Flow Service API建立Google雲端儲存空間來源連線](../../tutorials/api/create/cloud-storage/google.md)
- [使用Flow Service API探索雲端儲存系統](../../tutorials/api/explore/cloud-storage.md)
- [使用Flow Service API收集雲端儲存空間資料](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立Google雲端儲存空間來源連線](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [在UI中為雲端儲存區連線設定資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)