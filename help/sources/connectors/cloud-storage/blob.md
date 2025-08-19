---
title: Azure Blob Source聯結器總覽
description: 瞭解如何將您的Azure Blob帳戶連結至Experience Platform
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: f659d78eebc1c5e74021f9a41a2a489389a6588e
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 0%

---

# [!DNL Azure Blob Storage]來源

[!DNL Azure Blob Storage]是由[!DNL Microsoft Azure]提供的雲端型物件儲存服務。 專為儲存大量非結構化資料而設計，例如文字、影像、影片、備份及記錄檔。 您可以使用[!DNL Azure Blob Storage]來儲存和管理大量非結構化資料，例如檔案、影像、視訊和音訊檔案。 它非常適合備份及封存資料、支援災難回覆，以及處理大型資料工作負荷以利分析。

使用[!DNL Azure Blob Storage]來源連線您的帳戶，並將資料從[!DNL Azure Blob Storage]擷取到Adobe Experience Platform。

## 先決條件 {#prerequisites}

請先閱讀下列章節，完成先決條件設定，然後再將[!DNL Azure Blob Storage]帳戶連線至Experience Platform。

### IP位址允許清單

將來源連線至Experience Platform之前，您必須先將區域特定的IP位址新增至允許清單。 如需詳細資訊，請閱讀[允許列出IP位址以連線至Experience Platform](../../ip-address-allow-list.md)的指南。

>[!IMPORTANT]
>
>[!DNL Azure Blob]來源不支援與Experience Platform的相同區域連線。 如果您的[!DNL Azure]執行個體使用與Experience Platform相同的網路區域，則無法建立與Experience Platform來源的連線。 目前僅支援跨區域連線。

### 檔案和目錄的命名限制

以下是在命名雲端儲存空間檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)結尾。 如果提供，則會自動移除。
- 必須正確逸出下列保留的URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許下列字元： `" \ / : | < > * ?`。
- 不允許非法URL路徑字元。 類似`\uE000`的程式碼點雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的規則，請參閱[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許下列檔案名稱： LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

### 向Experience Platform驗證[!DNL Azure Blob Storage] {#authentication}

您可以使用下列驗證型別，將您的[!DNL Azure Blob Storage]帳戶連線至Experience Platform：

- **帳戶金鑰驗證**：使用儲存體帳戶的存取金鑰來驗證並連線至您的[!DNL Azure Blob Storage]帳戶。
- **共用存取簽章(SAS)**：使用SAS URI提供您[!DNL Azure Blob Storage]帳戶中資源的委派、有限時間存取權。
- **以服務主體為基礎的驗證**：使用Azure Active Directory (AAD)服務主體（使用者端ID和密碼）來安全地驗證您的Azure Blob儲存帳戶。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

提供下列認證的值，以使用帳戶金鑰驗證將您的[!DNL Azure Blob Storage]帳戶連線至Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `connectionString` | 儲存體帳戶的[!DNL Azure Blob Storage]連線字串。 此字串包含驗證及連線至您的[!DNL Azure Blob Storage]執行個體所需的資訊。 範例格式： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net` |
| `container` | 儲存資料檔的[!DNL Azure Blob Storage]容器名稱。 容器可組織一組Blob，類似於檔案系統中的目錄。 |
| `folderPath` | 指定容器內檔案所在的路徑。 這是容器內的選用子目錄路徑（虛擬資料夾）。 如果保留為空白，則會使用容器的根。 |
| `connectionSpec.id` | 連線規格ID會傳回來源的連線器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Azure Blob Storage]的連線規格識別碼為`4c10e202-c428-4796-9208-5f1f5732b1cf`。 **注意**：只有在透過[!DNL Flow Service] API連線時才需要此認證。 |

若要進一步瞭解如何搭配[!DNL Azure Blob Storage]使用帳戶金鑰驗證，請閱讀官方[Microsoft Azure驗證指南](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#account-key-authentication)。

>[!TAB 共用存取權簽章]

提供下列認證的值，以使用共用存取簽章將您的[!DNL Azure Blob Storage]帳戶連線至Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `SasURI` | 共用存取簽章URI，您可將其用作連線帳戶的替代驗證型別。 SAS URI模式為： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`。 如需詳細資訊，請參閱[!DNL Azure]共用存取簽章URI[上的此](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)檔案。 |
| `container` | 儲存資料檔的[!DNL Azure Blob Storage]容器名稱。 容器可組織一組Blob，類似於檔案系統中的目錄。 |
| `folderPath` | 指定容器內檔案所在的路徑。 這是容器內的選用子目錄路徑（虛擬資料夾）。 如果保留為空白，則會使用容器的根。 |
| `connectionSpec.id` | 連線規格ID會傳回來源的連線器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Azure Blob Storage]的連線規格識別碼為`4c10e202-c428-4796-9208-5f1f5732b1cf`。 **注意**：只有在透過[!DNL Flow Service] API連線時才需要此認證。 |

若要進一步瞭解如何搭配[!DNL Azure Blob Storage]使用共用存取簽章，請閱讀官方[Microsoft Azure驗證指南](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)。

>[!TAB 以服務主體為基礎的驗證]

提供下列認證的值，以使用以服務主體為基礎的驗證，將您的[!DNL Azure Blob Storage]帳戶連線至Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `serviceEndpoint` | [!DNL Azure Blob Storage]帳戶的端點URL。 通常格式為： `https://{ACCOUNT_NAME}.blob.core.windows.net`。 |
| `accountKind` | [!DNL Azure Blob Storage]帳戶的型別。 通用值包括`StorageV2`、`BlobStorage`或`Storage`。 |
| `servicePrincipalId` | 用於驗證的Azure Active Directory (AAD)服務主體的使用者端/應用程式ID。 |
| `servicePrincipalKey` | 與Azure服務主體關聯的使用者端密碼或密碼。 |
| `tenant` | 註冊服務主體的Azure Active Directory (AAD)租使用者ID。 |
| `container` | 儲存資料檔案的Azure Blob儲存體容器的名稱。 |
| `folderPath` | 指定容器內檔案所在的路徑。 這是容器內的選用子目錄路徑（虛擬資料夾）。 如果保留為空白，則會使用容器的根。 |
| `connectionSpec.id` | 連線規格ID會傳回來源的連線器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 Azure Blob儲存體的連線規格ID是`4c10e202-c428-4796-9208-5f1f5732b1cf`。 **注意**：只有在透過[!DNL Flow Service] API連線時才需要此認證。 |

若要進一步瞭解如何搭配[!DNL Azure Blob Storage]使用以服務主體為基礎的驗證，請閱讀官方[Microsoft Azure驗證指南](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#service-principal-authentication)。

>[!ENDTABS]

## 將[!DNL Azure Blob Storage]連線至[!DNL Experience Platform]

以下檔案提供如何使用API或使用者介面將Azure Blob連線至Adobe Experience Platform的資訊：

### 使用API

- [連線 [!DNL Azure Blob Storage] 至Experience Platform](../../tutorials/api/create/cloud-storage/blob.md)
- [使用流量服務API探索雲端儲存空間來源的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
- [使用流量服務API為雲端儲存空間來源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [連線 [!DNL Azure Blob Storage] 至Experience Platform](../../tutorials/ui/create/cloud-storage/blob.md)
- [在UI中為雲端儲存空間連線建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
