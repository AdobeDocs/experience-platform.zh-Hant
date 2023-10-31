---
description: 此頁面說明從Adobe Experience Platform匯出至目的地的資料中的訊息格式和設定檔轉換。
title: 訊息格式
exl-id: ab05d34e-530f-456c-b78a-7f3389733d35
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 1%

---

# 訊息格式

## 先決條件 — Adobe Experience Platform概念 {#prerequisites}

若要瞭解Adobe端的訊息格式及設定檔設定和轉換程式，請熟悉下列Experience Platform概念：

* **體驗資料模式 (XDM)**. [XDM概覽](../../../../xdm/home.md) 和  [如何在Adobe Experience Platform中建立XDM結構描述](../../../../xdm/tutorials/create-schema-ui.md).
* **類別**. [在UI中建立和編輯類別](../../../../xdm/ui/resources/classes.md).
* **身分對應**. 身分對應代表Adobe Experience Platform中所有一般使用者身分的對應。 請參閱 `xdm:identityMap` 在 [XDM欄位字典](../../../../xdm/schema/field-dictionary.md).
* **SegmentMembership**. 此 [區段會籍](../../../../xdm/schema/field-dictionary.md) XDM屬性會通知設定檔所屬的對象。 針對中的三個不同值 `status` 欄位，請閱讀以下檔案： [對象成員資格詳細資料結構欄位群組](../../../../xdm/field-groups/profile/segmentation.md).

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值如下 **區分大小寫**. 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是（只有下圖中的步驟1和2） |

## 概觀 {#overview}

此頁面說明從Adobe Experience Platform匯出至目的地的資料中的訊息格式和設定檔轉換。

Adobe Experience Platform會以各種資料格式，將資料匯出至大量的目的地。 廣告平台(Google)、社交網路(Facebook)和雲端儲存位置(Amazon S3、Azure事件中樞)是一些目的地型別的範例。

Experience Platform可以調整匯出設定檔的訊息格式，以符合您側的預期格式。 若要瞭解此自訂，請務必瞭解下列概念：

* Adobe Experience Platform中的來源(1)和目標(2) XDM結構
* 合作夥伴端的預期訊息格式(3)，以及
* XDM結構描述和預期訊息格式之間的轉換層，您可透過建立 [訊息轉換範本](#using-templating).

![結構描述至JSON轉換](../../assets/functionality/destination-server/transformations-3-steps.png)

Experience Platform使用XDM結構描述，以一致且可重複使用的方式說明資料結構。

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**來源XDM結構描述(1)**：此專案代表客戶在Experience Platform中使用的結構描述。 在Experience Platform中，在 [對應步驟](../../../ui/activate-segment-streaming-destinations.md#mapping) 在啟用目的地工作流程中，客戶會將欄位從其XDM結構描述對應到您目的地的目標結構描述(2)。

**目標XDM結構描述(2)**：根據您目的地預期格式的JSON標準結構描述(3)和目的地可解譯的屬性，您可以在目標XDM結構描述中定義設定檔屬性和身分。 您可以在目的地設定的下列位置執行此操作： [schemaConfig](../../functionality/destination-configuration/schema-configuration.md) 和 [identityNamespaces](../../functionality/destination-configuration/identity-namespace-configuration.md) 物件。

**目的地設定檔屬性的JSON標準結構描述(3)**：此範例代表 [JSON結構描述](https://json-schema.org/learn/miscellaneous-examples.html) 平台支援的所有設定檔屬性及其型別（例如：物件、字串、陣列）。 目的地可支援的範例欄位可能是 `firstName`， `lastName`， `gender`， `email`， `phone`， `productId`， `productName`、等等。 您需要 [訊息轉換範本](#using-templating) 量身打造資料匯出的不Experience Platform，使其符合您的預期格式。

根據上述結構描述轉換，以下說明來源XDM結構描述和合作夥伴端範例結構描述之間的設定檔設定變更方式：

![轉換訊息範例](../../assets/functionality/destination-server/transformations-with-examples.png)

## 快速入門 — 轉換三個基本屬性 {#getting-started}

為了示範設定檔轉換程式，以下範例在Adobe Experience Platform中使用三個常見的設定檔屬性： **名字**， **姓氏**、和 **電子郵件地址**.

>[!NOTE]
>
>客戶將屬性從來源XDM結構描述對應到Adobe Experience Platform UI中的合作夥伴XDM結構描述，在 **對應** 的步驟 [啟用目標工作流程](../../../ui/activate-segment-streaming-destinations.md#mapping).

假設您的平台可以接收類似以下的訊息格式：

```shell
POST https://YOUR_REST_API_URL/users/
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY

{
  "attributes":
    {
      "first_name": "Yours",
      "last_name": "Truly",
      "external_id": "yourstruly@adobe.com"
    }
}
```

考量訊息格式，對應的轉換如下：

| Adobe端的合作夥伴XDM結構描述中的屬性 | 轉換 | 您這邊HTTP訊息中的屬性 |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

{style="table-layout:auto"}

## Experience Platform中的設定檔結構 {#profile-structure}

若要進一步瞭解頁面上以下的範例，請務必瞭解Experience Platform中的設定檔結構。

設定檔有3個區段：

* `segmentMembership` （永遠出現在設定檔上）
   * 此區段包含設定檔中存在的所有對象。 對象可以有兩種狀態之一： `realized` 或 `exited`.
* `identityMap` （永遠出現在設定檔上）
   * 本節包含設定檔上存在的所有身分識別(電子郵件、Google GAID、Apple IDFA等)，以及使用者在啟動工作流程中對應以匯出的身分識別。
* 屬性（視目的地設定而定，這些屬性可能會出現在設定檔中）。 預先定義的屬性與自由格式屬性之間也有細微的差異：
   * 的 *自由格式屬性*，這些內含 `.value` 路徑（如果屬性出現在設定檔上） (請參閱 `lastName` 屬性（來自範例1）。 如果設定檔上不存在這些變數，則不會包含 `.value` 路徑(請參閱 `firstName` 屬性（來自範例1）。
   * 的 *預先定義的屬性*，這些不包含 `.value` 路徑。 設定檔中存在的所有對應屬性都會出現在屬性對應中。 不會出現的不存在的專案(請參閱範例2 - `firstName` 屬性不存在於設定檔上)。

請參閱以下兩個Experience Platform中的設定檔範例：

### 範例1搭配 `segmentMembership`， `identityMap` 自由格式屬性的和屬性 {#example-1}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "firstName": {
    },
    "lastName": {
      "value": "lastName"
    }
  }
}
```

### 範例2，具有 `segmentMembership`， `identityMap` 預先定義屬性的和屬性 {#example-2}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "lastName": "lastName"
  }
}
```

## 使用範本語言進行身分、屬性和對象成員資格轉換 {#using-templating}

Adobe使用 [卵石範本](https://pebbletemplates.io/)，類似於 [金家](https://jinja.palletsprojects.com/en/2.11.x/)，將欄位從Experience PlatformXDM結構描述轉換為目的地支援的格式。

本節提供如何進行這些轉換的數個範例，從輸入XDM結構描述，透過範本，以及輸出為目的地接受的裝載格式。 以下範例是透過增加複雜性來呈現，如下所示：

1. 簡單轉換範例。 瞭解範本化如何與簡單的轉換搭配運作 [設定檔屬性](#attributes)， [對象會籍](#segment-membership)、和 [身分](#identities) 欄位。
2. 結合上述欄位的範本範例複雜性增加： [建立可傳送對象和身分的範本](./message-format.md#segments-and-identities) 和 [建立可傳送區段、身分和設定檔屬性的範本](#segments-identities-attributes).
3. 包含彙總索引鍵的範本。 當您使用 [可設定的彙總](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 在目標設定中，Experience Platform會根據對象ID、對象狀態或身分名稱空間等條件，將匯出至目標的設定檔分組。

### 設定檔屬性 {#attributes}

若要轉換匯出至目的地的設定檔屬性，請參閱以下的JSON和程式碼範例。

>[!IMPORTANT]
>
>如需Adobe Experience Platform中所有可用設定檔屬性的清單，請參閱 [XDM欄位字典](../../../../xdm/schema/field-dictionary.md).


**輸入**

設定檔1：

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
    },
    "birthDate": {}
  }
}
```

設定檔2：

```json
{
  "attributes": {
    "firstName": {
      "value": "Harry"
    },
    "birthDate": {
        "value": "1980/07/31"
    }
  }
}
```

**範本**

>[!IMPORTANT]
>
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 插入之前 [範本](../../functionality/destination-server/templating-specs.md) 在 [目的地伺服器設定](../../authoring-api/destination-server/create-destination-server.md). 如需有關逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            {% for attribute in profile.attributes %}
            "{{ attribute.key }}":
                {% if attribute.value is empty %}
                    null
                {% else %}
                    "{{ attribute.value.value }}"
                {% endif %}
            {% if not loop.last %},{% endif %}
            {% endfor %}
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**結果**


```json
{
    "profiles": [
        {
            "firstName": "Hermione",
            "birthDate": null
        },
        {
            "firstName": "Harry",
            "birthDate": "1980/07/31"
        }
    ]
}
```

### 對象會籍 {#audience-membership}

此 [區段會籍](../../../../xdm/schema/field-dictionary.md) XDM屬性會通知設定檔所屬的對象。
針對中的三個不同值 `status` 欄位，請閱讀以下檔案： [對象成員資格詳細資料結構欄位群組](../../../../xdm/field-groups/profile/segmentation.md).

**輸入**

設定檔1：

```json
{
  "segmentMembership": {
    "ups": {
      "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "8f812592-3f06-416b-bd50-e7831848a31a": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      }
    }
  }
}
```

設定檔2：

```json
{
  "segmentMembership": {
    "ups": {
      "32396e4b-16f6-4033-9702-fc69b5e24e7c": {
        "lastQualificationTime": "2021-08-20T17:23:04Z",
        "status": "realized"
      },
      "af854278-894a-4192-a96b-320fbf2623fd": {
        "lastQualificationTime": "2021-08-20T16:44:37Z",
        "status": "realized"
      },
      "66505bf9-bc08-4bac-afbc-8b6706650ea4": {
        "lastQualificationTime": "2019-08-20T17:23:04Z",
        "status": "realized"
      }
    }
  }
}
```

**範本**

>[!IMPORTANT]
>
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 插入之前 [範本](../../functionality/destination-server/templating-specs.md) 在 [目的地伺服器設定](../../authoring-api/destination-server/create-destination-server.md). 如需有關逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).


```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering audiences by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**結果**

```json
{
    "profiles": [
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "32396e4b-16f6-4033-9702-fc69b5e24e7c",
                    "af854278-894a-4192-a96b-320fbf2623fd",
                    "66505bf9-bc08-4bac-afbc-8b6706650ea4"
                ],
                "remove": [
                ]
            }
        }
    ]
}
```

### 身分 {#identities}

如需Experience Platform中身分的相關資訊，請參閱 [身分名稱空間總覽](../../../../identity-service/namespaces.md).

**輸入**

設定檔1：

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    }
}
```

設定檔2：

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    }
}
```

**範本**

>[!IMPORTANT]
>
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 插入之前 [範本](../../functionality/destination-server/templating-specs.md) 在 [目的地伺服器設定](../../authoring-api/destination-server/create-destination-server.md). 如需有關逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ]
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**結果**

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ]
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ]
        }
    ]
}
```

### 建立可傳送對象和身分的範本 {#segments-and-identities}

本節提供AdobeXDM結構描述和合作夥伴目的地結構描述之間常用轉換的範例。
以下範例說明如何轉換對象會籍和身分格式，並將其輸出至您的目的地。

**輸入**

設定檔1：

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

設定檔2：

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2021-08-31T10:01:42Z",
                "status": "realized"
            }
        }
    }
}
```

**範本**

>[!IMPORTANT]
>
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 插入之前 [範本](../../functionality/destination-server/templating-specs.md) 在 [目的地伺服器設定](../../authoring-api/destination-server/create-destination-server.md). 如需有關逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
                
                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}
                
                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ],
                "remove": [
                    {# Alternative syntax for filtering audiences by status: #}
                    {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**結果**

此 `json` 以下表示從Adobe Experience Platform匯出的資料。

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### 建立可傳送區段、身分和設定檔屬性的範本 {#segments-identities-attributes}

本節提供AdobeXDM結構描述和合作夥伴目的地結構描述之間常用轉換的範例。

另一個常見的使用案例是匯出包含對象成員資格、身分（例如：電子郵件地址、電話號碼、廣告ID）和個人檔案屬性的資料。 若要以此方式匯出資料，請參閱下列範例：

**輸入**

設定檔1：

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
        },
        "birthDate": {}
    },
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

設定檔2：

```json
{
    "attributes": {
        "firstName": {
            "value": "Harry"
        },
        "birthDate": {
            "value": "1980/07/31"
        }
    },
    "identityMap": {
        "email": [
            {
                "id": "harry.p@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            }
        }
    }
}
```

**範本**

>[!IMPORTANT]
>
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 插入之前 [範本](../../functionality/destination-server/templating-specs.md) 在 [目的地伺服器設定](../../authoring-api/destination-server/create-destination-server.md). 如需有關逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "attributes": {
            {% for attribute in profile.attributes %}
                "{{ attribute.key }}":
                    {% if attribute.value is empty %}
                        null
                    {% else %}
                        "{{ attribute.value.value }}"
                    {% endif %}
                {% if not loop.last %},{% endif %}
            {% endfor %}
            },
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if we have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering audiences by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }
    ]
}
```

**結果**

此 `json` 以下表示從Adobe Experience Platform匯出的資料。

```json
{
    "profiles": [
        {
            "attributes": {
                "firstName": "Hermione",
                "birthDate": null
            },
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "attributes": {
                "firstName": "Harry",
                "birthDate": "1980/07/21"
            },
            "identities": [
                {
                    "type": "email",
                    "id": "harry.p@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### 在您的範本中加入彙總金鑰，以存取依不同條件分組的匯出設定檔 {#template-aggregation-key}

當您使用 [可設定的彙總](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 在目標設定中，您可以根據對象ID、對象別名、對象成員資格或身分名稱空間等條件，將匯出至目標的設定檔分組。

在訊息轉換範本中，您可以存取上述彙總索引鍵，如下列章節的範例所示。 使用彙總金鑰來建構匯出為Experience Platform之外的HTTP訊息，以符合目的地預期的格式和速率限制。

#### 在範本中使用對象ID彙總索引鍵 {#aggregation-key-segment-id}

如果您使用 [可設定的彙總](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 並設定 `includeSegmentId` 若設為true，則匯出至目的地的HTTP訊息中的設定檔會依對象ID分組。 請參閱下方以瞭解如何在範本中存取對象ID。

**輸入**

請考量下列四個設定檔，其中：

* 前兩個是具有對象ID的對象的一部分 `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* 第三個設定檔是具有對象ID的對象的一部分 `8f812592-3f06-416b-bd50-e7831848a31a`
* 第四個設定檔是上述兩個對象的一部分。

設定檔1：

```json
{
   "attributes":{
      "firstName":{
         "value":"Hermione"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

設定檔2：

```json
{
   "attributes":{
      "firstName":{
         "value":"Harry"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

設定檔3：

```json
{
   "attributes":{
      "firstName":{
         "value":"Tom"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         }
      }
   }
}
```

設定檔4：

```json
{
   "attributes":{
      "firstName":{
         "value":"Jerry"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

**範本**

>[!IMPORTANT]
>
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 插入之前 [範本](../../functionality/destination-server/templating-specs.md) 在 [目的地伺服器設定](../../authoring-api/destination-server/create-destination-server.md). 如需有關逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

請注意以下方式 `audienceId` 用於範本中存取對象ID。 此範例假設您使用 `audienceId` 目的地分類法的對象成員資格。 您可以改用任何其他欄位名稱，視您自己的分類法而定。

```python
{
    "audienceId": "{{ input.aggregationKey.segmentId }}",
    "profiles": [
        {% for profile in input.profiles %}
        {
            "first_name": "{{ profile.attributes.firstName.value }}"
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**結果**

將設定檔匯出至目的地時，會根據其對象ID將設定檔分割為兩個群組。

```json
{
   "audienceId":"788d8874-8007-4253-92b7-ee6b6c20c6f3",
   "profiles":[
      {
         "firstName":"Hermione"
      },
      {
         "firstName":"Harry"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

```json
{
   "audienceId":"8f812592-3f06-416b-bd50-e7831848a31a",
   "profiles":[
      {
         "firstName":"Tom"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

#### 在範本中使用對象別名彙總索引鍵 {#aggregation-key-segment-alias}

如果您使用 [可設定的彙總](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 並設定 `includeSegmentId` 若設為true，您也可以在範本中存取對象別名。

將下行的內容新增至範本，以存取依對象別名分組的匯出設定檔。

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### 在範本中使用對象狀態彙總索引鍵 {#aggregation-key-segment-status}

如果您使用 [可設定的彙總](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 並設定 `includeSegmentId` 和 `includeSegmentStatus` 若設為true，您可以存取範本中的對象狀態。 如此一來，您就可以根據應從區段新增還是移除設定檔，將匯出至目的地的HTTP訊息中的設定檔分組。

可能的值包括：

* 已實現
* 現有
* 已退出

根據上述值，將以下行新增到範本中，以在區段中新增或移除設定檔：

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### 在範本中使用身分名稱空間彙總金鑰 {#aggregation-key-identity}

以下範例說明 [可設定的彙總](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 在目的地設定中，設定為依身分名稱空間彙總匯出的設定檔，採用形式 `"namespaces": ["email", "phone"]` 和 `"namespaces": ["GAID", "IDFA"]`. 請參閱 `groups` 中的引數 [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md) 檔案，以瞭解有關分組的更多詳細資訊。

**輸入**

設定檔1：

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e1@example.com"
         },
         {
            "id":"e2@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744111222"
         }
      ],
      "IDFA":[
         {
            "id":"AEBE52E7-03EE-455A-B3C4-E57283966239"
         }
      ],
      "GAID":[
         {
            "id":"e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         }
      ]
   }
}
```

設定檔2：

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e3@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744333444"
         },
         {
            "id":"+40744555666"
         }
      ],
      "IDFA":[
         {
            "id":"134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         }
      ],
      "GAID":[
         {
            "id":"47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         }
      ]
   }
}
```

**範本**

>[!IMPORTANT]
>
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 插入之前 [範本](../../functionality/destination-server/templating-specs.md) 在 [目的地伺服器設定](../../authoring-api/destination-server/create-destination-server.md). 如需有關逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

請注意 `input.aggregationKey.identityNamespaces` 用於以下的範本

```python
{
            "profiles": [
            {% for profile in input.profiles %}
            {
                {% for ns in input.aggregationKey.identityNamespaces %}
                "{{ns}}": [
                    {% for id in profile.identityMap[ns] %}
                    "{{id.id}}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]{% if not loop.last %},{% endif %}
                {% endfor %}
            }{% if not loop.last %},{% endif %}
            {% endfor %}
        ]
}
```

**結果**

將設定檔匯出至目的地時，會根據其身分名稱空間將設定檔分割為兩個群組。 電子郵件和電話位於一個群組中，而GAID和IDFA位於另一個群組中。

```json
{
   "profiles":[
      {
         "email":[
            "e1@example.com",
            "e2@example.com"
         ],
         "phone":[
            "+40744111222"
         ]
      },
      {
         "email":[
            "e3@example.com"
         ],
         "phone":[
            "+40744333444",
            "+40744555666"
         ]
      }
   ]
}
```

```json
{
   "profiles":[
      {
         "IDFA":[
            "AEBE52E7-03EE-455A-B3C4-E57283966239"
         ],
         "GAID":[
            "e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         ]
      },
      {
         "IDFA":[
            "134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         ],
         "GAID":[
            "47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         ]
      }
   ]
}
```

#### 在URL範本中使用彙總金鑰 {#aggregation-key-url-template}

視您的使用案例而定，您也可以在URL中使用這裡所述的彙總索引鍵，如下所示：

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### 參考：轉換範本中使用的內容與函式 {#reference}

提供給範本的內容包含 `input`  （此呼叫中匯出的設定檔/資料）和 `destination` (有關Adobe將資料傳送至哪個目的地的資料，適用於所有設定檔)。

下表提供上述範例中函式的說明。

| 函數 | 說明 |
|---------|----------|
| `input.profile` | 設定檔，表示為 [JsonNode](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). 依照此頁面中進一步提及的合作夥伴XDM結構描述。 |
| `destination.segmentAliases` | 從Adobe Experience Platform名稱空間中的對象ID對應至合作夥伴系統中的對象別名。 |
| `destination.segmentNames` | 從Adobe Experience Platform名稱空間中的對象名稱對應至合作夥伴系統中的對象名稱。 |
| `addedSegments(listOfSegments)` | 僅傳回具有狀態的對象 `realized`. |
| `removedSegments(listOfSegments)` | 僅傳回具有狀態的對象 `exited`. |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在瞭解從Experience Platform匯出的資料如何轉換。 接下來，請閱讀下列頁面，完成您為目的地建立訊息轉換範本的相關知識：

* [建立及測試訊息轉換範本](../../testing-api/streaming-destinations/create-template.md)
* [轉譯器範本API作業](../../testing-api/streaming-destinations/render-template-api.md)
* [Destination SDK中支援的轉換函式](../destination-server/supported-functions.md)

若要深入瞭解其他目的地伺服器元件，請參閱下列文章：

* [以Destination SDK建立的目的地的伺服器規格](server-specs.md)
* [範本規格](templating-specs.md)
* [檔案格式設定](file-formatting.md)
