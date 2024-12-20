---
title: AI助理的隱私權、安全性和控管
description: 瞭解AI Assistant的隱私權、安全性和治理實務。
exl-id: 371e065d-c2dd-4233-b78e-a42757fce853
source-git-commit: e14bf4191319d646c6c4bfd55656fc6de141e9ca
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# AI助理的隱私權、安全性和控管

Adobe Experience Platform中的AI助理是透過隱私、安全性和治理機制所建置，並排在首位。

閱讀本檔案以瞭解您可以期待AI Assistant提供的以客戶信任為中心的功能：

* AI助理目前沒有使用任何個人資料，即使用於訓練目的亦然。
* AI助理不知道消費者資料。
* AI助理會遵循所有現有的[存取控制](../access-control/home.md)原則。
   * 任何以屬性為基礎的新存取控制原則都會在最多24小時後反映在AI助理中*
* 您必須被授予明確許可權才能與AI助理互動。
   * 您可以使用[許可權UI](../access-control/abac/ui/permissions.md)為Experience Platform和Journey Optimizer設定不同的許可權，也可以使用[Admin Console](../access-control/ui/browse.md)為Customer Journey Analytics指派許可權。
   * 許可權很細微，您的沙箱管理員可以設定哪些使用者可以詢問不同類別的問題（使用AI Assistant時的產品知識型問題或操作深入分析問題）。
* AI Assistant是與Adobe Experience Platform Healthcare Shield搭配使用時可支援HIPAA的功能。
* 您可以透過30天保留原則檢視您先前與AI助理互動的記錄。
* AI助理在回應使用者提示時是以沙箱特定的資料和公開Adobe檔案為基礎。 資料不會跨沙箱共用。
* 您提供給AI助理的提示不會分享給其他客戶。

**這表示如果有任何新標籤新增到欄位和物件，或建立任何新原則，則需要AI助理最多24小時才能執行。 在這24小時內，新受限制存取許可權的使用者仍可存取這些欄位和物件。*
