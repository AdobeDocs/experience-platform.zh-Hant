---
keywords: text classification;Text classification
solution: Experience Platform
title: 文字分類API端點
topic: Developer guide
description: 文字分類服務在給定文字片段時，可將其分類為一或多個標籤。 分類可以是單一標籤、多標籤或階層式。
translation-type: tm+mt
source-git-commit: e69f4e8ddc0fe5f7be2b2b2bd89c09efdfca8e75
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 4%

---


# 文字分類

>[!NOTE]
>
>內容與商務AI為測試版。 說明檔案可能會有所變更。

文字分類服務在給定文字片段時，可將其分類為一或多個標籤。 分類可以是單一標籤、多標籤或階層式。

文字分類使用 [FastText](https://fasttext.cc/) ，其模型已使用自訂資料進行訓練。

**API格式**

```http
POST /services/v1/predict
```

**請求**

以下請求根據有效載荷中提供的輸入參數對片段中的文本進行分類。 請參閱範例裝載下表，以取得有關所示輸入參數的詳細資訊。

>[!CAUTION]
>
>`analyzer_id` 決定使 [!DNL Sensei Content Framework] 用的項目。 在提出要求前，請先檢查 `analyzer_id` 您是否有適當。

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
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"Server and Workstation Processors, Microcode Update is a self-extracting executable file containing the latest beta microcode updates (System Configuration Data) and software license agreement.\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
         "parameters": {}
    }]
}'
```

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| `analyzer_id` | 您 [!DNL Sensei] 的請求所部署的服務ID。 此ID決定使用哪 [!DNL Sensei Content Frameworks] 個。 | 是 |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `data` | 包含JSON物件的陣列，其中每個物件都代表檔案。 作為此陣列的一部分傳遞的任何參數都將覆蓋在陣列外部指定的全 `data` 局參數。 下表中概述的任何其他屬性都可從中覆蓋 `data`。 | 是 |
| `language` | 輸入文字的語言。 預設值為 `en`。 | 無 |
| `content-type` | 用於指出輸入是請求內文的一部分，還是S3儲存貯體的已簽署URL。 此屬性的預設值為 `inline`。 | 無 |
| `encoding` | 輸入文字的編碼格式。 這可以是 `utf-8` 或 `utf-16`。 此屬性的預設值為 `utf-8`。 | 無 |
| `threshold` | 需要傳回結果的分數臨界值（0到1）。 使用值可 `0` 傳回所有結果。 此屬性的預設值為 `0`。 | 無 |
| `top-N` | 要傳回的結果數（不能是負整數）。 使用值可 `0` 傳回所有結果。 當與搭配使用時， `threshold`傳回的結果數量會是任一限制集的較小者。 此屬性的預設值為 `0`。 | 無 |
| `custom` | 要傳遞的任何自訂參數。 此屬性需要有效的JSON物件才能運作。 | 無 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 如果未傳遞此資訊，則會指派自動產生的ID。 | 無 |
| `content` | 文字分類服務所使用的內容。 內容可以是原始文字（「內嵌」內容類型）。 <br> 如果內容是S3(&#39;s3-bucket&#39; content-type)上的檔案，請傳遞已簽署的URL。 | 是 |

**回應**

成功的回應會傳回回應陣列中的分類文字。

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_name": "abc123",
            "feature_value": [
              {
                "feature_value": [
                  {
                    "feature_value": 0.6899315714836121,
                    "feature_name": "Embedded & IoT"
                  }
                ],
                "feature_name": "labels"
              },
              {
                "feature_name": "status",
                "feature_value": "success"
              }
            ]
          }
        ]
      }
    }
  ],
  "error": []
}
```
