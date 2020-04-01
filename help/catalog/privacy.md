---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料湖中的隱私權要求處理
topic: overview
translation-type: tm+mt
source-git-commit: 5f0e0deb4a2fae636ac4d2313a6541c25309c294

---


# 資料湖中的隱私權要求處理

Adobe Experience Platform隱私服務會處理客戶存取、選擇退出銷售或刪除其個人資料的要求，這些資料由隱私權法規(例如通用資料保護規則(GDPR)和加州消費者隱私法(CCPA)規定。

本檔案涵蓋處理儲存在資料湖中之客戶資料之隱私權要求的相關基本概念。

## 快速入門

建議您在閱讀本指南之前，先瞭解下列Experience Platform服務：

* [隱私權服務](../privacy-service/home.md):管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的要求。
* [目錄服務](home.md):Experience Platform中資料位置和世系的記錄系統。 提供可用來更新資料集中繼資料的API。
* [體驗資料模型(XDM)系統](../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。

## 新增隱私權標籤至資料集 {#privacy-labels}

為了讓資料集在資料湖的隱私權要求中處理，必須為資料集指定隱私權標籤。 隱私權標籤會指出資料集關聯結構中的哪些欄位適用於您預期在隱私權要求中傳送的命名空間。

本節將示範如何新增隱私權標籤至資料集，以便用於Data Lake隱私權要求。 首先，請考慮以下資料集：

```json
{
    "5d8e9cf5872f18164763f971": {
        "name": "Loyalty Members",
        "description": "Dataset for the Loyalty Members schema",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "loyalty_members"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "id": "5d8e9cf5872f18164763f971",
        "dule": {
            "identity": [],
            "contract": [
                "C2",
                "C5"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C5"
            ],
            "identifiability": [],
            "specialTypes": []
        },
        "version": "1.0.2",
        "created": 1569627381749,
        "updated": 1569880723282,
        "createdClient": "acp_ui_platform",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "viewId": "5d8e9cf5872f18164763f972",
        "aspect": "production",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/5d8e9cf5872f18164763f971/views/5d8e9cf5872f18164763f972/files",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [
                {
                    "path": "/properties/personalEmail/properties/address",
                    "identity": [
                        "I1"
                    ],
                    "contract": [],
                    "sensitive": [],
                    "contracts": [],
                    "identifiability": [
                        "I1"
                    ],
                    "specialTypes": []
                }
            ],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

資 `schemaMetadata` 料集的屬性包含目 `gdpr` 前空的陣列。 若要將隱私權標籤新增至資料集，必須使用目錄服務API的PATCH要求 [更新此陣列](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

>[!NOTE] 雖然陣列已命名， `gdpr`但在陣列中添加標籤將允許對GDPR和CCPA管理法規要求隱私權工作。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 要 `id` 更新的資料集值。 |

**請求**

在此範例中，資料集在欄位中包含電子郵件地址 `personalEmail.address` 。 為了讓此欄位作為Data Lake隱私請求的標識符，必須將使用未註冊命名空間的標籤添加到其陣 `gdpr` 列。

下列請求會新增隱私權標籤，將命名空間&quot;email_label&quot;指派給欄 `personalEmail.address` 位。

>[!IMPORTANT] 在資料集的屬性上執行PATCH `schemaMetadata` 作業時，請務必複製請求裝載中的任何現有子屬性。 從裝載中排除任何現有值將導致從資料集中移除這些值。

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/catalog/dataSets/5d8e9cf5872f18164763f971' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{ 
    "schemaMetadata": { 
      "primaryKey": [],
      "delta": [],
      "dule": [
        {
          "path": "/properties/personalEmail/properties/address",
          "identity": [
              "I1"
          ],
          "contract": [],
          "sensitive": [],
          "contracts": [],
          "identifiability": [
              "I1"
          ],
          "specialTypes": []
        }
      ],
      "gdpr": [
          {
              "namespace": ["email_label"],
              "path": "/properties/personalEmail/properties/address"
          }
      ]
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `namespace` | 列出要與中指定欄位關聯的命名空間的陣列 `path`。 在「隱私服務API」中提交存取或刪除請求 [時，使用名稱空間來識別與隱私權](#submit) 相關的欄位。 |
| `path` | 資料集關聯架構中適用於的欄位路徑 `namespace`。 理想情況下，隱私權標籤僅應套用至「葉」欄位（不含子欄位的欄位）。 |

**回應**

成功的回應會傳回HTTP狀態200(OK)，其ID為裝載中提供的資料集。 使用ID再次查看資料集會顯示已新增隱私權標籤。

```json
[
    "@/dataSets/5d8e9cf5872f18164763f971"
]
```

### 標籤巢狀映射類型欄位

請務必注意，有兩種巢狀映射類型欄位不支援隱私權標籤：

* 陣列類型欄位中的映射類型欄位
* 另一個映射類型欄位中的映射類型欄位

上述兩個範例中的任一範例的隱私權工作處理最終會失敗。 因此，建議您避免使用巢狀對應類型欄位來儲存私人客戶資料。 相關的使用者ID應儲存為記錄型資料集的欄位 `identityMap` （本身為映射類型欄位）內的非映射資料類型，或時間 `endUserID` 系列型資料集的欄位。

## 提交請求 {#submit}

>[!NOTE] 本節說明如何設定資料湖的隱私權要求的格式。 強烈建議您檢閱 [Privacy Service API](../privacy-service/api/getting-started.md) 或 [Privacy Service UI](../privacy-service/ui/overview.md) 檔案，以取得如何提交隱私權工作的完整步驟，包括如何在請求負載中正確格式化已提交的使用者身分資料。

下節將說明如何使用隱私權服務API或UI來提出資料湖的隱私權要求。

### 使用API

在API中建立工作請求時，所 `userIDs` 提供的任何作業請求都必須使用特 `namespace` 定 `type` 的作業請求，並視其套用的資料儲存區而定。 資料湖的ID必須使用「未註冊」作為其 `type` 值，且值 `namespace` 必須符合已新增至適用資料集的 [隱私權標籤](#privacy-labels) 。

此外，請求 `include` 裝載的陣列必須包含請求所針對之不同資料存放區的產品值。 向Data Lake請求時，陣列必須包含值&quot;aepDataLake&quot;。

下列請求會使用未註冊的「email_label」命名空間，為資料湖建立新的隱私權工作。 它還包括陣列中Data Lake的產品 `include` 值：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

### 使用UI

在UI中建立工作請求時，請務必在 **Products下選取** AEP Data Lake **和／或** Profile __ ，以便分別處理儲存在Data Lake或Real-time Customer Profile中的資料的工作。

<img src="images/privacy/product-value.png" width="450"><br>

## 刪除請求處理

當Experience Platform收到來自隱私權服務的刪除要求時，平台會向隱私權服務傳送確認該要求已收到且受影響的資料已標示為刪除。 然後在七天內將記錄從資料湖中移除。 在該七天的時段內，資料會被軟刪除，因此無法由任何平台服務存取。

在未來版本中，平台會在實際刪除資料後傳送確認給隱私權服務。

## 後續步驟

閱讀本檔案後，您便瞭解處理資料湖的隱私權要求所涉及的重要概念。 建議您繼續閱讀本指南中提供的檔案，以加深您對如何管理身分資料和建立隱私權工作的瞭解。

如需處理描述檔 [商店的隱私權要求的步驟](../profile/privacy.md) ，請參閱即時客戶描述檔的隱私權要求處理檔案。