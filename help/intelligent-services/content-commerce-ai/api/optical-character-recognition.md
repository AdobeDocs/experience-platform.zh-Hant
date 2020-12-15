---
keywords: OCR;text presence;optical character recognition
solution: Experience Platform, Intelligent Services
title: 光學字元識別
topic: Developer guide
description: 文字存在／光學字元識別(OCR)服務在給定影像時，可指出影像中是否有文字。 如果存在文本，OCR可以返回文本
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 3%

---


# 文本存在與光學字元識別

>[!NOTE]
>
>內容與商務AI為測試版。 說明檔案可能會有所變更。

文字存在／光學字元識別(OCR)服務在給定影像時，可指出影像中是否有文字。 如果存在文本，OCR可以返回文本。

本檔案所示的範例請求中使用了下列影像：

![測試影像](../images/shef.jpeg)

**API格式**

```http
POST /services/v1/predict
```

**請求**

下列請求會根據裝載中提供的輸入影像來檢查文字是否存在。 請參閱範例裝載下表，以取得有關所示輸入參數的詳細資訊。

>[!CAUTION]
>
>`analyzer_id` 決定使 [!DNL Sensei Content Framework] 用的項目。 在提出要求前，請先檢查 `analyzer_id` 您是否有適當。 請連絡內容與商務AI測試版團隊，以取得您 `analyzer_id` 的這項服務。

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
| `analyzer_id` | 您 [!DNL Sensei] 的請求所部署的服務ID。 此ID決定使用哪 [!DNL Sensei Content Frameworks] 個。 如需自訂服務，請聯絡「內容與商務AI」團隊以設定自訂ID。 | 是 |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `data` | 包含JSON物件的陣列，其中每個物件在陣列中代表傳遞的一個影像。 作為此陣列的一部分傳遞的任何參數都將覆蓋在陣列外部指定的全 `data` 局參數。 下表中概述的任何其他屬性都可從中覆蓋 `data`。 | 是 |
| `language` | 輸入文字的語言。 預設值為 `en`。 | 無 |
| `content-type` | 用於指出輸入是請求內文的一部分，還是S3儲存貯體的已簽署URL。 此屬性的預設值為 `inline`。 | 無 |
| `encoding` | 輸入影像的檔案格式。 目前只能處理JPEG和PNG影像。 此屬性的預設值為 `jpeg`。 | 無 |
| `threshold` | 需要傳回結果的分數臨界值（0到1）。 使用值可 `0` 傳回所有結果。 此屬性的預設值為 `0`。 | 無 |
| `top-N` | 要傳回的結果數（不能是負整數）。 使用值可 `0` 傳回所有結果。 當與搭配使用時， `threshold`傳回的結果數量會是任一限制集的較小者。 此屬性的預設值為 `0`。 | 無 |
| `custom` | 要傳遞的任何自訂參數。 此屬性需要有效的JSON物件才能運作。 | 無 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 如果未傳遞此資訊，則會指派自動產生的ID。 | 無 |
| `content` | 內容可以是原始影像（「內嵌」內容類型）。 <br> 如果內容是S3(&#39;s3-bucket&#39; content-type)上的檔案，請傳遞已簽署的URL。 | 是 |

**回應**

成功的響應返回陣列中檢測到的文 `feature_value` 本。 文字會從左至右讀取並從上往下傳回。 這表示如果偵測到「I love Adobe」，您的裝載會在個別物件中傳回「I」、「love」和「Adobe」。 在物件中，您會收到 `feature_name` 包含該字詞的字詞和 `feature_value` 包含該文字之信賴度量的字詞。

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
