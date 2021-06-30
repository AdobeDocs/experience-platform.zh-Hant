---
keywords: Experience Platform；首頁；熱門主題；Google雲端儲存空間；Google雲端儲存空間
solution: Experience Platform
title: Google雲端儲存來源連接器概觀
topic-legacy: overview
description: 了解如何使用API或使用者介面將Google雲端儲存空間連線至Adobe Experience Platform。
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Google雲端儲存空間連接器

Adobe Experience Platform為AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等雲提供商提供本機連接，允許您從這些系統中帶來資料。

雲端儲存來源可將您自己的資料匯入Platform，而無須下載、格式化或上傳。 擷取的資料可格式為符合Experience Data Model(XDM)的JSON或Parquet，或使用分隔格式。 流程的每個步驟都整合至來源工作流程中。 Platform可讓您透過批次從[!DNL Google Cloud Storage]匯入資料。

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 連接[!DNL Google Cloud Storage]帳戶的先決條件設定

若要連接到Platform，必須首先啟用[!DNL Google Cloud Storage]帳戶的互操作性。 要訪問互操作性設定，請開啟[!DNL Google Cloud Platform]並從導航面板的&#x200B;**[!UICONTROL 雲儲存]**&#x200B;選項中選擇&#x200B;**[!UICONTROL 設定]**。

![](../../images/tutorials/create/google-cloud-storage/nav.png)

此時將顯示「**[!UICONTROL 設定]**」頁。 從這裡，您可以看到[!DNL Google]專案ID的相關資訊，以及[!DNL Google Cloud Storage]帳戶的詳細資訊。 要訪問互操作性設定，請從頂部標頭中選擇&#x200B;**[!UICONTROL 互操作性]**。

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

**[!UICONTROL 互操作性]**&#x200B;頁包含有關身份驗證、訪問密鑰和與服務帳戶關聯的預設項目的資訊。 要為服務帳戶生成新的訪問密鑰ID和秘密訪問密鑰，請選擇&#x200B;**[!UICONTROL 為服務帳戶建立密鑰]**。

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新生成的訪問密鑰ID和秘密訪問密鑰將[!DNL Google Cloud Storage]帳戶連接到Platform。

## 檔案和目錄的命名限制

以下是在命名雲儲存檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以斜線(`/`)結尾。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出：`! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元：`" \ / : | < > * ?`。
- 不允許使用非法的URL路徑字元。 代碼點（如`\uE000`）在NTFS檔案名中有效，但不是有效的Unicode字元。 此外，某些ASCII或Unicode字元，如控制字元（0x00到0x1F、\u0081等）也不允許使用。 有關HTTP/1.1中管理Unicode字串的規則，請參閱[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許使用下列檔案名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、NUL、CON、CON$、點字元(............................................................................

## 連接[!DNL Google Cloud Storage]到平台

以下檔案提供如何使用API或使用者介面將[!DNL Google Cloud Storage]連線至Platform的資訊：

### 使用API

- [使用流量服務API建立Google雲端儲存空間基本連線](../../tutorials/api/create/cloud-storage/google.md)
- [使用流量服務API探索雲端儲存空間來源的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服務API為雲儲存源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立Google雲端儲存空間來源連線](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [在UI中為雲儲存連線建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
