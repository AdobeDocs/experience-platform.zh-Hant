---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 資料登錄區源
topic-legacy: overview
description: 了解如何將資料登陸區連接至Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform布建的儲存介面，可授予您存取安全、雲端型檔案儲存功能，將檔案匯入Platform。 您可以存取 [!DNL Data Landing Zone] 每個沙箱的容器，且所有容器的資料量總計僅限於您的Platform產品與服務授權隨附的資料總計。 Platform及其應用程式服務的所有客戶，例如 [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]，和 [!DNL Adobe Real-Time Customer Data Platform] 已布建一個 [!DNL Data Landing Zone] 每個沙箱的容器。 您可以透過 [!DNL Azure Storage Explorer] 或命令列介面。

[!DNL Data Landing Zone] 支援基於SAS的身份驗證，其資料受標準保護 [!DNL Azure Blob] 儲存安全機制處於閒置狀態和在途。 基於SAS的身份驗證允許您安全地訪問 [!DNL Data Landing Zone] 容器。 訪問您的 [!DNL Data Landing Zone] 容器，這表示您不需要為網路設定任何允許清單或跨地區設定。 平台會對上傳至 [!DNL Data Landing Zone] 容器。 所有檔案會在七天後刪除。

## 檔案和目錄的命名限制

以下是在命名雲儲存檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以斜線結尾(`/`)。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元： `" \ / : | < > * ?`.
- 不允許使用非法的URL路徑字元。 程式碼點，例如 `\uE000`，但在NTFS檔案名中有效，則不是有效的Unicode字元。 此外，有些ASCII或Unicode字元，例如控制字元(例如 `0x00` to `0x1F`, `\u0081`、等)，也不允許。 如需HTTP/1.1中管理Unicode字串的規則，請參閱 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允許使用下列檔案名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、NUL、CON、CON$、點字元(............................................................................

## 管理 [!DNL Data Landing Zone]

您可以使用 [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) 管理 [!DNL Data Landing Zone] 容器。

在 [!DNL Azure Storage Explorer] UI，在左側導覽中選取連線圖示。 此 **選擇資源** 窗口，提供連接到的選項。 選擇 **[!DNL Blob container]** 連接到 [!DNL Data Landing Zone].

![select-resource](../../images/tutorials/create/dlz/select-resource.png)

下一步，選擇 **共用訪問簽名URL(SAS)** 作為連接方法，然後選取 **下一個**.

![select-connection-method](../../images/tutorials/create/dlz/select-connection-method.png)

選取連線方法後，您接下來必須提供 **顯示名稱** 和 **[!DNL Blob]容器SAS URL** 與 [!DNL Data Landing Zone] 容器。

>[!TIP]
>
>您可以擷取 [!DNL Data Landing Zone] 平台UI中來源目錄的憑證。

提供您的 [!DNL Data Landing Zone] SAS URL，然後選擇 **下一個**

![enter-connection-info](../../images/tutorials/create/dlz/enter-connection-info.png)

此 **摘要** 視窗中顯示，提供設定的概觀，包括您 [!DNL Blob] 端點和權限。 準備就緒時，請選取 **Connect**.

![摘要](../../images/tutorials/create/dlz/summary.png)

成功的連線會更新您的 [!DNL Azure Storage Explorer] UI搭配您的 [!DNL Data Landing Zone] 容器。

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

使用 [!DNL Data Landing Zone] 連接至 [!DNL Azure Storage Explorer]，您現在可以開始將檔案上傳至 [!DNL Data Landing Zone] 容器。 若要上傳，請選取 **上傳** 然後選取 **上傳檔案**.

![上傳](../../images/tutorials/create/dlz/upload.png)

選取要上傳的檔案後，您必須識別 [!DNL Blob] 輸入您要上傳的作為和所需目的地目錄。 完成後，請選取 **上傳**.

| [!DNL Blob] 類型 | 說明 |
| --- | --- |
| 區塊 [!DNL Blob] | 區塊 [!DNL Blobs] 已針對以有效方式上傳大量資料而最佳化。 區塊 [!DNL Blobs] 是 [!DNL Data Landing Zone]. |
| 附加 [!DNL Blob] | 附加 [!DNL Blobs] 會針對將資料附加至檔案結尾而最佳化。 |

![上傳檔案](../../images/tutorials/create/dlz/upload-files.png)

## 將檔案上傳至 [!DNL Data Landing Zone] 使用命令行介面

您也可以使用裝置的命令列介面，並存取上傳檔案至 [!DNL Data Landing Zone].

### 使用Bash上傳檔案

下列範例使用Bash和cURL將檔案上傳至 [!DNL Data Landing Zone] 和 [!DNL Azure Blob Storage] REST API:

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

下列範例使用 [!DNL Microsoft's] Python v12 SDK可將檔案上傳至 [!DNL Data Landing Zone]:

>[!TIP]
>
>下面的示例使用完整的SAS URI連接到 [!DNL Azure Blob] 容器，則可以使用其他方法和操作來驗證。 看這個 [[!DNL Microsoft] 關於Python v12 SDK的文檔](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) 以取得更多資訊。

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

### 使用上傳檔案 [!DNL AzCopy]

下列範例使用 [!DNL Microsoft's] [!DNL AzCopy] 上傳檔案至 [!DNL Data Landing Zone]:

>[!TIP]
>
>以下範例是使用 `copy` 命令，可使用其他命令和選項將檔案上載到 [!DNL Data Landing Zone]，使用 [!DNL AzCopy]. 看這個 [[!DNL Microsoft AzCopy] 檔案](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) 以取得更多資訊。

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Connect [!DNL Data Landing Zone] to [!DNL Platform]

以下檔案提供如何從 [!DNL Data Landing Zone] 容器至Adobe Experience Platform。

### 使用API

- [建立 [!DNL Data Landing Zone] 源連接（使用流服務API）](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [使用流服務API為雲儲存源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [Connect [!DNL Data Landing Zone] 使用UI設為Platform](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [在UI中為雲儲存連線建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
