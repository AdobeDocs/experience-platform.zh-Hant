---
keywords: Experience Platform；快速入門；內容；內容標籤；顏色標籤；顏色擷取；
solution: Experience Platform
title: 內容標籤API中的顏色標籤
description: 給定影像時，「顏色標籤」服務可計算像素顏色的色階分佈圖，並依主色將其排序為貯體。
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: fd8891bdc7d528e327d2a72c2427f7bbc6dc8a03
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 5%

---

# 顏色標籤

給定影像時，顏色標籤服務可計算像素顏色的色階分佈圖，並依主色將其排序為貯體。 影像像素中的顏色被分組成40種主要顏色，這些顏色代表色譜。 然後，在這40種顏色中計算顏色值的直方圖。 服務有兩種變體：

**顏色標籤（完整影像）**

此方法會擷取整個影像的色彩色階分佈圖。

**顏色標籤（含遮色片）**

此方法使用基於深度學習的前景提取器來識別前景中的對象。 一旦提取前景對象，就會根據前景和背景區域以及整個影像的主色來計算直方圖。

**色調提取**

除了上述變體外，您還可以設定服務以擷取以下項目的色調色階分佈圖：

- 整體影像（使用完整影像變體時）
- 整體影像、前景和背景區域（當使用帶掩碼的變體時）

本檔案所示範例中使用了下列影像：

![測試影像](../images/QQAsset1.jpg)

**API格式**

```http
POST /services/v2/predict
```

**請求 — 完整影像變體**

下列範例要求使用完整影像方法進行顏色標籤，並根據有效負載中提供的輸入參數從影像中擷取顏色。 如需所示輸入參數的詳細資訊，請參閱範例裝載下方的表格。

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005      
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

**回應 — 完整影像變體**

成功的回應會傳回擷取顏色的詳細資訊。 每種顏色由 `feature_value` 索引鍵，其中包含下列資訊：

- 顏色名稱
- 此顏色相對於影像的百分比
- 顏色的RGB值

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`表示所找到的顏色為白色，在影像的58.34%中找到，其平均RGB值為254、254、243。

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "bfpzaJxKDxtgxpjUj5QDrN1jasjUw2RM"
}  
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        }
    }
}]
```

請注意，此處的結果是在「整體」影像區域上擷取顏色。

**請求 — 遮罩的影像變體**

下列範例要求使用遮罩方法進行顏色標籤。 這可透過設定 `enable_mask` 參數 `true` 中。

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005,
        "enable_mask": true,
        "retrieve_tone": true     
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

>[!NOTE]
>
>此外， `retrieve_tone` 參數也設為 `true` 中。 這使我們能夠在影像的整體、前景和背景區域中檢索溫、中和和涼爽色調上的色調分佈直方圖。

**回應 — 遮罩的影像變體**

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "gpeCyJsrJvOWd94WwZOyPBPrKi2BQyla"
}  
 
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        },
        "tones": {
            "warm": 0.4084,
            "neutral": 0.5916,
            "cool": 0
        }
    },
    "foreground": {
        "colors": {
            "Orange": {
                "coverage": 0.6022,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.1935,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.1722,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0173,
                "rgb": {
                    "red": 253,
                    "green": 235,
                    "blue": 170
                }
            },
            "Yellow": {
                "coverage": 0.0148,
                "rgb": {
                    "red": 254,
                    "green": 229,
                    "blue": 117
                }
            }
        },
        "tones": {
            "warm": 0.9827,
            "neutral": 0.0173,
            "cool": 0
        }
    },
    "background": {
        "colors": {
            "White": {
                "coverage": 0.9923,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Dark_Brown": {
                "coverage": 0.0077,
                "rgb": {
                    "red": 83,
                    "green": 68,
                    "blue": 57
                }
            }
        },
        "tones": {
            "warm": 0,
            "neutral": 1.0,
            "cool": 0
        }
    }
}]
```

除了整體影像中的顏色之外，您現在還可以從前景和背景區域中看到顏色。 由於已為上述每個區域啟用色調檢索，因此您也可以檢索色調的直方圖。

**輸入參數**

| 名稱 | 資料類型 | 必填 | 預設 | 值 | 說明 |
| --- | --- | --- | --- | --- | --- |
| `documents` | array(Document-Object) | 是 | - | 請參閱下方 | JSON元素清單，清單中的每個項目代表一個檔案。 |
| `top_n` | 數字 | 無 | 0 | 非負整數 | 要返回的結果數。 0，返回所有結果。 與臨界值搭配使用時，傳回的結果數量會少於任一限制。 |
| `min_coverage` | 數字 | 無 | 0.05 | 實數 | 需要返回結果的覆蓋範圍閾值。 排除參數以傳回所有結果。 |
| `resize_image` | 數字 | 無 | True | True/False | 是否調整輸入影像的大小。 在執行顏色提取之前，預設會將影像調整為320*320像素。 為了偵錯目的，我們也可以將此設為，讓程式碼在完整影像上執行 `False`. |
| `enable_mask` | 數字 | 無 | False | True/False | 啟用/停用顏色提取 |
| `retrieve_tone` | 數字 | 無 | False | True/False | 啟用/禁用音調提取 |

**文檔對象**

| 名稱 | 資料類型 | 必填 | 預設 | 值 | 說明 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 字串 | - | - | - | 文檔的預簽URL。 |
| `sensei:repoType` | 字串 | - | - | HTTPS | 儲存影像的存放庫類型。 |
| `sensei:multipart_field_name` | 字串 | - | - | - | 以多部分引數傳遞影像檔案時，請使用此選項，而非使用預先簽署的URL。 |
| `dc:format` | 字串 | 是 | - | &quot;image/jpg&quot;,<br>&quot;image/jpeg&quot;,<br>&quot;image/png&quot;,<br>&quot;image/tiff&quot; | 在處理之前，會根據允許的輸入編碼類型檢查影像編碼。 |