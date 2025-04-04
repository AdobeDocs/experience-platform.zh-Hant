---
description: 瞭解如何使用目的地測試API為您的目的地產生測試訊息轉換範本。
title: 產生範例訊息轉換範本
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---


# 產生範例訊息轉換範本 {#get-sample-template-api-operations}

>[!IMPORTANT]
>
>**API端點**： `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

此頁面列出並描述您可以使用`/authoring/testing/template/sample` API端點執行的所有API作業，以便為您的目的地產生[訊息轉換範本](../../functionality/destination-server/message-format.md#using-templating)。 如需此端點支援的功能的說明，請閱讀[建立範本](create-template.md)。

## 範本API操作快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](../../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 取得範例範本 {#generate-sample-template}

您可以向`authoring/testing/template/sample/`端點發出GET請求，並提供目的地組態的目的地ID （您正在根據其建立範本），以取得範例範本。

>[!TIP]
>
>* 您應在此使用的目的地ID是與使用`/destinations`端點建立的目的地組態相對應的`instanceId`。 如需詳細資訊，請參閱[擷取目的地組態](../../authoring-api/destination-configuration/retrieve-destination-configuration.md)。

**API格式**

```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 您要為其產生訊息轉換範本的目的地組態ID。 |

**要求**

以下請求會產生新的範例範本，由承載中提供的引數設定。

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

成功的回應會傳回HTTP狀態200和範例範本，您可加以編輯以符合預期的資料格式。

如果您提供的目的地ID對應到彙總原則中具有[最大努力彙總](../../functionality/destination-configuration/aggregation-policy.md)與`maxUsersPerRequest=1`的目的地組態，則要求會傳回類似下列範本的範本：

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
        {#- Alternative syntax for filtering audiences by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

如果您提供的目的地ID對應到具有[可設定的彙總](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation)或[最大努力彙總](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) （具有`maxUsersPerRequest`大於一）的目的地伺服器範本，則要求會傳回類似以下的範例範本：

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
                {#- Alternative syntax for filtering audiences by status: -#}
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

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何使用`/authoring/testing/template/sample` API端點產生訊息轉換範本。 接下來，您可以使用[轉譯器範本API端點](render-template-api.md)，根據範本產生匯出的設定檔，並將它們與目的地預期的資料格式進行比較。
