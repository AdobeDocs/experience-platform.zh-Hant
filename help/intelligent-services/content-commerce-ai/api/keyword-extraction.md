---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;keyword extraction;Keyword extraction
solution: Experience Platform
title: 色彩擷取
topic: Developer guide
description: 當給定文字檔案時，關鍵字擷取服務會自動擷取最能說明檔案主題的關鍵字或關鍵片語。 為了提取關鍵字，採用了命名實體識別(NER)和無監督關鍵字提取算法的組合。
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 3%

---


# 關鍵字擷取

>[!NOTE]
>
>[!DNL Content and Commerce AI] 是測試版。 說明檔案可能會有所變更。

當給定文字檔案時，關鍵字擷取服務會自動擷取最能說明檔案主題的關鍵字或關鍵片語。 為了提取關鍵字，採用了命名實體識別(NER)和無監督關鍵字提取算法的組合。

**無監督關鍵字擷取**

對於無監督的關鍵字 [提取，使用[!DNL YAKE]](http://yake.inesctec.pt/) 。 [!DNL YAKE] 是一種快速準確的無監督自動關鍵字提取方法，用於從文檔中選擇最重要的關鍵字。 然後過濾 [!DNL YAKE] 關鍵字提取以僅選擇名詞短語。

**命名實體識別**

對於命名實體識 [別，使用[!DNL spaCy]](https://spacy.io/)&#39;s OnNotes模型。 此模型會指派內容特定的代號向量、語音部分(POS)標籤、相依性剖析和命名實體。 OntoNotes模型是核心模型之 [!DNL spaCy] 一。 有關OntoNotes模型的更多資訊，請參 [閱](https://spacy.io/models/en)。

下表列出了所識 [!DNL Content and Commerce AI] 別的命名實體：

| 實體名稱 | 說明 |
| --- | --- |
| 人員 | 人，包括虛構。 |
| NORP | 民族或宗教或政治團體。 |
| GPE | 國家、城市和州。 |
| LOC | 非全球水體運動地點、山脈和水體。 |
| FAC | 建築、機場、公路、橋梁等 |
| 組織 | 公司、代理商、機構等 |
| 產品 | 物品、車輛、食品等 （非服務。） |
| 事件 | 指名的颶風、戰鬥、戰爭、體育活動等。 |
| WORK_OF_ART | 書籍、歌曲等標題 |
| LAW | 將檔案命名為法律。 |
| 語言 | 任何指名的語言。 |

結果與 [!DNL OntoNotes] 關鍵字組合，並 [!DNL YAKE]根據其重要性按排名順序返回。

**API格式**

```http
POST /services/v1/predict
```

**請求**

以下請求根據在裝載中提供的輸入參數從文檔中提取關鍵字。

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

請參閱範例裝載下表，以取得有關所示輸入參數的詳細資訊。

>[!CAUTION]
>
>`analyzer_id` 決定使 [!DNL Sensei Content Framework] 用的項目。 在提出要求前，請先檢查 `analyzer_id` 您是否有適當。 對於關鍵字擷取服務， `analyzer_id` ID為：
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
| `analyzer_id` | 您 [!DNL Sensei] 的請求所部署的服務ID。 此ID決定使用哪 [!DNL Sensei Content Frameworks] 個。 如需自訂服務，請聯絡「內容與商務AI」團隊以設定自訂ID。 | 是 |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `data` | 包含JSON物件的陣列，其中每個物件都代表檔案。 作為此陣列的一部分傳遞的任何參數都將覆蓋在陣列外部指定的全 `data` 局參數。 下表中概述的任何其他屬性都可從中覆蓋 `data`。 | 是 |
| `language` | 輸入文字的語言。 預設值為 `en`。 | 無 |
| `content-type` | 用於指出輸入是請求內文的一部分，還是S3儲存貯體的已簽署URL。 此屬性的預設值為 `inline`。 | 是 |
| `encoding` | 輸入文字的編碼格式。 這可以是 `utf-8` 或 `utf-16`。 此屬性的預設值為 `utf-8`。 | 無 |
| `threshold` | 需要傳回結果的分數臨界值（0到1）。 使用值可 `0` 傳回所有結果。 此屬性的預設值為 `0`。 | 無 |
| `top-N` | 要傳回的結果數（不能是負整數）。 使用值可 `0` 傳回所有結果。 當與搭配使用時， `threshold`傳回的結果數量會是任一限制集的較小者。 此屬性的預設值為 `0`。 | 無 |
| `custom` | 要傳遞的任何自訂參數。 此屬性需要有效的JSON物件才能運作。 如需自訂 [參數的詳細資訊](#appendix) ，請參閱附錄。 | 無 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 如果未傳遞此資訊，則會指派自動產生的ID。 | 無 |
| `content` | 關鍵字擷取服務所使用的內容。 內容可以是原始文字（「內嵌」內容類型）。 <br> 如果內容是S3(&#39;s3-bucket&#39; content-type)上的檔案，請傳遞已簽署的URL。 當內容是request-body的一部分時，資料元素清單應該只有一個物件。 如果傳遞多個物件，則只會處理第一個物件。 | 是 |

**回應**

成功的回應會傳回JSON物件，其中包含陣列中擷取的關 `response` 鍵字。

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

## 附錄 {#appendix}

下表包含可從中使用的可用參數 `custom`。

| 名稱 | 說明 | 必要 |
| --- | --- | --- |
| `min-n` | 關鍵字中所需的最小字詞數。 | 無 |
| `entity-types` | 要返回的實體類型。 請參閱本文檔開頭的命名實體識別表。 | 無 |