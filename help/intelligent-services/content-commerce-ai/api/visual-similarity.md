---
keywords: 視覺相似性；視覺相似性；ccai api
solution: Experience Platform
title: 內容與商務AI API中的視覺相似性
description: 當給定影像時，視覺相似性服務自動從目錄中找到視覺相似的影像。
exl-id: fe31d9be-ee42-44fa-b83f-3b8a718cb4e3
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# 視覺相似性

>[!NOTE]
>
>[!DNL Content and Commerce AI] 是β 文檔可能會更改。

當給定影像時，視覺相似性服務自動從目錄中找到視覺相似的影像。

在本文檔中顯示的示例請求中使用了以下影像：

![test影像](../images/Query_Image.jpeg)

**API格式**

```http
POST /services/v1/predict
```

**要求**

以下請求基於在負載中提供的輸入參數從目錄中檢索可視相似的影像。 有關所示輸入參數的詳細資訊，請參閱示例負載下表。

>[!CAUTION]
>
>`analyzer_id` 確定 [!DNL Sensei Content Framework] 的子菜單。 請檢查一下 `analyzer_id` 在你提出要求之前。 聯繫內容和商務AI測試團隊以接收您的 `analyzer_id` 為此服務。

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
| `analyzer_id` | 的 [!DNL Sensei] 部署請求的服務ID。 此ID確定 [!DNL Sensei Content Frameworks] 的子菜單。 有關自定義服務，請與Content and Commerce AI團隊聯繫以設定自定義ID。 | 是 |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `data` | 包含JSON對象的陣列，其中每個對象都位於表示影像的陣列中。 作為此陣列的一部分傳遞的任何參數都將覆蓋在 `data` 陣列。 此表中概述的任何剩餘屬性都可以從中覆蓋 `data`。 | 是 |
| `content-id` | 響應中返回的資料元素的唯一ID。 如果未傳遞此資訊，則分配自動生成的ID。 | 無 |
| `content` | 通過視覺相似性服務分析的內容。 如果影像是請求主體的一部分，請使用 `-F file=@<filename>` 在curl命令中傳遞影像，將此參數保留為空字串。 <br> 如果影像是S3上的檔案，請傳遞帶簽名的URL。 當內容是請求正文的一部分時，資料元素清單應只有一個對象。 如果傳遞了多個對象，則只處理第一個對象。 | 是 |
| `content-type` | 用於指示輸入是請求正文的一部分還是S3儲存段的帶簽名URL。 此屬性的預設值為 `inline`。 | 無 |
| `encoding` | 輸入影像的檔案格式。 目前只能處理JPEG和PNG影像。 此屬性的預設值為 `jpeg`。 | 無 |
| `threshold` | 需要返回結果的分數（0到1）的閾值。 使用值 `0` 返回所有結果。 此屬性的預設值為 `0`。 | 無 |
| `top-N` | 要返回的結果數（不能為負整數）。 使用值 `0` 返回所有結果。 與 `threshold`，返回的結果數是任一限制集的較小值。 此屬性的預設值為 `0`。 | 無 |
| `custom` | 要傳遞的任何自定義參數。 | 無 |
| `historic-metadata` | 可傳遞元資料的陣列。 | 無 |

**回應**

成功的響應返回 `response` 包含 `feature_value` 和 `feature_name` 目錄中找到的每個視覺相似影像。

在下面所示的示例響應中返回了以下外觀相似的影像：

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
