---
keywords: OCR；文字顯示；光學字元辨識
solution: Experience Platform
title: 文字顯示和光學字元辨識
description: 在內容標籤API中，「文字存在/光學字元辨識(OCR)」服務可指出文字是否存在於指定影像中。 如果存在文字，OCR可以傳回文字。
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: 82722ddf7ff543361177b555fffea730a7879886
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 3%

---

# 文字顯示和光學字元辨識

指定影像時，文字存在/光學字元辨識(OCR)服務可指出影像中是否有文字。 如果存在文字，OCR可以傳回文字。

本檔案所示的範例請求中使用了下列影像：

![範例影像](../images/sample_image.png)

**API格式**

```http
POST /services/v2/predict
```

**要求**

以下請求會根據承載中提供的輸入影像檢查文字是否存在。 請參閱裝載範例下表，以取得有關所示輸入引數的詳細資訊。

使用內嵌影像執行：

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

成功的回應會傳回在`tags`清單中偵測到的文字（針對要求中傳遞的每個影像）。 如果特定影像中沒有文字，`is_text_present`為0，`tags`為空白清單。

[result0， result1， ...]：每個輸入檔案的回應清單。 每個結果都是一個包含鍵的指令：

1. request_element_id：此回應之輸入檔案的對應索引，0代表請求檔案清單中的第一個影像，1代表下一個影像，以此類推。
2. 標籤：字典清單，每個字典有兩個索引鍵：文字（從影像中可辨識的字詞）和相關性（計算為擷取文字邊界方塊區域與完整影像相較之下的分數）。 0.01會翻譯成至少佔影像1%的文字。
3. is_text_present： 0或1，視影像中是否有文字而定。 如果標籤為0，則清單為空白。

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

以下請求會根據承載中提供的輸入影像檢查文字是否存在。 請參閱裝載範例下表，以取得有關所示輸入引數的詳細資訊。

以URL執行：

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

| 屬性 | 說明 | 強制 |
| --- | --- | --- |
| `documents` | JSON元素清單，清單中的每個專案代表一個影像。 作為此清單的一部分傳遞的任何引數，都會針對對應的清單元素覆寫在清單外部指定的全域引數。 | 是 |
| `sensei:multipart_field_name` | 要讀取輸入檔案路徑的field_name。 | 是 |
| `repo:path` | 影像資產的預先簽署url。 | 是 |
| `sensei:repoType` | &quot;HTTP&quot; （適用於預先簽署的url）。 | 無 |
| `dc:format` | 輸入影像的編碼格式。 影像編碼僅允許jpeg、jpg、png和tiff等影像格式。 dc：format與允許的格式相符。 | 無 |
| `correct_with_dictionary` | 是否使用英文字典來更正單字？ 如果未開啟此功能，您可能會辨識非英文單字。 預設值為True：開啟。) 請注意，當字典開啟時，您不一定一定要收到英文單字。 我們會嘗試修正它，但如果在一定編輯距離內無法修正，我們會傳回原始單字。 | 無 |
| `filter_with_dictionary` | 是否要篩選單字，使其僅包含英文字典中的單字？ 如果開啟此功能，傳回的單字將一律屬於大型英文，包含47萬個單字。 | 無 |
| `min_probability` | 已識別字詞的最小機率為何？ 服務只會傳回從影像擷取而來的單字，其機率大於min_probability。 預設值設定為0.2。 | 無 |
| `min_relevance` | 已識別字詞的最低關聯性為何？ 服務只會傳回從影像擷取而來的單字，其相關性大於min_relevance。 預設值設定為0.01。相關性的計算方式為擷取文字的邊界方塊區域與完整影像相較之下的比例。 0.01會翻譯成至少佔影像1%的文字。 | 無 |

| 名稱 | 資料類型 | 必要 | 預設 | 值 | 說明 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 字串 | - | - | - | 需要從中擷取文字之影像的預留URL。 |
| `sensei:repoType` | 字串 | - | - | HTTPS | 儲存影像的存放庫型別。 |
| `sensei:multipart_field_name` | 字串 | - | - | - | 將影像作為多部分引數傳遞時，請使用此選項，而非使用預先簽署的URL。 |
| `dc:format` | 字串 | 是 | - | &quot;image/jpg&quot;， <br>&quot;image/jpeg&quot;， <br>&quot;image/png&quot;， <br>&quot;image/tiff&quot; | 在處理之前，系統會根據允許的輸入編碼型別檢查影像編碼。 |