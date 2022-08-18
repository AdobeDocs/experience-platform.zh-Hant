---
description: 此頁提供您需要提交的所有資訊，以便複查使用Destination SDK創作的已生產化目標。
title: 提交以審閱在Destination SDK中創作的已生產化目標
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 50f205a5ddd9ec264d7390911fef45dc595ca6a1
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# 提交以審閱在Destination SDK中創作的已生產化目標

## 總覽 {#overview}

>[!IMPORTANT]
>
>* 此處記錄的流程僅對提交已生產化（公共）目標的合作夥伴是必需的。 如果您正在建立專用目標供您自用，則無需製作這些材料並與Adobe共用。
>
>* Adobe審查目標發佈請求的標準響應時間為5個工作日。
>
>* 如果Adobe團隊要求您在初次提交後對配置進行任何更新，則必須在您進行更新後提交另一個目標發佈請求。
>
>* 即使目標在Experience Platform目錄中生存後，如果您需要對配置進行任何更新，則必須提交新的目標發佈請求，以便更新反映在配置中。


在將目標發佈到 [Experience Platform目標目錄](/help/destinations/catalog/overview.md)，您必須向Adobe提供有關目標和您執行的測試的特定資訊，以確保用戶在將資料激活到您的平台時享受盡可能最好的體驗。

此頁列出了提交或更新您使用Adobe Experience Platform Destination SDK創作的目標時需要提供的所有資訊。 要成功提交Adobe Experience Platform的目標，請發送電子郵件至 <aepdestsdk@adobe.com> 包括：

* 目標解決的使用案例的說明。 如果要更新現有目標配置，則不需要這樣做。
* Test使用test目標API終結點對目標執行HTTP調用後的結果。 請與Adobe共用：
   * 對目標終結點進行的API調用。
   * 從目標終結點接收的API響應。
* 證明您已使用 [目標發佈API](./destination-publish-api.md)。
* 文檔PR（拉取請求），遵循中介紹的說明 [自助文檔處理](./docs-framework/documentation-instructions.md)。
* 將作為目標卡的徽標在Experience Platform目標目錄中顯示的影像檔案。

您可以在以下各節中找到有關每個項目的詳細資訊：

## 用例說明

提供目標為Experience Platform客戶解決的使用案例的說明。 您的描述與現有合作夥伴的使用案例類似：

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md):從您的客戶清單、訪問您站點的人員或已與您的內容在Pinterest進行互動的人員中建立受眾。
* [雅虎資料X](/help/destinations/catalog/advertising/datax.md#use-cases):DataX API可供廣告商使用，這些廣告商希望以Verizon Media(VMG)中鎖定的電子郵件地址的特定受眾群為目標，可以快速建立新的網段，並使用VMG的近即時API推送所需的受眾群。

## Test使用test目標API後的結果

在使用 [test目標API](./test-destination.md) 執行HTTP調用到目標的終結點。 其中包括:

* 使用測試API向目標終結點發出的完整API請求（標頭和正文）。
* 從目標終結點接收的API響應。

例如，您的請求和響應可能與以下示例類似：

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

## 提交目標發佈請求的證明

成功測試目標後，必須使用 [目標發佈API](./destination-publish-api.md) 將目標提交給Adobe以供審閱和發佈。

提供目標的發佈請求的ID。 有關如何檢索發佈請求ID的資訊，請閱讀 [列出目標發佈請求](./destination-publish-api.md#retrieve-list)。

## 針對產品化整合的目標文檔PR（拉式請求）

如果您是獨立軟體供應商(ISV)或系統整合商(SI)，則 [產品化整合](./overview.md#productized-custom-integrations)，使用 [自助文檔處理](./docs-framework/documentation-instructions.md) 為目標建立產品文檔頁面。 作為提交過程的一部分，請為目標文檔提供拉入請求(PR)。

## 目標徽標

目標目錄包括每個目標卡的徽標。 在您的提交電子郵件中，包括帶有目標徽標的影像。

映像要求為：
* **格式**: `SVG`
* **大小**:小於2 MB

## 下載示例電子郵件

[下載](./assets/sample-email-submit-destination.rtf) 一封示例電子郵件，其中包含您需要提供給Adobe的所有資訊。
