---
description: 本頁列出並說明了所有可使用「/authoring/testing/template/sample」 API端點來執行的API操作，以取得目的地的測試訊息轉換範本。
title: 取得範本API操作範例
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: 2ed132cd16db64b5921c5632445956f750fead56
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---

# 獲取範本API操作示例{#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**API端點**:  `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

本頁列出並說明了所有可使用`/authoring/testing/template/sample` API端點執行的API操作，以為目標生成[消息轉換模板](./message-format.md#using-templating)。 有關此終結點支援的功能的說明，請閱讀[create template](./create-template.md)。

## 範本API操作範例快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](./getting-started.md)，以取得成功呼叫API所需的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 取得範本範例 {#generate-sample-template}

您可以向`authoring/testing/template/sample/`端點提出GET請求，並根據您建立範本的目的地配置提供目的地ID，從而獲取範例範本。

>[!TIP]
>
>* 您應在此處使用的目標ID是與使用`/destinations`端點建立的目標配置對應的`instanceId`。 請參閱[目標配置API參考](./destination-configuration-api.md#retrieve-list)。


**API格式**


```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 要為其生成消息轉換模板的目標配置的ID。 |

**要求**

下列要求會產生新的範例範本，由裝載中提供的參數所設定。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，並附上範例範本，您可以編輯該範本以符合預期的資料格式。

如果您提供的目標ID與聚合策略中具有[盡力聚合](./destination-configuration.md#best-effort-aggregation)和`maxUsersPerRequest=1`的目標配置相對應，則請求將返回與以下類似的示例模板：

```python
{#- THIS is an example template for a single profile -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "identities": [
    {%- for idMapEntry in input.profile.identityMap -%}
    {%- set namespace = idMapEntry.key -%}
        {%- for identity in idMapEntry.value %}
        {
            "type": "{{ namespace }}",
            "id": "{{ identity.id }}"
        }{%- if not loop.last -%},{%- endif -%}
        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
        {%- for segment in input.profile.segmentMembership.ups | added %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ],
        "remove": [
        {#- Alternative syntax for filtering segments by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

如果您提供的目標ID與具有[可配置聚合](./destination-configuration.md#configurable-aggregation)或[最佳工作聚合](./destination-configuration.md#best-effort-aggregation)且`maxUsersPerRequest`大於1的目標伺服器模板相對應，則請求將返回與以下類似的示例模板：

```python
{#- THIS is an example template for multiple profiles -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "profiles": [
    {%- for profile in input.profiles %}
        {
            "identities": [
            {%- for idMapEntry in profile.identityMap -%}
            {%- set namespace = idMapEntry.key -%}
                {%- for identity in idMapEntry.value %}
                {
                    "type": "{{ namespace }}",
                    "id": "{{ identity.id }}"
                }{%- if not loop.last -%},{%- endif -%}
                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
            {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {%- for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ],
                "remove": [
                {#- Alternative syntax for filtering segments by status: -#}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ]
            }
        }{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ]
}
```

## API錯誤處理 {#api-error-handling}

目標SDK API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱平台疑難排解指南中的[API狀態代碼](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes)和[要求標題錯誤](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何使用`/authoring/testing/template/sample` API端點產生訊息轉換範本。 接下來，您可以使用[呈現範本API端點](./render-template-api.md)來根據範本產生匯出的設定檔，並與目的地的預期資料格式比較。
