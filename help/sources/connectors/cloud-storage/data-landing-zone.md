---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 資料登錄區源
description: 瞭解如何將資料登錄區連接到Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: d57060ddeed64d3863f71ac1ea34ccc5c97265ea
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>此頁面特定於 [!DNL Data Landing Zone] *源* Experience Platform中的連接器。 有關連接到的資訊 [!DNL Data Landing Zone] *目標* 連接器，請參閱 [[!DNL Data Landing Zone] 目標文檔頁](/help/destinations/catalog/cloud-storage/data-landing-zone.md)。

[!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform提供的儲存介面，允許您訪問安全、基於雲的檔案儲存設施，以將檔案帶入平台。 您可以訪問 [!DNL Data Landing Zone] 每個沙箱的容器，並且所有容器的總資料量僅限於隨平台產品和服務許可證提供的總資料。 平台及其應用服務(如 [!DNL Customer Journey Analytics]。 [!DNL Journey Orchestration]。 [!DNL Intelligent Services], [!DNL Adobe Real-Time Customer Data Platform] 已配置 [!DNL Data Landing Zone] 每個沙盒的容器。 您可以通過以下方式將檔案讀寫到容器 [!DNL Azure Storage Explorer] 或命令行介面。

[!DNL Data Landing Zone] 支援基於SAS的身份驗證，其資料受標準保護 [!DNL Azure Blob] 存放安全機制。 基於SAS的身份驗證允許您安全地訪問 [!DNL Data Landing Zone] 容器。 訪問您的 [!DNL Data Landing Zone] 容器，這意味著您不需要為網路配置任何允許清單或跨區域設定。 平台對上載到的所有檔案強制實施嚴格的七天過期時間 [!DNL Data Landing Zone] 容器。 七天後刪除所有檔案。

## 檔案和目錄的命名約束

以下是命名雲儲存檔案或目錄時必須考慮的約束條件清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以正斜槓結尾(`/`)。 如果提供，將自動刪除。
- 必須正確轉義以下保留URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用以下字元： `" \ / : | < > * ?`。
- 不允許使用非法的URL路徑字元。 代碼點類似 `\uE000`，但在NTFS檔案名中有效，則不是有效的Unicode字元。 此外，某些ASCII或Unicode字元，如控制字元(如 `0x00` 至 `0x1F`。 `\u0081`等)，也不允許。 有關HTTP/1.1中Unicode字串的規則，請參見 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許使用下列檔案名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM9、COM9prn、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 管理您的內容 [!DNL Data Landing Zone]

您可以使用 [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) 管理 [!DNL Data Landing Zone] 容器。

在 [!DNL Azure Storage Explorer] UI，選擇左導航中的連接表徵圖。 的 **選擇資源** 的子菜單。 選擇 **[!DNL Blob container]** 連接到 [!DNL Data Landing Zone]。

![選擇資源](../../images/tutorials/create/dlz/select-resource.png)

下一步，選擇 **共用訪問簽名URL(SAS)** 作為連接方法，然後選擇 **下一個**。

![選擇連接方法](../../images/tutorials/create/dlz/select-connection-method.png)

選擇連接方法後，必須下一步提供 **顯示名稱** 和 **[!DNL Blob]容器SAS URL** 與 [!DNL Data Landing Zone] 容器。

>[!TIP]
>
>你可以 [!DNL Data Landing Zone] 來自平台UI中的源目錄的憑據。

提供 [!DNL Data Landing Zone] SAS URL，然後選擇 **下一個**

![輸入連接資訊](../../images/tutorials/create/dlz/enter-connection-info.png)

的 **摘要** 的子菜單。 [!DNL Blob] 終結點和權限。 準備好後，選擇 **連接**。

![摘要](../../images/tutorials/create/dlz/summary.png)

成功連接將更新您的 [!DNL Azure Storage Explorer] UI與 [!DNL Data Landing Zone] 容器。

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

與 [!DNL Data Landing Zone] 連接的容器 [!DNL Azure Storage Explorer]，現在可以開始將檔案上載到 [!DNL Data Landing Zone] 容器。 要上載，請選擇 **上載** ，然後選擇 **上載檔案**。

![上載](../../images/tutorials/create/dlz/upload.png)

選擇要上載的檔案後，必須標識 [!DNL Blob] 鍵入要將其上載為的目錄和所需的目標目錄。 完成後，選擇 **上載**。

| [!DNL Blob] 類型 | 說明 |
| --- | --- |
| 阻止 [!DNL Blob] | 阻止 [!DNL Blobs] 已優化，以便以高效的方式上傳大量資料。 阻止 [!DNL Blobs] 為 [!DNL Data Landing Zone]。 |
| 追加 [!DNL Blob] | 追加 [!DNL Blobs] 已優化，以便將資料附加到檔案末尾。 |

![上傳檔案](../../images/tutorials/create/dlz/upload-files.png)

## 將檔案上載到 [!DNL Data Landing Zone] 使用命令行介面

您還可以使用設備的命令行介面並訪問上載檔案到 [!DNL Data Landing Zone]。

### 使用Bash上載檔案

以下示例使用Bash和cURL將檔案上載到 [!DNL Data Landing Zone] 和 [!DNL Azure Blob Storage] REST API:

```shell
# Set Azure Blob-related settings
DATE_NOW=$(date -Ru | sed 's/\+0000/GMT/')
AZ_VERSION="2018-03-28"
AZ_BLOB_URL="<URL TO BLOB ACCOUNT>"
AZ_BLOB_CONTAINER="<BLOB CONTAINER NAME>"
AZ_BLOB_TARGET="${AZ_BLOB_URL}/${AZ_BLOB_CONTAINER}"
AZ_SAS_TOKEN="<SAS TOKEN, STARTING WITH ? AND ENDING WITH %3D>"

# Path to the file we wish to upload
FILE_PATH="</PATH/TO/FILE>"
FILE_NAME=$(basename "$FILE_PATH")

# Execute HTTP PUT to upload file (remove '-v' flag to suppress verbose output)
curl -v -X PUT \
   -H "Content-Type: application/octet-stream" \
   -H "x-ms-date: ${DATE_NOW}" \
   -H "x-ms-version: ${AZ_VERSION}" \
   -H "x-ms-blob-type: BlockBlob" \
   --data-binary "@${FILE_PATH}" "${AZ_BLOB_TARGET}/${FILE_NAME}${AZ_SAS_TOKEN}"
```

### 使用Python上載檔案

以下示例使用 [!DNL Microsoft's] Python v12 SDK將檔案上載到 [!DNL Data Landing Zone]:

>[!TIP]
>
>下面的示例使用完整SAS URI連接到 [!DNL Azure Blob] 容器，可以使用其他方法和操作進行身份驗證。 查看 [[!DNL Microsoft] Python v12 SDK上的文檔](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) 的子菜單。

```py
import os
from azure.storage.blob import ContainerClient

try:
    # Set Azure Blob-related settings
    sasUri = "<SAS URI>"
    srcFilePath = "<FULL PATH TO FILE>" 
    srcFileName = os.path.basename(srcFilePath)

    # Connect to container using SAS URI
    containerClient = ContainerClient.from_container_url(sasUri)

    # Upload file to Data Landing Zone with overwrite enabled
    with open(srcFilePath, "rb") as fileToUpload:
        containerClient.upload_blob(srcFileName, fileToUpload, overwrite=True)

except Exception as ex:
    print("Exception: " + ex.strerror)
```

### 使用 [!DNL AzCopy]

以下示例使用 [!DNL Microsoft's] [!DNL AzCopy] 用於將檔案上載到 [!DNL Data Landing Zone]:

>[!TIP]
>
>下面的示例使用 `copy` 命令，可使用其他命令和選項將檔案上載到 [!DNL Data Landing Zone]，使用 [!DNL AzCopy]。 查看 [[!DNL Microsoft AzCopy] 文檔](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) 的子菜單。

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## 連接 [!DNL Data Landing Zone] 至 [!DNL Platform]

以下文檔提供了有關如何從您的 [!DNL Data Landing Zone] 使用API或用戶介面將容器連接到Adobe Experience Platform。

### 使用API

- [建立 [!DNL Data Landing Zone] 使用流服務API的源連接](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [使用流服務API為雲儲存源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [連接 [!DNL Data Landing Zone] 到使用UI的平台](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [在UI中為雲儲存連接建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
