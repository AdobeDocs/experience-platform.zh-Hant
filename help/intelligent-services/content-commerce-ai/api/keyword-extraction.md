---
keywords: Experience Platform；快速入門；content ai;commerce ai;content and commerce ai；關鍵字提取；關鍵字提取
solution: Experience Platform
title: 內容與商務AI API中的關鍵字擷取
description: 當給定文本文檔時，關鍵字提取服務會自動提取最能描述文檔主題的關鍵字或關鍵字。 為了提取關鍵字，使用命名實體識別(NER)和無監督關鍵字提取算法的組合。
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 3%

---

# 關鍵字擷取

>[!NOTE]
>
>[!DNL Content and Commerce AI] 是測試版。 說明檔案可能會有所變更。

當給定文本文檔時，關鍵字提取服務會自動提取最能描述文檔主題的關鍵字或關鍵字。 為了提取關鍵字，使用命名實體識別(NER)和無監督關鍵字提取算法的組合。

由 [!DNL Content and Commerce AI] 列於下表：

| 實體名稱 | 說明 |
| --- | --- |
| 人員 | 包括虛構的人。 |
| NORP | 民族或宗教或政治團體。 |
| GPE | 國家、城市和州。 |
| LOC | 非GPE地點、山脈、水體。 |
| FAC | 建築物、機場、公路、橋梁等 |
| ORG | 公司、機構、機構等 |
| 產品 | 物品、車輛、食品等 （非服務。） |
| 事件 | 颶風、戰鬥、戰爭、體育活動等。 |
| WORK_OF_ART | 書籍、歌曲等的標題。 |
| 法律 | 成為法律的具名檔案。 |
| 語言 | 任何已命名的語言。 |

>[!NOTE]
>
>如果您打算處理PDF，請跳至 [PDF關鍵字擷取](#pdf-extraction) 。 此外，對docx、ppt、amd xml等其他檔案類型的支援也設定在稍後發行。

**API格式**

```http
POST /services/v1/predict
```

**要求**

以下請求基於在有效負載中提供的輸入參數從文檔中提取關鍵字。

簡化輸入檔案的JSON:

```json
{
  "application-id": "1234",
  "language": "en",
  "content-type": "inline",
  "encoding": "utf-8",
  "threshold": 0.01,
  "top-N": 10,
  "custom": {
    "min-n": 2,
    "entity-types": ["PERSON"]
  },
  "data": [
    {
      "content-id": "abc123",
      "content": "But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31"
    }
  ]
}
```

如需所示輸入參數的詳細資訊，請參閱範例裝載下方的表格。

>[!CAUTION]
>
>`analyzer_id` 決定 [!DNL Sensei Content Framework] 中所有規則的URL區段。 請確認您有 `analyzer_id` 之後再提出要求。 對於關鍵字擷取服務， `analyzer_id` ID為：
>`Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\",
    \"threshold\": 0.01,
    \"top-N\": 10,
    \"custom\": {
        \"min-n\": 2,
        \"entity-types\": [\"PERSON\"]
      },
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
         "parameters": {}
    }]
}'
```

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| `analyzer_id` | 此 [!DNL Sensei] 請求部署的服務ID。 此ID決定 [!DNL Sensei Content Frameworks] 中所有規則的URL區段。 如需自訂服務，請連絡內容與商務AI團隊以設定自訂ID。 | 是 |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `data` | 陣列，包含JSON物件，陣列中每個物件代表檔案。 作為此陣列的一部分傳遞的任何參數都將覆蓋在 `data` 陣列。 下表中概述的任何剩餘屬性都可以從內覆蓋 `data`. | 是 |
| `language` | 輸入文本的語言。 預設值為 `en`。 | 無 |
| `content-type` | 用來指出輸入是請求內文的一部分，還是S3貯體的已簽署URL。 此屬性的預設值為 `inline`. | 是 |
| `encoding` | 輸入文本的編碼格式。 這可以是 `utf-8` 或 `utf-16`. 此屬性的預設值為 `utf-8`. | 無 |
| `threshold` | 需要返回結果的分數（0到1）的閾值。 使用值 `0` 返回所有結果。 此屬性的預設值為 `0`. | 無 |
| `top-N` | 要傳回的結果數（不能是負整數）。 使用值 `0` 返回所有結果。 搭配使用時 `threshold`，傳回的結果數是任一限制集的較小者。 此屬性的預設值為 `0`. | 無 |
| `custom` | 要傳遞的任何自訂參數。 此屬性需要有效的JSON物件才能運作。 請參閱 [附錄](#appendix) 以取得自訂參數的詳細資訊。 | 無 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 若未傳遞，則會指派自動產生的ID。 | 無 |
| `content` | 關鍵字擷取服務使用的內容。 內容可以是原始文字（「內嵌」內容類型）。 <br> 如果內容是S3上的檔案(&#39;s3-bucket&#39; content-type)，請傳遞已簽署的URL。 當內容屬於要求內文時，資料元素清單應該只包含一個物件。 如果傳遞了多個物件，則只會處理第一個物件。 | 是 |

**回應**

成功的回應會傳回JSON物件，其中包含 `response` 陣列。

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "success",
                "feature_name": "status"
              },
              {
                "feature_name": "labels",
                "feature_value": [
                  {
                    "feature_name": "atp player",
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ]
                  },
                  {
                    "feature_name": "Novak Djokovic",
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "PERSON"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0
                      }
                    ]
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_value": 0.00899321792126428,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "player council"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "kermodes regime"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0.0006052376660884209
                      }
                    ],
                    "feature_name": "atp player council"
                  }
                ]
              }
            ],
            "feature_name": "abc123"
          }
        ]
      }
    }
  ],
  "error": []
}
```

## PDF關鍵字擷取 {#pdf-extraction}

關鍵字提取服務支援PDF，但是，您需要對PDF檔案使用新的AnalyzerID，並將文檔類型更改為PDF。 如需詳細資訊，請參閱下列範例。

**API格式**

```http
POST /services/v1/predict
```

**要求**

以下請求根據在有效負載中提供的輸入參數從PDF文檔中提取關鍵字。

>[!CAUTION]
>
>`analyzer_id` 決定 [!DNL Sensei Content Framework] 中所有規則的URL區段。 請確認您有 `analyzer_id` 之後再提出要求。 若為PDF關鍵字擷取， `analyzer_id` ID為：
>`Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestPDF.pdf \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
    "parameters": {
      "application-id": "1234",
      "content-type": "file",
      "encoding": "pdf",
      "threshold": "0.01",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "abc123",
        "content": "file",
        }]
      }
    }]
  }'
```

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| `analyzer_id` | 此 [!DNL Sensei] 請求部署的服務ID。 此ID決定 [!DNL Sensei Content Frameworks] 中所有規則的URL區段。 如需自訂服務，請連絡內容與商務AI團隊以設定自訂ID。 | 是 |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `data` | 陣列，包含JSON物件，陣列中每個物件代表檔案。 作為此陣列的一部分傳遞的任何參數都將覆蓋在 `data` 陣列。 下表中概述的任何剩餘屬性都可以從內覆蓋 `data`. | 是 |
| `language` | 輸入的語言。 預設值為 `en` （英文）。 | 無 |
| `content-type` | 用於指示輸入內容類型。 此值應設為 `file`. | 是 |
| `encoding` | 輸入的編碼格式。 此值應設為 `pdf`. 日後將支援更多編碼類型。 | 是 |
| `threshold` | 需要返回結果的分數（0到1）的閾值。 使用值 `0` 返回所有結果。 此屬性的預設值為 `0`. | 無 |
| `top-N` | 要傳回的結果數（不能是負整數）。 使用值 `0` 返回所有結果。 搭配使用時 `threshold`，傳回的結果數是任一限制集的較小者。 此屬性的預設值為 `0`. | 無 |
| `custom` | 要傳遞的任何自訂參數。 此屬性需要有效的JSON物件才能運作。 請參閱 [附錄](#appendix) 以取得自訂參數的詳細資訊。 | 無 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 若未傳遞，則會指派自動產生的ID。 | 無 |
| `content` | 此值應設為 `file`. | 是 |

**回應**

成功的回應會傳回JSON物件，其中包含 `response` 陣列。

```json
{
  "statusCode": 200,
  "body": {
    "type": "JSON",
    "matchType": "strict",
    "json": {
      "status": 200,
      "content_id": "161hw2.pdf",
      "cas_responses": [
        {
          "status": 200,
          "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
          "content_id": "161hw2.pdf",
          "result": {
            "response_type": "feature",
            "response": [
              {
                "feature_value": [
                  {
                    "feature_name": "status",
                    "feature_value": "success"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "delbick",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0.03673855028832046
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "KEYWORD"
                          }
                        ]
                      },
                      {
                        "feature_name": "Ci",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "PERSON"
                          }
                        ]
                      }
                    ],
                    "feature_name": "labels"
                  }
                ],
                "feature_name": "abc123"
              }
            ]
          }
        }
      ],
      "error": []
    }
  }
}
```

如需詳細資訊和使用PDF擷取的範例，其中包含如何設定、部署以及與AEM雲端服務整合的指示。 造訪 [CCAIPDF擷取worker github存放庫](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract).

## 附錄 {#appendix}

下表包含可在內使用的可用參數 `custom`.

| 名稱 | 說明 | 必要 |
| --- | --- | --- |
| `min-n` | 關鍵字中需要的最小字詞數。 | 無 |
| `entity-types` | 要傳回的實體類型。 請參閱本文檔開頭的命名實體識別表。 | 無 |
