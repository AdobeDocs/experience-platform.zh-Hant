---
title: 使用流量服務API將資料登陸區域連線至Adobe Experience Platform
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至資料登陸區域。
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 1d4dd60180ef2a3cbf6dcd565c2f09dd575716b9
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 3%

---

# 使用流程服務API連線[!DNL Data Landing Zone]至Adobe Experience Platform

>[!IMPORTANT]
>
>此頁面是Experience Platform中[!DNL Data Landing Zone] *來源*&#x200B;聯結器的專屬頁面。 如需有關連線至[!DNL Data Landing Zone] *目的地*&#x200B;聯結器的資訊，請參閱[[!DNL Data Landing Zone] 目的地檔案頁面](/help/destinations/catalog/cloud-storage/data-landing-zone.md)。

[!DNL Data Landing Zone]是安全的雲端型檔案儲存裝置，可將檔案帶入Adobe Experience Platform。 資料會在七天後自動從[!DNL Data Landing Zone]中刪除。

本教學課程將逐步帶您瞭解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)建立[!DNL Data Landing Zone]來源連線的步驟。 此教學課程也提供如何擷取您的[!DNL Data Landing Zone]以及檢視和重新整理認證的說明。

## 快速入門

本指南需要您實際瞭解下列Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

本教學課程也要求您閱讀[平台API快速入門](../../../../../landing/api-guide.md)的指南，瞭解如何驗證平台API並解譯檔案中提供的範例呼叫。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功建立[!DNL Data Landing Zone]來源連線。

## 擷取可用的登陸區域

>[!IMPORTANT]
>
>您必須擁有&#x200B;**[!UICONTROL 管理來源]**&#x200B;存取控制許可權，才能使用[!DNL Data Landing Zone] API並擷取`type=user_drop_zone`。 如需詳細資訊，請閱讀[存取控制總覽](../../../../../access-control/home.md)，或連絡您的產品管理員以取得必要的許可權。

使用API存取[!DNL Data Landing Zone]的第一步是向[!DNL Connectors] API的`/landingzone`端點發出GET要求，同時提供`type=user_drop_zone`作為要求標頭的一部分。

**API格式**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| 標頭 | 說明 |
| --- | --- |
| `user_drop_zone` | `user_drop_zone`型別允許API將登陸區域容器與您可用的其他型別容器區分開來。 |

**要求**

以下請求會擷取現有的登陸區域。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**回應**

根據您的提供者，成功的請求會傳回以下內容：

>[!BEGINTABS]

>在Azure]上的[!TAB 回應

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| 屬性 | 說明 |
| --- | --- |
| `containerName` | 擷取的登陸區域名稱。 |
| `containerTTL` | 登陸區域內套用至您資料的到期時間（以天為單位）。 指定登陸區域中的任何專案都會在七天後刪除。 |


>在AWS上[!TAB 回應]

```json
{
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "dlz-adf-connectors"
  },
  "dataTTL": {
    "timeUnit": "days",
    "timeQuantity": 7
  },
  "dlzProvider": "Amazon S3"
}
```

>[!ENDTABS]


## 擷取[!DNL Data Landing Zone]認證

若要擷取[!DNL Data Landing Zone]的認證，請向[!DNL Connectors] API的`/credentials`端點提出GET要求。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
```

**要求**

以下請求範例會擷取現有登陸區域的認證。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**回應**

根據您的提供者，成功的請求會傳回以下內容：

>[!BEGINTABS]

>在Azure]上的[!TAB 回應

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "expiryDate": "2024-01-06"
}
```

| 屬性 | 說明 |
| --- | --- |
| `containerName` | [!DNL Data Landing Zone]的名稱。 |
| `SASToken` | 您的[!DNL Data Landing Zone]的共用存取權簽章權杖。 此字串包含授權請求所需的所有資訊。 |
| `storageAccountName` | 儲存體帳戶的名稱。 |
| `SASUri` | 您的[!DNL Data Landing Zone]的共用存取權簽章URI。 此字串是[!DNL Data Landing Zone]的URI組合，您要對其驗證以及它對應的SAS權杖。 |
| `expiryDate` | 您的SAS Token到期的日期。 您必須在到期日之前重新整理您的權杖，才能繼續在您的應用程式中使用它來上傳資料到[!DNL Data Landing Zone]。 如果您未在所述的到期日之前手動重新整理權杖，則會在執行GET認證呼叫時自動重新整理並提供新權杖。 |

>在AWS上[!TAB 回應]

```json
{
  "credentials": {
    "clientId": "example-client-id",
    "awsAccessKeyId": "example-access-key-id",
    "awsSecretAccessKey": "example-secret-access-key",
    "awsSessionToken": "example-session-token"
  },
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "user_drop_zone"
  },
  "dlzProvider": "Amazon S3",
  "expiryTime": 1735689599
}
```

| 屬性 | 說明 |
| --- | --- |
| `credentials.clientId` | 您在AWS中[!DNL Data Landing Zone]的使用者端ID。 |
| `credentials.awsAccessKeyId` | 您在AWS中[!DNL Data Landing Zone]的存取金鑰ID。 |
| `credentials.awsSecretAccessKey` | 您在AWS中[!DNL Data Landing Zone]的秘密存取金鑰。 |
| `credentials.awsSessionToken` | 您的AWS工作階段權杖。 |
| `dlzPath.bucketName` | 您的AWS貯體名稱。 |
| `dlzPath.dlzFolder` | 您正在存取的[!DNL Data Landing Zone]資料夾。 |
| `dlzProvider` | 您正在使用的[!DNL Data Landing Zone]提供者。 若為Amazon，則為[!DNL Amazon S3]。 |
| `expiryTime` | 到期時間（以Unix時間為單位）。 |

>[!ENDTABS]

### 使用API擷取必填欄位

產生Token後，您可以使用以下請求範例以程式設計方式擷取必填欄位：

>[!BEGINTABS]

>[!TAB Python]

```py
import requests
 
# API endpoint
url = "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone"
 
headers = {
    "Authorization": "{TOKEN}",
    "Content-Type": "application/json",
    "x-gw-ims-org-id": "{ORG_ID}",
    "x-api-key": "{API_KEY}"
}
 
# Send GET request to the API
response = requests.get(url, headers=headers)
 
# Check if the request was successful
if response.status_code == 200:
    # Parse the response as JSON (if applicable)
    data = response.json()
 
    # Print or work with the fetched data 
    print(" Sas Token:", data['SASToken'])
    print(" Container Name:",  data['containerName'])
    print("\n")
 
else:
    # Print an error message if the request failed
    print(f"Failed to fetch data. Status code: {response.status_code}")
    print(f"Response: {response.text}")
```

>[!TAB Java]


```java
package org.example;
 
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
 
import org.apache.http.HttpResponse;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.DefaultHttpClient;
 
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
 
public class Main {
    public static void main(String[] args) {
 
        ObjectMapper objectMapper = new ObjectMapper();
 
        try {
 
            DefaultHttpClient httpClient = new DefaultHttpClient();
            HttpGet getRequest = new HttpGet(
                "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone");
            getRequest.addHeader("accept", "application/json");
            getRequest.addHeader("Authorization","<TOKEN>");
            getRequest.addHeader("Content-Type", "application/json");
            getRequest.addHeader("x-gw-ims-org-id", "<ORG_ID>");
            getRequest.addHeader("x-api-key", "<API_KEY>");
 
            HttpResponse response = httpClient.execute(getRequest);
 
            if (response.getStatusLine().getStatusCode() != 200) {
                throw new RuntimeException("Failed : HTTP error code : "
                    + response.getStatusLine().getStatusCode());
            }
 
            final JsonNode jsonResponse = objectMapper.readTree(response.getEntity().getContent());
 
            System.out.println("\nOutput from API Response .... \n");
            System.out.printf("ContainerName: %s%n", jsonResponse.at("/containerName").textValue());
            System.out.printf("SASToken: %s%n", jsonResponse.at("/SASToken").textValue());
 
            httpClient.getConnectionManager().shutdown();
 
        } catch (ClientProtocolException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

>[!ENDTABS]


## 更新[!DNL Data Landing Zone]認證

您可以向[!DNL Connectors] API的`/credentials`端點發出POST要求，以更新您的`SASToken`。

**API格式**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| 標頭 | 說明 |
| --- | --- |
| `user_drop_zone` | `user_drop_zone`型別允許API將登陸區域容器與您可用的其他型別容器區分開來。 |
| `refresh` | `refresh`動作可讓您重設您的登陸區域認證，並自動產生新的`SASToken`。 |

**要求**

以下請求會更新您的登陸區域認證。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**回應**

下列回應會傳回您`SASToken`和`SASUri`的更新值。

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "expiryDate": "2024-01-06"
}
```

## 探索登陸區域檔案結構和內容

您可以向[!DNL Flow Service] API的`connectionSpecs`端點發出GET要求，以探索您登陸區域的檔案結構和內容。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | 對應至[!DNL Data Landing Zone]的連線規格識別碼。 此固定ID為： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回在查詢的目錄中找到的檔案和資料夾陣列。 記下您要上傳之檔案的`path`屬性，因為您必須在下個步驟中提供該屬性，才能檢查其結構。

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "dlz-user-container/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "data8.csv",
        "path": "dlz-user-container/data8.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "folder",
        "name": "userdata1",
        "path": "dlz-user-container/userdata1/",
        "canPreview": false,
        "canFetchSchema": false
    }
]
```

## 預覽登陸區域檔案結構和內容

若要檢查登入區域中的檔案結構，請在提供檔案路徑並輸入作為查詢引數的同時，執行GET要求。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | 對應至[!DNL Data Landing Zone]的連線規格識別碼。 此固定ID為： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |
| `{OBJECT_TYPE}` | 您要存取的物件型別。 | `file` |
| `{OBJECT}` | 您要存取之物件的路徑和名稱。 | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | 檔案的型別。 | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | 布林值，定義是否支援檔案預覽。 | </ul><li>`true`</li><li>`false`</li></ul> |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回查詢檔案的結構，包括檔案名稱和資料型別。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "FirstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "LastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Email": "rsmith@abc.com",
            "FirstName": "Richard",
            "Phone": "111111111",
            "Id": "12345",
            "LastName": "Smith"
        },
        {
            "Email": "morgan@bac.com",
            "FirstName": "Morgan",
            "Phone": "22222222222",
            "Id": "67890",
            "LastName": "Hart"
        }
    ]
}
```

### 使用`determineProperties`自動偵測[!DNL Data Landing Zone]的檔案屬性資訊

當進行GET呼叫以探索您來源的內容和結構時，您可以使用`determineProperties`引數自動偵測[!DNL Data Landing Zone]之檔案內容的內容資訊。

#### `determineProperties`個使用案例

下表概述使用`determineProperties`查詢引數或手動提供檔案資訊時可能會遇到的不同情況。

| `determineProperties` | `queryParams` | 回應 |
| --- | --- | --- |
| True | 不適用 | 如果將`determineProperties`提供為查詢引數，則會發生檔案屬性偵測，且回應會傳回新的`properties`索引鍵，其中包含檔案型別、壓縮型別和欄分隔符號的資訊。 |
| 不適用 | True | 如果檔案型別、壓縮型別和欄分隔符號的值是手動提供為`queryParams`的一部分，則會使用它們來產生結構描述，而相同的屬性會作為回應的一部分傳回。 |
| True | True | 如果兩個選項同時完成，則會傳回錯誤。 |
| 不適用 | 不適用 | 如果兩個選項均未提供，則會傳回錯誤，因為無法取得回應的屬性。 |

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `determineProperties` | 此查詢引數可讓[!DNL Flow Service] API偵測與檔案屬性相關的資訊，包括檔案型別、壓縮型別和欄分隔符號的相關資訊。 | `true` |

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回查詢檔案的結構，包括檔案名稱和資料型別，以及`properties`索引鍵，其中包含`fileType`、`compressionType`和`columnDelimiter`的資訊。

+++按一下我

```json
{
    "properties": {
        "fileType": "delimited",
        "compressionType": "tarGzip",
        "columnDelimiter": "~"
    },
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "firstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "lastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "birthday",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "birthday": "1313-0505-19731973",
            "firstName": "Yvonne",
            "lastName": "Thilda",
            "id": "100",
            "email": "Yvonne.Thilda@yopmail.com"
        },
        {
            "birthday": "1515-1212-19731973",
            "firstName": "Mary",
            "lastName": "Pillsbury",
            "id": "101",
            "email": "Mary.Pillsbury@yopmail.com"
        },
        {
            "birthday": "0505-1010-19751975",
            "firstName": "Corene",
            "lastName": "Joeann",
            "id": "102",
            "email": "Corene.Joeann@yopmail.com"
        },
        {
            "birthday": "2727-0303-19901990",
            "firstName": "Dari",
            "lastName": "Greenwald",
            "id": "103",
            "email": "Dari.Greenwald@yopmail.com"
        },
        {
            "birthday": "1717-0404-19651965",
            "firstName": "Lucy",
            "lastName": "Magdalen",
            "id": "199",
            "email": "Lucy.Magdalen@yopmail.com"
        }
    ]
}
```

+++

| 屬性 | 說明 |
| --- | --- |
| `properties.fileType` | 查詢檔案的對應檔案型別。 支援的檔案型別為： `delimited`、`json`和`parquet`。 |
| `properties.compressionType` | 用於查詢檔案的對應壓縮型別。 支援的壓縮型別為： <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | 用於查詢檔案的對應欄分隔符號。 任何單一字元值都是允許的欄分隔符號。 預設值為逗號`(,)`。 |


## 建立來源連線

來源連線會建立和管理與擷取資料的外部來源的連線。 來源連線包含資料來源、資料格式以及建立資料流所需的來源連線ID等資訊。 租使用者和組織專屬的來源連線例項。

若要建立來源連線，請向[!DNL Flow Service] API的`/sourceConnections`端點提出POST要求。


**API格式**

```http
POST /sourceConnections
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Data Landing Zone source connection",
        "data": {
            "format": "delimited"
        },
        "params": {
            "path": "dlz-user-container/data8.csv"
        },
        "connectionSpec": {
            "id": "26f526f2-58f4-4712-961d-e41bf1ccc0e8",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | [!DNL Data Landing Zone]來源連線的名稱。 |
| `data.format` | 您要帶到Platform的資料格式。 |
| `params.path` | 您要帶到Platform的檔案路徑。 |
| `connectionSpec.id` | 對應至[!DNL Data Landing Zone]的連線規格識別碼。 此固定ID為： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |

**回應**

成功的回應會傳回新建立的來源連線的唯一識別碼(`id`)。 在下一個教學課程中，需要此ID才能建立資料流。

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## 後續步驟

依照本教學課程，您已擷取您的[!DNL Data Landing Zone]認證、探索其檔案結構以尋找您要帶到Platform的檔案，並建立來源連線以開始將您的資料帶到Platform。 您現在可以繼續進行下一個教學課程，您將瞭解如何[建立資料流，以使用 [!DNL Flow Service] API](../../collect/cloud-storage.md)將雲端儲存空間資料帶入Platform。
