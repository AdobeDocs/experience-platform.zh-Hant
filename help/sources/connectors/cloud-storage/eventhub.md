---
keywords: Experience Platform;home;popular topics;Azure Event Hubs;azure event hubs;Event Hubs;event hubs
solution: Experience Platform
title: Azure事件集線器連接器
topic: overview
description: 以下檔案提供如何使用API或使用者介面將Azure事件中樞連接至平台的資訊。
translation-type: tm+mt
source-git-commit: c0c609e3f385665cf88129def0c69e7d153ce201
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# （測試版）Azure事件集線器連接器

>[!NOTE]
>
>Azure事件集線器連接器處於測試狀態。 如需使用 [測試版標籤連接器的詳細資訊](../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform為AWS和AWS等雲提供商提供 [!DNL Google Cloud Platform]原生連接 [!DNL Azure]。 您可以將這些系統的資料匯入其中 [!DNL Platform]。

雲端儲存來源可將您自己的資料匯入 [!DNL Platform] 其中，而不需下載、格式化或上傳。 收錄的資料可格式化為XDM JSON、XDM鑲木地板或分隔字元。 此程式的每個步驟都會整合至Sources工作流程中。 [!DNL Platform] 可讓您即時匯入 [!DNL Azure Event Hubs] 資料。

## IP位址允許清單

在使用來源連接器之前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細 [資訊，請參閱](../../ip-address-allow-list.md) 「IP位址允許清單」頁面。

## 連線 [!DNL Azure Event Hubs] 至 [!DNL Platform]

以下檔案提供如何連線至使用API [!DNL Azure Event Hubs] 或使 [!DNL Platform] 用者介面的資訊：

### 使用API

- [使用流程服務API建立Azure事件集線器連接器](../../tutorials/api/create/cloud-storage/eventhub.md)
- [使用Flow Service API收集串流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中建立Azure事件集線器來源連接器](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [在UI中為雲端儲存連接器設定資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)