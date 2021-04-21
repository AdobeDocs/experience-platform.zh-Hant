---
keywords: Experience Platform；首頁；熱門主題；Oracle對象儲存；oracle對象儲存
solution: Experience Platform
title: 使用流服務API建立Oracle對象儲存源連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連接至Oracle物件儲存。
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Oracle Object Storage]來源連線

本教學課程使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)來引導您完成將Adobe Experience Platform連接至[!DNL Oracle Object Storage]的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示並增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功連線至[!DNL Oracle Object Storage]。

### 收集必要的認證

要使[!DNL Flow Service]連接到[!DNL Oracle Object Storage]，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `serviceUrl` | 驗證所需的[!DNL Oracle Object Storage]端點。 端點格式為：`https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 驗證所需的[!DNL Oracle Object Storage]訪問密鑰ID。 |
| `secretKey` | 驗證需要[!DNL Oracle Object Storage]密碼。 |
| `bucketName` | 如果使用者有限制的存取權，則需要允許的儲存貯體名稱。 貯體名稱必須在3到63個字元之間，且必須以字母或數字開頭和結尾，且只能包含小寫字母、數字或連字型大小(`-`)。 貯體名稱的格式不能與IP位址相同。 |
| `folderPath` | 如果使用者有限制存取權，則需要允許的資料夾路徑。 |

有關如何獲取這些值的詳細資訊，請參閱[Oracle對象儲存身份驗證指南](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫平台API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個[!DNL Oracle Object Storage]帳戶只需要一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**要求**

要建立[!DNL Oracle Object Storage]連接，必須在POST請求中提供其唯一連接規範ID。 [!DNL Oracle Object Storage]的連接規範ID為`c85f9425-fb21-426c-ad0b-405e9bd8a46c`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.serviceUrl` | 驗證所需的[!DNL Oracle Object Storage]端點。 |
| `auth.params.accessKey` | 驗證所需的[!DNL Oracle Object Storage]訪問密鑰ID。 |
| `auth.params.secretKey` | 驗證需要[!DNL Oracle Object Storage]密碼。 |
| `auth.params.bucketName` | 如果使用者有限制的存取權，則需要允許的儲存貯體名稱。 |
| `auth.params.folderPath` | 如果使用者有限制存取權，則需要允許的資料夾路徑。 |
| `connectionSpec.id` | [!DNL Oracle Object Storage]連接規範ID:`c85f9425-fb21-426c-ad0b-405e9bd8a46c`。 |

**回應**

成功的響應返回新建立的連接的連接ID。 在下一個教學課程中，探索您的雲端儲存空間資料時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 後續步驟

在本教程中，您使用[!DNL Flow Service] API建立了[!DNL Oracle Object Storage]連接，並獲得了其唯一連接ID。 您可以使用此連線ID，使用流程服務API](../../explore/cloud-storage.md)探索雲端儲存空間。[
