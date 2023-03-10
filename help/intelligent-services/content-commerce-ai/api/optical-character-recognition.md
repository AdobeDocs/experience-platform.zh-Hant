---
keywords: OCR；文本是否存在；光學字元識別
solution: Experience Platform
title: 文本存在與光學字元識別
description: 在內容標籤API中，文字是否存在/光學字元辨識(OCR)服務可指出指定影像中是否有文字。 如果存在文本，OCR可以返回文本。
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 3%

---

# 文本存在與光學字元識別

文本存在/光學字元識別(OCR)服務在給定影像時可指示影像中是否存在文本。 如果存在文本，OCR可以返回文本。

本檔案中顯示的範例請求中使用了下列影像：

![範例影像](../images/sample_image.png)

**API格式**

```http
POST /services/v2/predict
```

**要求**

下列要求會根據裝載中提供的輸入影像來檢查文字是否存在。 如需所示輸入參數的詳細資訊，請參閱範例裝載下方的表格。

內嵌影像的執行：

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

成功的回應會傳回在 `tags` 清單中，列出請求中傳遞的每個影像。 如果某個影像中沒有文字， `is_text_present` 為0且 `tags` 是空白清單。

[結果0，結果1,...]:每個輸入文檔的響應清單。 每個結果都是含有鍵的字典：

1. request_element_id:此響應的輸入檔案的對應索引、請求文檔清單中第一個影像的0、下一個影像的1等。
2. 標籤：字典清單中，每個字典有兩個索引鍵：文本，是從影像中識別的字，關聯性，與全影像相比，其被計算為提取的文本邊界框的面積的分數。 0.01會轉譯為至少佔影像1%的文字。
3. is_text_present:0或1，視影像中是否有文字而定。 如果標籤為0，則清單為空。

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
          "relevance": 0.05604639115920341
        }
      ],
      "request_element_id": 0
    }
  ]
}
```

**要求**

下列要求會根據裝載中提供的輸入影像來檢查文字是否存在。 如需所示輸入參數的詳細資訊，請參閱範例裝載下方的表格。

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
| `documents` | JSON元素清單，清單中的每個項目代表一個影像。 作為此清單的一部分傳遞的任何參數，都會覆蓋在清單外部指定的對應清單元素的全局參數。 | 是 |
| `sensei:multipart_field_name` | field_name，從中讀取輸入檔案路徑。 | 是 |
| `repo:path` | 影像資產的預先簽署URL。 | 是 |
| `sensei:repoType` | &quot;HTTP&quot;（適用於預先簽署的URL）。 | 無 |
| `dc:format` | 輸入影像的編碼格式。 影像編碼僅允許使用jpeg、jpg、png和tiff等影像格式。 dc:format與允許的格式匹配。 | 無 |
| `correct_with_dictionary` | 是否用英語字典糾正這些單詞？ 如果未開啟此功能，您可能會辨識非英文單字。 預設為True:開啟。) 請注意，開啟字典時，您不一定要總是得到英文單字。 我們會嘗試加以修正，但如果無法在特定編輯距離內修正，我們會傳回原始字詞。 | 無 |
| `filter_with_dictionary` | 是否篩選單字以僅包含英文字典中的單字？ 如果開啟此功能，傳回的字詞將一律屬於包含47萬個字的大英文。 | 無 |
| `min_probability` | 所識別字詞的最小機率為何？ 服務只會傳回從影像擷取且機率大於min_probability的字詞。 預設值設定為0.2。 | 無 |
| `min_relevance` | 已識別字詞的最低相關性為何？ 服務只會傳回從影像中擷取且與min_relecative相關性較強的字詞。 預設值設定為0.01。相關性的計算方式為與完整影像相比，提取文本邊界框的面積的分數。 0.01會轉譯為至少佔影像1%的文字。 | 無 |

| 名稱 | 資料類型 | 必填 | 預設 | 值 | 說明 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 字串 | - | - | - | 需要擷取文字的影像預先標籤URL。 |
| `sensei:repoType` | 字串 | - | - | HTTPS | 儲存影像的存放庫類型。 |
| `sensei:multipart_field_name` | 字串 | - | - | - | 將影像以多部分引數傳遞時，請使用此選項，而非使用預先簽署的url。 |
| `dc:format` | 字串 | 是 | - | &quot;image/jpg&quot;, <br>&quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | 在處理之前，會根據允許的輸入編碼類型檢查影像編碼。 |