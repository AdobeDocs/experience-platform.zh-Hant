---
keywords: Experience Platform；首頁；熱門主題；Azure事件集線器；azure事件集線器；事件集線器；事件集線器
solution: Experience Platform
title: Azure事件集線器源連接器概述
topic-legacy: overview
description: 瞭解如何使用API或使用者介面將Azure事件中樞連線至Adobe Experience Platform。
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
translation-type: tm+mt
source-git-commit: 6dac267be93241bffb4eb5092a6e8da5093c63a6
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] 連接器

Adobe Experience Platform為AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等雲提供商提供本機連接。 您可以將這些系統中的資料導入[!DNL Platform]。

雲端儲存來源可將您自己的資料匯入[!DNL Platform]，而不需下載、格式化或上傳。 收錄的資料可格式化為XDM JSON、XDM Parce或分隔。 此程式的每個步驟都會整合至Sources工作流程中。 [!DNL Platform] 可讓您即時從資料 [!DNL Azure Event Hubs] 中匯入。

## IP位址允許清單

在使用來源連接器之前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 將[!DNL Azure Event Hubs]連接到[!DNL Platform]

下面的文檔提供了如何使用API或用戶介面將[!DNL Azure Event Hubs]連接到[!DNL Platform]的資訊：

### 使用API

- [使用流程服務API建立Azure事件集線器來源連線](../../tutorials/api/create/cloud-storage/eventhub.md)
- [使用Flow Service API收集串流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中建立Azure事件集線器來源連線](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [在UI中為雲端儲存區連線設定資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
