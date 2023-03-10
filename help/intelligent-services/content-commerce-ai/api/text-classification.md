---
keywords: 文本分類；文本分類
solution: Experience Platform
title: 內容與商務AI API中的文字分類
description: 文字分類服務在提供文字片段時，可將其分類為一或多個標籤。 分類可以是單一標籤、多標籤或階層。
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 4%

---

# 文字分類

>[!NOTE]
>
>內容與商務AI正在測試中。 說明檔案可能會有所變更。

文字分類服務在提供文字片段時，可將其分類為一或多個標籤。 分類可以是單一標籤、多標籤或階層。

**API格式**

```http
POST /services/v1/predict
```

**要求**

下列要求會根據裝載中提供的輸入參數來分類片段中的文字。 如需所示輸入參數的詳細資訊，請參閱範例裝載下方的表格。

>[!CAUTION]
>
>`analyzer_id` 決定 [!DNL Sensei Content Framework] 中所有規則的URL區段。 請確認您有 `analyzer_id` 之後再提出要求。 請連絡內容與商務AI測試版團隊，接收您的 `analyzer_id` 服務。

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
| `analyzer_id` | 此 [!DNL Sensei] 請求部署的服務ID。 此ID決定 [!DNL Sensei Content Frameworks] 中所有規則的URL區段。 如需自訂服務，請連絡內容與商務AI團隊以設定自訂ID。 | 是 |
| `application-id` | 已建立的應用程式ID。 | 是 |
| `data` | 陣列，包含JSON物件，陣列中每個物件代表檔案。 作為此陣列的一部分傳遞的任何參數都將覆蓋在 `data` 陣列。 下表中概述的任何剩餘屬性都可以從內覆蓋 `data`. | 是 |
| `language` | 輸入文本的語言。 預設值為 `en`。 | 無 |
| `content-type` | 用來指出輸入是請求內文的一部分，還是S3貯體的已簽署URL。 此屬性的預設值為 `inline`. | 無 |
| `encoding` | 輸入文本的編碼格式。 這可以是 `utf-8` 或 `utf-16`. 此屬性的預設值為 `utf-8`. | 無 |
| `threshold` | 需要返回結果的分數（0到1）的閾值。 使用值 `0` 返回所有結果。 此屬性的預設值為 `0`. | 無 |
| `top-N` | 要傳回的結果數（不能是負整數）。 使用值 `0` 返回所有結果。 搭配使用時 `threshold`，傳回的結果數是任一限制集的較小者。 此屬性的預設值為 `0`. | 無 |
| `custom` | 要傳遞的任何自訂參數。 此屬性需要有效的JSON物件才能運作。 | 無 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 若未傳遞，則會指派自動產生的ID。 | 無 |
| `content` | 文字分類服務使用的內容。 內容可以是原始文字（「內嵌」內容類型）。 <br> 如果內容是S3上的檔案(&#39;s3-bucket&#39; content-type)，請傳遞已簽署的URL。 | 是 |

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
