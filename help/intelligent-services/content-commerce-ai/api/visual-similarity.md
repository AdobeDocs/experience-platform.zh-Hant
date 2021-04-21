---
keywords: 視覺相似性；視覺相似性； ccai api
solution: Experience Platform, Intelligent Services
title: 內容與商務AI API中的視覺相似性
topic-legacy: Developer guide
description: 視覺相似性服務在給定影像時，會自動從目錄中尋找視覺相似的影像。
exl-id: fe31d9be-ee42-44fa-b83f-3b8a718cb4e3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# 視覺相似性

>[!NOTE]
>
>[!DNL Content and Commerce AI] 是測試版。說明檔案可能會有所變更。

視覺相似性服務在給定影像時，會自動從目錄中尋找視覺相似的影像。

本檔案所示的範例要求中使用了下列影像：

![測試影像](../images/Query_Image.jpeg)

**API格式**

```http
POST /services/v1/predict
```

**要求**

以下請求根據裝載中提供的輸入參數從目錄中檢索視覺上類似的影像。 請參閱範例裝載下表，以取得有關所示輸入參數的詳細資訊。

>[!CAUTION]
>
>`analyzer_id` 決定使 [!DNL Sensei Content Framework] 用的項目。請在提出要求之前，先檢查您是否有正確的`analyzer_id`。 請連絡內容與商務AI測試版團隊，以取得您的`analyzer_id`服務。

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer $API_TOKEN' \
  -H 'Content-Type: multipart/form-data' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-api-key: $API_KEY' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
         "parameters": {
          "application-id": "1234", 
          "content-type": "inline", 
          "encoding": "jpeg", 
          "threshold": "0", 
          "top-N": "0", 
          "custom": {}, 
          "data": [{
            "content-id": "0987", 
            "content": "inline-image", 
            "content-type": "inline", 
            "encoding": "jpeg", 
            "threshold": "0", 
            "top-N": "0", 
            "historic-metadata": [], 
            "custom": {}
            }]
          }
      }
    ]
}'
```

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| `analyzer_id` | 您的請求部署在下的[!DNL Sensei]服務ID。 此ID決定使用哪個[!DNL Sensei Content Frameworks]。 如需自訂服務，請聯絡「內容與商務AI」團隊以設定自訂ID。 | 是 |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `data` | 包含JSON物件的陣列，其中每個物件都代表影像。 作為此陣列的一部分傳遞的任何參數都將覆蓋在`data`陣列外指定的全局參數。 下表中概述的任何其他屬性都可從`data`中覆寫。 | 是 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 如果未傳遞此資訊，則會指派自動產生的ID。 | 無 |
| `content` | 通過視覺相似性服務來分析待分析的內容。 如果影像是請求主體的一部分，請在curl命令中使用`-F file=@<filename>`來傳遞影像，將此參數保留為空字串。 <br> 如果影像是S3上的檔案，請傳遞已簽署的URL。當內容是請求內文的一部分時，資料元素清單應該只有一個物件。 如果傳遞多個物件，則只會處理第一個物件。 | 是 |
| `content-type` | 用於指出輸入是請求內文的一部分，還是S3儲存貯體的已簽署URL。 此屬性的預設值為`inline`。 | 無 |
| `encoding` | 輸入影像的檔案格式。 目前只能處理JPEG和PNG影像。 此屬性的預設值為`jpeg`。 | 無 |
| `threshold` | 需要傳回結果的分數臨界值（0到1）。 使用`0`值返回所有結果。 此屬性的預設值為`0`。 | 無 |
| `top-N` | 要傳回的結果數（不能是負整數）。 使用`0`值返回所有結果。 當與`threshold`搭配使用時，傳回的結果數量會小於任一限制集。 此屬性的預設值為`0`。 | 無 |
| `custom` | 要傳遞的任何自訂參數。 | 無 |
| `historic-metadata` | 可傳遞中繼資料的陣列。 | 無 |

**回應**

成功的響應返回一個`response`陣列，該陣列包含`feature_value`和`feature_name`，用於目錄中找到的每個視覺相似影像。

在下列範例回應中傳回下列視覺上類似的影像：

![相似影像](../images/results.jpg)

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "678",
                "feature_name": "G34WS945.F1"
              },
              {
                "feature_value": "678",
                "feature_name": "1431RDM JANELLE RAW JACKE"
              },
              {
                "feature_value": "657",
                "feature_name": "GF4045877841 CARLA FLR"
              },
              {
                "feature_name": "1707-686-SGU PATCH XYZ",
                "feature_value": "657"
              },
              {
                "feature_name": "5495MJT AJA BLK",
                "feature_value": "646"
              },
              {
                "feature_name": "IDEAL",
                "feature_value": "645"
              },
              {
                "feature_value": "644",
                "feature_name": "HCAJRA439 CALI JEAN"
              },
              {
                "feature_name": "KT279RK-ONL",
                "feature_value": "644"
              },
              {
                "feature_name": "SP190404-ELLIS",
                "feature_value": "642"
              },
              {
                "feature_name": "GF4174848718 KENDALL DIS",
                "feature_value": "640"
              }
            ],
            "feature_name": "visual_similarity"
          }
        ]
      }
    }
  ],
  "error": []
}
```
