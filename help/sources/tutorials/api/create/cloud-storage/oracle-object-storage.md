---
keywords: Experience Platform；首頁；熱門主題；Oracle物件儲存；oracle物件儲存
solution: Experience Platform
title: 使用流服務API建立Oracle對象儲存基礎連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服務API將Adobe Experience Platform連線至Oracle物件儲存。
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Oracle Object Storage]基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)建立[!DNL Oracle Object Storage]基本連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL Oracle Object Storage]。

### 收集所需憑據

要使[!DNL Flow Service]連接到[!DNL Oracle Object Storage]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `serviceUrl` | 驗證所需的[!DNL Oracle Object Storage]端點。 端點格式為：`https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 驗證所需的[!DNL Oracle Object Storage]訪問密鑰ID。 |
| `secretKey` | 驗證所需的[!DNL Oracle Object Storage]密碼。 |
| `bucketName` | 如果使用者具有限制存取權，則需要允許的貯體名稱。 貯體名稱必須介於3到63個字元之間，其開頭和結尾必須是字母或數字，並且只能包含小寫字母、數字或連字型大小(`-`)。 儲存貯體名稱的格式無法與IP位址相同。 |
| `folderPath` | 如果用戶具有受限訪問權，則需要允許的資料夾路徑。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Oracle Object Storage]的連接規範ID為：`c85f9425-fb21-426c-ad0b-405e9bd8a46c`。 |

有關如何獲取這些值的詳細資訊，請參閱[Oracle對象儲存身份驗證指南](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Oracle Object Storage]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```http
POST /connections
```

**要求**

以下請求為[!DNL Oracle Object Storage]建立基本連接：

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
| `auth.params.secretKey` | 驗證所需的[!DNL Oracle Object Storage]密碼。 |
| `auth.params.bucketName` | 如果使用者具有限制存取權，則需要允許的貯體名稱。 |
| `auth.params.folderPath` | 如果用戶具有受限訪問權，則需要允許的資料夾路徑。 |
| `connectionSpec.id` | [!DNL Oracle Object Storage]連接規範ID:`c85f9425-fb21-426c-ad0b-405e9bd8a46c`。 |

**回應**

成功的回應會傳回新建立之連線的連線ID。 在下一個教學課程中探索您的雲端儲存空間資料時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Oracle Object Storage]連線，並取得其唯一連線ID。 您可以使用此連線ID來[使用流量服務API](../../explore/cloud-storage.md)探索雲端儲存空間。
