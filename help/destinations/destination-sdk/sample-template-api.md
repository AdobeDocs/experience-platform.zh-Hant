---
description: 此頁列出並說明了可以使用「/authoring/testing/template/sample」 API終結點執行的所有API操作，以獲取目標的test消息轉換模板。
title: 獲取示例模板API操作
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 1%

---

# 獲取示例模板API操作 {#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**API終結點**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

此頁列出並說明了可以使用 `/authoring/testing/template/sample` API終結點，用於生成 [消息轉換模板](./message-format.md#using-templating) 你的目的地。 有關此終結點支援的功能的說明，請閱讀 [建立模板](./create-template.md)。

## 示例模板API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](./getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 獲取示例模板 {#generate-sample-template}

您可以通過向Web站點發出GET請求來獲取示例模板 `authoring/testing/template/sample/` 端點，並根據建立模板的目標配置提供目標ID。

>[!TIP]
>
>* 在此應使用的目標ID是 `instanceId` 與目標配置對應，使用 `/destinations` 端點。 請參閱 [目標配置API參考](./destination-configuration-api.md#retrieve-list)。


**API格式**


```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 要為其生成消息轉換模板的目標配置的ID。 |

**要求**

以下請求生成新的示例模板，該模板由負載中提供的參數配置。

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

成功的響應返回HTTP狀態200，其中包含一個示例模板，您可以編輯該模板以匹配預期的資料格式。

如果提供的目標ID與目標配置相對應，則 [最佳工作聚合](./destination-configuration.md#best-effort-aggregation) 和 `maxUsersPerRequest=1` 在聚合策略中，請求返回與以下模板類似的示例模板：

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

如果您提供的目標ID與目標伺服器模板對應， [可配置聚合](./destination-configuration.md#configurable-aggregation) 或 [最佳工作聚合](./destination-configuration.md#best-effort-aggregation) 與 `maxUsersPerRequest` 大於1時，請求返回與此類似的示例模板：

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

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟 {#next-steps}

閱讀此文檔後，您現在知道如何使用 `/authoring/testing/template/sample` API終結點。 接下來，您可以 [呈現模板API終結點](./render-template-api.md) 根據模板生成導出的配置檔案，並將它們與目標的預期資料格式進行比較。
