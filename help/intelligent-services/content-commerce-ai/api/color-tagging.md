---
keywords: Experience Platform；快速入門；內容ai；商務ai；內容標籤；顏色標籤；顏色擷取；
solution: Experience Platform
title: 內容標籤API中的顏色標籤
description: 給定影像時，顏色標籤服務可計算像素顏色的色階分佈圖，並依主色將其排序為貯體。
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 4%

---

# 顏色標籤

給定影像時，顏色標籤服務可計算像素顏色的色階分佈圖，並依主色將其排序為貯體。 影像像素中的顏色被分組成40種主要顏色，這些顏色代表色譜。 然後，在這40種顏色中計算顏色值的直方圖。 服務有兩種變體：

**顏色標籤（完整影像）**

此方法會擷取整個影像的色彩色階分佈圖。

**顏色標籤（含遮色片）**

此方法使用基於深度學習的前景提取器來識別前景中的對象。 該模型在電子商務影像目錄上進行培訓。 一旦提取前景對象，就像先前所述，在主色上計算直方圖。

本檔案所示範例中使用了下列影像：

![測試影像](../images/QQAsset1.jpg)

**API格式**

```http
POST /services/v2/predict
```

**要求**

下列範例要求使用完整影像方法進行顏色標籤。

下列要求會根據有效負載中提供的輸入參數，從影像中擷取顏色。 如需所示輸入參數的詳細資訊，請參閱範例裝載下方的表格。

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "application-id": "1234",
        "enable_mask": 0
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
-F 'infile_1=@1431RDMJANELLERAWJACKE_2.jpg'
```

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| `application-id` | 已建立應用程式的ID。 | 是 |
| `documents` | JSON元素的清單，清單中的每個項目代表一個檔案。 | 是 |
| `top_n` | 要傳回的結果數（不能是負整數）。 使用值 `0` 返回所有結果。 搭配使用時 `threshold`，傳回的結果數是任一限制集的較小者。 此屬性的預設值為 `0`. | 無 |
| `min_coverage` | 需要返回結果的覆蓋範圍閾值。 排除參數以傳回所有結果。 | 無 |
| `resize_image` | 指示輸入影像是否要調整大小。 在執行顏色標籤之前，預設會將影像調整為320*320像素。 為了偵錯目的，我們可將此值設為False，以允許程式碼在完整影像上執行。 | 無 |
| `enable_mask` | 啟用/停用遮色片內的顏色標籤。 | 無 |

| 名稱 | 資料類型 | 必填 | 預設 | 值 | 說明 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 字串 | - | - | - | 要從中提取關鍵片語的文檔的預簽URL。 |
| `sensei:repoType` | 字串 | - | - | HTTPS | 儲存影像的存放庫類型。 |
| `sensei:multipart_field_name` | 字串 | - | - | - | 以多部分引數傳遞影像檔案時，請使用此選項，而非使用預先簽署的url。 |
| `dc:format` | 字串 | 是 | - | &quot;image/jpg&quot;, <br> &quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | 在處理之前，會根據允許的輸入編碼類型檢查影像編碼。 |

**回應**

成功的回應會傳回擷取顏色的詳細資訊。 每種顏色由 `feature_value` 索引鍵，其中包含下列資訊：

- 顏色名稱
- 此顏色相對於影像的百分比
- 顏色的RGB值

在下方的第一個範例物件中， `feature_value` of `Mud_Green,0.069,102,72,95` 指發現的顏色是泥綠，泥綠在影像的6.9%中，RGB值為102,72,95。

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
{
  "statuses": [
    {
      "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
      "invocations": [
        {
          "sensei:outputs": {
            "result": {
              "sensei:multipart_field_name": "result",
              "dc:format": "application/json"
            }
          },
          "message": null,
          "status": "200"
        }
      ]
    }
  ],
  "request_id": "hsxycVq5Q9KbZ7MWrt6NXcSNWbonSLf3"
}

[
  {
    "request_element_id": "0",
    "colors": {
      "Mud_Green": {
        "coverage": 0.0694,
        "rgb": {
          "red": 102,
          "blue": 72,
          "green": 95
        }
      },
      "Dark_Brown": {
        "coverage": 0.1226,
        "rgb": {
          "red": 113,
          "blue": 77,
          "green": 84
        }
      },
      "Pink": {
        "coverage": 0.0731,
        "rgb": {
          "red": 234,
          "blue": 201,
          "green": 209
        }
      },
      "Dark_Gray": {
        "coverage": 0.1533,
        "rgb": {
          "red": 63,
          "blue": 58,
          "green": 59
        }
      },
      "Olive": {
        "coverage": 0.492,
        "rgb": {
          "red": 177,
          "blue": 126,
          "green": 170
        }
      },
      "Brown": {
        "coverage": 0.0896,
        "rgb": {
          "red": 141,
          "blue": 85,
          "green": 105
        }
      }
    }
  }
]
}
```
