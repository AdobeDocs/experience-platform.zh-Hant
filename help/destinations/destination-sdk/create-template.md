---
description: Destination SDK中包含Adobe，提供開發人員工具，協助您設定和測試目的地。 本頁面說明如何建立和測試訊息轉換範本。
title: 建立並測試訊息轉換範本
source-git-commit: cf6c6adf128ec867cd67af609a40b04d2c632bf9
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# 建立並測試訊息轉換範本 {#create-template}

## 概覽 {#overview}

Destination SDK中包含Adobe，提供開發人員工具，協助您設定和測試目的地。 本頁面說明如何建立和測試訊息轉換範本。 有關如何測試目標的資訊，請參閱[測試目標配置](./test-destination.md)。

若要在Adobe Experience Platform中的目標架構與目的地支援的訊息格式之間建立並測試訊息轉換範本&#x200B;**，請使用下文進一步說明的&#x200B;*範本製作工具*。**&#x200B;閱讀[消息格式文檔](./message-format.md#using-templating)中有關源架構和目標架構之間資料轉換的更多資訊。

下圖說明如何建立和測試訊息轉換範本，以符合Destination SDK中[目標設定工作流程](./configure-destination-instructions.md)的要求：

![建立範本步驟適用於目標配置工作流程的圖形](./assets/create-template-step.png)

## 為何需要建立和測試訊息轉換範本 {#why-create-message-transformation-template}

在目的地SDK中建立目的地的前幾個步驟之一，就是思考從Adobe Experience Platform匯出至目的地時，區段成員資格、身分和設定檔屬性的資料格式會如何轉換。 在[消息格式文檔](./message-format.md#using-templating)中查找有關AdobeXDM架構與目標架構之間轉換的資訊。

為了轉換成功，您必須提供類似以下範例的轉換範本：[建立可傳送區段、身分和設定檔屬性的範本](./message-format.md#segments-identities-attributes)。

Adobe提供的範本工具可讓您建立和測試訊息範本，將資料從AdobeXDM格式轉換為目的地支援的格式。 此工具有兩個API端點可供您使用：
* 使用&#x200B;*範本API*&#x200B;來取得範本。
* 使用&#x200B;*呈現範本API*&#x200B;來呈現範例範本，以便將結果與目的地的預期資料格式比較。 將匯出的資料與目的地預期的資料格式進行比較後，您可以編輯範本。 如此一來，您產生的匯出資料就會符合目的地預期的資料格式。

## 如何使用範例範本API和轉譯範本API，為您的目的地建立範本 {#iterative-process}

獲取和測試模板的過程是迭代的。 重複下列步驟，直到匯出的設定檔符合您目的地的預期資料格式。

1. 首先，[獲取示例模板](./create-template.md#sample-template-api)。
2. 以範例範本為起點，建立自己的草稿。
3. 使用您自己的範本呼叫[呈現範本API端點](./create-template.md#render-template-api)。 Adobe會根據您的架構產生範例設定檔，並傳回結果或遇到的任何錯誤。
4. 將匯出的資料與目的地預期的資料格式比較。 如有需要，請編輯範本。
5. 重複此程式，直到匯出的設定檔符合您目的地的預期資料格式為止。

## 建立範本之前完成的步驟 {#prerequisites}

建立範本之前，請務必完成下列步驟：

1. [建立目標伺服器配置](./destination-server-api.md)。您將產生的範本會因為`maxUsersPerRequest`參數所提供的值而有所不同。
   * 如果您想要目的地的API呼叫包含單一設定檔，以及其區段資格、身分和設定檔屬性，請使用`maxUsersPerRequest=1`。
   * 如果您想要將目的地的API呼叫包含多個設定檔，以及其區段資格、身分和設定檔屬性，請使用大於1的`maxUsersPerRequest`。
2. [建立目標](./destination-configuration-api.md#create) 配置，並在中添加目標伺服器配置的 `destinationDelivery.destinationServerId`ID。
3. [取得您剛建立之目](./destination-configuration-api.md#retrieve-list) 標設定的ID，以便在範本建立工具中使用。

## 使用範本API取得範例範本 {#sample-template-api}

>[!NOTE]
>
>如需完整的API參考檔案，請參閱[取得範本API操作範例](./sample-template-api.md)。

將目標ID新增至呼叫，如下所示，回應會傳回與目標ID對應的範本範例。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

如果您提供的目標ID與具有`maxUsersPerRequest=1`的目標伺服器範本對應，則請求會傳回與以下範本類似的範例範本：

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

如果您提供的目標ID與大於1的目標伺服器範本對應，則請求會傳回與以下範本類似的範例範本：`maxUsersPerRequest`

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

您可以使用線上字元逸出工具。 上述示範使用[JSON Escape格式化程式](https://jsonformatter.org/json-escape)。

## 呈現範本API {#render-template-api}

使用[範本API](./create-template.md#sample-template-api)範例建立訊息轉換範本後，您可以[呈現範本](./render-template-api.md)，以便根據範本產生匯出的資料。 這可讓您驗證Adobe Experience Platform將匯出至目的地的設定檔是否符合目的地的預期格式。

如需可執行之呼叫的範例，請參閱API參考：

* [呈現範本，但內文中未傳送設定檔](./render-template-api.md#multiple-profiles-no-body)
* [呈現內文中傳送設定檔的範本](./render-template-api.md#multiple-profiles-with-body)

編輯範本並呼叫轉譯範本API端點，直到匯出的設定檔符合目的地的預期資料格式為止。

## 將字元逸出範本新增至目標伺服器設定

對您的消息轉換模板感到滿意後，將其添加到`httpTemplate.requestBody.value`中的[目標伺服器配置](./server-and-template-configuration.md)中。