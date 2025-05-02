---
title: Azure Databricks
description: 瞭解將Azure Databricks連線至Experience Platform所需的先決條件步驟。
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: 2f082898-aa0e-47a1-a4bf-077c21afdfee
source-git-commit: 5637a12d5f9cc14b6cf3d88f018aa92de06ab739
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 2%

---

# [!DNL Azure Databricks]

>[!IMPORTANT]
>
>[!DNL Azure Databricks]來源可在來源目錄中提供給已購買Real-Time CDP Ultimate的使用者。

[!DNL Azure Databricks]是雲端型平台，專為資料分析、機器學習和AI而設計。 您可以使用[!DNL Databricks]與[!DNL Azure]整合，並提供整體環境，以大規模建置、部署及管理資料解決方案。

您可以使用[!DNL Databricks]來源來連線您的帳戶，並將您的[!DNL Databricks]資料擷取到Adobe Experience Platform。

## 先決條件

完成先決條件步驟，成功將您的[!DNL Databricks]帳戶連線至Experience Platform。

### 擷取您的容器認證

擷取您的Experience Platform [!DNL Azure Blob Storage]認證，讓您的[!DNL Databricks]帳戶稍後可以存取。

若要擷取您的認證，請向[!DNL Connectors] API的`/credentials`端點發出GET請求。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source
```

**要求**

下列要求會擷取您Experience Platform [!DNL Azure Blob Storage]的認證。

+++檢視請求範例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**回應**

成功的回應提供您的認證(`containerName`、`SASToken`、`storageAccountName`)，以供稍後在[!DNL Databricks]的[!DNL Apache Spark]設定中使用。

+++檢視回應範例

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "expiryDate": "2025-07-05"
}
```

| 屬性 | 說明 |
| --- | --- |
| `containerName` | [!DNL Azure Blob Storage]容器的名稱。 稍後當您完成[!DNL Databricks]的[!DNL Apache Spark]設定時，將會使用此值。 |
| `SASToken` | 您的[!DNL Azure Blob Storage]的共用存取權簽章權杖。 此字串包含授權請求所需的所有資訊。 |
| `storageAccountName` | 儲存體帳戶的名稱。 |
| `SASUri` | 您的[!DNL Azure Blob Storage]的共用存取權簽章URI。 此字串是[!DNL Azure Blob Storage]的URI組合，您要對其驗證以及它對應的SAS權杖。 |
| `expiryDate` | 您的SAS Token到期的日期。 您必須在到期日之前重新整理您的權杖，才能繼續在您的應用程式中使用它來上傳資料到[!DNL Azure Blob Storage]。 如果您未在所述的到期日之前手動重新整理權杖，則會在執行GET認證呼叫時自動重新整理並提供新權杖。 |

+++

### 重新整理您的認證

>[!NOTE]
>
>您重新整理認證後，現有的認證將會被撤銷。 因此，每當您重新整理儲存體認證時，都必須相應地更新[!DNL Spark]設定。 否則，您的資料流將會失敗。

若要重新整理您的認證，請提出POST要求並加入`action=refresh`作為查詢引數。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh
```

**要求**

下列要求會重新整理您[!DNL Azure Blob Storage]的認證。

+++檢視請求範例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**回應**

成功的回應會傳回您的新認證。

+++檢視回應範例

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "expiryDate": "2025-07-20"
}
```

+++

### 設定對您[!DNL Azure Blob Storage]的存取權

>[!IMPORTANT]
>
>* 如果您的叢集已終止，服務會在流程執行期間自動重新啟動。 不過，在建立連線或資料流時，您必須確保您的叢集為作用中。 此外，如果您正在執行資料預覽或探索等動作，您的叢集必須處於作用中狀態，因為這些動作無法提示自動重新啟動已終止的叢集。
>
>* 您的[!DNL Azure]容器包含名為`adobe-managed-staging`的資料夾。 為確保資料能順暢擷取，**不要**&#x200B;修改此資料夾。


接下來，您必須確定您的[!DNL Databricks]叢集可以存取Experience Platform [!DNL Azure Blob Storage]帳戶。 如此一來，您就可以使用[!DNL Azure Blob Storage]作為寫入[!DNL delta lake]資料表資料的臨時位置。

若要提供存取權，您必須在[!DNL Databricks]叢集上設定SAS權杖，作為[!DNL Apache Spark]設定的一部分。

在您的[!DNL Databricks]介面中，選取&#x200B;**[!DNL Advanced options]**，然後在[!DNL Spark config]輸入方塊中輸入下列內容。

```shell
fs.azure.sas.{CONTAINER_NAME}.{STORAGE-ACCOUNT}.blob.core.windows.net {SAS-TOKEN}
```

| 屬性 | 說明 |
| --- | --- |
| 容器名稱 | 容器的名稱。 您可以擷取[!DNL Azure Blob Storage]認證以取得此值。 |
| 儲存體帳戶 | 儲存體帳戶的名稱。 您可以擷取[!DNL Azure Blob Storage]認證以取得此值。 |
| SAS 權杖 | 您的[!DNL Azure Blob Storage]的共用存取權簽章權杖。 您可以擷取[!DNL Azure Blob Storage]認證以取得此值。 |

![Azure上的Databricks UI。](../../images/tutorials/create/databricks/databricks-ui.png)

## 使用API連線[!DNL Databricks]至Experience Platform

現在您已完成先決條件步驟，接下來可以使用API ](../../tutorials/api/create/databases/databricks.md)將您的 [!DNL Databricks] 帳戶連線至Experience Platform [，繼續參閱指南。
