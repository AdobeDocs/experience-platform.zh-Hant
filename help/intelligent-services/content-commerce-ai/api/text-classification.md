---
keywords: 文本分類；文本分類
solution: Experience Platform
title: 內容與商務AI API中的文本分類
description: 當給定文本片段時，文本分類服務可以將其分類為一個或多個標籤。 分類可以是單標籤、多標籤或分層。
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 4%

---

# 文本分類

>[!NOTE]
>
>內容和商務AI處於測試版。 文檔可能會更改。

當給定文本片段時，文本分類服務可以將其分類為一個或多個標籤。 分類可以是單標籤、多標籤或分層。

**API格式**

```http
POST /services/v1/predict
```

**要求**

以下請求基於在負載中提供的輸入參數對來自片段的文本進行分類。 有關所示輸入參數的詳細資訊，請參閱示例負載下表。

>[!CAUTION]
>
>`analyzer_id` 確定 [!DNL Sensei Content Framework] 的子菜單。 請檢查一下 `analyzer_id` 在你提出要求之前。 聯繫內容和商務AI測試團隊以接收您的 `analyzer_id` 為此服務。

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
| `analyzer_id` | 的 [!DNL Sensei] 部署請求的服務ID。 此ID確定 [!DNL Sensei Content Frameworks] 的子菜單。 有關自定義服務，請與Content and Commerce AI團隊聯繫以設定自定義ID。 | 是 |
| `application-id` | 已建立的應用程式的ID。 | 是 |
| `data` | 包含JSON對象的陣列，其中每個對象都位於表示文檔的陣列中。 作為此陣列的一部分傳遞的任何參數都將覆蓋在 `data` 陣列。 此表中概述的任何剩餘屬性都可以從中覆蓋 `data`。 | 是 |
| `language` | 輸入文本的語言。 預設值為 `en`。 | 無 |
| `content-type` | 用於指示輸入是請求正文的一部分還是S3儲存段的帶簽名URL。 此屬性的預設值為 `inline`。 | 無 |
| `encoding` | 輸入文本的編碼格式。 這可以是 `utf-8` 或 `utf-16`。 此屬性的預設值為 `utf-8`。 | 無 |
| `threshold` | 需要返回結果的分數（0到1）的閾值。 使用值 `0` 返回所有結果。 此屬性的預設值為 `0`。 | 無 |
| `top-N` | 要返回的結果數（不能為負整數）。 使用值 `0` 返回所有結果。 與 `threshold`，返回的結果數是任一限制集的較小值。 此屬性的預設值為 `0`。 | 無 |
| `custom` | 要傳遞的任何自定義參數。 此屬性需要有效的JSON對象才能運行。 | 無 |
| `content-id` | 響應中返回的資料元素的唯一ID。 如果未傳遞此資訊，則會分配自動生成的ID。 | 無 |
| `content` | 文本分類服務使用的內容。 內容可以是原始文本（「內聯」內容類型）。 <br> 如果內容是S3(&#39;s3-bucket&#39; content-type)上的檔案，請傳遞帶簽名的URL。 | 是 |

**回應**

成功的響應返迴響應陣列中的分類文本。

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
