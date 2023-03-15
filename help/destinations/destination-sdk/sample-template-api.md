---
description: 本頁列出並說明所有可使用「/authoring/testing/template/sample」 API端點來執行的API操作，以取得目的地的測試訊息轉換範本。
title: 取得範本API操作範例
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 1%

---

# 取得範本API操作範例 {#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**API端點**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

此頁面列出並說明您可使用 `/authoring/testing/template/sample` API端點，產生 [消息轉換模板](./message-format.md#using-templating) 你的目的地。 有關此端點支援的功能的說明，請閱讀 [建立範本](./create-template.md).

## 範本API操作範例快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 取得範本範例 {#generate-sample-template}

您可以向提出GET要求，以取得範本範例 `authoring/testing/template/sample/` 端點，並根據您建立範本的目的地設定提供目的地ID。

>[!TIP]
>
>* 您應在此處使用的目的地ID為 `instanceId` 與目標設定對應，使用 `/destinations` 端點。 請參閱 [目的地設定API參考](./destination-configuration-api.md#retrieve-list).


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
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，並附上範例範本，您可以編輯該範本以符合預期的資料格式。

如果您提供的目的地ID與具有 [最佳成果匯總](./destination-configuration.md#best-effort-aggregation) 和 `maxUsersPerRequest=1` 在聚合策略中，請求返回與以下類似的示例模板：

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

如果您提供的目標ID與具有的目標伺服器範本對應 [可配置聚合](./destination-configuration.md#configurable-aggregation) 或 [最佳成果匯總](./destination-configuration.md#best-effort-aggregation) with `maxUsersPerRequest` 大於1時，要求會傳回類似以下範本的範例範本：

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

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何使用 `/authoring/testing/template/sample` API端點。 接下來，您可以使用 [呈現模板API端點](./render-template-api.md) 以根據範本產生匯出的設定檔，並與目的地的預期資料格式比較。
