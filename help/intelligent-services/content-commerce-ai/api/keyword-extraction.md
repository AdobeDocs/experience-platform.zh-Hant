---
keywords: Experience Platform；入門；內容ai;commerce ai;content and commerce ai；關鍵字提取；關鍵字提取
solution: Intelligent Services
title: Content and Commerce AI API中的關鍵字提取
topic-legacy: Developer guide
description: 當給定文本文檔時，關鍵字提取服務自動提取最能描述文檔主題的關鍵字或關鍵字短語。 為了提取關鍵字，使用命名實體識別(NER)和無監督關鍵字提取算法的組合。
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 3%

---

# 關鍵字提取

>[!NOTE]
>
>[!DNL Content and Commerce AI] 是β 文檔可能會更改。

當給定文本文檔時，關鍵字提取服務自動提取最能描述文檔主題的關鍵字或關鍵字短語。 為了提取關鍵字，使用命名實體識別(NER)和無監督關鍵字提取算法的組合。

已命名實體由 [!DNL Content and Commerce AI] 列於下表：

| 實體名稱 | 說明 |
| --- | --- |
| 人員 | 人，包括虛構。 |
| 諾普 | 民族或宗教或政治團體。 |
| GPE | 國家、城市和州。 |
| 位置 | 非全境保護區地點、山脈、水體。 |
| FAC | 建築物、機場、公路、橋梁等 |
| 組織 | 公司、機構、機構等 |
| 產品 | 物品、車輛、食品等 （不是服務。） |
| 事件 | 有名的颶風、戰鬥、戰爭、體育活動等 |
| 藝術作品 | 書名、歌曲等 |
| 法律 | 被命名為法律的檔案。 |
| 語言 | 任何已命名語言。 |

>[!NOTE]
>
>如果您計畫處理PDF，請跳至 [PDF關鍵字提取](#pdf-extraction) 的下界。 此外，還將支援其他檔案類型（如docx、ppt、amd xml）設定為稍後發佈。

**API格式**

```http
POST /services/v1/predict
```

**要求**

以下請求基於在負載中提供的輸入參數從文檔中提取關鍵字。

輸入檔案的簡化JSON:

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

有關所示輸入參數的詳細資訊，請參閱示例負載下表。

>[!CAUTION]
>
>`analyzer_id` 確定 [!DNL Sensei Content Framework] 的子菜單。 請檢查一下 `analyzer_id` 在你提出要求之前。 對於關鍵字提取服務， `analyzer_id` ID是：
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
| `analyzer_id` | 的 [!DNL Sensei] 部署請求的服務ID。 此ID確定 [!DNL Sensei Content Frameworks] 的子菜單。 有關自定義服務，請與Content and Commerce AI團隊聯繫以設定自定義ID。 | 是 |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `data` | 包含JSON對象的陣列，其中每個對象都位於表示文檔的陣列中。 作為此陣列的一部分傳遞的任何參數都將覆蓋在 `data` 陣列。 此表中概述的任何剩餘屬性都可以從中覆蓋 `data`。 | 是 |
| `language` | 輸入文本的語言。 預設值為 `en`。 | 無 |
| `content-type` | 用於指示輸入是請求正文的一部分還是S3儲存段的帶簽名URL。 此屬性的預設值為 `inline`。 | 是 |
| `encoding` | 輸入文本的編碼格式。 這可以是 `utf-8` 或 `utf-16`。 此屬性的預設值為 `utf-8`。 | 無 |
| `threshold` | 需要返回結果的分數（0到1）的閾值。 使用值 `0` 返回所有結果。 此屬性的預設值為 `0`。 | 無 |
| `top-N` | 要返回的結果數（不能為負整數）。 使用值 `0` 返回所有結果。 與 `threshold`，返回的結果數是任一限制集的較小值。 此屬性的預設值為 `0`。 | 無 |
| `custom` | 要傳遞的任何自定義參數。 此屬性需要有效的JSON對象才能運行。 查看 [附錄](#appendix) 的子菜單。 | 無 |
| `content-id` | 響應中返回的資料元素的唯一ID。 如果未傳遞此資訊，則分配自動生成的ID。 | 無 |
| `content` | 關鍵字提取服務使用的內容。 內容可以是原始文本（「內聯」內容類型）。 <br> 如果內容是S3(&#39;s3-bucket&#39; content-type)上的檔案，請傳遞帶簽名的URL。 當內容是request-body的一部分時，資料元素清單應只有一個對象。 如果傳遞了多個對象，則只處理第一個對象。 | 是 |

**回應**

成功的響應返回JSON對象，該對象包含 `response` 陣列。

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

## PDF關鍵字提取 {#pdf-extraction}

關鍵字提取服務支援PDF，但是，您需要使用新的AnalyzerID來PDF檔案，並將文檔類型更改為PDF。 有關詳細資訊，請參閱下面的示例。

**API格式**

```http
POST /services/v1/predict
```

**要求**

以下請求基於在有效負載中提供的輸入參數從PDF文檔中提取關鍵字。

>[!CAUTION]
>
>`analyzer_id` 確定 [!DNL Sensei Content Framework] 的子菜單。 請檢查一下 `analyzer_id` 在你提出要求之前。 對於PDF關鍵字提取， `analyzer_id` ID是：
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
| `analyzer_id` | 的 [!DNL Sensei] 部署請求的服務ID。 此ID確定 [!DNL Sensei Content Frameworks] 的子菜單。 有關自定義服務，請與Content and Commerce AI團隊聯繫以設定自定義ID。 | 是 |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `data` | 包含JSON對象的陣列，其中每個對象都位於表示文檔的陣列中。 作為此陣列的一部分傳遞的任何參數都將覆蓋在 `data` 陣列。 此表中概述的任何剩餘屬性都可以從中覆蓋 `data`。 | 是 |
| `language` | 輸入語言。 預設值為 `en` （英語）。 | 無 |
| `content-type` | 用於指示輸入內容類型。 此值應設定為 `file`。 | 是 |
| `encoding` | 輸入的編碼格式。 此值應設定為 `pdf`。 以後將支援更多編碼類型。 | 是 |
| `threshold` | 需要返回結果的分數（0到1）的閾值。 使用值 `0` 返回所有結果。 此屬性的預設值為 `0`。 | 無 |
| `top-N` | 要返回的結果數（不能為負整數）。 使用值 `0` 返回所有結果。 與 `threshold`，返回的結果數是任一限制集的較小值。 此屬性的預設值為 `0`。 | 無 |
| `custom` | 要傳遞的任何自定義參數。 此屬性需要有效的JSON對象才能運行。 查看 [附錄](#appendix) 的子菜單。 | 無 |
| `content-id` | 響應中返回的資料元素的唯一ID。 如果未傳遞此資訊，則分配自動生成的ID。 | 無 |
| `content` | 此值應設定為 `file`。 | 是 |

**回應**

成功的響應返回JSON對象，該對象包含 `response` 陣列。

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

有關使用PDF提取的詳細資訊和示例，其中包含有關如何設定、部署和整合雲服務AEM的說明。 訪問 [CCAIPDF提取工作器github儲存庫](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract)。

## 附錄 {#appendix}

下表包含可從中使用的可用參數 `custom`。

| 名稱 | 說明 | 必要 |
| --- | --- | --- |
| `min-n` | 關鍵字中所需的最小字數。 | 無 |
| `entity-types` | 要返回的實體類型。 請參閱本文檔開頭的命名實體識別表。 | 無 |
