---
keywords: OCR；文本存在；光學字元識別
solution: Intelligent Services
title: 文本存在與光學字元識別
topic-legacy: Developer guide
description: 在Content and Commerce AI API中，文本存在/光學字元識別(OCR)服務可以指示給定影像中是否存在文本。 如果存在文本，OCR可以返回文本。
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 3%

---

# 文本存在與光學字元識別

>[!NOTE]
>
>內容和商務AI處於測試版。 文檔可能會更改。

當給定影像時，「文本存在/光學字元識別」(OCR)服務可指示影像中是否存在文本。 如果存在文本，OCR可以返回文本。

在本文檔中顯示的示例請求中使用了以下影像：

![test影像](../images/shef.jpeg)

**API格式**

```http
POST /services/v1/predict
```

**要求**

以下請求基於負載中提供的輸入影像檢查文本是否存在。 有關所示輸入參數的詳細資訊，請參閱示例負載下表。

>[!CAUTION]
>
>`analyzer_id` 確定 [!DNL Sensei Content Framework] 的子菜單。 請檢查一下 `analyzer_id` 在你提出要求之前。 聯繫內容和商務AI測試團隊以接收您的 `analyzer_id` 為此服務。

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
| `analyzer_id` | 的 [!DNL Sensei] 部署請求的服務ID。 此ID確定 [!DNL Sensei Content Frameworks] 的子菜單。 有關自定義服務，請與Content and Commerce AI團隊聯繫以設定自定義ID。 | 是 |
| `application-id` | 已建立的應用程式的ID。 | 是 |
| `data` | 包含JSON對象的陣列，其中每個對象都表示傳遞的一個影像。 作為此陣列的一部分傳遞的任何參數都將覆蓋在 `data` 陣列。 此表中概述的任何剩餘屬性都可以從中覆蓋 `data`。 | 是 |
| `language` | 輸入文本的語言。 預設值為 `en`。 | 無 |
| `content-type` | 用於指示輸入是請求正文的一部分還是S3儲存段的帶簽名URL。 此屬性的預設值為 `inline`。 | 無 |
| `encoding` | 輸入影像的檔案格式。 目前只能處理JPEG和PNG影像。 此屬性的預設值為 `jpeg`。 | 無 |
| `threshold` | 需要返回結果的分數（0到1）的閾值。 使用值 `0` 返回所有結果。 此屬性的預設值為 `0`。 | 無 |
| `top-N` | 要返回的結果數（不能為負整數）。 使用值 `0` 返回所有結果。 與 `threshold`，返回的結果數是任一限制集的較小值。 此屬性的預設值為 `0`。 | 無 |
| `custom` | 要傳遞的任何自定義參數。 此屬性需要有效的JSON對象才能運行。 | 無 |
| `content-id` | 響應中返回的資料元素的唯一ID。 如果未傳遞此資訊，則分配自動生成的ID。 | 無 |
| `content` | 內容可以是原始影像（「內聯」內容類型）。 <br> 如果內容是S3(&#39;s3-bucket&#39; content-type)上的檔案，請傳遞簽名的URL。 | 是 |

**回應**

成功的響應返回在 `feature_value` 陣列。 文本將被讀取並從左到右返回。 這意味著，如果檢測到「我愛Adobe」，則您的負載會在單獨的對象中返回「I」、「愛」和「Adobe」。 在對象中 `feature_name` 包含單詞和 `feature_value` 包含該文本的置信度。

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
