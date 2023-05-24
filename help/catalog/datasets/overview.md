---
keywords: Experience Platform；主題；熱門主題；資料位置；資料位置；資料管理；資料管理；沿襲；沿襲；資料類型；資料類型；資料類型；資料類型
solution: Experience Platform
title: 資料集概述
description: 本文件提供 Experience Platform 資料集的高層級總覽。
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 8%

---

# 資料集概述

成功接收到Adobe Experience Platform的所有資料都保留在 [!DNL Data Lake] 作為資料集。 資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 資料集也包含中繼資料，可說明其儲存資料的各個層面。 

本文檔提供了中資料集的高級概述 [!DNL Experience Platform]。

## 建立資料集和跟蹤元資料

[!DNL Catalog Service] 是資料位置和沿襲的記錄系統 [!DNL Experience Platform]，用於建立和管理資料集。 [!DNL Catalog] 跟蹤每個資料集的元資料，該元資料包括對 [!DNL Experience Data Model] (XDM)模式資料集符合（在下一節中說明）和該資料集中接收的記錄數。

查看 [目錄服務概述](../home.md) 的子菜單。

## 對資料集資料強制約束

[!DNL Experience Data Model] (XDM)是標準化框架， [!DNL Platform] 組織客戶體驗資料。 所有被攝入的資料 [!DNL Platform] 必須符合預定義的XDM架構，才能將其保留在 [!DNL Data Lake] 作為資料集。

所有資料集都包含對XDM架構的引用，該引用限制了它們可以儲存的資料的格式和結構。 嘗試將資料上載到不符合資料集的XDM架構的資料集將導致接收失敗。

有關XDM的詳細資訊，請參見 [XDM系統概述](../../xdm/home.md)。

## 將資料插入資料集

Adobe Experience Platform資料接收表示 [!DNL Platform] 從各種來源接收資料。 無論採用何種接收方法，所有成功接收的資料都會轉換為批處理檔案。 批次是多個資料單位，由一或多個要作為一個單位進行內嵌的檔案所組成。然後，這些批處理檔案將添加到專用資料集並保留在 [!DNL Data Lake]。

查看 [資料接收概述](../../ingestion/home.md) 的子菜單。

## 將使用標籤應用於資料集

Adobe Experience Platform資料治理允許您管理客戶資料，以確保遵守適用於資料使用的法規、限制和策略。 資料治理框架允許您應用使用標籤，根據應用於該資料的使用策略對資料進行分類。

>[!IMPORTANT]
>
>僅在資料治理使用案例中支援在資料集級別應用標籤。 如果嘗試為資料建立訪問策略，則必須 [將標籤應用於架構](../../xdm/tutorials/labels.md) 資料集所基於。 請參閱 [基於屬性的訪問控制](../../access-control/abac/overview.md) 的子菜單。

資料使用標籤可以應用於整個資料集或單個資料集欄位。 在資料集級別添加的標籤由該資料集中的所有欄位繼承。

查看 [資料治理概述](../../data-governance/home.md) 的子菜單。 有關如何使用中的使用標籤的步驟 [!DNL Platform]，請參閱以下指南：

* [管理UI中的標籤](../../data-governance/labels/user-guide.md)
* [在API中管理資料集標籤](../../data-governance/labels/dataset-api.md)

## 下游資料集 [!DNL Platform] 服務

一旦使用資料集來儲存所攝取的資料，則下游將使用這些資料集 [!DNL Platform] 更新客戶配置檔案、通過機器學習獲得洞察力等。

以下是使用資料集執行各種操作的下游服務的清單。 請查看每項服務的文檔以瞭解更多資訊。

* [[!DNL Data Access API]](../../data-access/home.md):允許您訪問和下載資料集中儲存的檔案的內容。
* [Adobe Experience Platform身份服務](../../identity-service/home.md):跨設備和系統橋接身份，根據它們遵循的XDM架構定義的身份欄位將資料集連結在一起。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):利用 [!DNL Identity Service] 從您的資料集中即時建立詳細的客戶配置檔案。 [!DNL Real-Time Customer Profile] 從 [!DNL Data Lake] 並將客戶配置檔案保留在其單獨的資料儲存中。
* [Adobe Experience Platform分段服務](../../segmentation/home.md):允許您構建網段並從 [!DNL Real-Time Customer Profile] 資料。 然後，可以將這些訪問群體導出到他們自己的資料集中 [!DNL Data Lake]。
* [Adobe Experience Platform資料科學工作區](../../data-science-workspace/home.md):使用機器學習和人工智慧在大資料集中發現洞見。
* [Adobe Experience Platform查詢服務](../../query-service/home.md):允許您使用標準SQL在 [!DNL Experience Platform]，加入所有資料集 [!DNL Data Lake] 將查詢結果捕獲為用於報告的新資料集， [!DNL Data Science Workspace]或 [!DNL Real-Time Customer Profile]。
* [Adobe Experience Platform航點](../../destinations/home.md):允許您 [導出資料集](/help/destinations/ui/export-datasets.md) 到您所需的雲儲存或電子郵件營銷目的地，用於報告或資料科學活動。

## 後續步驟

通過閱讀本文檔，您已介紹了資料集在 [!DNL Experience Platform]，以及 [!DNL Platform] 服務。 有關資料集使用方式的詳細資訊 [!DNL Platform]，請查看本概述中連結的服務文檔。

有關如何與中的資料集交互的步驟 [!DNL Experience Platform] UI，請參見 [資料集使用手冊](user-guide.md)。
