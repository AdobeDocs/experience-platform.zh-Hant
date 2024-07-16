---
keywords: Experience Platform；首頁；熱門主題；Microsoft Dynamics；microsoft dynamics；dynamics；Dynamics
solution: Experience Platform
title: 使用流量服務API建立Microsoft Dynamics基本連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Platform連線至Microsoft Dynamics帳戶。
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API建立[!DNL Microsoft Dynamics]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Microsoft Dynamics] （以下稱為「[!DNL Dynamics]」）建立基礎連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線Platform至Dynamics帳戶。

### 收集必要的認證

為了讓[!DNL Flow Service]連線到[!DNL Dynamics]，您必須提供下列連線屬性的值：

>[!BEGINTABS]

>[!TAB 基本驗證]

| 認證 | 說明 |
| --- | --- |
| `serviceUri` | [!DNL Dynamics]執行個體的服務URL。 |
| `username` | 您的[!DNL Dynamics]使用者帳戶的使用者名稱。 |
| `password` | 您的[!DNL Dynamics]帳戶密碼。 |

>[!TAB 服務主體和金鑰驗證]

| 認證 | 說明 |
| --- | --- |
| `servicePrincipalId` | 您[!DNL Dynamics]帳戶的使用者端識別碼。 使用服務主體和金鑰式驗證時，需要此ID。 |
| `servicePrincipalKey` | 服務主體秘密金鑰。 使用服務主體和金鑰式驗證時，需要此認證。 |

>[!ENDTABS]

如需開始使用的詳細資訊，請參閱[此 [!DNL Dynamics] 檔案](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

>[!TIP]
>
>建立後，您無法變更[!DNL Dynamics]基本連線的驗證型別。 若要變更驗證型別，您必須建立新的基礎連線。

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供[!DNL Dynamics]驗證認證作為要求引數的一部分時，向`/connections`端點提出POST要求。

### 建立[!DNL Dynamics]基本連線

>[!TIP]
>
>建立後，您無法變更[!DNL Dynamics]基本連線的驗證型別。 若要變更驗證型別，您必須建立新的基礎連線。

建立來源連線的第一個步驟是驗證您的[!DNL Dynamics]來源並產生基本連線識別碼。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供[!DNL Dynamics]驗證認證作為要求引數的一部分時，向`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 基本驗證]

若要使用基本驗證建立[!DNL Dynamics]基本連線，請在提供連線的`serviceUri`、`username`和`password`的值時，向[!DNL Flow Service] API提出POST要求。

+++要求

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
| `auth.params.serviceUri` | 與您的[!DNL Dynamics]執行個體關聯的服務URI。 |
| `auth.params.username` | 與您的[!DNL Dynamics]帳戶相關聯的使用者名稱。 |
| `auth.params.password` | 與您的[!DNL Dynamics]帳戶關聯的密碼。 |
| `connectionSpec.id` | [!DNL Dynamics]連線規格識別碼： `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

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

>[!TAB 服務主要金鑰式驗證]

若要使用服務主體金鑰式驗證來建立[!DNL Dynamics]基底連線，請在提供連線的`serviceUri`、`servicePrincipalId`和`servicePrincipalKey`的值時，向[!DNL Flow Service] API提出POST要求。

+++要求

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
| `auth.params.serviceUri` | 與您的[!DNL Dynamics]執行個體關聯的服務URI。 |
| `auth.params.servicePrincipalId` | 您[!DNL Dynamics]帳戶的使用者端識別碼。 使用服務主體和金鑰式驗證時，需要此ID。 |
| `auth.params.servicePrincipalKey` | 服務主體秘密金鑰。 使用服務主體和金鑰式驗證時，需要此認證。 |
| `connectionSpec.id` | [!DNL Dynamics]連線規格識別碼： `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

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

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Microsoft Dynamics]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將CRM資料帶入Platform](../../collect/crm.md)
