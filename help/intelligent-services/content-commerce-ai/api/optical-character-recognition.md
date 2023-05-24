---
keywords: OCR；文本存在；光學字元識別
solution: Experience Platform
title: 文本存在與光學字元識別
description: 在內容標籤API中，文本存在/光學字元識別(OCR)服務可以指示給定影像中是否存在文本。 如果存在文本，OCR可以返回文本。
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: 82722ddf7ff543361177b555fffea730a7879886
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 3%

---

# 文本存在與光學字元識別

當給定影像時，「文本存在/光學字元識別」(OCR)服務可指示影像中是否存在文本。 如果存在文本，OCR可以返回文本。

在本文檔中顯示的示例請求中使用了以下影像：

![示例影像](../images/sample_image.png)

**API格式**

```http
POST /services/v2/predict
```

**要求**

以下請求基於負載中提供的輸入影像檢查文本是否存在。 有關所示輸入參數的詳細資訊，請參閱示例負載下表。

使用內聯映像執行：

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F file=@sample_image.png \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "sensei:multipart_field_name": "file",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true,
        "min_probability": 0.2,
        "min_relevance": 0.01,
        "filter_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

**回應**

成功的響應返回在 `tags` 請求中傳遞的每個影像的清單。 如果某個影像中沒有文本， `is_text_present` 0和 `tags` 清單為空。

[結果0、結果1、...]:每個輸入文檔的響應清單。 每個結果都是帶鍵的指令：

1. request_element_id:對此響應的輸入檔案對應的索引，請求文檔清單中的第一個影像的索引為0，下一個影像的索引為1，依此類推。
2. 標籤：詞典清單，每個詞典有兩個鍵：文本，是影像中識別的詞，相關性，計算為與全影像相比所提取文本的邊界框區域的分數。 0.01將翻譯為至少佔影像1%的文本。
3. is_text_present:0或1，具體取決於影像中是否存在文本。 如果標籤為0，則清單為空。

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "dttklFR7DPtMtEmjlRSx5BYP5WGg3tTx"
  },
  "result": [
    {
      "is_text_present": 1,
      "tags": [
        {
          "text": "yosemite",
          "relevance": 0.06
        }
      ],
      "request_element_id": 0
    }
  ]
}
```

**要求**

以下請求基於負載中提供的輸入影像檢查文本是否存在。 有關所示輸入參數的詳細資訊，請參閱示例負載下表。

使用URL執行：

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "repo:path": <IMG_URL_PATH>,
          "sensei:repoType": "HTTP",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "ZbdhcK0JqS4Wg1wGdlEHGR3JOm530YNn"
  },
  "result": [
    {
      "is_text_present": 0,
      "tags": [],
      "request_element_id": 0
    }
  ]
}
```

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| `documents` | JSON元素清單，其中每個項都代表一個影像。 作為此清單的一部分傳遞的任何參數，都會覆蓋在清單之外為相應清單元素指定的全局參數。 | 是 |
| `sensei:multipart_field_name` | field_name，從中讀取輸入檔案路徑。 | 是 |
| `repo:path` | 影像資產的預簽名URL。 | 是 |
| `sensei:repoType` | &quot;HTTP&quot;（用於預簽URL）。 | 無 |
| `dc:format` | 輸入影像的編碼格式。 影像編碼只允許使用jpeg、jpg、png和tiff等影像格式。 dc:format與允許的格式匹配。 | 無 |
| `correct_with_dictionary` | 是否用英語詞典來更正單詞？ 如果未啟用此功能，則可能會識別非英語單詞。 預設值為True:開啟。) 請注意，當字典開啟時，您不必總是得到一個英文單詞。 我們嘗試更正它，但如果在一定編輯距離內不可能，我們會返回原始單詞。 | 無 |
| `filter_with_dictionary` | 是否過濾單詞以僅包含英語詞典中的單詞？ 如果開啟，則返回的單詞將始終屬於包含470k個單詞的大英語。 | 無 |
| `min_probability` | 識別單詞的最小概率是多少？ 服務僅返回從影像中提取且概率大於min_probability的字。 預設值設定為0.2。 | 無 |
| `min_relevance` | 識別單詞的最低相關性是多少？ 服務僅返回從影像中提取的具有大於min_relecative的相關性的字。 預設值設定為0.01。與全影像相比，將相關性計算為所提取文本的邊界框的區域的分數。 0.01將翻譯為至少佔影像1%的文本。 | 無 |

| 名稱 | 資料類型 | 必填 | 預設 | 值 | 說明 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 字串 | - | - | - | 需要從中提取文本的影像的預簽名URL。 |
| `sensei:repoType` | 字串 | - | - | HTTPS | 儲存影像的回購類型。 |
| `sensei:multipart_field_name` | 字串 | - | - | - | 將影像作為多部分參數傳遞時，請使用此選項，而不是使用預簽名的URL。 |
| `dc:format` | 字串 | 是 | - | &quot;影像/jpg&quot;, <br>&quot;影像/jpeg&quot;, <br>&quot;影像/png&quot;, <br>&quot;影像/tiff&quot; | 在處理之前，根據允許的輸入編碼類型檢查影像編碼。 |