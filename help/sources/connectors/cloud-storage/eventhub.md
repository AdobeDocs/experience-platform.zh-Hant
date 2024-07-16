---
title: Azure事件中樞Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Azure事件中樞連線至Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 12ddf87d594b7e25a0356cd419e990b262c1734e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# [!DNL Azure Event Hubs]來源

>[!IMPORTANT]
>
>[!DNL Azure Event Hubs]來源可在來源目錄中提供給已購買Real-time Customer Data Platform Ultimate的使用者。

Adobe Experience Platform為AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等雲端提供者提供原生連線。 您可以將資料從這些系統帶入Platform。

雲端儲存空間來源可將您自己的資料帶入Platform，無需下載、格式化或上傳。 內嵌的資料可以格式化為XDM JSON、XDM Parquet或分隔。 流程的每個步驟都會整合至來源工作流程。 Platform可讓您即時從[!DNL Event Hubs]匯入資料。

## 使用[!DNL Event Hubs]縮放

如果您需要擷取大量資料、增加平行度或提高擷取平台的速度，必須增加[!DNL Event Hubs]執行個體的比例因數。

### 匯入較大量的資料

目前，您可以從[!DNL Event Hubs]帳戶帶入Platform的最大資料量為每秒2000筆記錄。 若要擴充並擷取較大量的資料，請聯絡您的Adobe代表。

### 增加[!DNL Event Hubs]和平台上的平行程度

平行度是指在多個處理單元上同時執行相同工作，以提高速度和效能。 您可以透過增加分割或為您的[!DNL Event Hubs]帳戶取得更多處理單位來增加[!DNL Event Hubs]端的平行程度。 如需詳細資訊，請參閱有關縮放](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability)的[[!DNL Event Hubs] 檔案。

若要提高平台端的擷取速度，平台必須增加來源聯結器中要從[!DNL Event Hubs]資料分割讀取的工作數量。 增加[!DNL Event Hubs]端的平行程度後，請連絡您的Adobe代表，以根據您的新磁碟分割調整平台工作。 目前，此程式尚未自動化。

## 使用虛擬網路連線至[!DNL Event Hubs]至平台

您可以設定虛擬網路，在啟用防火牆測量時，將[!DNL Event Hubs]連線至平台。 若要設定虛擬網路，請前往此[[!DNL Event Hubs] 網路規則集檔案](https://learn.microsoft.com/en-us/azure/event-hubs/network-security)，然後遵循下列步驟：

* 從REST API面板選取&#x200B;**試用**；
* 在相同瀏覽器中使用您的認證驗證您的[!DNL Azure]帳戶；
* 選取您要帶到Platform的[!DNL Event Hubs]名稱空間、資源群組和訂閱，然後選取&#x200B;**執行**；
* 在出現的JSON內文中，在`properties`內的`virtualNetworkRules`下新增下列Platform子網路：


>[!IMPORTANT]
>
>在使用Platform子網路更新`virtualNetworkRules`之前，您必須備份您收到的JSON內文，因為它包含您現有的IP篩選規則。 否則，會在呼叫後刪除規則。


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

有關Platform子網路的不同區域，請參閱以下清單：

### VA7：北美

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

### NLD2：歐洲

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2-vnet/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        }, 
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### AUS5：澳洲

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5-vnet/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

如需網路規則集的詳細資訊，請參閱下列[[!DNL Event Hubs] 檔案](https://learn.microsoft.com/en-us/azure/event-hubs/network-security)。

## 將[!DNL Event Hubs]連線至平台

以下檔案提供如何使用API或使用者介面將[!DNL Event Hubs]連線到Platform的資訊：

### 使用API

* [使用流程服務API建立事件中樞來源連線](../../tutorials/api/create/cloud-storage/eventhub.md)
* [使用流量服務API收集串流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

* [在UI中建立事件中樞來源連線](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [在UI中為雲端儲存空間連線設定資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
