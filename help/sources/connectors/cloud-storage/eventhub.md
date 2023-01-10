---
keywords: Experience Platform；首頁；熱門主題；Azure事件中心；Azure事件中心；事件中心；事件中心
solution: Experience Platform
title: Azure事件集線器源連接器概述
description: 了解如何使用API或使用者介面將Azure事件中心連線至Adobe Experience Platform。
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] 連接器

Adobe Experience Platform為AWS等雲端提供者提供原生連線， [!DNL Google Cloud Platform]，和 [!DNL Azure]. 您可以將這些系統的資料匯入Platform。

雲端儲存來源可將您自己的資料匯入Platform，而無須下載、格式化或上傳。 擷取的資料可格式化為XDM JSON、XDM Parquet或分隔字元。 流程的每個步驟都整合至來源工作流程中。 Platform可讓您將資料 [!DNL Event Hubs] 即時。

## 使用 [!DNL Event Hubs]

您的 [!DNL Event Hubs] 如果您需要導入高容量資料、增加並行性或提高獲取平台的速度，則必須增加實例。

### 入口較高的卷資料

目前，您可從 [!DNL Event Hubs] 帳戶對Platform的影響是每秒2000條記錄。 若要放大並擷取較多數量的資料，請聯絡您的Adobe代表。

### 增加並行性 [!DNL Event Hubs] 和平台

並行性是指在多個處理單元上同時執行相同的任務，以提高速度和效能。 可以在 [!DNL Event Hubs] 通過增加分區，或通過獲取更多處理單元 [!DNL Event Hubs] 帳戶。 看這個 [[!DNL Event Hubs] 縮放比例的文檔](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) 以取得更多資訊。

若要提高平台端擷取速度，Platform必須增加來源連接器中要從您的 [!DNL Event Hubs] 分區。 一旦在 [!DNL Event Hubs] 側面，請連絡您的Adobe代表，以根據您的新分區來調整Platform任務。 目前，此程式未自動執行。

## 使用虛擬網路連接到 [!DNL Event Hubs] 到平台

您可以設定要連接的虛擬網路 [!DNL Event Hubs] 啟用防火牆測量時傳送至Platform。 要設定虛擬網路，請轉到此 [[!DNL Event Hubs] 網路規則集文檔](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) 並遵循下列步驟：

* 選擇 **試試看** 從REST API面板；
* 驗證您的 [!DNL Azure] 在相同瀏覽器中使用您的憑證的帳戶；
* 選取 [!DNL Event Hubs] 您要帶入Platform的命名空間、資源群組和訂閱，然後選取 **執行**;
* 在顯示的JSON內文中，將下列Platform子網新增至 `virtualNetworkRules` in `properties`:


>[!IMPORTANT]
>
>您必須先備份收到的JSON內文，才能更新 `virtualNetworkRules` Platform子網，因為它包含您現有的IP篩選規則。 否則，規則會在呼叫後刪除。


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

請參閱下面的清單，了解Platform子網的不同區域：

### VA7:北美

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### NLD2:歐洲

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2_network_10_20_40_0_23/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        }, 
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### 澳大利亞5:澳大利亞

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5_network_10_21_116_0_22/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

請參閱下列內容 [[!DNL Event Hubs] 檔案](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set) ，了解有關網路規則集的詳細資訊。

## Connect [!DNL Event Hubs] 到平台

以下檔案提供如何連線的資訊 [!DNL Event Hubs] 若要使用API或使用者介面來建立平台：

### 使用API

* [使用流服務API建立事件中心源連接](../../tutorials/api/create/cloud-storage/eventhub.md)
* [使用流量服務API收集串流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

* [在UI中建立事件中心源連接](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [在UI中為雲儲存連接配置資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
