---
description: 作為Destination SDK的一部分，Adobe提供開發人員工具，協助您設定和測試目的地。 本頁面說明如何建立和測試訊息轉換範本。
title: 建立並測試訊息轉換範本
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# 建立並測試訊息轉換範本 {#create-template}

## 總覽 {#overview}

作為Destination SDK的一部分，Adobe提供開發人員工具，協助您設定和測試目的地。 本頁面說明如何建立和測試訊息轉換範本。 如需如何測試目的地的詳細資訊，請參閱 [測試您的目標配置](./test-destination.md).

結束日期 **建立和測試消息轉換模板** 在Adobe Experience Platform中的目標結構與目的地支援的訊息格式之間，請使用 *範本製作工具* 下文進一步說明。  在 [消息格式文檔](./message-format.md#using-templating).

下圖說明如何建立和測試訊息轉換範本 [目標配置工作流](./configure-destination-instructions.md) 在Destination SDK中：

![建立範本步驟適用於目標配置工作流程的圖形](./assets/create-template-step.png)

## 為何需要建立和測試訊息轉換範本 {#why-create-message-transformation-template}

在Destination SDK中建立目的地的前幾個步驟之一，是思考從Adobe Experience Platform匯出至目的地時，區段成員資格、身分和設定檔屬性的資料格式會如何轉換。 如需AdobeXDM架構與目標架構之間轉換的相關資訊，請參閱 [消息格式文檔](./message-format.md#using-templating).

為了轉換成功，您必須提供類似以下範例的轉換範本： [建立可傳送區段、身分和設定檔屬性的範本](./message-format.md#segments-identities-attributes).

Adobe提供的範本工具可讓您建立和測試訊息範本，將資料從AdobeXDM格式轉換為目的地支援的格式。 此工具有兩個API端點可供您使用：
* 使用 *範本API範例* 來取得範本。
* 使用 *呈現範本API* 呈現範例範本，以便將結果與目的地的預期資料格式比較。 將匯出的資料與目的地預期的資料格式進行比較後，您可以編輯範本。 如此一來，您產生的匯出資料就會符合目的地預期的資料格式。

## 建立範本之前完成的步驟 {#prerequisites}

建立範本之前，請務必完成下列步驟：

1. [建立目標伺服器配置](./destination-server-api.md). 您將產生的範本會因為 `maxUsersPerRequest` 參數。
   * 使用 `maxUsersPerRequest=1` 如果您希望目的地的API呼叫包含單一設定檔，以及其區段資格、身分和設定檔屬性。
   * 使用 `maxUsersPerRequest` 值大於1的值。如果您想要目的地的API呼叫包含多個設定檔，以及其區段資格、身分和設定檔屬性。
2. [建立目標配置](./destination-configuration-api.md#create) 和新增目標伺服器設定的ID至 `destinationDelivery.destinationServerId`.
3. [取得目標設定的ID](./destination-configuration-api.md#retrieve-list) ，以便在範本建立工具中使用。
4. 了解 [您可以使用哪些函式和篩選器](./supported-functions.md) 在消息轉換模板中。

## 如何使用範例範本API和轉譯範本API，為您的目的地建立範本 {#iterative-process}

>[!TIP]
>
>在建立和編輯您的郵件轉換模板之前，您可以先呼叫 [呈現模板API端點](./render-template-api.md#render-exported-data) 簡單範本，可匯出原始設定檔而不套用任何轉換。 簡單範本的語法為： <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

獲取和測試模板的過程是迭代的。 重複下列步驟，直到匯出的設定檔符合您目的地的預期資料格式。

1. 首先， [取得範本](./create-template.md#sample-template-api).
2. 以範例範本為起點，建立自己的草稿。
3. 呼叫 [呈現模板API端點](./create-template.md#render-template-api) 使用您自己的範本。 Adobe會根據您的架構產生範例設定檔，並傳回結果或遇到的任何錯誤。
4. 將匯出的資料與目的地預期的資料格式比較。 如有需要，請編輯範本。
5. 重複此程式，直到匯出的設定檔符合您目的地的預期資料格式為止。

## 使用範本API取得範例範本 {#sample-template-api}

>[!NOTE]
>
>如需完整的API參考檔案，請參閱 [取得範本API操作範例](./sample-template-api.md).

將目標ID新增至呼叫，如下所示，回應會傳回與目標ID對應的範本範例。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

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

## 字元逸出範本 {#character-escape-template}

使用範本來呈現符合目的地預期格式的設定檔之前，您必須以字元逸出範本，如下方的畫面記錄所示。

![說明如何使用線上字元逸出工具來逸出範本的影片](./assets/escape-characters.gif)

您可以使用線上字元逸出工具。 上述示範使用 [JSON逸出格式](https://jsonformatter.org/json-escape).

## 呈現範本API {#render-template-api}

使用 [範本API範例](./create-template.md#sample-template-api)，您可以 [呈現範本](./render-template-api.md) 以便根據其生成導出資料。 這可讓您驗證Adobe Experience Platform將匯出至目的地的設定檔是否符合目的地的預期格式。

如需可執行之呼叫的範例，請參閱API參考：

* [呈現範本，但內文中未傳送設定檔](./render-template-api.md#multiple-profiles-no-body)
* [呈現內文中傳送設定檔的範本](./render-template-api.md#multiple-profiles-with-body)

編輯範本並呼叫轉譯範本API端點，直到匯出的設定檔符合目的地的預期資料格式為止。

## 將字元逸出範本新增至目標伺服器設定

對您的訊息轉換範本感到滿意後，請將其新增至 [目標伺服器配置](./server-and-template-configuration.md)，在 `httpTemplate.requestBody.value`.
