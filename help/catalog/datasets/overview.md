---
keywords: Experience Platform;home；熱門主題；資料位置；資料位置；資料管理；資料管理；世系；資料類型；資料類型；資料類型；資料類型
solution: Experience Platform
title: 資料集概述
topic-legacy: datasets
description: 本檔案提供Experience Platform中資料集的高階概觀。
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 2%

---

# 資料集總覽

成功收錄到Adobe Experience Platform的所有資料都會以資料集的形式保存在[!DNL Data Lake]中。 資料集是資料集合的儲存和管理結構，通常是包含結構（欄）和欄（列）的表格。 資料集也包含描述其儲存之資料各方面的中繼資料。

本文檔提供[!DNL Experience Platform]中資料集的高級概述。

## 建立資料集和追蹤中繼資料

[!DNL Catalog Service] 是資料位置和世系的記錄系統， [!DNL Experience Platform]用於建立和管理資料集。[!DNL Catalog] 追蹤每個資料集的中繼資料，包括對資料集符合的 [!DNL Experience Data Model] (XDM)架構的參考（在下一節中說明）以及該資料集所吸收的記錄數。

如需詳細資訊，請參閱[目錄服務概觀](../home.md)。

## 對資料集資料強制限制

[!DNL Experience Data Model] (XDM)是組織客戶體驗資料的 [!DNL Platform] 標準化架構。所有被收錄到[!DNL Platform]的資料都必須符合預先定義的XDM架構，才能將它以資料集的形式保存在[!DNL Data Lake]中。

所有資料集都包含對XDM模式的引用，該引用限制了它們可以儲存的資料的格式和結構。 嘗試上傳不符合資料集XDM架構的資料集會導致擷取失敗。

有關XDM的詳細資訊，請參見[XDM系統概述](../../xdm/home.md)。

## 將資料擷取至資料集

Adobe Experience Platform資料擷取代表[!DNL Platform]從各種來源擷取資料的多種方法。 不論擷取方法為何，所有成功擷取的資料都會轉換為批次檔案。 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。然後，這些批處理檔案將添加到專用資料集並保存在[!DNL Data Lake]中。

如需詳細資訊，請參閱[資料擷取概觀](../../ingestion/home.md)。

## 將使用情況標籤套用至資料集

Adobe Experience Platform[!DNL Data Governance]可讓您管理客戶資料，以確保符合資料使用適用的法規、限制和政策。 [!DNL Data Governance]框架允許您應用使用標籤，以根據應用於該資料的使用策略對資料進行分類。

資料使用標籤可套用至整個資料集或個別資料集欄位。 在資料集層級新增的標籤會由該資料集內的所有欄位繼承。

有關服務的詳細資訊，請參閱[資料治理概述](../../data-governance/home.md)。 有關如何在[!DNL Platform]中使用使用標籤的步驟，請參閱以下指南：

* [管理UI中的標籤](../../data-governance/labels/user-guide.md)
* [在API中管理資料集標籤](../../data-governance/labels/dataset-api.md)

## 下游[!DNL Platform]服務中的資料集

一旦使用資料集來儲存收錄的資料，下游[!DNL Platform]服務就會使用這些資料集來更新客戶個人檔案、透過機器學習獲得深入資訊等。

以下是使用資料集進行各種操作的下游服務的清單。 請檢視每項服務的檔案，以取得更多資訊。

* [[!DNL Data Access API]](../../data-access/home.md):允許您訪問和下載儲存在資料集中的檔案的內容。
* [Adobe Experience Platform身分服務](../../identity-service/home.md):跨裝置和系統橋接身分識別，並根據資料集符合的XDM架構所定義的身分欄位，將資料集連結在一起。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):利用 [!DNL Identity Service] 資料集即時建立詳細的客戶個人檔案。[!DNL Real-time Customer Profile] 從資料中提取資 [!DNL Data Lake] 料，並將客戶個人檔案保留在其個別的資料儲存中。
* [Adobe Experience Platform區段服務](../../segmentation/home.md):可讓您建立區段並從資料產生 [!DNL Real-time Customer Profile] 觀眾。然後，這些對象可以導出到[!DNL Data Lake]中自己的資料集。
* [Adobe Experience Platform資料科學工作區](../../data-science-workspace/home.md):使用機器學習和人工智慧發掘大型資料集的見解。
* [Adobe Experience Platform查詢服務](../../query-service/home.md):允許您使用標準SQL來查詢中的資料、 [!DNL Experience Platform]連接中的任何資料 [!DNL Data Lake] 集，並將查詢結果捕獲為新資料集以用於報告、 [!DNL Data Science Workspace]或中 [!DNL Real-time Customer Profile]。

## 後續步驟

閱讀本文檔後，您將瞭解[!DNL Experience Platform]中資料集的核心用途，以及使用資料集的各種[!DNL Platform]服務。 有關[!DNL Platform]中使用資料集的多種方式的詳細資訊，請查看本概述中連結的服務文檔。

有關如何與[!DNL Experience Platform] UI中的資料集交互的步驟，請參見[資料集使用手冊](user-guide.md)。
