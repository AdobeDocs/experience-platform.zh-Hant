---
description: 本頁面說明從Adobe Experience Platform匯出至目的地之資料中的訊息格式和設定檔轉換。
title: 訊息格式
exl-id: 1212c1d0-0ada-4ab8-be64-1c62a1158483
source-git-commit: 9aba3384b320b8c7d61a875ffd75217a5af04815
workflow-type: tm+mt
source-wordcount: '2267'
ht-degree: 2%

---

# 訊息格式

## 必要條件 — Adobe Experience Platform概念 {#prerequisites}

若要了解訊息格式以及Adobe端的設定檔設定和轉換程式，請熟悉下列Experience Platform概念：

* **Experience Data Model(XDM)**. [XDM概觀](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant) 和  [如何在Adobe Experience Platform中建立XDM結構](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=zh-Hant).
* **類別**. [在UI中建立和編輯類](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **IdentityMap**. 身分對應代表Adobe Experience Platform中所有一般使用者身分的對應。 請參閱 `xdm:identityMap` 在 [XDM欄位字典](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).
* **區段成員資格**. 此 [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM屬性會通知設定檔是的成員區段。 對於 `status` 欄位，請閱讀 [區段成員資格詳細資料結構欄位群組](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

## 總覽 {#overview}

將此頁面的內容與其餘內容一起使用 [合作夥伴目的地的設定選項](./configuration-options.md). 本頁面說明從Adobe Experience Platform匯出至目的地之資料中的訊息格式和設定檔轉換。 其他頁面則說明連線及驗證目的地的詳細資訊。

Adobe Experience Platform會以各種資料格式將資料匯出至大量目的地。 目的地類型的一些範例包括廣告平台(Google)、社交網路(Facebook)和雲端儲存位置(Amazon S3、Azure事件中樞)。

Experience Platform可以調整匯出設定檔的訊息格式，以符合您這邊的預期格式。 若要了解此自訂，下列概念非常重要：
* Adobe Experience Platform中的來源(1)和目標(2)XDM結構
* 合作夥伴端(3)的預期訊息格式，以及
* XDM架構與預期訊息格式之間的轉換層，您可以透過建立 [消息轉換模板](./message-format.md#using-templating).

![結構轉換為JSON](./assets/transformations-3-steps.png)

Experience Platform使用XDM結構，以一致且可重複使用的方式說明資料結構。

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**源XDM架構(1)**:此項目指客戶在Experience Platform中使用的結構。 在Experience Platform中，在 [對應步驟](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping) 在啟用目標工作流程中，客戶將欄位從其XDM架構對應至目標的目標架構(2)。

**Target XDM結構(2)**:您可以根據目的地預期格式的JSON標準結構(3)，以及目的地可解譯的屬性，在目標XDM結構中定義設定檔屬性和身分。 您可以在目的地設定中，於 [schemaConfig](./destination-configuration.md#schema-configuration) 和 [identityNamespaces](./destination-configuration.md#identities-and-attributes) 對象。

**目的地設定檔屬性的JSON標準結構(3)**:此範例代表 [JSON結構](https://json-schema.org/learn/miscellaneous-examples.html) 平台支援的所有設定檔屬性及其類型(例如：物件、字串、陣列)。 目標可支援的欄位範例為 `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName`等。 您需要 [消息轉換模板](./message-format.md#using-templating) 量身打造出Experience Platform的資料，使其符合您預期的格式。

根據上述結構轉換，以下是來源XDM結構與合作夥伴端範例結構之間的設定檔組態變更方式：

![轉換消息示例](./assets/transformations-with-examples.png)

## 快速入門 — 轉換三個基本屬性 {#getting-started}

為了示範設定檔轉換程式，下列範例在Adobe Experience Platform中使用三個常見的設定檔屬性： **名字**, **姓氏**，和 **電子郵件地址**.

>[!NOTE]
>
>客戶會將來源XDM結構的屬性對應至Adobe Experience Platform UI中的合作夥伴XDM結構(位於 **對應** 步驟 [啟動目標工作流程](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

假設您的平台可接收如下的訊息格式：

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

考慮到報文格式，相應的轉換如下：

| 合作夥伴XDM結構中的Adobe端屬性 | 轉換 | HTTP訊息中的屬性 |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

{style="table-layout:auto"}

## Experience Platform中的設定檔結構 {#profile-structure}

若要進一步了解頁面上的下列範例，請務必了解Experience Platform中設定檔的結構。

設定檔有3個區段：

* `segmentMembership` （一律顯示在設定檔中）
   * 本節包含設定檔上呈現的所有區段。 區段可以有兩種狀態之一： `realized` 或 `exited`.
* `identityMap` （一律顯示在設定檔中）
   * 本節包含設定檔(電子郵件、Google GAID、Apple IDFA等)上呈現的所有身分識別，以及在啟用工作流程中對應以匯出的使用者。
* 屬性（視目標設定而定，這些屬性可能存在於設定檔中）。 預先定義的屬性和自由格式屬性之間也有些許差異：
   * for *自由格式屬性*，這些包含 `.value` 路徑(如果屬性存在於設定檔中，請參閱 `lastName` 屬性)。 如果設定檔上沒有，則不會包含 `.value` 路徑(請參閱 `firstName` 屬性)。
   * for *預先定義的屬性*，這些不包含 `.value` 路徑。 設定檔上呈現的所有已對應屬性都會顯示在屬性對應中。 不存在的則不會出現(請參閱範例2 - `firstName` 屬性不存在於設定檔中)。

請參閱以下兩個Experience Platform中的設定檔範例：

### 範例1，包含 `segmentMembership`, `identityMap` 和自由格式屬性 {#example-1}

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

### 範例2，包含 `segmentMembership`, `identityMap` 和預先定義屬性的屬性 {#example-2}

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

## 使用範本語言進行身分、屬性和區段成員資格轉換 {#using-templating}

Adobe使用 [卵石模板](https://pebbletemplates.io/)，範本語言類似 [金子](https://jinja.palletsprojects.com/en/2.11.x/)，將Experience PlatformXDM結構的欄位轉換為目的地支援的格式。

本節提供幾個進行這些轉換的範例：從輸入XDM架構、透過範本，以及輸出為目的地接受的裝載格式。 以下範例以日益複雜的方式呈現，如下所示：

1. 簡單的轉換範例。 了解範本如何與 [設定檔屬性](./message-format.md#attributes), [區段成員資格](./message-format.md#segment-membership)，和 [身分](./message-format.md#identities) 欄位。
2. 結合上述欄位的範本，其複雜度增加範例： [建立可傳送區段和身分的範本](./message-format.md#segments-and-identities) 和 [建立可傳送區段、身分和設定檔屬性的範本](./message-format.md#segments-identities-attributes).
3. 包含聚合鍵的模板。 使用 [可配置聚合](./destination-configuration.md#configurable-aggregation) 在目的地設定中，Experience Platform會根據區段ID、區段狀態或身分識別命名空間等條件，將匯出至目的地的設定檔分組。

### 設定檔屬性 {#attributes}

若要轉換匯出至目的地的設定檔屬性，請參閱下方的JSON和程式碼範例。

>[!IMPORTANT]
>
>如需Adobe Experience Platform中所有可用設定檔屬性的清單，請參閱 [XDM欄位字典](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).


**輸入**

配置檔案1:

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

配置檔案2:

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
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 在 [目標伺服器配置](./server-and-template-configuration.md#template-specs). 如需逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

### 區段成員資格 {#segment-membership}

此 [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM屬性會通知設定檔是的成員區段。
對於 `status` 欄位，請閱讀 [區段成員資格詳細資料結構欄位群組](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

**輸入**

配置檔案1:

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

配置檔案2:

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
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 在 [目標伺服器配置](./server-and-template-configuration.md#template-specs). 如需逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                {# Alternative syntax for filtering segments by status: #}
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

如需Experience Platform中身分的相關資訊，請參閱 [身分命名空間概觀](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en).

**輸入**

配置檔案1:

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

配置檔案2:

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
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 在 [目標伺服器配置](./server-and-template-configuration.md#template-specs). 如需逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

### 建立可傳送區段和身分的範本 {#segments-and-identities}

本節提供AdobeXDM結構與合作夥伴目標結構之間常用轉換的範例。
以下範例說明如何轉換區段成員資格和身分格式，並將其輸出至您的目的地。

**輸入**

配置檔案1:

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

配置檔案2:

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
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 在 [目標伺服器配置](./server-and-template-configuration.md#template-specs). 如需逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                    {# Alternative syntax for filtering segments by status: #}
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

此 `json` 以下代表從Adobe Experience Platform匯出的資料。

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

本節提供AdobeXDM結構與合作夥伴目標結構之間常用轉換的範例。

另一個常見的使用案例是匯出包含區段成員資格、身分識別的資料(例如：電子郵件地址、電話號碼、廣告ID)和設定檔屬性。 若要以此方式匯出資料，請參閱下列範例：

**輸入**

配置檔案1:

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

配置檔案2:

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
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 在 [目標伺服器配置](./server-and-template-configuration.md#template-specs). 如需逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                {# Alternative syntax for filtering segments by status: #}
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

此 `json` 以下代表從Adobe Experience Platform匯出的資料。

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

### 在您的範本中包含匯總金鑰，以存取依各種准則分組的匯出設定檔 {#template-aggregation-key}

使用 [可配置聚合](./destination-configuration.md#configurable-aggregation) 在目的地設定中，您可以根據區段ID、區段別名、區段成員資格或身分識別命名空間等條件，將匯出至目的地的設定檔分組。

在訊息轉換範本中，您可以存取上述的匯總索引鍵，如下節的範例所示。 使用匯總金鑰來結構匯出為非Experience Platform的HTTP訊息，以符合目的地預期的格式和速率限制。

#### 在範本中使用區段ID匯總金鑰 {#aggregation-key-segment-id}

如果您使用 [可配置聚合](./destination-configuration.md#configurable-aggregation) 設定 `includeSegmentId` 若設為true，則匯出至您目的地的HTTP訊息中的設定檔會依區段ID分組。 請參閱下方範本中如何存取區段ID。

**輸入**

請考量下列四個設定檔，其中：
* 前兩個項目是區段ID的一部分 `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* 第三個設定檔是具有區段ID之區段的一部分 `8f812592-3f06-416b-bd50-e7831848a31a`
* 第四個設定檔是上述兩個區段的一部分。

配置檔案1:

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

配置檔案2:

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

配置檔案3:

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

配置檔案4:

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
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 在 [目標伺服器配置](./server-and-template-configuration.md#template-specs). 如需逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

請注意以下方式 `audienceId` 用於範本中以存取區段ID。 此範例假設您使用 `audienceId` 目的地分類法中的區段成員資格。 您可以根據自己的分類法，改用任何其他欄位名稱。

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

將設定檔匯出至目的地時，會根據其區段ID分割為兩個群組。

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

#### 在範本中使用區段別名匯總金鑰 {#aggregation-key-segment-alias}

如果您使用 [可配置聚合](./destination-configuration.md#configurable-aggregation) 設定 `includeSegmentId` 若設為true，您也可以存取範本中的區段別名。

將下面的行新增至範本，以存取依區段別名分組的匯出設定檔。

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### 在範本中使用區段狀態匯總金鑰 {#aggregation-key-segment-status}

如果您使用 [可配置聚合](./destination-configuration.md#configurable-aggregation) 設定 `includeSegmentId` 和 `includeSegmentStatus` 若設為true，您可以存取範本中的區段狀態。 如此一來，您就可以根據是否應新增或移除區段的設定檔，將匯出至目的地的HTTP訊息中的設定檔分組。

可能的值包括：

* 實現
* 現有
* 退出

將下列行新增至範本，以根據上述值從區段新增或移除設定檔：

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### 在範本中使用身分命名空間匯總金鑰 {#aggregation-key-identity}

以下範例說明 [可配置聚合](./destination-configuration.md#configurable-aggregation) 在目標設定中，設定為依身分識別命名空間匯總匯出的設定檔，格式為 `"namespaces": ["email", "phone"]` 和 `"namespaces": ["GAID", "IDFA"]`. 請參閱 `groups` 參數 [目的地設定API參考](./destination-configuration-api.md) 以取得此分組的詳細資訊。

**輸入**

配置檔案1:

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

配置檔案2:

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
>對於您使用的所有範本，您必須逸出非法字元，例如雙引號 `""` 在 [目標伺服器配置](./server-and-template-configuration.md#template-specs). 如需逸出雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

請注意 `input.aggregationKey.identityNamespaces` 用於以下範本

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

將設定檔匯出至目的地時，會根據其身分識別命名空間，分割為兩個群組。 電子郵件和電話位於一個群組，而GAID和IDFA位於另一個群組。

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

#### 在URL範本中使用匯總索引鍵 {#aggregation-key-url-template}

您也可以根據您的使用案例，在URL中使用此處所述的匯總索引鍵，如下所示：

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### 參考資料：轉換範本中使用的內容和函式 {#reference}

提供給範本的內容包含 `input`  （此呼叫中匯出的設定檔/資料）和 `destination` (關於Adobe要傳送資料的目的地的資料，對所有設定檔有效)。

下表提供上述範例中函式的說明。

| 函數 | 說明 |
|---------|----------|
| `input.profile` | 設定檔，表示為 [JsonNode](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). 遵循本頁上述的合作夥伴XDM結構。 |
| `destination.segmentAliases` | 從Adobe Experience Platform命名空間中的區段ID對應至合作夥伴系統中的區段別名。 |
| `destination.segmentNames` | 從Adobe Experience Platform命名空間中的區段名稱對應至合作夥伴系統中的區段名稱。 |
| `addedSegments(listOfSegments)` | 僅傳回具有狀態的區段 `realized`. |
| `removedSegments(listOfSegments)` | 僅傳回具有狀態的區段 `exited`. |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道匯出自Experience Platform的資料會如何轉換。 接下來，請閱讀以下頁面，以完成您為目的地建立訊息轉換範本的相關知識：

* [建立並測試訊息轉換範本](/help/destinations/destination-sdk/create-template.md)
* [呈現範本API操作](/help/destinations/destination-sdk/render-template-api.md)
* [支援的Destination SDK轉換函式](/help/destinations/destination-sdk/supported-functions.md)
