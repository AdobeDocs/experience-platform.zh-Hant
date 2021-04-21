---
keywords: Experience Platform; home；熱門主題；通知
description: 透過訂閱Adobe I/O事件，您可以使用網頁勾點來接收有關來源連線之流程執行狀態的通知。 這些通知包含有關流式執行成功或導致執行失敗的錯誤的資訊。
solution: Experience Platform
title: 流量執行通知
topic-legacy: overview
exl-id: 0f1cde97-3030-4b8e-be08-21f64e78b794
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# 流量執行通知

Adobe Experience Platform允許從外部來源接收資料，同時提供使用[!DNL Platform]服務構建、標籤和增強傳入資料的能力。 您可以從多種來源收錄資料，例如Adobe應用程式、雲端儲存空間、資料庫等。

[[!DNL Adobe Experience Platform Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) 用於收集和集中來自內部不同來源的客戶資料 [!DNL Platform]。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

有了Adobe I/O事件，您可以訂閱事件，並使用網頁勾點來接收有關流程執行狀態的通知。 這些通知包含有關流式執行成功或導致執行失敗的錯誤的資訊。

本檔案提供如何訂閱事件、註冊網頁勾選和接收通知的步驟，其中包含有關您流程執行狀態的資訊。

## 快速入門

本教學課程假設您至少已建立了一個源連接，其流運行要監視。 如果您尚未配置源連接，請首先訪問[源概述](./home.md)以配置您選擇的源，然後再返回本指南。

本檔案也要求您瞭解網頁勾點，以及如何將網頁勾點從一個應用程式連接至另一個應用程式。 有關Webhook的簡介，請參閱[[!DNL I/O Events] documentation](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md)。

## 註冊網路掛接以取得流程執行通知

若要接收流程執行通知，您必須使用Adobe開發人員主控台來註冊您的[!DNL Experience Platform]整合的網頁掛接。

請依照[訂閱 [!DNL I/O Event] 通知](../observability/notifications/subscribe.md)的教學課程，瞭解如何完成此作業的詳細步驟。

>[!IMPORTANT]
>
>在訂閱程式中，請確定您選擇&#x200B;**[!UICONTROL Platform notifications]**&#x200B;作為事件提供者，並選取下列事件訂閱：
>
>* **[!UICONTROL Experience Platform Source's Flow Run Succeeded]**
>* **[!UICONTROL Experience Platform Source's Flow Run Failed]**


## 接收流量執行通知

連線網頁掛接並完成事件訂閱後，您就可以開始透過網頁掛接控制面板接收流量執行通知。

通知會傳回執行的擷取工作數、檔案大小和錯誤等資訊。 通知也會傳回與您以JSON格式執行的流程相關聯的裝載。 響應有效負載可分類為`sources_flow_run_success`或`sources_flow_run_failure`。

>[!IMPORTANT]
>
>如果流程建立過程中啟用了部分提取，則只有當錯誤數低於流程建立過程中設定的錯誤閾值百分比時，包含成功和失敗提取的流程才會標籤為`sources_flow_run_success`。 如果成功的流運行包含錯誤，這些錯誤仍將作為返回裝載的一部分被包括在內。

### 成功

成功的響應返回一組`metrics`，這些定義了特定流運行的特性，並且`activities`概述了如何轉換資料。

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
    "imsOrgId": "{IMS_ORG}",
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
              "fileInfo": "https://platform-int.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
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
        "imsOrgId": "{IMS_ORG}",
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
| `metrics` | 定義流運行中資料的特性。 |
| `activities` | 定義轉換資料所執行的不同步驟和活動。 |
| `durationSummary` | 定義流運行的開始和結束時間。 |
| `sizeSummary` | 定義資料的卷（以位元組為單位）。 |
| `recordSummary` | 定義資料的記錄計數。 |
| `fileSummary` | 定義資料的檔案計數。 |
| `fileInfo` | 導致成功收錄檔案概覽的URL。 |
| `statusSummary` | 定義流運行是成功還是失敗。 |

### 失敗

以下響應是失敗的流運行示例，在處理複製的資料時出現錯誤。 從來源複製資料時，也可能發生錯誤。 失敗的流程運行包含導致運行失敗的錯誤的相關資訊，包括其錯誤和說明。

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{IMS_ORG}",
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
          "imsOrgId": "{IMS_ORG}",
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
| `fileInfo` | URL，可導致成功和未成功收錄檔案的概述。 |

>[!NOTE]
>
>有關錯誤消息的詳細資訊，請參見[附錄](#errors)。

## 後續步驟

您現在可以訂閱事件，讓您接收有關流程執行狀態的即時通知。 有關流運行和源的詳細資訊，請參閱[源概述](./home.md)。

## 附錄

以下章節提供使用流程執行通知的其他資訊。

### 瞭解錯誤消息{#errors}

當從來源複製資料或將複製的資料處理至[!DNL Platform]時，可能會發生擷取錯誤。 有關特定錯誤的詳細資訊，請參閱下表。

| 錯誤 | 說明 |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | 從源複製資料時出錯。 |
| `CONNECTOR-2001-500` | 將複製的資料處理到[!DNL Platform]時出錯。 此錯誤可能與剖析、驗證或轉換有關。 |
