---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 建立類
topic: developer guide
translation-type: tm+mt
source-git-commit: 60911e32fd9235be2a258e60818011a42cd5ceba

---


# 建立類

模式的主構建塊是類。 類包含必須定義的最小欄位集，以捕獲方案的核心資料。 例如，如果您為汽車和卡車設計一個模式，他們很可能會使用一個叫做Vehicle的類，它描述了所有車輛的基本公共屬性。

Adobe和其他Experience Platform合作夥伴提供了數種標準類別，但您也可以定義自己的類別，並將它們儲存至架構註冊表。 然後，您可以合成實現所建立類的架構，並定義與新定義類相容的混合。

>[!NOTE] 根據您定義的類合成模式時，將無法使用標準混音。 每個mixin都定義其屬性中相容的類 `meta:intendedToExtend` 別。 一旦開始定義與新類相容的混音(使用混音的欄位中的 `$id``meta:intendedToExtend` 新類)，您每次定義實現所定義類的方案時，都可以重複使用這些混音。 如需詳細資訊，請 [參閱有關建立](create-mixin.md)[混合](create-schema.md) 檔案和建立結構的章節。

**API格式**

```http
POST /tenant/classes
```

**請求**

建立(POST)類別的請求必須包含包含 `allOf` 兩個值之 `$ref` 一的屬性：或 `https://ns.adobe.com/xdm/data/record` 者 `https://ns.adobe.com/xdm/data/time-series`。 這些值代表類別所依據的行為（分別是記錄或時間序列）。 有關記錄資料和時間序列資料之間差異的詳細資訊，請參閱架構構成基礎中有關行 [為類型的部分](../schema/composition.md)。

在定義類時，您也可以在類定義中包含混合或自訂欄位。 這會導致新增的混音和欄位包含在實施類別的所有結構中。 下列範例請求定義名為&quot;Property&quot;的類別，可擷取公司擁有和經營之不同屬性的相關資訊。 它包含 `propertyId` 每次使用類時要包含的欄位。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `_{TENANT_ID}` | 組織 `TENANT_ID` 的命名空間。 您的組織建立的所有資源都必須包含此屬性，以避免與「方案註冊表」中的其他資源發生衝突。 |
| `allOf` | 要由新類繼承其屬性的資源清單。 陣列中 `$ref` 的一個對象定義類的行為。 在此示例中，類繼承了「記錄」行為。 |

**回應**

成功的回應會傳回HTTP狀態201（已建立）和包含新建立類別詳細資訊的裝載，包括 `$id`、 `meta:altId`和 `version`。 這三個值是只讀的，由架構註冊表指定。

```JSON
{
    "title": "Property",
    "description": "Properties owned and operated by the company.",
    "type": "object",
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "property": {
                            "title": "Property Information",
                            "type": "object",
                            "description": "Information about different owned and operated properties.",
                            "properties": {
                                "propertyId": {
                                    "title": "Property Identification Number",
                                    "type": "string",
                                    "description": "Unique Property identification number",
                                    "meta:xdmType": "string"
                                }
                            },
                            "meta:xdmType": "object"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/record"
        },
        {
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "version": "1.0",
    "meta:resourceType": "classes",
    "meta:registryMetadata": {
        "repo:createDate": 1552086405448,
        "repo:lastModifiedDate": 1552086405448,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

執行GET請求以列出租用戶容器中的所有類別，現在會包含屬性類別。 您也可以使用URL編碼的 `$id` URI來執行查閱(GET)請求，以直接檢視新類別。 執行查閱請求時，請 `version` 務必在「接受」標題中加入。
