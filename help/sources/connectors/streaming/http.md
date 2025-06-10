---
keywords: Experience Platform；首頁；熱門主題；http api
solution: Experience Platform
title: HTTP API Source聯結器總覽
description: 瞭解如何建立串流聯結器，以使用API或使用者介面與Adobe Experience Platform連線。
exl-id: 41e079f3-75b2-4033-8138-73162c31461a
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# [!DNL HTTP API]聯結器

>[!IMPORTANT]
>
>您現在可以在Amazon Web Services (AWS)上執行Adobe Experience Platform時使用[!DNL HTTP API]來源。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../landing/multi-cloud.md)。

Adobe Experience Platform允許從外部來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

您可以使用[!DNL HTTP API]來源聯結器將資料串流到Experience Platform。 [!DNL Data Prep]函式支援[!DNL HTTP API]來源，可讓您將任何不符合XDM的資料對應到符合XDM的資料集。

>[!NOTE]
>
>在您建立或更新串流資料流後，需要短暫暫停資料擷取5分鐘，以防止任何可能的資料遺失或資料中斷情況。

以下檔案提供有關如何使用API或使用者介面建立HTTP API串流聯結器以與[!DNL Experience Platform]連線的資訊：

## 使用API建立HTTP API串流聯結器

- [使用流量服務API建立HTTP串流連線](../../tutorials/api/create/streaming/http.md)

## 使用UI建立HTTP API串流聯結器

- [在使用者介面中建立HTTP API串流連線](../../tutorials/ui/create/streaming/http.md)
