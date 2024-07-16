---
keywords: Experience Platform；首頁；熱門主題；Google雲端儲存空間；google雲端儲存空間
solution: Experience Platform
title: Google雲端儲存空間Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Google Cloud Storage連線至Adobe Experience Platform。
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: ae22e423119bf378a068349d481f0717a75171bb
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Google雲端儲存空間聯結器

Adobe Experience Platform為AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等雲端提供者提供原生連線，可讓您從這些系統帶入資料。

雲端儲存空間來源可將您自己的資料帶入Platform，無需下載、格式化或上傳。 內嵌的資料可以格式化為符合Experience Data Model (XDM)的JSON或Parquet，或以分隔格式提供。 流程的每個步驟都會整合到來源工作流程中。 平台可讓您透過批次從[!DNL Google Cloud Storage]匯入資料。

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 連線您的[!DNL Google Cloud Storage]帳戶的先決條件設定

若要連線到平台，您必須先為您的[!DNL Google Cloud Storage]帳戶啟用互通性。 若要存取互通性設定，請開啟[!DNL Google Cloud Platform]，然後從導覽面板的&#x200B;**[!UICONTROL 雲端儲存空間]**&#x200B;選項中選取&#x200B;**[!UICONTROL 設定]**。

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

**[!UICONTROL 設定]**&#x200B;頁面隨即顯示。 從這裡，您可以檢視有關您的[!DNL Google]專案ID的資訊，以及有關您的[!DNL Google Cloud Storage]帳戶的詳細資料。 若要存取互通性設定，請從頂端標頭選取&#x200B;**[!UICONTROL 互通性]**。

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

**[!UICONTROL 互通性]**&#x200B;頁面包含驗證、存取金鑰以及與您的服務帳戶關聯的預設專案的資訊。 若要為您的服務帳戶產生新的存取金鑰ID和機密存取金鑰，請選取&#x200B;**[!UICONTROL 為服務帳戶建立金鑰]**。

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

您可以使用新產生的存取金鑰ID和機密存取金鑰，將您的[!DNL Google Cloud Storage]帳戶連線至Platform。

如需詳細資訊，請參閱[!DNL Google Cloud]檔案中[建立和管理服務帳戶金鑰](https://cloud.google.com/iam/docs/creating-managing-service-account-keys)的指南。

## 檔案和目錄的命名限制

以下是在命名雲端儲存空間檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)結尾。 如果提供，則會自動移除。
- 必須正確逸出下列保留的URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許下列字元： `" \ / : | < > * ?`。
- 不允許非法URL路徑字元。 類似`\uE000`的程式碼點雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的規則，請參閱[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許下列檔案名稱： LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 將[!DNL Google Cloud Storage]連線至平台

以下檔案提供如何使用API或使用者介面將[!DNL Google Cloud Storage]連線到Platform的資訊：

### 使用API

- [使用流量服務API建立Google雲端儲存空間基本連線](../../tutorials/api/create/cloud-storage/google.md)
- [使用流量服務API探索雲端儲存空間來源的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
- [使用流量服務API為雲端儲存空間來源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立Google雲端儲存空間來源連線](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [在UI中為雲端儲存空間連線建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
