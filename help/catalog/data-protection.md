---
keywords: Experience Platform;home；熱門主題；目錄；資料保護；加密資料湖
solution: Experience Platform
title: Adobe Experience Platform的資料保護
topic-legacy: data protection
description: 所有保留在資料湖中的資料都會在您組織專屬的隔離Microsoft Azure資料湖儲存帳戶中加密、儲存及管理。 以下流程圖說明了資料如何由Experience Platform接收、處理、加密和保存。
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Adobe Experience Platform的資料保護

Adobe Experience Platform所吸收和使用的所有資料都儲存在[!DNL Data Lake]中，這是一個高度精細的資料儲存，包含由[!DNL Platform]管理的所有資料，而不考慮源或檔案格式。 所有保存在[!DNL Data Lake]中的資料都會加密、儲存並管理在對您的組織唯一的隔離[!DNL Microsoft Azure Data Lake]儲存帳戶中。

以下流程圖說明[!DNL Experience Platform]如何接收、處理、加密和保存資料：

![](images/data-protection/flow.png)

有關在[!DNL Data Lake Storage]中如何加密靜態資料的詳細資訊，請參閱Azure資料湖儲存中[資料加密的文檔。 ](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)有關在[!DNL Cosmos DB]中如何加密靜態資料的資訊，請參閱Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)中[資料加密的文檔。
