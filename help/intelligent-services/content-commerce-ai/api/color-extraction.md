---
keywords: Experience Platform；入門；內容ai；商務ai；內容與商務ai；顏色提取；顏色提取
solution: Experience Platform, Intelligent Services
title: 內容與商務AI API中的顏色提取
topic-legacy: Developer guide
description: 當給定影像時，顏色提取服務可以計算像素顏色的直方圖，並按主色排序到桶中。
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# 色彩擷取

>[!NOTE]
>
>[!DNL Content and Commerce AI] 是測試版。說明檔案可能會有所變更。

當給定影像時，色彩擷取服務可計算像素色彩的色階分佈圖，並依主色排序成桶。 影像像素中的顏色被分成40種主要顏色，這些顏色代表色譜。 然後，在這40種顏色中計算顏色值的直方圖。 該服務有兩種變體：

**色彩擷取（完整影像）**

此方法會擷取整個影像的色彩色階分佈圖。

**色彩擷取（含遮色片）**

該方法採用基於深度學習的前景提取器來識別前景中的對象。 該模型在電子商務影像目錄上進行培訓。 一旦提取前景對象，就像先前所述那樣計算佔優勢顏色的直方圖。

本文檔中的示例使用了以下影像：

![測試影像](../images/QQAsset1.jpg)

**API格式**

```http
POST /services/v1/predict
```

**要求**

下列範例要求使用完整影像方法進行色彩擷取。

下列請求基於在有效載荷中提供的輸入參數從影像中提取顏色。 請參閱範例裝載下表，以取得有關所示輸入參數的詳細資訊。

>[!CAUTION]
>
>`analyzer_id` 決定使 [!DNL Sensei Content Framework] 用的項目。請在提出要求之前，先檢查您是否有正確的`analyzer_id`。 對於顏色提取服務，`analyzer_id` ID為：
>`Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7`

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'cache-control: no-cache,no-cache' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7",
         "parameters": {
          "application-id": "1234", 
          "content-type": "inline", 
          "encoding": "jpeg", 
          "threshold": "0", 
          "top-N": "0", 
          "custom": {}, 
          "data": [{
            "content-id": "0987", 
            "content": "inline-image", 
            "content-type": "inline", 
            "encoding": "jpeg", 
            "threshold": "0", 
            "top-N": "0", 
            "historic-metadata": [], 
            "custom": {"exclude_mask": 1}
            }]
          }
      }
    ]
}'
```

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| `analyzer_id` | 您的請求部署在下的[!DNL Sensei]服務ID。 此ID決定使用哪個[!DNL Sensei Content Frameworks]。 如需自訂服務，請聯絡「內容與商務AI」團隊以設定自訂ID。 | 是 |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `data` | 包含JSON物件的陣列。 陣列中的每個對象都代表一個影像。 作為此陣列的一部分傳遞的任何參數都將覆蓋在`data`陣列外指定的全局參數。 下表中概述的任何其他屬性都可從`data`中覆寫。 | 是 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 如果未傳遞此資訊，則會指派自動產生的ID。 | 無 |
| `content` | 要由顏色提取服務分析的內容。 如果影像是請求主體的一部分，請在curl命令中使用`-F file=@<filename>`來傳遞影像，將此參數保留為空字串。 <br> 如果影像是S3上的檔案，請傳遞已簽署的URL。當內容是請求內文的一部分時，資料元素清單應該只有一個物件。 如果傳遞多個物件，則只會處理第一個物件。 | 是 |
| `content-type` | 用於指出輸入是請求內文的一部分，還是S3儲存貯體的已簽署URL。 此屬性的預設值為`inline`。 | 無 |
| `encoding` | 輸入影像的檔案格式。 目前只能處理JPEG和PNG影像。 此屬性的預設值為`jpeg`。 | 無 |
| `threshold` | 需要傳回結果的分數臨界值（0到1）。 使用`0`值返回所有結果。 此屬性的預設值為`0`。 | 無 |
| `top-N` | 要傳回的結果數（不能是負整數）。 使用`0`值返回所有結果。 當與`threshold`搭配使用時，傳回的結果數量會小於任一限制集。 此屬性的預設值為`0`。 | 無 |
| `custom` | 要傳遞的任何自訂參數。 | 無 |
| `historic-metadata` | 可傳遞中繼資料的陣列。 | 無 |

**回應**

成功的回應會傳回擷取色彩的詳細資料。 每種顏色都由`feature_value`鍵表示，其中包含以下資訊：

- 顏色名稱
- 此顏色相對於影像顯示的百分比
- 顏色的RGB值

在下面的第一個範例物件中，`White,0.59,251,251,243`的`feature_value`表示所找到的顏色為白色，在影像的59%中為白色，且RGB值為251,251,243。

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-color-histogram:Service-e952f4acd7c2425199b476a2eb459635",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "White,0.59,251,251,243"
              },
              {
                "feature_value": "Orange,0.30,248,169,48",
                "feature_name": "color_name_and_rgb"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Mustard,0.08,251,199,77"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Gold,0.02,250,191,55"
              }
            ],
            "feature_name": "color"
          }
        ]
      }
    }
  ],
  "error": []
}
```

| 屬性 | 說明 |
| --- | --- |
| `content_id` | 在您的POST請求中上傳的影像名稱。 |
| `feature_value` | 其對象包含具有相同屬性名稱的鍵的陣列。 這些鍵包含一個字串，代表顏色名稱、此顏色相對於在`content_id`中傳送的影像顯示的百分比，以及顏色的RGB值。 |
