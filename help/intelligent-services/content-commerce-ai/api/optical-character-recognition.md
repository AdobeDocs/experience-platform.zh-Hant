---
keywords: OCR；文本存在；光學字元識別
solution: Experience Platform, Intelligent Services
title: 文本存在與光學字元識別
topic-legacy: Developer guide
description: 在「內容與商務AI API」中，文字存在／光學字元辨識(OCR)服務可指出特定影像中是否有文字。 如果存在文本，OCR可以返回文本。
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 3%

---

# 文本存在與光學字元識別

>[!NOTE]
>
>內容與商務AI為測試版。 說明檔案可能會有所變更。

文字存在／光學字元識別(OCR)服務在給定影像時，可指出影像中是否有文字。 如果存在文本，OCR可以返回文本。

本檔案所示的範例要求中使用了下列影像：

![測試影像](../images/shef.jpeg)

**API格式**

```http
POST /services/v1/predict
```

**要求**

下列請求會根據裝載中提供的輸入影像來檢查文字是否存在。 請參閱範例裝載下表，以取得有關所示輸入參數的詳細資訊。

>[!CAUTION]
>
>`analyzer_id` 決定使 [!DNL Sensei Content Framework] 用的項目。請在提出要求之前，先檢查您是否有正確的`analyzer_id`。 請連絡內容與商務AI測試版團隊，以取得您的`analyzer_id`服務。

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestImage.jpg \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
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
    }]
  }'
```

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| `analyzer_id` | 您的請求部署在下的[!DNL Sensei]服務ID。 此ID決定使用哪個[!DNL Sensei Content Frameworks]。 如需自訂服務，請聯絡「內容與商務AI」團隊以設定自訂ID。 | 是 |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `data` | 包含JSON物件的陣列，其中每個物件在陣列中代表傳遞的一個影像。 作為此陣列的一部分傳遞的任何參數都將覆蓋在`data`陣列外指定的全局參數。 下表中概述的任何其他屬性都可從`data`中覆寫。 | 是 |
| `language` | 輸入文字的語言。 預設值為 `en`。 | 無 |
| `content-type` | 用於指出輸入是請求內文的一部分，還是S3儲存貯體的已簽署URL。 此屬性的預設值為`inline`。 | 無 |
| `encoding` | 輸入影像的檔案格式。 目前只能處理JPEG和PNG影像。 此屬性的預設值為`jpeg`。 | 無 |
| `threshold` | 需要傳回結果的分數臨界值（0到1）。 使用`0`值返回所有結果。 此屬性的預設值為`0`。 | 無 |
| `top-N` | 要傳回的結果數（不能是負整數）。 使用`0`值返回所有結果。 當與`threshold`搭配使用時，傳回的結果數量會小於任一限制集。 此屬性的預設值為`0`。 | 無 |
| `custom` | 要傳遞的任何自訂參數。 此屬性需要有效的JSON物件才能運作。 | 無 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 如果未傳遞此資訊，則會指派自動產生的ID。 | 無 |
| `content` | 內容可以是原始影像（「內嵌」內容類型）。 <br> 如果內容是S3(&#39;s3-bucket&#39; content-type)上的檔案，請傳遞已簽署的URL。 | 是 |

**回應**

成功的響應返回在`feature_value`陣列中檢測到的文本。 文字會從左至右讀取並從上往下傳回。 這表示如果偵測到「I loveAdobe」，您的裝載會在個別物件中傳回「I」、「love」和「Adobe」。 在物件中，您會得到包含單字的`feature_name`和包含該文字信賴度量的`feature_value`。

```json
{
  "status": 200,
  "content_id": "TestImage.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
      "content_id": "TestImage.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "yes",
                "feature_name": "has_text"
              },
              {
                "feature_value": "0.977",
                "feature_name": "CHEF"
              },
              {
                "feature_value": "success",
                "feature_name": "text_processing_status"
              }
            ],
            "feature_name": "ocr"
          }
        ]
      }
    }
  ],
  "error": []
}
```
