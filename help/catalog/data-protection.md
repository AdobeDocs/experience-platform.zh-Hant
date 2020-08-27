---
keywords: Experience Platform;home;popular topics;catalog;data protection;encryption data lake
solution: Experience Platform
title: Adobe Experience Platform中的資料保護
topic: data protection
description: 所有保留在資料湖中的資料都會在您組織專屬的隔離Microsoft Azure資料湖儲存帳戶中加密、儲存及管理。 下列流程圖說明Experience Platform如何吸收、處理、加密和保存資料。
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Adobe Experience Platform中的資料保護

Adobe Experience Platform所吸收和使用的所有資料都會儲存在 [!DNL Data Lake]，這是高度精細的資料存放區，包含所有由管理的資料，不論來源或檔案 [!DNL Platform]格式為何。 所有保存在中的資料 [!DNL Data Lake] 都會加密、儲存並管理在您組織所獨有的隔 [!DNL Microsoft Azure Data Lake] 離儲存帳戶中。

以下流程圖說明了資料如何通過以下方式接收、處理、加密和保存 [!DNL Experience Platform]:

![](images/data-protection/flow.png)

如需閒置資料在中加密的詳細資訊，請 [!DNL Data Lake Storage]參閱Azure資料湖 [儲存區中的資料加密檔案](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)。 如需閒置資料在中如何加密的詳細資訊 [!DNL Cosmos DB]，請參閱Azure Cosmos DB中 [的資料加密檔案](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)。