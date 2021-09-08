---
description: 將本頁的內容與合作夥伴目的地的其他設定選項搭配使用。 本頁說明從Adobe Experience Platform匯出至目的地之資料的傳訊格式，而其他頁面則說明連線及驗證至目的地的詳細資訊。
seo-description: Use the content on this page together with the rest of the configuration options for partner destinations. This page addresses the messaging format of data exported from Adobe Experience Platform to destinations, while the other page addresses specifics about connecting and authenticating to your destination.
seo-title: Message format
title: 訊息格式
source-git-commit: d60933d2083b7befcfa8beba4b1630f372c08cfa
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 3%

---

# 訊息格式

## 必要條件 — Adobe Experience Platform概念 {#prerequisites}

若要了解Adobe端的程式，請熟悉下列Experience Platform概念：

* **Experience Data Model(XDM)**。[XDM概](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant) 述及  [如何在Adobe Experience Platform中建立XDM結構](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en)。
* **類別**。[在UI中建立和編輯類](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en)。
* **欄位群組**。[欄位群組](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#field-group) 定義， [以及欄位群組的詳細資訊](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#field-group)。
* **IdentityMap**。身分對應代表Adobe Experience Platform中所有一般使用者身分的對應。 請參閱[XDM欄位字典](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en)中的`xdm:identityMap`。
* **區段成員資格**。[segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM屬性會通知設定檔是哪些區段的成員。 對於`status`欄位中的三個不同值，請閱讀[區段成員資格詳細資訊架構欄位群組](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html)上的檔案。

## 概覽 {#overview}

將此頁面上的內容與合作夥伴目標](./configuration-options.md)的其餘[配置選項一起使用。 本頁說明從Adobe Experience Platform匯出至目的地之資料的傳訊格式，而其他頁面則說明連線及驗證至目的地的詳細資訊。

Adobe Experience Platform會以各種資料格式將資料匯出至大量目的地。 目的地類型的一些範例包括廣告平台(Google)、社交網路(Facebook)、雲端儲存位置(Amazon S3、Azure事件中心)。

Experience Platform可調整匯出的訊息格式，以符合您旁邊的預期格式。 若要了解此自訂，下列概念非常重要：
* Adobe Experience Platform中的來源(1)和目標(2)XDM結構
* 合作夥伴端(3)的訊息格式，以及
* 兩個之間的轉換層，可通過建立[消息轉換模板](./message-format.md#using-templating)來定義。

![結構轉換為JSON](./assets/transformations-3-steps.png)

Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。

想要將資料啟用至您目的地的使用者，必須將其Experience Platform中資料集所使用的欄位，對應至將轉譯為您目的地預期格式的結構。 Adobe會為您的公司建立自訂欄位群組，以新增至目標結構。 欄位群組中的欄位取決於您可接收的設定檔屬性欄位。

**源XDM架構(1)**:這是指客戶在Experience Platform中使用的結構。在Experience Platform中，在啟動目標工作流的[映射步驟](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping)中，客戶將從其源架構將欄位映射到目標的目標架構(2)。

**Target XDM結構(2)**:根據您與Adobe共用的JSON標準結構(3),Adobe的團隊將為您的目的地建立自訂結構。請注意，在專案](./overview.md#phased-approach)的未來階段中，您將能自行建立目的地的自訂架構。[

**目的地設定檔屬性的JSON標準結構(3)**:請與我們共用您 [的](https://json-schema.org/learn/miscellaneous-examples.html) 平台支援的所有設定檔屬性及其類型的JSON結構(例如：物件、字串、陣列)。目標可支援的範例欄位可以是`firstName`、`lastName`、`gender`、`email`、`phone`、`productId`、`productName`等。

根據上述架構轉換，以下說明來源XDM架構與合作夥伴端範例架構之間訊息結構的變更方式：

![轉換消息示例](./assets/transformations-with-examples.png)

<br>


## 快速入門 — 轉換三個基本屬性 {#getting-started}

為了示範轉換程式，下列範例在Adobe Experience Platform中使用三個常見的設定檔屬性：**名字**、**姓氏**&#x200B;和&#x200B;**電子郵件地址**。

>[!NOTE]
>
>客戶將屬性從來源XDM結構對應至Adobe Experience Platform UI中&#x200B;**啟動目標工作流程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate-destinations.html#mapping)之[對應**&#x200B;步驟的合作夥伴XDM結構。

假設您的平台可接收如下的訊息格式：

```curl
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

## 使用範本語言進行身分、屬性和區段成員資格轉換 {#using-templating}

Adobe使用類似[Jinja](https://jinja.palletsprojects.com/en/2.11.x/)的範本語言，將XDM結構的欄位轉換為目的地支援的格式。

本節提供幾個範例，說明如何從輸入XDM架構、透過範本進行這些轉換，以及將輸出為目的地接受的裝載格式。 以下範例依複雜度增加排序，如下所示：

1. 簡單的轉換範例。 了解模板如何處理[配置檔案屬性](./message-format.md#attributes)、[段成員資格](./message-format.md#segment-membership)和[標識](./message-format.md#identities)欄位的簡單轉換。
2. 結合上述欄位的範本，其複雜度增加範例：[建立傳送區段和身分的範本](./message-format.md#segments-and-identities)及[建立傳送區段、身分和設定檔屬性的範本](./message-format.md#segments-identities-attributes)。
3. 深入探討，展示產業合作夥伴的兩個範本範例。

### 設定檔屬性 {#attributes}

若要轉換匯出至目的地的設定檔屬性，請參閱下方的JSON和程式碼範例。


>[!IMPORTANT]
>
>如需Adobe Experience Platform中所有可用設定檔屬性的清單，請參閱[XDM欄位字典](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en)。



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
>對於您使用的所有模板，在[目標伺服器配置](./server-and-template-configuration.md#template-specs)中插入模板之前，必須先逸出非法字元，如雙引號`""`。 如需逸出雙引號的詳細資訊，請參閱[JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)中的第9章。

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

[segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM屬性會通知設定檔是哪些區段的成員。
對於`status`欄位中的三個不同值，請閱讀[區段成員資格詳細資訊架構欄位群組](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html)上的檔案。

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
        "status": "existing"
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
        "status": "existing"
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
>對於您使用的所有模板，在[目標伺服器配置](./server-and-template-configuration.md#template-specs)中插入模板之前，必須先逸出非法字元，如雙引號`""`。 如需逸出雙引號的詳細資訊，請參閱[JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)中的第9章。

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

如需Experience Platform中身分的相關資訊，請參閱[身分命名空間概述](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)。

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
>對於您使用的所有模板，在[目標伺服器配置](./server-and-template-configuration.md#template-specs)中插入模板之前，必須先逸出非法字元，如雙引號`""`。 如需逸出雙引號的詳細資訊，請參閱[JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)中的第9章。

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
              "status": "existing"
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
>對於您使用的所有模板，在[目標伺服器配置](./server-and-template-configuration.md#template-specs)中插入模板之前，必須先逸出非法字元，如雙引號`""`。 如需逸出雙引號的詳細資訊，請參閱[JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)中的第9章。

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

以下`json`代表從Adobe Experience Platform匯出的資料。

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
              "status": "existing"
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
>對於您使用的所有模板，在[目標伺服器配置](./server-and-template-configuration.md#template-specs)中插入模板之前，必須先逸出非法字元，如雙引號`""`。 如需逸出雙引號的詳細資訊，請參閱[JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)中的第9章。

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

以下`json`代表從Adobe Experience Platform匯出的資料。

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

### 參考資料：轉換範本中使用的內容和函式

提供給範本的內容包含`input`（此呼叫中匯出的設定檔/資料）和`destination`(關於Adobe正將資料傳送至哪個目的地的資料，對所有設定檔有效)。

下表提供上述範例中函式的說明。

| 函數 | 說明 |
|---------|----------|
| `input.profile` | 描述檔，以[JsonNode](http://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html)表示。 遵循本頁上述的合作夥伴XDM結構。 |
| `destination.segmentAliases` | 從Adobe Experience Platform命名空間中的區段ID對應至合作夥伴系統中的區段別名。 |
| `destination.segmentNames` | 從Adobe Experience Platform命名空間中的區段名稱對應至合作夥伴系統中的區段名稱。 |
| `addedSegments(listOfSegments)` | 僅傳回狀態為`realized`或`existing`的區段。 |
| `removedSegments(listOfSegments)` | 僅傳回狀態`exited`的區段。 |

<!--

## What Adobe needs from you to set up your destination {#what-adobe-needs}

Based on the transformations outlined in the sections above, Adobe needs the following information to set up your destination:

* Considering *all* the fields that your platform can receive, Adobe needs the standard JSON schema that corresponds to your expected message format. Having the template allows Adobe to define transformations and to create a custom XDM schema for your company, which customers would use to export data to your destination.

-->
