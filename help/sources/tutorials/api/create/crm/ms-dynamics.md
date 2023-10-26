---
keywords: Experience Platform；首頁；熱門主題；Microsoft Dynamics；microsoft dynamics；dynamics；Dynamics
solution: Experience Platform
title: 使用流量服務API建立Microsoft Dynamics基本連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Platform連線至Microsoft Dynamics帳戶。
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 3%

---

# 建立 [!DNL Microsoft Dynamics] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Microsoft Dynamics] (以下稱「[!DNL Dynamics]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下章節提供您需瞭解的其他資訊，才能使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線到 [!DNL Dynamics]，您必須提供下列連線屬性的值：

>[!BEGINTABS]

>[!TAB 基本驗證]

| 認證 | 說明 |
| --- | --- |
| `serviceUri` | 您的服務URL [!DNL Dynamics] 執行個體。 |
| `username` | 您的使用者名稱 [!DNL Dynamics] 使用者帳戶。 |
| `password` | 您的密碼 [!DNL Dynamics] 帳戶。 |

>[!TAB 服務主體和金鑰驗證]

| 認證 | 說明 |
| --- | --- |
| `servicePrincipalId` | 您的使用者端識別碼 [!DNL Dynamics] 帳戶。 使用服務主體和金鑰式驗證時，需要此ID。 |
| `servicePrincipalKey` | 服務主體秘密金鑰。 使用服務主體和金鑰式驗證時，需要此認證。 |

>[!ENDTABS]

如需開始使用的詳細資訊，請參閱 [此 [!DNL Dynamics] 檔案](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南： [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

>[!TIP]
>
>建立後，您就無法變更的驗證型別 [!DNL Dynamics] 基礎連線。 若要變更驗證型別，您必須建立新的基礎連線。

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基本連線ID，請向以下連線ID發出POST請求： `/connections` 端點，同時提供 [!DNL Dynamics] 要求引數中的驗證認證。

### 建立 [!DNL Dynamics] 基礎連線

>[!TIP]
>
>建立後，您就無法變更的驗證型別 [!DNL Dynamics] 基礎連線。 若要變更驗證型別，您必須建立新的基礎連線。

建立來源連線的第一個步驟是驗證您的 [!DNL Dynamics] 來源並產生基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基本連線ID，請向以下連線ID發出POST請求： `/connections` 端點，同時提供 [!DNL Dynamics] 要求引數中的驗證認證。

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 基本驗證]

若要建立 [!DNL Dynamics] 使用基本驗證的基礎連線，向發出POST請求 [!DNL Flow Service] API，同時為您的連線提供值 `serviceUri`， `username`、和 `password`.

+++請求

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.serviceUri` | 與您的關聯的服務URI [!DNL Dynamics] 執行個體。 |
| `auth.params.username` | 與您的相關聯的使用者名稱 [!DNL Dynamics] 帳戶。 |
| `auth.params.password` | 與您的關聯的密碼 [!DNL Dynamics] 帳戶。 |
| `connectionSpec.id` | 此 [!DNL Dynamics] 連線規格ID： `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++回應

成功的回應會傳回新建立的連線，包括其唯一識別碼(`id`)。 在下一個步驟中探索您的CRM系統時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB 服務主體金鑰型驗證]

若要建立 [!DNL Dynamics] 使用服務主體金鑰式驗證的基礎連線，向發出POST要求 [!DNL Flow Service] API，同時為您的連線提供值 `serviceUri`， `servicePrincipalId`、和 `servicePrincipalKey`.

+++請求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using key-based authentication",
      "auth": {
          "specName": "Service Principal Key Based Authentication",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
              "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.serviceUri` | 與您的關聯的服務URI [!DNL Dynamics] 執行個體。 |
| `auth.params.servicePrincipalId` | 您的使用者端識別碼 [!DNL Dynamics] 帳戶。 使用服務主體和金鑰式驗證時，需要此ID。 |
| `auth.params.servicePrincipalKey` | 服務主體秘密金鑰。 使用服務主體和金鑰式驗證時，需要此認證。 |
| `connectionSpec.id` | 此 [!DNL Dynamics] 連線規格ID： `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++回應

成功的回應會傳回新建立的連線，包括其唯一識別碼(`id`)。 在下一個步驟中探索您的CRM系統時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]


## 後續步驟

依照本教學課程，您已建立 [!DNL Microsoft Dynamics] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用瀏覽資料表的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，以將CRM資料帶入Platform，使用 [!DNL Flow Service] API](../../collect/crm.md)
