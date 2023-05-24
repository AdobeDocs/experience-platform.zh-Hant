---
keywords: Experience Platform；首頁；熱門主題；通知
description: 通過訂閱「Adobe I/O事件」，您可以使用webhook來接收有關源連接的流運行狀態的通知。 這些通知包含有關流運行成功或導致運行失敗的錯誤的資訊。
solution: Experience Platform
title: 流運行通知
exl-id: 0f1cde97-3030-4b8e-be08-21f64e78b794
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# 流運行通知

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 用於收集和集中來自不同來源的客戶資料 [!DNL Platform]。 該服務提供了用戶介面和REST風格的API，所有支援的源都可從中連接。

使用Adobe I/O事件，您可以訂閱事件並使用webhook接收有關流運行狀態的通知。 這些通知包含有關流運行成功或導致運行失敗的錯誤的資訊。

本文檔提供了有關如何訂閱事件、註冊Webhook和接收包含有關流運行狀態資訊的通知的步驟。

## 快速入門

本教程假定您至少已建立了一個源連接，該源連接的流運行要監視。 如果尚未配置源連接，請首先訪問 [源概述](./home.md) 在返回本指南之前配置您選擇的源。

本文檔還要求瞭解Webhook以及如何將Webhook從一個應用程式連接到另一個應用程式。 請參閱 [[!DNL I/O Events] 文檔](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) 網鈎簡介。

## 註冊流運行通知的Webhook

要接收流運行通知，您必須使用Adobe Developer控制台向您的 [!DNL Experience Platform] 整合。

按照本教程 [訂閱[!DNL I/O事件]通知](../observability/alerts/subscribe.md) 詳細的步驟。

>[!IMPORTANT]
>
>在訂閱過程中，確保選擇 **[!UICONTROL 平台通知]** 作為事件提供程式，並選擇以下事件訂閱：
>
>* **[!UICONTROL Experience Platform源的流運行成功]**
>* **[!UICONTROL Experience Platform源的流運行失敗]**


## 接收流運行通知

在已連接Webhook並完成事件訂閱後，您可以開始通過Webhook儀表板接收流運行通知。

通知返回資訊，如運行的接收作業數、檔案大小和錯誤。 通知還返回與JSON格式的流運行關聯的負載。 響應負載可以被分類為 `sources_flow_run_success` 或 `sources_flow_run_failure`。

>[!IMPORTANT]
>
>如果在流建立過程中啟用了部分攝取，則包含成功攝取和失敗攝取的流將被標籤為 `sources_flow_run_success` 僅當錯誤數低於在流建立過程中設定的錯誤閾值百分比時。 如果成功的流運行包含錯誤，則這些錯誤仍將作為返回負載的一部分包括在內。

### 成功

成功的響應返回一組 `metrics` 定義特定流運行的特徵 `activities` 描述了資料是如何轉換的。

```json
{
  "event_id": "aec55616-1715-487f-8044-ba648cc8ffee",
  "event": {
    "createdAt": 1597213529158,
    "updatedAt": 1597213530760,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "7127a4f0-def8-11e9-83ce-e79494b1c2a5",
    "sandboxName": "prod",
    "imsOrgId": "{ORG_ID}",
    "id": "933cf9f4-cf01-4d75-bcf9-f4cf010d750a",
    "flowId": "1c6f1047-dcaf-48fe-af10-47dcaf08feaf",
    "providerRefId": "test1234",
    "etag": "\"5100ec97-0000-0200-0000-5f338b5b0000\"",
    "metrics": {
      "durationSummary": {
        "startedAtUTC": 1590512053,
        "completedAtUTC": 1590512053
      },
      "sizeSummary": {
        "inputBytes": 2048,
        "outputBytes": 1024
      },
      "recordSummary": {
        "inputRecordCount": 100,
        "outputRecordCount": 70
      },
      "fileSummary": {
        "inputFileCount": 10,
        "outputFileCount": 10
      },
      "statusSummary": {
        "status": "success"
      }
    },
    "activities": [
      {
        "id": "copyActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "startedAtUTC": 1590512053,
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 2048,
          "outputBytes": 1098
        },
        "recordSummary": {
          "inputRecordCount": 100,
          "outputRecordCount": 100
        },
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "adf/pipeline/id": "abcd",
            "adf/run/id": "1234"
          }
        },
        "sourceInfo": [
          {
            "id": "sourceConnectionId1",
            "type": "SourceConnection",
            "reference": {
              "type": "AdfRunId"
            }
          }
        ]
      },
      {
        "id": "promotionActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 1098,
          "outputBytes": 1024
        },
        "recordSummary": {},
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10,
          "extensions": {
            "manifest": {
              "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
            }
          }
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "batchId": "b1",
            "acp_request_id": "1234"
          }
        },
        "targetInfo": [
          {
            "id": "targetConnectionId1",
            "type": "TargetConnection",
            "reference": {
              "type": "batch"
            }
          }
        ]
      }
    ],
    "slaCreatedAt": 1597213531124,
    "processStartTime": 1597213531213,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
        "providerMetadata": "platform_notifications",
        "eventCode": "sources_flow_run_success"
      }
    },
    "transformedTime": 1597213531214
  }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `metrics` | 定義流運行中資料的特徵。 |
| `activities` | 定義為轉換資料而執行的不同步驟和活動。 |
| `durationSummary` | 定義流運行的開始和結束時間。 |
| `sizeSummary` | 定義資料的卷（以位元組為單位）。 |
| `recordSummary` | 定義資料的記錄計數。 |
| `fileSummary` | 定義資料的檔案計數。 |
| `fileInfo` | 一個URL，它導致成功攝取的檔案的概述。 |
| `statusSummary` | 定義流運行是成功還是失敗。 |

### 失敗

以下響應是失敗流運行的示例，在處理複製的資料時出錯。 在從源複製資料時也可能出錯。 失敗的流運行包含有關導致運行失敗的錯誤的資訊，包括其錯誤和說明。

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{ORG_ID}",
        "schema": {
          "name": "run-notification",
          "version": "1.0"
        },
        "provider": "FlowService",
        "_eventNotificationMeta": {
          "category": "Platform Notifications",
          "type": "sources_flow_run_failed"
        },
        "value": {
          "createdAt": 1597434147259,
          "updatedAt": 1597434157567,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "e49ebb00-d0fa-11e9-b164-ed6a398c8b35",
          "sandboxName": "prod",
          "imsOrgId": "{ORG_ID}",
          "id": "d9024c32-2174-4271-824c-322174627101",
          "flowId": "cf4fce79-8822-456d-8fce-798822556dc6",
          "etag": "\"0c003dbf-0000-0200-0000-5f36e92d0000\"",
          "metrics": {
            "durationSummary": {
              "startedAtUTC": 1597434147190
            },
            "sizeSummary": {
              "inputBytes": -1
            },
            "fileSummary": {
              "inputFileCount": -1
            },
            "statusSummary": {
              "status": "failed",
              "errors": [
                {
                  "code": "CONNECTOR-2001-500",
                  "message": "Error in processing (parsing, validation or transformation) the copied data."
                }
              ]
            }
          },
          "activities": [
            {
              "id": "promotionActivity",
              "updatedAtUTC": 1597434157529,
              "durationSummary": {
                "startedAtUTC": 1597434147190,
                "completedAtUTC": 1597434157212
              },
              "sizeSummary": {
                "inputBytes": -1
              },
              "recordSummary": {},
              "fileSummary": {
                "inputFileCount": -1,
                "extensions": {
                  "manifest": {
                    "fileInfo": "https://platform-stage.adobe.io/data/foundation/export/batches/6f6a900f-e40d-4f0e-9bb9-b614436c3465/meta?path=input_files"
                  }
                }
              },
              "statusSummary": {
                "status": "failed",
                "errors": [
                  {
                    "code": "CONNECTOR-2001-500",
                    "message": "Error in processing (parsing, validation or transformation) the copied data."
                  }
                ],
                "extensions": {
                  "errors": [
                    {
                      "code": "133",
                      "message": "We are unable to locate any files uploaded for this batch. Please upload files to ingest."
                    }
                  ]
                }
              },
              "targetInfo": [
                {
                  "id": "e88737aa-27b8-4795-8737-aa27b8f7959e",
                  "type": "TargetConnection",
                  "reference": {
                    "type": "Batch",
                    "ids": [
                      "6f6a900f-e40d-4f0e-9bb9-b614436c3465"
                    ]
                  }
                }
              ]
            }
          ]
        }
      }
    ]
  }
]
```

| 屬性 | 說明 |
| ---------- | ----------- |
| `fileInfo` | 一個URL，它導致對成功和未成功接收的檔案進行概述。 |

>[!NOTE]
>
>查看 [附錄](#errors) 的子菜單。

## 後續步驟

您現在可以訂閱允許您在流運行狀態上接收即時通知的事件。 有關流運行和源的詳細資訊，請參閱 [源概述](./home.md)。

## 附錄

以下各節提供了有關處理流運行通知的附加資訊。

### 瞭解錯誤消息 {#errors}

當從源複製資料或將複製的資料處理到 [!DNL Platform]。 有關特定錯誤的詳細資訊，請參閱下表。

| 錯誤 | 說明 |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | 從源複製資料時出錯。 |
| `CONNECTOR-2001-500` | 將複製的資料處理到時出錯 [!DNL Platform]。 此錯誤可能與分析、驗證或轉換有關。 |
