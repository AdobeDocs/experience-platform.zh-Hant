---
keywords: OCR；文本是否存在；光學字元識別
solution: Experience Platform
title: 文本存在與光學字元識別
description: 在內容與商務AI API中，文字是否存在/光學字元識別(OCR)服務可指出指定影像中是否存在文字。 如果存在文本，OCR可以返回文本。
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 3%

---

# 文本存在與光學字元識別

>[!NOTE]
>
>內容與商務AI正在測試中。 說明檔案可能會有所變更。

文本存在/光學字元識別(OCR)服務在給定影像時，可以指示影像中是否存在文本。 如果存在文本，OCR可以返回文本。

本檔案中顯示的範例請求中使用了下列影像：

![測試影像](../images/shef.jpeg)

**API格式**

```http
POST /services/v1/predict
```

**要求**

下列要求會根據裝載中提供的輸入影像來檢查文字是否存在。 如需所示輸入參數的詳細資訊，請參閱範例裝載下方的表格。

>[!CAUTION]
>
>`analyzer_id` 決定 [!DNL Sensei Content Framework] 中所有規則的URL區段。 請確認您有 `analyzer_id` 之後再提出要求。 請連絡內容與商務AI測試版團隊，接收您的 `analyzer_id` 服務。

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
| `analyzer_id` | 此 [!DNL Sensei] 請求部署的服務ID。 此ID決定 [!DNL Sensei Content Frameworks] 中所有規則的URL區段。 如需自訂服務，請連絡內容與商務AI團隊以設定自訂ID。 | 是 |
| `application-id` | 已建立的應用程式ID。 | 是 |
| `data` | 陣列包含JSON物件，陣列中的每個物件代表所傳遞的一個影像。 作為此陣列的一部分傳遞的任何參數都將覆蓋在 `data` 陣列。 下表中概述的任何剩餘屬性都可以從內覆蓋 `data`. | 是 |
| `language` | 輸入文本的語言。 預設值為 `en`。 | 無 |
| `content-type` | 用來指出輸入是請求內文的一部分，還是S3貯體的已簽署URL。 此屬性的預設值為 `inline`. | 無 |
| `encoding` | 輸入影像的檔案格式。 目前只能處理JPEG和PNG影像。 此屬性的預設值為 `jpeg`. | 無 |
| `threshold` | 需要返回結果的分數（0到1）的閾值。 使用值 `0` 返回所有結果。 此屬性的預設值為 `0`. | 無 |
| `top-N` | 要傳回的結果數（不能是負整數）。 使用值 `0` 返回所有結果。 搭配使用時 `threshold`，傳回的結果數是任一限制集的較小者。 此屬性的預設值為 `0`. | 無 |
| `custom` | 要傳遞的任何自訂參數。 此屬性需要有效的JSON物件才能運作。 | 無 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 若未傳遞，則會指派自動產生的ID。 | 無 |
| `content` | 內容可以是原始影像（「內嵌」內容類型）。 <br> 如果內容是S3上的檔案(&#39;s3-bucket&#39; content-type)，請傳遞已簽署的URL。 | 是 |

**回應**

成功的回應會傳回在 `feature_value` 陣列。 文字會從左到右讀取並傳回。 這表示，如果偵測到「I loveAdobe」，您的裝載會在個別物件中傳回「I」、「love」和「Adobe」。 在物件中，您 `feature_name` 包含單詞和 `feature_value` 包含該文字的信賴度量。

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
