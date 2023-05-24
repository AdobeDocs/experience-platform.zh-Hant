---
keywords: Experience Platform；入門；內容；內容；標籤；顏色；顏色；color tagging;color extraction;
solution: Experience Platform
title: 內容標籤API中的顏色標籤
description: 當給定影像時，「顏色標籤」服務可以計算像素顏色的直方圖，並按主色將它們排序為桶。
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: fd8891bdc7d528e327d2a72c2427f7bbc6dc8a03
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 5%

---

# 顏色標籤

當給定影像時，顏色標籤服務可以計算像素顏色的直方圖並按主色將它們排序成桶。 影像像素中的顏色被分段成代表色譜的40種主要顏色。 然後，在這40種顏色中計算顏色值的直方圖。 該服務有兩個變型：

**顏色標籤（完整影像）**

該方法在整個影像上提取顏色直方圖。

**顏色標籤（帶蒙版）**

該方法採用基於深度學習的前景提取器來識別前景中的對象。 一旦提取前景對象，就在前景和背景區域以及整個影像的主色上計算直方圖。

**音調提取**

除上述變型外，您還可以配置服務以檢索以下內容的色調直方圖：

- 整個影像（使用完整影像變數時）
- 整體影像以及前景和背景區域（當將變數與掩碼一起使用時）

本文檔所示的示例中使用了以下影像：

![test影像](../images/QQAsset1.jpg)

**API格式**

```http
POST /services/v2/predict
```

**請求 — 完整映像變型**

以下示例請求使用全影像方法進行顏色標籤，並基於在負載中提供的輸入參數從影像中提取顏色。 有關所示輸入參數的詳細資訊，請參閱示例負載下表。

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

**響應 — 完整映像變型**

成功的響應返回提取顏色的詳細資訊。 每種顏色由 `feature_value` 鍵，其中包含以下資訊：

- 顏色名稱
- 此顏色相對於影像顯示的百分比
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

請注意，此處的結果在「整體」影像區域上提取了顏色。

**請求 — 已屏蔽的影像變數**

下面的示例請求使用掩碼方法進行顏色標籤。 通過設定 `enable_mask` 參數 `true` 中。

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
>此外， `retrieve_tone` 參數也設定為 `true` 上面的請求。 這使我們能夠在影像的整體、前景和背景區域中檢索溫、中和冷色調上的色調分佈直方圖。

**響應 — 掩碼影像變數**

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

除了整個影像中的顏色外，您現在還可以從前景和背景區域中看到顏色。 由於對上述每個區域都啟用了色調檢索，因此您還可以檢索色調的直方圖。

**輸入參數**

| 名稱 | 資料類型 | 必填 | 預設 | 值 | 說明 |
| --- | --- | --- | --- | --- | --- |
| `documents` | 陣列（文檔對象） | 是 | - | 請參閱下面 | JSON元素清單，其中每個項都代表一個文檔。 |
| `top_n` | 數字 | 無 | 0 | 非負整數 | 要返回的結果數。 0，返回所有結果。 與閾值結合使用時，返回的結果數將少於任一限制。 |
| `min_coverage` | 數字 | 無 | 0.05 | 實數 | 需要返回結果的覆蓋範圍閾值。 排除參數以返回所有結果。 |
| `resize_image` | 數字 | 無 | True | 真/假 | 是否調整輸入影像的大小。 預設情況下，在執行顏色提取之前，將影像調整到320*320像素。 為了進行調試，我們還可以通過將此代碼設定為 `False`。 |
| `enable_mask` | 數字 | 無 | False | 真/假 | 啟用/禁用顏色提取 |
| `retrieve_tone` | 數字 | 無 | False | 真/假 | 啟用/禁用音調提取 |

**文檔對象**

| 名稱 | 資料類型 | 必填 | 預設 | 值 | 說明 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 字串 | - | - | - | 文檔的預簽名URL。 |
| `sensei:repoType` | 字串 | - | - | HTTPS | 儲存影像的回購類型。 |
| `sensei:multipart_field_name` | 字串 | - | - | - | 將影像檔案作為多部分參數傳遞時，請使用此選項，而不是使用預簽名的URL。 |
| `dc:format` | 字串 | 是 | - | &quot;影像/jpg&quot;,<br>&quot;影像/jpeg&quot;,<br>&quot;影像/png&quot;,<br>&quot;影像/tiff&quot; | 在處理之前，根據允許的輸入編碼類型檢查影像編碼。 |