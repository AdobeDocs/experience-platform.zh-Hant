---
keywords: Experience Platform;home；熱門主題；Google PubSub;google pubsub
solution: Experience Platform
title: Google PubSub Source Connector概觀
topic-legacy: overview
description: 瞭解如何使用API或使用者介面將Google PubSub連線至Adobe Experience Platform。
exl-id: 7c78173d-2639-47cb-8935-77fb7841a121
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# （測試版）[!DNL Google PubSub]連接器

>[!NOTE]
>
>[!DNL Google PubSub]介面處於測試狀態。 如需使用beta標籤連接器的詳細資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

Adobe Experience Platform為[!DNL AWS]、[!DNL Google Cloud Platform]和[!DNL Azure]等雲端提供者提供原生連線，讓您將這些系統的資料匯入平台，以用於下游服務和目的地。

雲端儲存來源可將您的資料匯入平台，而不需下載、格式化或上傳。 收錄的資料可格式化為XDM JSON、XDM Parce或分隔。 流程的每個步驟都整合在來源工作流程中。 平台可讓您即時從[!DNL Azure Event Hubs]匯入資料。

## IP位址允許清單

在使用來源連接器之前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 將[!DNL Google PubSub]連接到平台

以下檔案提供如何使用API或使用者介面將[!DNL Google PubSub]連線至平台的資訊：

### 使用API

- [使用Flow Service API建立Google PubSub來源連線](../../tutorials/api/create/cloud-storage/google-pubsub.md)
- [使用Flow Service API收集串流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中建立Google PubSub來源連線](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
- [在UI中為雲端儲存區連線設定資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
