---
description: 本頁提供您提交以審核使用Destination SDK製作的已產品化目標所需的所有資訊。
title: 提交以審閱在Destination SDK中創作的已產品化目標
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: e68ae7d1cb87d078d9fce5a5df501cc6ce944403
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# 提交以審閱在Destination SDK中創作的已產品化目標

## 總覽 {#overview}

>[!IMPORTANT]
>
>* 此處記錄的流程僅對提交產品化（公開）目的地的合作夥伴是必需的。 如果您要建立私人目的地供自己使用，則不需要製作這些材料並與Adobe共用。
>
>* Adobe檢閱目標發佈請求的標準回應時間為五個工作天。
>
>* 如果Adobe團隊在您初次提交後要求您對設定進行任何更新，您必須在您進行更新後提交另一個目標發佈請求。
>
>* 即使您的目的地在Experience Platform目錄中上線，如果您需要對設定進行任何更新，也必須提交新的目的地發佈請求，以便更新反映在設定中。


將您的目的地發佈至 [Experience Platform目的地目錄](/help/destinations/catalog/overview.md)，您必須向Adobe提供關於您所執行之目的地和測試的特定資訊，以確保使用者在將資料啟動至您的平台時，能享受盡可能最佳的體驗。

此頁面列出您在提交或更新使用Adobe Experience Platform Destination SDK製作的目的地時需要提供的所有資訊。 若要在Adobe Experience Platform中成功提交目的地，請傳送電子郵件至 <aepdestsdk@adobe.com> 包括：

* 目的地解決的使用案例說明。 如果要更新現有的目標配置，則不需要此操作。
* 使用測試目的地API端點對您的目的地執行HTTP呼叫後的測試結果。 請與Adobe共用：
   * 對您的目的地端點發出API呼叫。
   * 從目的地端點收到的API回應。
* 證明您已使用 [目的地發佈API](./destination-publish-api.md).
* 說明檔案PR（提取請求），請遵循 [自助服務檔案程式](./docs-framework/documentation-instructions.md).
* 影像檔案，會在Experience Platform目的地目錄中顯示為目的地卡的標誌。

您可以在以下各節中找到有關每個項目的詳細資訊：

## 使用案例說明

提供目的地為Experience Platform客戶解決的使用案例說明。 您的說明可類似於現有合作夥伴的使用案例：

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md):從您的客戶清單、造訪過您網站的人員或已在Pinterest上與您的內容互動的人員建立對象。
* [Yahoo資料X](/help/destinations/catalog/advertising/datax.md#use-cases):廣告商若想鎖定在Verizon Media(VMG)中輸入電子郵件地址的特定對象群組，可使用VMG的近乎即時API快速建立新區段，並推送所需的對象群組，即可使用DataX API。

## 使用測試目的地API後的測試結果

使用 [測試目的地API](./test-destination.md) 端點，對您的目的地執行HTTP呼叫。 其中包括:

* 使用測試API向目的地端點提出的完整API請求（標題和內文）。
* 從目的地端點收到的API回應。

例如，您的請求和回應可能如下所示：

**要求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**回應**

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

## 已提交目標發佈請求的證明

成功測試目的地後，您必須使用 [目的地發佈API](./destination-publish-api.md) 提交目的地給Adobe以供審核和發佈。

提供目的地的發佈請求ID。 如需如何擷取發佈請求ID的相關資訊，請參閱 [列出目標發佈請求](./destination-publish-api.md#retrieve-list).

## 產品化整合的目的地檔案PR（提取要求）

如果您是獨立軟體供應商(ISV)或系統整合商(SI)，則建立 [產品化整合](./overview.md#productized-custom-integrations)，請使用 [自助服務檔案程式](./docs-framework/documentation-instructions.md) 為目的地建立產品檔案頁面的方式。 在提交程式中，請提供目的地檔案的提取請求(PR)。

## 目的地標誌 {#logo}

目的地目錄包含每個目的地卡的標誌。 在您的提交電子郵件中，加入含有目的地標誌的影像。

影像需求為：
* **格式**: `SVG`
* **大小**:小於2 MB

## 下載範例電子郵件

[下載](./assets/sample-email-submit-destination.rtf) 範例電子郵件，內含您需要提供給Adobe的所有資訊。
