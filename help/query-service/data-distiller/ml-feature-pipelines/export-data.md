---
title: 將資料匯出至外部ML環境
description: 瞭解如何將使用Data Distiller建立的已準備好的訓練資料集共用到雲端儲存位置，讓ML環境可讀取該位置來訓練和評分您的模型。
source-git-commit: a23100e8fbca93f14490e639f05991f06c113b93
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 3%

---

# 將資料匯出至外部ML環境

本檔案會示範如何將使用Data Distiller建立的已準備好的訓練資料集共用至雲端儲存位置，讓ML環境可讀取該位置來訓練和評分您的模型。 此處的範例將訓練資料集匯出至 [資料登陸區(DLZ)](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/create/cloud-storage/data-landing-zone.html?lang=en). 您可以視需要變更儲存目的地，以搭配機器學習環境使用。

此 [目的地的流量服務](https://developer.adobe.com/experience-platform-apis/references/destinations/) 用於將已計算功能的資料集著陸至適當的雲端儲存位置，以完成功能管道。

## 建立來源連線 {#create-source-connection}

來源連線負責設定與您的Adobe Experience Platform資料集的連線，以便產生的流程能確切知道應在何處尋找資料以及採用何種格式。

```python
from aepp import flowservice
flow_conn = flowservice.FlowService()

training_dataset_id = <YOUR_TRAINING_DATASET_ID>

source_res = flow_conn.createSourceConnectionDataLake(
    name=f"[CMLE] Featurized Dataset source connection created by {username}",
    dataset_ids=[training_dataset_id],
    format="parquet"
)
source_connection_id = source_res["id"]
```

## 建立目標連線 {#create-target-connection}

目標連線負責連線到目的地檔案系統。 這首先需要建立與雲端儲存空間帳戶（在此範例中為資料登陸區域）的基本連線，然後使用指定的壓縮和格式選項建立與特定檔案路徑的目標連線。

可用的雲端儲存空間目的地會分別以連線規格ID識別：

| 雲端儲存型別 | 連線規格ID |
|-----------------------|--------------------------------------|
| Amazon S3 | 4fce964d-3f37-408f-9778-e597338a21ee |
| Azure Blob 儲存體 | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |
| Azure資料湖 | be2c3209-53bc-47e7-ab25-145db8b873e1 |
| Data Landing Zone | 10440537-2a7b-4583-ac39-ed38d4b848e8 |
| Google雲端儲存空間 | c5d93acb-ea8b-4b14-8f53-02138444ae99 |
| SFTP | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

```python
connection_spec_id = "10440537-2a7b-4583-ac39-ed38d4b848e8"
base_connection_res = flow_conn.createConnection(data={
    "name": "Base Connection to DLZ created by",
    "auth": None,
    "connectionSpec": {
        "id": connection_spec_id,
        "version": "1.0"
    }
})
base_connection_id = base_connection_res["id"]

target_res = flow_conn.createTargetConnection(
    data={
        "name": "Data Landing Zone target connection",
        "baseConnectionId": base_connection_id,
        "params": {
            "mode": "Server-to-server",
            "compression": config.get("Cloud", "compression_type"),
            "datasetFileType": config.get("Cloud", "data_format"),
            "path": config.get("Cloud", "export_path")
        },
        "connectionSpec": {
            "id": connection_spec_id,
            "version": "1.0"
        }
    }
)
target_connection_id = target_res["id"]
```

## 建立資料流程 {#create-data-flow}

最後一個步驟是在來源連線中所指定的資料集和目標連線中所指定的目的地檔案路徑之間建立資料流。

每種可用的雲端儲存型別都透過流量規格ID識別：

| 雲端儲存型別 | 流量規格ID |
|-----------------------|--------------------------------------|
| Amazon S3 | 269ba276-16fc-47db-92b0-c1049a3c131f |
| Azure Blob 儲存體 | 95bd8965-fc8a-4119-b9c3-944c2c2df6d2 |
| Azure資料湖 | 17be2013-2549-41ce-96e7-a70363bec293 |
| Data Landing Zone | cd2fc47e-e838-4f38-a581-8fff2f99b63a |
| Google雲端儲存空間 | 585c15c4-6cbf-4126-8f87-e26bff78b657 |
| SFTP | 354d6aad-4754-46e4-a576-1b384561c440 |

下列程式碼會建立資料流程，其中排程設定為從遙遠的未來開始。 這可讓您在模型開發期間觸發隨機流程。 當您擁有受過訓練的模型後，您可以更新資料流的排程，以按照所需的排程共用功能資料集。

```python
import time

on_schedule = False
if on_schedule:
    schedule_params = {
        "interval": 3,
        "timeUnit": "hour",
        "startTime": int(time.time())
    }
else:
    schedule_params = {
        "interval": 1,
        "timeUnit": "day",
        "startTime": int(time.time() + 60*60*24*365) # Start the schedule far in the future
    }

flow_spec_id = "cd2fc47e-e838-4f38-a581-8fff2f99b63a"
flow_obj = {
    "name": "Flow for Feature Dataset to DLZ",
    "flowSpec": {
        "id": flow_spec_id,
        "version": "1.0"
    },
    "sourceConnectionIds": [
        source_connection_id
    ],
    "targetConnectionIds": [
        target_connection_id
    ],
    "transformations": [],
    "scheduleParams": schedule_params
}
flow_res = flow_conn.createFlow(
    obj = flow_obj,
    flow_spec_id = flow_spec_id
)
dataflow_id = flow_res["id"]
```

建立資料流程後，您現在可以觸發隨機流程執行，以隨選共用功能資料集：

```python
from aepp import connector

connector = connector.AdobeRequest(
  config_object=aepp.config.config_object,
  header=aepp.config.header,
  loggingEnabled=False,
  logger=None,
)

endpoint = aepp.config.endpoints["global"] + "/data/core/activation/disflowprovider/adhocrun"

payload = {
    "activationInfo": {
        "destinations": [
            {
                "flowId": dataflow_id, 
                "datasets": [
                    {"id": created_dataset_id}
                ]
            }
        ]
    }
}

connector.header.update({"Accept":"application/vnd.adobe.adhoc.dataset.activation+json; version=1"})
activation_res = connector.postData(endpoint=endpoint, data=payload)
activation_res
```

## 簡化與資料登陸區域的共用

若要更輕鬆地將資料集共用至資料登陸區域，請 `aepp` 程式庫提供 `exportDatasetToDataLandingZone` 在單一函式呼叫中執行上述步驟的函式：

```python
from aepp import exportDatasetToDataLandingZone

export = exportDatasetToDataLandingZone.ExportDatasetToDataLandingZone()

dataflow_id = export.createDataFlowRunIfNotExists(
    dataset_id = created_dataset_id,
    data_format = data_format, 
    export_path= export_path, 
    compression_type = compression_type, 
    on_schedule = False, 
    config_path = config_path, 
    entity_name = "Flow for Featurized Dataset to DLZ"
)
```

此程式碼會根據提供的引數建立來源連線、目標連線和資料流程，並在單一步驟中執行資料流程的隨機執行。
