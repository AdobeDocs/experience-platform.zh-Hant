---
keywords: 文字分類；文字分類
solution: Experience Platform
title: 內容和Commerce AI API中的文字分類
description: 文字分類服務在提供文字片段時，可以將它分類為一個或多個標籤。 分類可以是單一標籤、多標籤或階層式。
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 4%

---

# 文字分類

>[!NOTE]
>
>內容和Commerce AI為測試版。 檔案內容可能會有所變更。

文字分類服務在提供文字片段時，可以將它分類為一個或多個標籤。 分類可以是單一標籤、多標籤或階層式。

**API格式**

```http
POST /services/v1/predict
```

**要求**

以下請求會根據承載中提供的輸入引數來分類片段中的文字。 請參閱裝載範例下表，以取得有關所示輸入引數的詳細資訊。

>[!CAUTION]
>
>`analyzer_id`決定使用哪個[!DNL Sensei Content Framework]。 提出要求前，請檢查您是否擁有適當的`analyzer_id`。 請連絡內容與Commerce AI測試版團隊，接收此服務的`analyzer_id`。

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

| 屬性 | 說明 | 強制 |
| --- | --- | --- |
| `analyzer_id` | 您的要求部署所在的[!DNL Sensei]服務ID。 此ID決定使用[!DNL Sensei Content Frameworks]中的哪一個。 若要自訂服務，請聯絡內容和Commerce AI團隊以設定自訂ID。 | 是 |
| `application-id` | 建立的應用程式ID。 | 是 |
| `data` | 一個陣列，其中包含JSON物件，且陣列中的每個物件分別代表一個檔案。 作為此陣列的一部分傳遞的任何引數都會覆寫`data`陣列外部指定的全域引數。 此表格中下面列出的任何剩餘屬性都可以從`data`內覆寫。 | 是 |
| `language` | 輸入文字的語言。 預設值為 `en`。 | 無 |
| `content-type` | 用於指出輸入是請求內文的一部分，還是S3儲存貯體的已簽署URL。 此屬性的預設值為`inline`。 | 無 |
| `encoding` | 輸入文字的編碼格式 這可以是`utf-8`或`utf-16`。 此屬性的預設值為`utf-8`。 | 無 |
| `threshold` | 分數（0至1）的臨界值，超過該臨界值即需要傳回結果。 使用值`0`傳回所有結果。 此屬性的預設值為`0`。 | 無 |
| `top-N` | 要傳回的結果數目（不能為負整數）。 使用值`0`傳回所有結果。 當與`threshold`一起使用時，傳回的結果數是設定的任一限制中的較小值。 此屬性的預設值為`0`。 | 無 |
| `custom` | 任何要傳遞的自訂引數。 此屬性需要有效的JSON物件才能運作。 | 無 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 如果未傳遞，則會指派自動產生的ID。 | 無 |
| `content` | 文字分類服務使用的內容。 內容可以是原始文字（「inline」內容型別）。 <br>如果內容是S3 （&#39;s3-bucket&#39;內容型別）上的檔案，請傳遞已簽署的URL。 | 是 |

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
