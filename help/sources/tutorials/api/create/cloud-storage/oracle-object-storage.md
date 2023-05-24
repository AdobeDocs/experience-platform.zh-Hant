---
keywords: Experience Platform；首頁；熱門主題；Oracle對象儲存；oracle對象儲存
solution: Experience Platform
title: 使用流服務API建立Oracle對象儲存基連接
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到Oracle對象儲存。
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# 建立 [!DNL Oracle Object Storage] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Oracle Object Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL Oracle Object Storage] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接到 [!DNL Oracle Object Storage]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `serviceUrl` | 的 [!DNL Oracle Object Storage] 驗證所需的終結點。 終結點格式為： `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 的 [!DNL Oracle Object Storage] 驗證所需的訪問密鑰ID。 |
| `secretKey` | 的 [!DNL Oracle Object Storage] 驗證所需的密碼。 |
| `bucketName` | 如果用戶具有限制訪問權限，則需要允許的儲存段名稱。 儲存桶名稱必須長3到63個字元，它必須以字母或數字開頭和結尾，並且只能包含小寫字母、數字或連字元(`-`)。 儲存段名稱的格式不能與IP地址相同。 |
| `folderPath` | 如果用戶具有限制訪問權限，則需要允許的資料夾路徑。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Oracle Object Storage] 為： `c85f9425-fb21-426c-ad0b-405e9bd8a46c`。 |

有關如何獲取這些值的詳細資訊，請參閱 [Oracle對象儲存身份驗證指南](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Oracle Object Storage] 身份驗證憑據作為請求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

以下請求為 [!DNL Oracle Object Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle Object Storage connection",
        "description": "Oracle Object Storage connection",
        "auth": {
            "specName": "Access Key",
            "params": {
                "serviceUrl": "{SERVICE_URL}",
                "accessKey": "{ACCESS_KEY}",
                "secretKey": "{SECRET_KEY}",
                "bucketName": "{BUCKET_NAME}",
                "folderPath", "{FOLDER_PATH}"
            }
        },
        "connectionSpec": {
            "id": "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.serviceUrl` | 的 [!DNL Oracle Object Storage] 驗證所需的終結點。 |
| `auth.params.accessKey` | 的 [!DNL Oracle Object Storage] 驗證所需的訪問密鑰ID。 |
| `auth.params.secretKey` | 的 [!DNL Oracle Object Storage] 驗證所需的密碼。 |
| `auth.params.bucketName` | 如果用戶具有限制訪問權限，則需要允許的儲存段名稱。 |
| `auth.params.folderPath` | 如果用戶具有限制訪問權限，則需要允許的資料夾路徑。 |
| `connectionSpec.id` | 的 [!DNL Oracle Object Storage] 連接規範ID: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`。 |

**回應**

成功的響應返回新建立的連接的連接ID。 在下一教程中瀏覽雲儲存資料時需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Oracle Object Storage] 使用 [!DNL Flow Service] API，並已獲取其唯一連接ID。 您可以使用此連接ID [使用流服務API瀏覽雲儲存](../../explore/cloud-storage.md)。
