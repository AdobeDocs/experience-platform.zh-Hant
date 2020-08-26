---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 通用OData連接器
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# （測試版）連 [!DNL Generic OData] 接器

>[!NOTE]
>
>連接 [!DNL Generic OData] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform可讓您從外部來源擷取資料，同時提供您使用服務建構、標示及增強傳入資料的 [!DNL Platform] 能力。 您可以從多種來源（例如Adobe應用程式、雲端儲存空間、資料庫等）擷取資料。

[!DNL Experience Platform] 支援從協力廠商通訊協定應用程式擷取資料。 支援通訊協定提供者包括 [!DNL Generic OData]。

## IP位址允許清單

在使用源連接器之前，必須將下列IP位址新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。

### 美國東部地區

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### 西歐地區

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### 澳洲東部

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

以下檔案提供如何連線至使用API [!DNL Generic OData] 或使 [!DNL Platform] 用者介面的資訊：

## 連線 [!DNL Generic OData] 至使 [!DNL Platform] 用API

- [使用Flow Service API建立通用OData連接器](../../tutorials/api/create/protocols/odata.md)
- [使用Flow Service API探索通訊協定應用程式](../../tutorials/api/explore/protocols.md)
- [使用Flow Service API從通訊協定應用程式收集資料](../../tutorials/api/collect/protocols.md)

## 使用 [!DNL Generic OData] UI [!DNL Platform] 連線至

- [在UI中建立通用OData來源連接器](../../tutorials/ui/create/protocols/odata.md)
- [在UI中為協定連接器配置資料流](../../tutorials/ui/dataflow/protocols.md)