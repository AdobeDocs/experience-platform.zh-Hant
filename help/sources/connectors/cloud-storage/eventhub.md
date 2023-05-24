---
keywords: Experience Platform；首頁；熱門主題；Azure事件中心；Azure事件中心；事件中心；事件中心
solution: Experience Platform
title: Azure事件集線器源連接器概述
description: 瞭解如何使用API或用戶介面將Azure事件集線器連接到Adobe Experience Platform。
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] 連接器

Adobe Experience Platform提供本地連接，如AWS, [!DNL Google Cloud Platform], [!DNL Azure]。 您可以將這些系統中的資料帶入平台。

雲儲存源可以將您自己的資料帶入平台，而無需下載、格式化或上載。 所攝取的資料可以格式化為XDM JSON、XDM Parke或分隔。 流程的每個步驟都整合到「源」工作流中。 平台允許您從 [!DNL Event Hubs] 即時。

## 使用 [!DNL Event Hubs]

您的比例因子 [!DNL Event Hubs] 如果需要導入高容量資料、增加並行性或提高接收平台的速度，則必須增加實例。

### 入口更高的卷資料

當前，可以從 [!DNL Event Hubs] 平台每秒有2000條記錄。 要擴展並接收更高的卷資料，請與Adobe代表聯繫。

### 在上增加並行 [!DNL Event Hubs] 和平台

並行性是指在多個處理單元上同時執行相同的任務，以提高速度和效能。 可以增加 [!DNL Event Hubs] 通過增加分區或通過獲取更多處理單元 [!DNL Event Hubs] 帳戶。 查看 [[!DNL Event Hubs] 文檔縮放](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) 的子菜單。

要提高平台端接收速度，平台必須增加源連接器中要從您的 [!DNL Event Hubs] 分區。 一旦在 [!DNL Event Hubs] 另外，請聯繫您的Adobe代表，根據您的新分區擴展平台任務。 當前，此過程未自動執行。

## 使用虛擬網路連接到 [!DNL Event Hubs] 到平台

您可以設定虛擬網路以連接 [!DNL Event Hubs] 啟用防火牆度量時連接到平台。 要設定虛擬網路，請轉到此 [[!DNL Event Hubs] 網路規則集文檔](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) 並執行下列步驟：

* 選擇 **試試** 從REST API面板；
* 驗證您的 [!DNL Azure] 在同一瀏覽器中使用您的憑據；
* 選擇 [!DNL Event Hubs] 要帶到平台的命名空間、資源組和訂閱，然後選擇 **運行**;
* 在顯示的JSON正文中，在 `virtualNetworkRules` 內 `properties`:


>[!IMPORTANT]
>
>在更新之前，必須備份您收到的JSON正文 `virtualNetworkRules` 平台子網，因為它包含您現有的IP過濾規則。 否則，在調用後將刪除規則。


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

有關平台子網的不同區域，請參閱以下清單：

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

請參閱以下內容 [[!DNL Event Hubs] 文檔](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set) 的子菜單。

## 連接 [!DNL Event Hubs] 到平台

以下文檔提供了有關如何連接的資訊 [!DNL Event Hubs] 到使用API或用戶介面的平台：

### 使用API

* [使用流服務API建立事件中心源連接](../../tutorials/api/create/cloud-storage/eventhub.md)
* [使用流服務API收集流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

* [在UI中建立事件集線器源連接](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [在UI中為雲儲存連接配置資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
