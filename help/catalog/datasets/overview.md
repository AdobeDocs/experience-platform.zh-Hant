---
keywords: Experience Platform；首頁；熱門主題；資料位置；資料位置；資料管理；資料管理；世系；世系；資料類型；資料類型；資料類型
solution: Experience Platform
title: 資料集概述
topic-legacy: datasets
description: 本文件提供 Experience Platform 資料集的高層級總覽。
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 8%

---

# 資料集概觀

成功擷取至Adobe Experience Platform的所有資料都會保存在 [!DNL Data Lake] 做為資料集。 資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 資料集也包含中繼資料，可說明其儲存資料的各個層面。 

本檔案概略介紹 [!DNL Experience Platform].

## 建立資料集和追蹤中繼資料

[!DNL Catalog Service] 是內用於資料位置和世系的記錄系統 [!DNL Experience Platform]，可用來建立和管理資料集。 [!DNL Catalog] 追蹤每個資料集的中繼資料，包括對 [!DNL Experience Data Model] (XDM)資料集符合（在下一節中說明）的資料集結構，以及擷取至該資料集的記錄數。

請參閱 [目錄服務概述](../home.md) 以取得更多資訊。

## 強制限制資料集資料

[!DNL Experience Data Model] (XDM)為標準化架構，據以 [!DNL Platform] 組織客戶體驗資料。 擷取至的所有資料 [!DNL Platform] 必須符合預先定義的XDM架構，才能持續保存在 [!DNL Data Lake] 作為資料集。

所有資料集都包含XDM結構的參考，這會限制其可儲存的資料格式和結構。 若嘗試將資料上傳至不符合資料集XDM結構的資料集，會導致擷取失敗。

如需XDM的詳細資訊，請參閱 [XDM系統概觀](../../xdm/home.md).

## 將資料擷取至資料集

Adobe Experience Platform資料擷取代表 [!DNL Platform] 從各種來源擷取資料。 無論擷取方法為何，所有成功擷取的資料都會轉換為批次檔案。 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。這些批次檔案會新增至專用的資料集，並保存在 [!DNL Data Lake].

請參閱 [資料擷取概觀](../../ingestion/home.md) 以取得更多資訊。

## 將使用量標籤套用至資料集

Adobe Experience Platform資料控管可讓您管理客戶資料，以確保符合適用於資料使用的法規、限制和政策。 資料控管架構可讓您套用使用標籤，以根據套用至該資料的使用原則來分類資料。

>[!IMPORTANT]
>
>只有資料控管使用案例才支援在資料集層級套用標籤。 如果您嘗試為資料建立訪問策略，則必須 [將標籤應用於方案](../../xdm/tutorials/labels.md) 資料集所依據之資料集。 請參閱 [基於屬性的訪問控制](../../access-control/abac/overview.md) 以取得更多資訊。

資料使用量標籤可套用至整個資料集或個別資料集欄位。 在資料集層級新增的標籤，會由該資料集內的所有欄位繼承。

請參閱 [資料控管概觀](../../data-governance/home.md) 以取得服務的詳細資訊。 有關如何在 [!DNL Platform]，請參閱下列指南：

* [在UI中管理標籤](../../data-governance/labels/user-guide.md)
* [在API中管理資料集標籤](../../data-governance/labels/dataset-api.md)

## 下游資料集 [!DNL Platform] 服務

使用資料集來儲存擷取的資料後，下游就會使用這些資料集 [!DNL Platform] 更新客戶設定檔、透過機器學習獲得深入分析等服務。

以下是將資料集用於各種作業的下游服務清單。 請查閱每項服務的檔案以取得詳細資訊。

* [[!DNL Data Access API]](../../data-access/home.md):可讓您存取和下載資料集中儲存的檔案內容。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md):橋接跨裝置和系統的身分，根據資料集所遵循的XDM結構所定義的身分欄位，將資料集連結在一起。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):利用 [!DNL Identity Service] 即時從資料集建立詳細的客戶設定檔。 [!DNL Real-Time Customer Profile] 從 [!DNL Data Lake] 並將客戶設定檔保存在其自己的個別資料存放區中。
* [Adobe Experience Platform區段服務](../../segmentation/home.md):可讓您建立區段，並從 [!DNL Real-Time Customer Profile] 資料。 然後，這些對象可匯出至 [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md):使用機器學習和人工智慧發掘大型資料集的深入分析。
* [Adobe Experience Platform查詢服務](../../query-service/home.md):允許使用標準SQL在中查詢資料 [!DNL Experience Platform]，在中加入任何資料集 [!DNL Data Lake] 將查詢結果擷取為新資料集以用於報表， [!DNL Data Science Workspace]，或 [!DNL Real-Time Customer Profile].
* [Adobe Experience Platform目的地服務](../../destinations/home.md):可讓您 [匯出資料集](/help/destinations/ui/export-datasets.md) 至您所需的雲端儲存空間或電子郵件行銷目的地，以利進行報表或資料科學活動。

## 後續步驟

閱讀本檔案後，您便了解中資料集的核心用途 [!DNL Experience Platform]，以及 [!DNL Platform] 利用資料集的服務。 如需中資料集使用方式的詳細資訊，請參閱 [!DNL Platform]，請參閱本概述中連結的服務檔案。

如需如何在中與資料集互動的步驟 [!DNL Experience Platform] UI，請參閱 [資料集使用指南](user-guide.md).
