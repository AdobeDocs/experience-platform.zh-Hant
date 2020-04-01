---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料集總覽
topic: datasets
translation-type: tm+mt
source-git-commit: 06733eb374d1b9409102a7cf13d61ed266cedaad

---


# 資料集總覽

成功收錄至Adobe Experience Platform的所有資料都會以資料集的形式保存在資料湖中。 資料集是資料集合的儲存和管理結構，通常是包含結構（欄）和欄（列）的表格。 資料集也包含描述其儲存之資料各方面的中繼資料。

本檔案提供Experience Platform中資料集的高階概述。

## 建立資料集和追蹤中繼資料

目錄服務是Experience Platform中資料位置和世系的記錄系統，用於建立和管理資料集。 目錄會追蹤每個資料集的中繼資料，其中包括資料集所遵循的「體驗資料模型」(XDM)架構的參考（在下一節中說明），以及該資料集所收錄的記錄數。

如需詳細 [資訊，請參閱目錄服務](../home.md) 。

## 對資料集資料強制限制

Experience Data Model(XDM)是Platform組織客戶體驗資料的標準化架構。 所有收錄到平台的資料都必須符合預先定義的XDM架構，才能以資料集的形式保存在資料湖中。

所有資料集都包含對XDM模式的引用，該引用限制了它們可以儲存的資料的格式和結構。 嘗試上傳不符合資料集XDM架構的資料集會導致擷取失敗。

有關XDM的詳細資訊，請參閱 [XDM系統概述](../../xdm/home.md)。

## 將資料擷取至資料集

Adobe Experience Platform資料擷取代表平台從各種來源擷取資料的多種方法。 不論擷取方法為何，所有成功擷取的資料都會轉換為批次檔案。 批是由一個或多個要作為單個單位接收的檔案組成的資料單位。 然後，這些批次檔案會新增至專用的資料集，並保存在資料湖中。

如需詳細 [資訊，請參閱資料擷取](../../ingestion/home.md) 概觀。

## 將使用情況標籤套用至資料集

Adobe Experience Platform資料治理可讓您管理客戶資料，以確保符合資料使用適用的法規、限制和政策。 使用「資料使用標籤與實施」(DULE)作為其核心架構，「資料管理」可讓您套用使用標籤，以根據套用至該資料的使用原則來分類資料。

資料使用標籤可套用至整個資料集或個別資料集欄位。 在資料集層級新增的標籤會由該資料集內的所有欄位繼承。

如需服務 [的詳細資訊](../../data-governance/home.md) ，請參閱資料管理概觀。 如需如何在Experience Platform UI中使用使用標籤的步驟，請參閱資 [料使用標籤使用指南](../../data-governance/labels/user-guide.md)。

## 下游平台服務中的資料集

一旦使用資料集來儲存收錄的資料，下游平台服務就會使用這些資料集來更新客戶個人檔案、透過機器學習獲得深入資訊等。

以下是使用資料集進行各種操作的下游服務的清單。 請檢視每項服務的檔案，以取得更多資訊。

* [資料存取API](../../data-access/home.md):允許您訪問和下載儲存在資料集中的檔案的內容。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md):跨裝置和系統橋接身分識別，並根據資料集符合的XDM架構所定義的身分欄位，將資料集連結在一起。
* [即時客戶個人檔案](../../profile/home.md):利用Identity Service從資料集即時建立詳細的客戶個人檔案。 即時客戶從資料湖提取資料，並將客戶個人檔案保存在其個別的資料儲存中。
* [Adobe Experience Platform細分服務](../../segmentation/home.md):可讓您建立細分，並從即時客戶個人檔案資料產生受眾。 然後，這些觀眾可匯出至資料湖中的專屬資料集。
* [Adobe Experience Platform資料科學工作區](../../data-science-workspace/home.md):使用機器學習和人工智慧發掘大型資料集的見解。
* [Adobe Experience Platform查詢服務](../../query-service/home.md):可讓您使用標準SQL來查詢Experience Platform中的資料、加入Data Lake中的任何資料集，並將查詢結果擷取為新資料集，以用於報告、Data Science Workspace或即時客戶個人檔案。
* [Adobe Experience Platform決策服務](../../decisioning-service/home.md):利用「即時客戶配置檔案」，根據「配置檔案」從啟用的資料集提取的行為資料，確定客戶從一組選項中最可能做出的選擇。

## 後續步驟

閱讀本檔案後，您便瞭解了Experience Platform中資料集的核心用途，以及運用資料集的各種平台服務。 有關資料集在Platform中的多種使用方式的詳細資訊，請查看本概述中連結的服務文檔。

如需如何在Experience Platform UI中與資料集互動的步驟，請參閱資料 [集使用指南](user-guide.md)。