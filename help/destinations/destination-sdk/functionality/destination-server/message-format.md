---
description: 本頁介紹從Adobe Experience Platform導出到目標的資料中的消息格式和配置檔案轉換。
title: 訊息格式
source-git-commit: ab87a2b7190a0365729ba7bad472fde7a489ec02
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 1%

---


# 訊息格式

## 先決條件 — Adobe Experience Platform概念 {#prerequisites}

要瞭解消息格式以及Adobe端的配置和轉換過程，請熟悉以下Experience Platform概念：

* **體驗資料模型(XDM)**。 [XDM概述](../../../../xdm/home.md) 和  [如何在Adobe Experience Platform建立XDM架構](../../../../xdm/tutorials/create-schema-ui.md)。
* **類別**. [在UI中建立和編輯類](../../../../xdm/ui/resources/classes.md)。
* **標識映射**。 標識映射表示Adobe Experience Platform所有最終用戶標識的映射。 請參閱 `xdm:identityMap` 的 [XDM欄位字典](../../../../xdm/schema/field-dictionary.md)。
* **段成員資格**。 的 [segmentMembership](../../../../xdm/schema/field-dictionary.md) XDM屬性通知配置檔案是其成員的段。 對於 `status` 欄位，閱讀 [段成員身份詳細資訊架構欄位組](../../../../xdm/field-groups/profile/segmentation.md)。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 支援的整合類型 {#supported-integration-types}

有關哪些類型的整合支援本頁所述功能的詳細資訊，請參閱下表。

| 整合類型 | 支援功能 |
|---|---|
| 即時（流）整合 | 是 |
| 基於檔案（批處理）的整合 | 是（僅下圖中的步驟1和2） |

## 總覽 {#overview}

本頁介紹從Adobe Experience Platform導出到目標的資料中的消息格式和配置檔案轉換。

Adobe Experience Platform以各種資料格式向大量目的地輸出資料。 目標類型的一些示例包括廣告平台(Google)、社交網路(Facebook)和雲儲存位置(AmazonS3、Azure事件中心)。

Experience Platform可以調整導出的配置檔案的消息格式，使其與您所在位置的預期格式相匹配。 要瞭解此自定義項，以下概念非常重要：

* Adobe Experience Platform的源(1)和目標(2)XDM架構
* 夥伴端(3)上的預期消息格式，以及
* XDM架構和預期消息格式之間的轉換層，可通過建立 [消息轉換模板](#using-templating)。

![架構到JSON轉換](../../assets/functionality/destination-server/transformations-3-steps.png)

Experience Platform使用XDM模式以一致和可重用的方式描述資料結構。

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**源XDM架構(1)**:此項目指客戶在Experience Platform中使用的架構。 在Experience Platform，在 [映射步驟](../../../ui/activate-segment-streaming-destinations.md#mapping) 在激活目標工作流中，客戶將欄位從其XDM架構映射到目標架構(2)。

**目標XDM架構(2)**:根據目標的預期格式的JSON標準架構(3)和目標可以解釋的屬性，可以在目標XDM架構中定義配置檔案屬性和標識。 可以在目標配置中執行此操作， [架構配置](../../functionality/destination-configuration/schema-configuration.md) 和 [identityNamespaces](../../functionality/destination-configuration/identity-namespace-configuration.md) 對象。

**目標配置檔案屬性的JSON標準架構(3)**:此示例表示 [JSON架構](https://json-schema.org/learn/miscellaneous-examples.html) 支援的所有配置檔案屬性及其類型(例如：對象、字串、陣列)。 目標可以支援的示例欄位 `firstName`。 `lastName`。 `gender`。 `email`。 `phone`。 `productId`。 `productName`等等。 你需要 [消息轉換模板](#using-templating) 將導出的資料裁切為Experience Platform格式。

基於上述模式轉換，下面是配置檔案配置在源XDM模式和夥伴端示例模式之間的更改方式：

![轉換消息示例](../../assets/functionality/destination-server/transformations-with-examples.png)

## 入門 — 轉換三個基本屬性 {#getting-started}

為了演示配置檔案轉換過程，以下示例在Adobe Experience Platform使用三個常用配置檔案屬性： **名字**。 **姓氏**, **電子郵件地址**。

>[!NOTE]
>
>客戶將屬性從源XDM架構映射到Adobe Experience PlatformUI中的夥伴XDM架構 **映射** 的 [激活目標工作流](../../../ui/activate-segment-streaming-destinations.md#mapping)。

假設您的平台可以接收消息格式，如：

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

考慮到消息格式，相應的轉換如下：

| 夥伴XDM架構中的Adobe | 轉換 | HTTP消息中的屬性 |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

{style="table-layout:auto"}

## Experience Platform中的輪廓結構 {#profile-structure}

要進一步瞭解該頁下面的示例，必須瞭解Experience Platform中配置檔案的結構。

配置式有3個部分：

* `segmentMembership` （始終在配置檔案中顯示）
   * 此部分包含配置檔案上存在的所有段。 段可以具有兩種狀態之一： `realized` 或 `exited`。
* `identityMap` （始終在配置檔案中顯示）
   * 此部分包含配置檔案(電子郵件、GoogleGAID、AppleIDFA等)上以及用戶在激活工作流中映射以導出的所有標識。
* 屬性（根據目標配置，這些屬性可能存在於配置檔案中）。 此外，預定義屬性和自由形式屬性之間還有一點差別：
   * 為 *自由形式屬性*，這些包含 `.value` 路徑（如果屬性在配置檔案中存在）(請參見 `lastName` 屬性)。 如果配置檔案中不存在它們，則它們將不包含 `.value` 路徑（請參見） `firstName` 屬性)。
   * 為 *預定義屬性*，這些不包含 `.value` 路徑。 配置檔案上的所有映射屬性都將出現在屬性映射中。 沒有的將不存在(請參見示例2 - `firstName` 配置檔案上不存在屬性)。

請參閱下面兩個Experience Platform中的配置檔案示例：

### 示例1 `segmentMembership`。 `identityMap` 和自由形式屬性 {#example-1}

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

### 示例2 `segmentMembership`。 `identityMap` 和預定義屬性 {#example-2}

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

## 使用模板語言進行身份、屬性和段成員身份轉換 {#using-templating}

Adobe使用 [卵石模板](https://pebbletemplates.io/)，類似於 [金賈](https://jinja.palletsprojects.com/en/2.11.x/)，將Experience PlatformXDM架構中的欄位轉換為目標支援的格式。

本節提供了如何進行這些轉換的幾個示例 — 從輸入XDM架構、通過模板，以及輸出到目標接受的負載格式。 以下示例以增加複雜性的方式呈現，如下所示：

1. 簡單的轉換示例。 瞭解模板如何與簡單轉換一起工作 [配置檔案屬性](#attributes)。 [段成員資格](#segment-membership), [身份](#identities) 的子菜單。
2. 組合上述欄位的模板的複雜性增加示例： [建立發送段和標識的模板](./message-format.md#segments-and-identities) 和 [建立發送段、標識和配置檔案屬性的模板](#segments-identities-attributes)。
3. 包含聚合鍵的模板。 使用 [可配置聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 在目標配置中，Experience Platform根據段ID、段狀態或標識命名空間等條件對導出到目標的配置檔案進行分組。

### 配置檔案屬性 {#attributes}

要轉換導出到目標的配置檔案屬性，請參閱下面的JSON和代碼示例。

>[!IMPORTANT]
>
>有關Adobe Experience Platform所有可用配置檔案屬性的清單，請參閱 [XDM欄位字典](../../../../xdm/schema/field-dictionary.md)。


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
>對於您使用的所有模板，必須轉義非法字元，如雙引號 `""` 插入 [模板](../../functionality/destination-server/templating-specs.md) 的 [目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)。 有關轉義雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)。

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

的 [segmentMembership](../../../../xdm/schema/field-dictionary.md) XDM屬性通知配置檔案是其成員的段。
對於 `status` 欄位，閱讀 [段成員身份詳細資訊架構欄位組](../../../../xdm/field-groups/profile/segmentation.md)。

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
>對於您使用的所有模板，必須轉義非法字元，如雙引號 `""` 插入 [模板](../../functionality/destination-server/templating-specs.md) 的 [目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)。 有關轉義雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)。


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

有關Experience Platform中標識的資訊，請參見 [Identity命名空間概述](../../../../identity-service/namespaces.md)。

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
>對於您使用的所有模板，必須轉義非法字元，如雙引號 `""` 插入 [模板](../../functionality/destination-server/templating-specs.md) 的 [目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)。 有關轉義雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)。

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

### 建立發送段和標識的模板 {#segments-and-identities}

本節提供了AdobeXDM架構與夥伴目標架構之間常用轉換的示例。
以下示例說明如何轉換段成員資格和標識格式並將它們輸出到目標。

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
>對於您使用的所有模板，必須轉義非法字元，如雙引號 `""` 插入 [模板](../../functionality/destination-server/templating-specs.md) 的 [目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)。 有關轉義雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)。

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

的 `json` 下面是從Adobe Experience Platform輸出的資料。

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

### 建立發送段、標識和配置檔案屬性的模板 {#segments-identities-attributes}

本節提供了AdobeXDM架構與夥伴目標架構之間常用轉換的示例。

另一個常見用例是導出包含段成員身份、標識的資料(例如：電子郵件地址、電話號碼、廣告ID)和配置檔案屬性。 要以此方式導出資料，請參見以下示例：

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
>對於您使用的所有模板，必須轉義非法字元，如雙引號 `""` 插入 [模板](../../functionality/destination-server/templating-specs.md) 的 [目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)。 有關轉義雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)。

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

的 `json` 下面是從Adobe Experience Platform輸出的資料。

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

### 在模板中包括聚合鍵以訪問按各種標準分組的導出配置檔案 {#template-aggregation-key}

使用 [可配置聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 在目標配置中，您可以根據段ID、段別名、段成員資格或標識命名空間等條件對導出到目標的配置檔案進行分組。

在消息轉換模板中，可以訪問上述聚合鍵，如以下各節的示例所示。 使用聚合鍵來構造導出為Experience Platform之外的HTTP消息，以匹配目標所期望的格式和速率限制。

#### 在模板中使用段ID聚合鍵 {#aggregation-key-segment-id}

如果您使用 [可配置聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 設定 `includeSegmentId` 若為true，則導出到目標的HTTP消息中的配置檔案將按段ID分組。 請參閱下面如何訪問模板中的段ID。

**輸入**

請考慮以下四個配置檔案，其中：

* 前兩個是段ID為段的一部分 `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* 第三個輪廓是段ID的一部分 `8f812592-3f06-416b-bd50-e7831848a31a`
* 第四輪廓是上述兩段的一部分。

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
>對於您使用的所有模板，必須轉義非法字元，如雙引號 `""` 插入 [模板](../../functionality/destination-server/templating-specs.md) 的 [目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)。 有關轉義雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)。

請注意以下方式 `audienceId` 用於訪問段ID。 此示例假定您使用 `audienceId` 用於目標分類中的段成員身份。 您可以改用任何其他欄位名，具體取決於您自己的分類。

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

導出到目標時，配置檔案會根據其段ID分成兩組。

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

#### 在模板中使用段別名聚合鍵 {#aggregation-key-segment-alias}

如果您使用 [可配置聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 設定 `includeSegmentId` 如果為true，則還可以訪問模板中的段別名。

將下面的行添加到模板以訪問按段別名分組的導出配置檔案。

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### 在模板中使用段狀態聚合鍵 {#aggregation-key-segment-status}

如果您使用 [可配置聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 設定 `includeSegmentId` 和 `includeSegmentStatus` 如果為true，則可以訪問模板中的段狀態。 這樣，您就可以根據是否應添加或從段中刪除配置檔案來對導出到目標的HTTP消息中的配置檔案進行分組。

可能的值為：

* 實現
* 現有
* 退出

將下面的行添加到模板中，以根據以上值添加或刪除段中的配置檔案：

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### 在模板中使用標識名稱空間聚合鍵 {#aggregation-key-identity}

下面是一個示例， [可配置聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 在目標配置中，設定為按標識命名空間聚合導出的配置檔案，格式為 `"namespaces": ["email", "phone"]` 和 `"namespaces": ["GAID", "IDFA"]`。 請參閱 `groups` 參數 [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md) 文檔，瞭解有關分組的詳細資訊。

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
>對於您使用的所有模板，必須轉義非法字元，如雙引號 `""` 插入 [模板](../../functionality/destination-server/templating-specs.md) 的 [目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)。 有關轉義雙引號的詳細資訊，請參閱 [JSON標準](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)。

注意 `input.aggregationKey.identityNamespaces` 在下面的模板中使用

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

導出到目標後，配置檔案將根據其標識命名空間分為兩個組。 電子郵件和電話位於一個組中，而GAID和IDFA位於另一個組中。

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

#### 在URL模板中使用聚合鍵 {#aggregation-key-url-template}

根據您的使用案例，您還可以使用URL中此處描述的聚合鍵，如下所示：

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### 參考：轉換模板中使用的上下文和函式 {#reference}

提供給模板的上下文包含 `input`  （此調用中導出的配置檔案/資料）和 `destination` (有關Adobe正在向其發送資料的目標的資料，適用於所有配置檔案)。

下表提供了上例中各函式的說明。

| 函數 | 說明 |
|---------|----------|
| `input.profile` | 配置檔案，表示為 [Json節點](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html)。 按照本頁上進一步提到的合作夥伴XDM架構。 |
| `destination.segmentAliases` | 從Adobe Experience Platform命名空間中的段ID映射到夥伴系統中的段別名。 |
| `destination.segmentNames` | 從Adobe Experience Platform命名空間中的段名稱映射到合作夥伴系統中的段名稱。 |
| `addedSegments(listOfSegments)` | 僅返回具有狀態的段 `realized`。 |
| `removedSegments(listOfSegments)` | 僅返回具有狀態的段 `exited`。 |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

讀取此文檔後，您現在知道從Experience Platform導出的資料是如何轉換的。 接下來，閱讀以下頁面，以完成有關為目標建立消息轉換模板的知識：

* [建立和test消息轉換模板](../../testing-api/streaming-destinations/create-template.md)
* [呈現模板API操作](../../testing-api/streaming-destinations/render-template-api.md)
* [支援的轉換函式在Destination SDK](../destination-server/supported-functions.md)

要瞭解有關其他目標伺服器元件的詳細資訊，請參閱以下文章：

* [使用Destination SDK建立的目標的伺服器規格](server-specs.md)
* [模板規格](templating-specs.md)
* [檔案格式配置](file-formatting.md)