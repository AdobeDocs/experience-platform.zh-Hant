---
keywords: 目的地；adobe experience platform；平台；目的地概述；啟動資料；啟動；
title: 目的地概觀
seo-title: 目的地概觀
description: 了解如何針對跨通路行銷宣傳、電子郵件、目標廣告等目的地啟用Adobe Experience Platform資料。
seo-description: 目的地是預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用Adobe Experience Platform中的目的地，針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: f73598224d527535aaf9ecb2aa1c26786cae2d82
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---

# [!DNL Destinations] 概觀 {#overview}

![目的地概述橫幅](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

## 目的地和來源 {#destinations-and-sources}

Platform的其中一項核心功能是擷取您的第一方資料，並根據您的業務需求加以啟用。 使用[sources](../sources/home.md)將資料內嵌至Platform和目的地，以便從Platform匯出資料。

## 目的地步驟 {#steps}

* 從Platform中所有可用目的地的[自助目錄](./catalog/overview.md)中選擇。
* 使用目的地來[啟用](./ui/activate-destinations.md)，並將設定檔或區段傳送至行銷自動化平台、數位廣告平台等。
* 定期排程匯出至您偏好目的地的資料。

## 控制項 {#controls}

[Destinations workspace](./ui/destinations-workspace.md)中的控制項可讓您：

* 瀏覽可啟用資料的目的地平台目錄；
* 建立、編輯、啟用和停用流向目錄中目的地的資料流；
* 在儲存位置中建立帳戶，或將Platform連結至目標平台中的帳戶；
* 選取應將哪些區段啟動至目的地；
* 在啟用區段至電子郵件行銷目的地時，選取要匯出的[體驗資料模型(XDM)欄位](../xdm/home.md)。

## 目的地類型和類別 {#types-and-categories}

如需詳細資訊，請參閱[目標類型和類別概述](./destination-types.md)。

## 目的地和存取控制 {#access-controls}

Platform中的目的地功能可與Adobe Experience Platform存取控制權限搭配使用。 您可以檢視、管理和啟用目的地，視使用者的權限層級而定。 如需個別權限的相關資訊，請參閱Adobe Experience Platform中的[存取控制項](../access-control/home.md)，然後向下捲動至頁面底部。

有關訪問控制的詳細資訊，請參閱[訪問控制使用手冊](../access-control/ui/overview.md)。

## [!DNL Data Governance] 對目的地啟用資料的限制 {#data-governance}

Platform目的地的資料控管會透過下列方式強制執行：

* *您可* 以在建立目標工作流程中選取的行銷動作；
* *限制包含* 特定使用標籤的資料啟動至具有特定行銷動作的目的地的資料使用政策。

如需[行銷動作](../data-governance/policies/overview.md)和[解決資料原則違反](../data-governance/enforcement/auto-enforcement.md)的詳細資訊，請參閱Platform檔案中的[!DNL Data Governance]。

如需在建立目標工作流程中選取行銷動作的詳細資訊，請參閱下列頁面，了解Platform中不同目標類型的資訊：

* [廣告目的地 — Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [廣告目的地 — Google Ads](./catalog/advertising/google-ads-destination.md)
* [廣告目的地 — Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [雲端儲存目的地](./catalog/cloud-storage/overview.md)
* [電子郵件行銷目的地](./catalog/email-marketing/overview.md)
* [社交目的地](./catalog/social/overview.md)

如需區段啟動工作流程中違反資料原則的詳細資訊，請參閱[啟動設定檔和區段至目的地](./ui/activate-destinations.md#review)中的檢閱步驟。
