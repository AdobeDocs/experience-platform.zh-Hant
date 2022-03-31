---
keywords: Experience Platform；入門；內容；商務；內容和商務；顏色提取；顏色提取
solution: Experience Platform
title: 內容與商務AI API中的顏色提取
topic-legacy: Developer guide
description: 當給定影像時，顏色提取服務可以計算像素顏色的直方圖並按主色將它們排序成桶。
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# 顏色提取

>[!NOTE]
>
>[!DNL Content and Commerce AI] 是β 文檔可能會更改。

當給定影像時，顏色提取服務可以計算像素顏色的直方圖並按主色將它們排序成桶。 影像像素中的顏色被分段成代表色譜的40種主要顏色。 然後，在這40種顏色中計算顏色值的直方圖。 該服務有兩個變型：

**顏色提取（完整影像）**

該方法在整個影像上提取顏色直方圖。

**顏色提取（帶蒙版）**

該方法採用基於深度學習的前景提取器來識別前景中的對象。 該模型是在電子商務影像目錄上進行的。 一旦提取前景對象，就像先前描述的那樣在主色上計算直方圖。

本文檔所示的示例中使用了以下影像：

![test影像](../images/QQAsset1.jpg)

**API格式**

```http
POST /services/v1/predict
```

**要求**

下面的示例請求使用全影像方法進行顏色提取。

以下請求基於在負載中提供的輸入參數從影像中提取顏色。 有關所示輸入參數的詳細資訊，請參閱示例負載下表。

>[!CAUTION]
>
>`analyzer_id` 確定 [!DNL Sensei Content Framework] 的子菜單。 請檢查一下 `analyzer_id` 在你提出要求之前。 對於顏色提取服務， `analyzer_id` ID是：
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
| `analyzer_id` | 的 [!DNL Sensei] 部署請求的服務ID。 此ID確定 [!DNL Sensei Content Frameworks] 的子菜單。 有關自定義服務，請與Content and Commerce AI團隊聯繫以設定自定義ID。 | 是 |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `data` | 包含JSON對象的陣列。 陣列中的每個對象都表示影像。 作為此陣列的一部分傳遞的任何參數都將覆蓋在 `data` 陣列。 此表中概述的任何剩餘屬性都可以從中覆蓋 `data`。 | 是 |
| `content-id` | 響應中返回的資料元素的唯一ID。 如果未傳遞此資訊，則分配自動生成的ID。 | 無 |
| `content` | 由顏色提取服務分析的內容。 如果影像是請求主體的一部分，請使用 `-F file=@<filename>` 在curl命令中傳遞影像，將此參數保留為空字串。 <br> 如果影像是S3上的檔案，請傳遞帶簽名的URL。 當內容是請求正文的一部分時，資料元素清單應只有一個對象。 如果傳遞了多個對象，則只處理第一個對象。 | 是 |
| `content-type` | 用於指示輸入是請求正文的一部分還是S3儲存段的帶簽名URL。 此屬性的預設值為 `inline`。 | 無 |
| `encoding` | 輸入影像的檔案格式。 目前只能處理JPEG和PNG影像。 此屬性的預設值為 `jpeg`。 | 無 |
| `threshold` | 需要返回結果的分數（0到1）的閾值。 使用值 `0` 返回所有結果。 此屬性的預設值為 `0`。 | 無 |
| `top-N` | 要返回的結果數（不能為負整數）。 使用值 `0` 返回所有結果。 與 `threshold`，返回的結果數是任一限制集的較小值。 此屬性的預設值為 `0`。 | 無 |
| `custom` | 要傳遞的任何自定義參數。 | 無 |
| `historic-metadata` | 可傳遞元資料的陣列。 | 無 |

**回應**

成功的響應返回提取顏色的詳細資訊。 每種顏色由 `feature_value` 鍵，其中包含以下資訊：

- 顏色名稱
- 此顏色相對於影像顯示的百分比
- 顏色的RGB值

在下面的第一個示例對象中， `feature_value` 共 `White,0.59,251,251,243` 表示找到的顏色為白色，在影像的59%中找到白色，其RGB值為251,251,243。

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
| `content_id` | 在您的POST請求中上載的映像的名稱。 |
| `feature_value` | 對象包含具有相同屬性名稱的鍵的陣列。 這些鍵包含一個表示顏色名稱的字串，此顏色相對於在 `content_id`和顏色的RGB值。 |
