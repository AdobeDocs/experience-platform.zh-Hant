---
keywords: Experience Platform；快速入門；content ai;commerce ai；內容標籤ai；關鍵字標籤；關鍵字標籤
solution: Experience Platform
title: 內容標籤AI API中的關鍵字標籤
description: 關鍵字標籤服務在給定文本文檔時，會自動提取最能描述文檔主題的關鍵字或關鍵字。 為了提取關鍵字，使用命名實體識別(NER)和無監督關鍵字標籤算法的組合。
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
source-git-commit: feebf4c20d20afcdcfe4523e0b61bff5b999084c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 5%

---

# 關鍵字標籤

給定文本文檔時，關鍵字標籤服務會自動提取最能描述文檔主題的關鍵字或關鍵短語。 為了提取關鍵字，使用命名實體識別(NER)和無監督關鍵字標籤算法的組合。

下表列出了 [!DNL Content Tagging AI] 已識別：

| 實體名稱 | 說明 |
| --- | --- |
| 人員 | 包括虛構的。 |
| GPE | 國家、城市和州。 |
| LOC | 非GPE地點、山脈和水體。 |
| FAC | 建築物、機場、公路、橋梁等 |
| ORG | 公司、機構、機構等 |
| 產品 | 物品、車輛、食品等 （非服務。） |
| 事件 | 颶風、戰鬥、戰爭、體育活動等。 |
| WORK_OF_ART | 書籍、歌曲等的標題。 |
| 法律 | 成為法律的具名檔案。 |
| 語言 | 任何已命名的語言。 |

**API格式**

```http
POST /services/v2/predict
```

**要求**

以下請求基於在有效負載中提供的輸入參數從文檔中提取關鍵字。

如需所示輸入參數的詳細資訊，請參閱範例裝載下方的表格。

此 [範例pdf](../pdf-files/simple-text.pdf) 檔案用於本檔案中所示的範例中。

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "test",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-ner:Service-1e9081c865214d1e8bace51dd918b5c0"
      },
      "sensei:inputs": {
        "documents": [
          {
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "application/pdf"
          }
        ]
      },
      "sensei:params": {
        "application-id": "1234",
        "min_key_phrase_length": 1,
        "max_key_phrase_length": 3,
        "top_n": 5,
        "last_semantic_unit_type": "concept"
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}' \
-F 'infile_1=@simple-text.pdf'
```

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `top_n` | 要返回的結果數。 0，返回所有結果。 與臨界值搭配使用時，傳回的結果數量將小於任一限制。 | 無 |
| `min_relevance` | 必須傳回結果的分數臨界值。 排除參數以傳回所有結果。 | 無 |
| `min_key_phrase_length` | 關鍵片語中需要的字詞數量下限。 | 無 |
| `max_key_phrase_length` | 關鍵片語中需要的字詞數上限。 | 無 |
| `last_semantic_unit_type` | 在分層響應中只返回到給定級別的語義單位。 &quot;key_phrase&quot;僅返回關鍵片語，&quot;linked_entity&quot;僅返回關鍵片語及其對應的連結實體，而&quot;concept&quot;返回關鍵片語、連結實體和概念。 | 無 |
| `entity_types` | 要傳回為關鍵片語的實體類型。 | 無 |

| 名稱 | 資料類型 | 必填 | 預設 | 值 | 說明 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 字串 | - | - | - | 要從中提取關鍵片語的文檔的預簽URL。 |
| `sensei:repoType` | 字串 | - | - | HTTPS | 儲存文檔的儲存庫類型。 |
| `sensei:multipart_field_name` | 字串 | - | - | - | 將檔案以多部分引數傳遞時，請使用此選項，而非使用預先簽署的url。 |
| `dc:format` | 字串 | 是 | - | &quot;文本/純文字檔案&quot;,<br>&quot;application/pdf&quot;,<br>&quot;text/pdf&quot;,<br>&quot;text/html&quot;,<br>&quot;text/rtf&quot;,<br>&quot;application/rtf&quot;,<br>&quot;application/msword&quot;,<br>&quot;application/vnd.openxmlformats-officedocument.wordprocessingml.document&quot;,<br>&quot;application/mspowerpoint&quot;,<br>&quot;application/vnd.ms-powerpoint&quot;,<br>&quot;application/vnd.openxmlformats-officedocument.presentationml.presentation&quot; | 在處理前，將根據允許的輸入編碼類型來檢查文檔編碼。 |

**回應**

成功的回應會傳回JSON物件，其中包含 `response` 陣列。

```json
{
  [
  {
    "key_phrases": [
      {
        "name": "Canada",
        "type": "GPE",
        "relevance": 0.9525035277863068,
        "confidence": 1.0,
        "linked_entity": {
          "name": "Canada",
          "id": "b27a82e6-e963-45de-add8-dc4f3f0dd399",
          "confidence": 1.0,
          "relevance": 0.9706433035237365,
          "concepts": [
            {
              "name": "Commonwealth realm",
              "relationship": "instance_of",
              "id": "f5354ab6-ad25-406a-b289-9209db0db8ea",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "sovereign state",
              "relationship": "instance_of",
              "id": "10c24191-beef-43cc-a823-c170f217fe12",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "dominion of the British Empire",
              "relationship": "instance_of",
              "id": "4ffabaee-e6ab-422d-b121-145dcdbcf427",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "country",
              "relationship": "instance_of",
              "id": "6e8f43cb-7e64-41fc-93b4-119adfe87926",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "North America",
              "relationship": "part_of",
              "id": "0f4b1f78-9681-414a-91c6-576ed643941a",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            }
          ]
        }
      },
      {
        "name": "Sherlock Homles",
        "type": "ENTITY_UNKNOWN_TYPE",
        "relevance": 0.9516463011782174,
        "confidence": 1.0,
        "linked_entity": null
      },
      {
        "name": "Albert Einstein",
        "type": "PERSON",
        "relevance": 0.95080732382989,
        "confidence": 1.0,
        "linked_entity": {
          "name": "Albert Einstein",
          "id": "0fdb37f6-f575-4b4d-91e9-fbff57eae0ab",
          "confidence": 1.0,
          "relevance": 0.9695742180192723,
          "concepts": [
            {
              "name": "pedagogue",
              "relationship": "occupation",
              "id": "1439eb14-2988-43cc-865d-ad5a60d3ea62",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "philosopher of science",
              "relationship": "occupation",
              "id": "eefb9bbf-e617-4434-abb2-56b5853abd3a",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "university teacher",
              "relationship": "occupation",
              "id": "bb2c4745-4116-46ef-a122-c28c2f902026",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "science writer",
              "relationship": "occupation",
              "id": "5084431d-9073-45cb-be82-4a6898becd5b",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "non-fiction writer",
              "relationship": "occupation",
              "id": "57cc1f7b-5391-458b-9303-ec35b3ba01a4",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "patent examiner",
              "relationship": "occupation",
              "id": "d3f10fc5-ca81-4049-8c48-3d935552d9e7",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "philosopher",
              "relationship": "occupation",
              "id": "04d3cd32-68ad-4b71-9231-bdf3acfb09b2",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "scientist",
              "relationship": "occupation",
              "id": "dc8c068b-aa75-4ece-acd7-06fa304964fb",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "physicist",
              "relationship": "occupation",
              "id": "56ac942c-12a2-42c1-b10c-d1394a7971af",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "teacher",
              "relationship": "occupation",
              "id": "c70301bd-bcf4-47ab-b958-b983f0b0a6bd",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "human",
              "relationship": "instance_of",
              "id": "ead8a1d7-f901-44e6-b80f-63ebbbca4ffe",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "professor",
              "relationship": "occupation",
              "id": "c6d691f2-1e26-49fd-8481-58cb2d64d3e9",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "mathematician",
              "relationship": "occupation",
              "id": "23bf46db-a69a-4546-b18a-690a41144caa",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "theoretical physics",
              "relationship": "field_of_work",
              "id": "d6c03027-4efd-49d6-a7e5-ac4994c9143e",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "theoretical physicist",
              "relationship": "occupation",
              "id": "eedb6531-c2bf-4d05-af92-6f21751bc894",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "inventor",
              "relationship": "occupation",
              "id": "7baf322e-5913-4e2a-997a-90a039b0ff5c",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "writer",
              "relationship": "occupation",
              "id": "4c4c287c-0d83-4da3-b8c7-26df5adc9b33",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            }
          ]
        }
      },
      {
        "name": "Toronto",
        "type": "GPE",
        "relevance": 0.9370046727951885,
        "confidence": 1.0,
        "linked_entity": {
          "name": "Toronto",
          "id": "762db630-b272-4828-b1af-e7c65334e1d3",
          "confidence": 1.0,
          "relevance": 0.9608202651283239,
          "concepts": [
            {
              "name": "provincial or territorial capital city in Canada",
              "relationship": "instance_of",
              "id": "d7447629-e940-43b1-a726-4ac3f675410c",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "city",
              "relationship": "instance_of",
              "id": "d9d95c34-a2ce-4098-bd9d-3616b85620a8",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "big city",
              "relationship": "instance_of",
              "id": "68275742-3451-40af-8f5a-84211953a438",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "single-tier municipality",
              "relationship": "instance_of",
              "id": "a0f67ef3-52bb-44d9-bc52-9059d37c6d0c",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "city with millions of inhabitants",
              "relationship": "instance_of",
              "id": "b08def76-4b71-4545-9efb-f4858aaf253d",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            }
          ]
        }
      },
      {
        "name": "vacation",
        "type": "KEY_PHRASE",
        "relevance": 0.933964522339908,
        "confidence": 1.0,
        "linked_entity": null
      }
    ],
    "detected_languages": [
      {
        "language": "en",
        "confidence": 0.9999951616458576
      }
    ],
    "word_count": 183
  }
]   
}
```
