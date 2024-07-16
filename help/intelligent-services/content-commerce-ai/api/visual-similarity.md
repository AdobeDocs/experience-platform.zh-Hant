---
keywords: 視覺相似度；視覺相似度； ccai api
solution: Experience Platform
title: 內容和Commerce AI API中的視覺相似度
description: 視覺相似度服務在提供影像時，會自動從目錄中尋找視覺上類似的影像。
exl-id: fe31d9be-ee42-44fa-b83f-3b8a718cb4e3
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---

# 視覺相似度

>[!NOTE]
>
>[!DNL Content and Commerce AI]為測試版。 檔案內容可能會有所變更。

視覺相似度服務在提供影像時，會自動從目錄中尋找視覺上類似的影像。

本檔案所示的範例請求中使用了下列影像：

![測試影像](../images/Query_Image.jpeg)

**API格式**

```http
POST /services/v1/predict
```

**要求**

下列請求會根據裝載中提供的輸入引數，從目錄中擷取視覺上類似的影像。 請參閱裝載範例下表，以取得有關所示輸入引數的詳細資訊。

>[!CAUTION]
>
>`analyzer_id`決定使用哪個[!DNL Sensei Content Framework]。 提出要求前，請檢查您是否擁有適當的`analyzer_id`。 請連絡內容與Commerce AI測試版團隊，接收此服務的`analyzer_id`。

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

| 屬性 | 說明 | 強制 |
| --- | --- | --- |
| `analyzer_id` | 您的要求部署所在的[!DNL Sensei]服務ID。 此ID決定使用[!DNL Sensei Content Frameworks]中的哪一個。 若要自訂服務，請聯絡內容和Commerce AI團隊以設定自訂ID。 | 是 |
| `application-id` | 您建立的應用程式ID。 | 是 |
| `data` | 一個陣列，其中包含JSON物件，且陣列中的每個物件分別代表一個影像。 作為此陣列的一部分傳遞的任何引數都會覆寫`data`陣列外部指定的全域引數。 此表格中下面列出的任何剩餘屬性都可以從`data`內覆寫。 | 是 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 如果未傳遞，則會指派自動產生的ID。 | 無 |
| `content` | 視覺相似度服務要分析的內容。 如果影像是要求內文的一部分，請在curl命令中使用`-F file=@<filename>`傳遞影像，將此引數保留為空字串。 <br>如果影像是S3上的檔案，請傳遞已簽署的URL。 當內容屬於請求內文的一部分時，資料元素清單應該只有一個物件。 如果傳遞了多個物件，則只會處理第一個物件。 | 是 |
| `content-type` | 用於指出輸入是請求內文的一部分，還是S3儲存貯體的已簽署URL。 此屬性的預設值為`inline`。 | 無 |
| `encoding` | 輸入影像。 目前只能處理JPEG和PNG影像。 此屬性的預設值為`jpeg`。 | 無 |
| `threshold` | 分數（0至1）的臨界值，超過該臨界值即需要傳回結果。 使用值`0`傳回所有結果。 此屬性的預設值為`0`。 | 無 |
| `top-N` | 要傳回的結果數目（不能為負整數）。 使用值`0`傳回所有結果。 當與`threshold`一起使用時，傳回的結果數是設定的任一限制中的較小值。 此屬性的預設值為`0`。 | 無 |
| `custom` | 任何要傳遞的自訂引數。 | 無 |
| `historic-metadata` | 可傳遞中繼資料的陣列。 | 無 |

**回應**

成功的回應會傳回`response`陣列，其中包含在目錄中找到的每個視覺上類似影像的`feature_value`和`feature_name`。

以下範例回應中傳回視覺上相似的影像：

![類似的影像](../images/results.jpg)

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
