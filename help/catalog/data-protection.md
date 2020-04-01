---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform中的資料保護
topic: data protection
translation-type: tm+mt
source-git-commit: edf7cef0991ceef0465d5c1d750bd1885754f716

---


# Adobe Experience Platform中的資料保護

Adobe Experience Platform所擷取和使用的所有資料都儲存在資料湖中，資料湖是高度精細的資料存放區，包含平台管理的所有資料，不論來源或檔案格式為何。 所有保留在資料湖中的資料都會在您組織專屬的隔離Microsoft Azure資料湖儲存帳戶中加密、儲存及管理。

以下流程圖說明Experience Platform如何吸收、處理、加密和保存資料：

![](images/data-protection/flow.png)

如需資料湖儲存區中閒置資料加密方式的詳細資訊，請參閱Azure資料湖儲存 [區中資料加密的檔案](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)。 有關在Cosmos DB中如何加密閒置資料的資訊，請參閱Azure Cosmos DB中 [的資料加密文檔](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)。