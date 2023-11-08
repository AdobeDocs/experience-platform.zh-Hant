---
keywords: Experience Platform；首頁；熱門主題；資料位置；資料位置；資料管理；資料管理；譜系；譜系；資料型別；資料型別；資料型別
solution: Experience Platform
title: 資料集概述
description: 本文件提供 Experience Platform 資料集的高層級總覽。
user-guide-description: 透過本指南取得Experience Platform資料集的高層級概觀。 在此處瞭解如何建立資料集、強制執行資料限制，以及將資料擷取到資料集中。
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 81f570f8e5401624ccac74696b2323252a4de0a9
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 7%

---

# 資料集總覽

所有成功內嵌至Adobe Experience Platform的資料都會儲存在 [!DNL Data Lake] 作為資料集。 資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 資料集也包含中繼資料，可說明其儲存資料的各個層面。 

本檔案提供中資料集的高層級總覽 [!DNL Experience Platform].

## 建立資料集和追蹤中繼資料

[!DNL Catalog Service] 是內資料位置和歷程的記錄系統 [!DNL Experience Platform]、和可用來建立及管理資料集。 [!DNL Catalog] 追蹤每個資料集的中繼資料，包括 [!DNL Experience Data Model] (XDM)結構描述資料集符合（下節將加以說明）並擷取至該資料集的記錄數。

請參閱 [目錄服務總覽](../home.md) 以取得詳細資訊。

## 強制資料集資料限制

[!DNL Experience Data Model] (XDM)是標準化的架構，其中 [!DNL Platform] 組織客戶體驗資料。 擷取到的所有資料 [!DNL Platform] 必須符合預先定義的XDM結構描述，才能將其儲存在 [!DNL Data Lake] 作為資料集。

所有資料集都包含XDM架構的參考，這會限制可儲存資料的格式和結構。 嘗試上傳資料到不符合資料集XDM結構的資料集會導致擷取失敗。

如需XDM的詳細資訊，請參閱 [XDM系統概覽](../../xdm/home.md).

## 將資料擷取至資料集

Adobe Experience Platform資料擷取代表使用下列多種方法 [!DNL Platform] 從各種來源擷取資料。 無論擷取方法為何，所有成功擷取的資料都會轉換為批次檔案。 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。然後，這些批次檔案會新增到專用資料集，並儲存在 [!DNL Data Lake].

請參閱 [資料擷取概觀](../../ingestion/home.md) 以取得詳細資訊。

## 從結構描述套用到資料集的標籤

Adobe Experience Platform資料控管可讓您管理客戶資料，以確保遵守適用於資料使用的法規、限制和政策。 資料控管架構可讓您套用使用標籤，以根據套用至該資料的使用原則來分類資料。 標籤可套用至個別結構描述、這些結構描述內的欄位以及整個個別資料集。 標籤直接套用至結構描述時，這些標籤會傳播至以該結構描述為基礎的所有現有和未來資料集。

>[!IMPORTANT]
>
>標籤無法再套用至資料集層級的欄位。 此工作流程已淘汰，而改為在結構描述層級套用標籤。 在2024年5月31日之前，先前在資料集物件層級套用的任何標籤仍會透過Platform UI受到支援。 為確保您的標籤在所有結構描述中保持一致，您必須在未來一年將之前附加至資料集層級欄位的任何標籤移轉至結構描述層級。 請參閱以下小節： [移轉先前套用的標籤](../../data-governance/e2e.md#migrate-labels) 以取得執行此動作的指示。

請參閱 [資料控管概觀](../../data-governance/home.md) 以取得服務的詳細資訊。 有關如何使用中的使用標籤的步驟 [!DNL Platform]，請參閱下列指南：

* [在UI中管理標籤](../../data-governance/labels/user-guide.md)
* [在API中管理資料集標籤](../../data-governance/labels/dataset-api.md)

## 下游的資料集 [!DNL Platform] 服務

資料集一旦用來儲存擷取的資料後，下游就會使用這些資料集 [!DNL Platform] 更新客戶設定檔、透過機器學習獲得深入分析等功能的服務。

以下是使用資料集進行各種操作的下游服務清單。 如需詳細資訊，請參閱各服務的檔案。

* [[!DNL Data Access API]](../../data-access/home.md)：可讓您存取及下載儲存在資料集中的檔案內容。
* [Adobe Experience Platform Identity服務](../../identity-service/home.md)：跨裝置和系統橋接身分，根據資料集符合的XDM結構描述所定義的身分欄位將其連結在一起。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：利用 [!DNL Identity Service] 以即時從資料集建立詳細的客戶設定檔。 [!DNL Real-Time Customer Profile] 從提取資料 [!DNL Data Lake] 並將客戶設定檔儲存在其自己的獨立資料存放區中。
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md)：可讓您建立區段，並從產生對象 [!DNL Real-Time Customer Profile] 資料。 然後，這些對象可匯出至他們在 [!DNL Data Lake].
* [Adobe Experience Platform資料科學工作區](../../data-science-workspace/home.md)：使用機器學習和人工智慧來發掘大型資料集中的深入分析。
* [Adobe Experience Platform查詢服務](../../query-service/home.md)：可讓您使用標準SQL在中查詢資料 [!DNL Experience Platform]，在中聯結任何資料集 [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表， [!DNL Data Science Workspace]，或 [!DNL Real-Time Customer Profile].
* [Adobe Experience Platform目標服務](../../destinations/home.md)：可讓您 [匯出資料集](/help/destinations/ui/export-datasets.md) 至您所需的雲端儲存空間或電子郵件行銷目的地，以用於報表或資料科學活動。

## 後續步驟

閱讀本檔案後，您已經瞭解中資料集的核心用途 [!DNL Experience Platform]，以及各種 [!DNL Platform] 使用資料集的服務。 如需有關資料集使用方式的詳細資訊，請參閱 [!DNL Platform]，請檢閱本總覽中所連結的服務檔案。

如需如何與內的資料集互動的相關步驟， [!DNL Experience Platform] UI，請參閱 [資料集使用手冊](user-guide.md).
