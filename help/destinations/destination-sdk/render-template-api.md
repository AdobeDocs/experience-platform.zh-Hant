---
description: 本頁列出並說明了您可使用「/authoring/testing/template/render」 API端點來執行的所有API操作，以便根據您的訊息轉換範本，呈現目的地的匯出資料。
title: 呈現範本API操作
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 1%

---

# 呈現範本API操作 {#render-template-api-operations}

>[!IMPORTANT]
>
>**API端點**:  `https://platform.adobe.io/data/core/activation/authoring/testing/template/render`

本頁列出並說明了所有可使用`/authoring/testing/template/render` API端點執行的API操作，以根據您的[訊息轉換範本](./message-format.md#using-templating)呈現目的地的匯出資料。 有關此終結點支援的功能的說明，請閱讀[create template](./create-template.md)。

## 演算範本API作業快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](./getting-started.md)，以取得成功呼叫API所需的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 根據模板呈現導出的資料 {#render-exported-data}

您可以向`authoring/testing/template/render`端點提出POST請求，並提供目標配置的目標ID以及使用[示例模板API端點](./sample-template-api.md)建立的模板，以呈現導出的資料。

>[!TIP]
>
>* 您應在此處使用的目標ID是與使用`/destinations`端點建立的目標配置對應的`instanceId`。 請參閱[目標配置API參考](./destination-configuration-api.md#retrieve-list)。



**API格式**


```http
POST authoring/testing/template/render
```

| 參數 | 說明 |
| -------- | ----------- |
| `destinationId` | 要為其呈現導出資料的目標配置的ID。 |
| `template` | 根據要呈現導出資料的模板的字元逸出版本。 |
| `profiles` | 如果您想要將設定檔新增至呼叫的內文，可以使用[範例設定檔產生API](./sample-profile-generation-api.md)來產生一些設定檔。 |


您可以呈現匯出的資料，如下列範例所示：

* [呈現範本，但內文中未傳送設定檔](./render-template-api.md#multiple-profiles-no-body)
* [呈現內文中傳送設定檔的範本](./render-template-api.md#multiple-profiles-with-body)

<!--

### Render a template for single profile, no profiles sent in body {#single-profile-no-body}

**Request**

The following request renders sample profiles that match the format expected by your destination.

```shell

curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
    "destinationId": "a9fb4f0f-3983-4756-b756-00cf25fe5a35",
    "template": "{# THIS is an example template for a single profile #}\r\n{\r\n    \"identities\": [\r\n        {% for email in input.profile.identityMap.email %}\r\n            {\r\n                \"type\": \"email\",\r\n                \"id\": \"{{ email.id }}\"\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n\r\n        {# Add a comma only if we have both emails and external_ids. #}\r\n        {% if input.profile.identityMap.email is not empty and input.profile.identityMap.external_id is not empty %}\r\n            ,\r\n        {% endif %}\r\n\r\n        {% for external in input.profile.identityMap.external_id %}\r\n            {\r\n                \"type\": \"external_id\",\r\n                \"id\": \"{{ external.id }}\"\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n            {% for segment in input.profile.segmentMembership.ups | added %}\r\n                \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n            {% endfor %}\r\n        ],\r\n        \"remove\": [\r\n            {# Alternative syntax for filtering segments by status: #}\r\n            {% for segment in removedSegments(input.profile.segmentMembership.ups) %}\r\n                \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n            {% endfor %}\r\n        ]\r\n    }\r\n}"
}'

```

**Response**

The response returns the result of rendering the template, or any errors encountered.
A successful response returns HTTP status 200 with details of the exported data.
An unsuccessful response returns HTTP status 500 along with descriptions of the encountered errors.

```json

{
    "identities": [
        {
            "type": "email",
            "id": "email_lc_sha256-cBltJ"
        },
        {
            "type": "external_id",
            "id": "extern_id-cP732"
        }
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
            "segmentid1",
            "segmentid2"
        ],
        "remove": [
            "segmentid3"
        ]
    }
}

```

### Render a template for single profile, with profiles sent in body {#single-profile-with-body}

**Request**

The following request renders a profile that matches the format expected by your destination. You can generate profiles to send on the call by using the [sample profile generation API](./sample-profile-generation-api.md).

```shell

curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
    "destinationId": "a9fb4f0f-3983-4756-b756-00cf25fe5a35",
    "template": "{# THIS is an example template for a single profile #}\r\n{\r\n    \"identities\": [\r\n        {% for email in input.profile.identityMap.email %}\r\n            {\r\n                \"type\": \"email\",\r\n                \"id\": \"{{ email.id }}\"\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n\r\n        {# Add a comma only if we have both emails and external_ids. #}\r\n        {% if input.profile.identityMap.email is not empty and input.profile.identityMap.external_id is not empty %}\r\n            ,\r\n        {% endif %}\r\n\r\n        {% for external in input.profile.identityMap.external_id %}\r\n            {\r\n                \"type\": \"external_id\",\r\n                \"id\": \"{{ external.id }}\"\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n            {% for segment in input.profile.segmentMembership.ups | added %}\r\n                \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n            {% endfor %}\r\n        ],\r\n        \"remove\": [\r\n            {# Alternative syntax for filtering segments by status: #}\r\n            {% for segment in removedSegments(input.profile.segmentMembership.ups) %}\r\n                \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n            {% endfor %}\r\n        ]\r\n    }\r\n}",
    "profiles": [
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-17T11:49:06.626238Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-17T11:49:06.626240Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-17T11:49:06.626240Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-c3fjU"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-VNq0z"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-HATAl"
                }
            ],
            "external_id": [
                {
                    "id": "extern_id-cP732"
                }
            ],
            "email": [
                {
                    "id": "email_lc_sha256-cBltJ"
                }
            ]
        }
    }
    ]
}'

```

**Response**

A successful response returns HTTP status 200 with details of the exported data.

```json

{
    "identities": [
        {
            "type": "email",
            "id": "email_lc_sha256-cBltJ"
        },
        {
            "type": "external_id",
            "id": "extern_id-cP732"
        }
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
            "segmentid1",
            "segmentid2"
        ],
        "remove": [
            "segmentid3"
        ]
    }
}

```

-->

### 呈現範本，但內文中未傳送設定檔 {#multiple-profiles-no-body}

**要求**

下列要求會轉譯多個範例設定檔，這些設定檔符合目的地預期的格式。

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
   "destinationId":"{DESTINATION_ID}",
   "template":"{# THIS is an example template for multiple profiles #}\r\n{\r\n    \"profiles\": [\r\n        {% for profile in input.profiles %}\r\n            {\r\n                \"identities\": [\r\n                    {% for email in profile.identityMap.email %}\r\n                        {\r\n                            \"type\": \"email\",\r\n                            \"id\": \"{{ email.id }}\"\r\n                        }{% if not loop.last %},{% endif %}\r\n                    {% endfor %}\r\n\r\n                    {# Add a comma only if we have both emails and external_ids. #}\r\n                    {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}\r\n                        ,\r\n                    {% endif %}\r\n\r\n                    {% for external in profile.identityMap.external_id %}\r\n                        {\r\n                            \"type\": \"external_id\",\r\n                            \"id\": \"{{ external.id }}\"\r\n                        }{% if not loop.last %},{% endif %}\r\n                    {% endfor %}\r\n                ],\r\n                \"AdobeExperiencePlatformSegments\": {\r\n                    \"add\": [\r\n                        {% for segment in profile.segmentMembership.ups | added %}\r\n                            \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n                        {% endfor %}\r\n                    ],\r\n                    \"remove\": [\r\n                        {# Alternative syntax for filtering segments by status: #}\r\n                        {% for segment in removedSegments(profile.segmentMembership.ups) %}\r\n                            \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n                        {% endfor %}\r\n                    ]\r\n                }\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n    ]\r\n}",
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "segmentid1":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870859Z",
                  "status":"existing"
               },
               "segmentid3":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870860Z",
                  "status":"exited"
               },
               "segmentid2":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870860Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "email":[
               {
                  "id":"Email-gq3zZ"
               }
            ],
            "external_id":[
               {
                  "id":"external_id"
               }
            ]
         }
      }
   ]
}'
```

**回應**

回應會傳回轉譯範本的結果，或遇到的任何錯誤。
成功的回應會傳回HTTP狀態200，並包含匯出資料的詳細資訊。
失敗的回應會傳回HTTP狀態500，並傳回所遇到錯誤的說明。

```json
{
   "profiles":[
      {
         "identities":[
            
         ],
         "AdobeExperiencePlatformSegments":{
            "add":[
               "segmentid1",
               "segmentid2"
            ],
            "remove":[
               "segmentid3"
            ]
         }
      },
      {
         "identities":[
            
         ],
         "AdobeExperiencePlatformSegments":{
            "add":[
               "segmentid1",
               "segmentid2"
            ],
            "remove":[
               "segmentid3"
            ]
         }
      },
      {
         "identities":[
            
         ],
         "AdobeExperiencePlatformSegments":{
            "add":[
               "segmentid1",
               "segmentid2"
            ],
            "remove":[
               "segmentid3"
            ]
         }
      }
   ]
}       
```

### 呈現內文中傳送設定檔的範本 {#multiple-profiles-with-body}

**要求**

下列要求會呈現符合目的地預期格式的範例設定檔。 您可以使用[範例設定檔產生API](./sample-profile-generation-api.md)產生要在呼叫時傳送的設定檔。

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
   "destinationId":"{DESTINATION_ID}",
   "template":"{# THIS is an example template for multiple profiles #}\r\n{\r\n    \"profiles\": [\r\n        {% for profile in input.profiles %}\r\n            {\r\n                \"identities\": [\r\n                    {% for email in profile.identityMap.email %}\r\n                        {\r\n                            \"type\": \"email\",\r\n                            \"id\": \"{{ email.id }}\"\r\n                        }{% if not loop.last %},{% endif %}\r\n                    {% endfor %}\r\n\r\n                    {# Add a comma only if we have both emails and external_ids. #}\r\n                    {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}\r\n                        ,\r\n                    {% endif %}\r\n\r\n                    {% for external in profile.identityMap.external_id %}\r\n                        {\r\n                            \"type\": \"external_id\",\r\n                            \"id\": \"{{ external.id }}\"\r\n                        }{% if not loop.last %},{% endif %}\r\n                    {% endfor %}\r\n                ],\r\n                \"AdobeExperiencePlatformSegments\": {\r\n                    \"add\": [\r\n                        {% for segment in profile.segmentMembership.ups | added %}\r\n                            \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n                        {% endfor %}\r\n                    ],\r\n                    \"remove\": [\r\n                        {# Alternative syntax for filtering segments by status: #}\r\n                        {% for segment in removedSegments(profile.segmentMembership.ups) %}\r\n                            \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n                        {% endfor %}\r\n                    ]\r\n                }\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n    ]\r\n}",
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "segmentid1":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870859Z",
                  "status":"existing"
               },
               "segmentid3":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870860Z",
                  "status":"exited"
               },
               "segmentid2":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870860Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "email":[
               {
                  "id":"Email-gq3zZ"
               }
            ],
            "external_id":[
               {
                  "id":"external_id"
               }
            ]
         }
      }
   ]
}'
```

**回應**

回應會傳回轉譯範本的結果，或遇到的任何錯誤。
成功的回應會傳回HTTP狀態200，並包含匯出資料的詳細資訊。
失敗的回應會傳回HTTP狀態500，並傳回所遇到錯誤的說明。

```json
{
   "profiles":[
      {
         "identities":[
            {
               "type":"email",
               "id":"Email-gq3zZ"
            },
            {
               "type":"external_id",
               "id":"external_id"
            }
         ],
         "AdobeExperiencePlatformSegments":{
            "add":[
               "segmentid1",
               "segmentid2"
            ],
            "remove":[
               "segmentid3"
            ]
         }
      }
   ]
}
```

## API錯誤處理 {#api-error-handling}

目標SDK API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱平台疑難排解指南中的[API狀態代碼](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes)和[要求標題錯誤](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何使用訊息轉換範本，產生符合目的地預期資料格式的匯出設定檔。 請參閱[如何使用目標SDK來設定目標](./configure-destination-instructions.md) ，了解此步驟在設定目標程式中的適用位置。