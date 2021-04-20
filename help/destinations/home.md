---
keywords: 目的地；adobe體驗平台；平台；目的地概觀；啟動資料；啟動；
title: 目的地概觀
seo-title: 目的地概觀
description: 瞭解如何將Adobe Experience Platform資料啟動至跨通道行銷宣傳、電子郵件、目標廣告等目的地。
seo-description: 目的地是與目的地平台預先建立的整合，可以順暢地啟動來自Adobe Experience Platform的資料。 您可以使用Adobe Experience Platform的「目的地」來啟用您已知和未知的跨通道行銷宣傳、電子郵件宣傳、目標廣告和許多其他使用案例資料。
exl-id: afd07ddc-652e-4e22-b298-feba27332462
translation-type: tm+mt
source-git-commit: 805cb72e91e6446f74cc3461d39841740eb576c7
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---

# [!DNL Destinations] 概觀 {#overview}

![目標概述橫幅](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** 是與目標平台預先建立的整合，讓Adobe Experience Platform的資料得以順暢啟動。您可以使用目的地來啟用跨通道行銷宣傳、電子郵件宣傳、目標廣告和許多其他使用案例的已知和未知資料。

## 目標和源{#destinations-and-sources}

Platform的核心功能之一是吸收您的第一方資料，並根據您的業務需求加以啟動。 使用[sources](../sources/home.md)將資料內嵌至平台，並使用目的地從平台匯出資料。

## 目標步驟{#steps}

* 從平台中所有可用目標的[自助目錄](./catalog/overview.md)中選擇。
* 使用目標[activate](./ui/activate-destinations.md)，並傳送個人檔案或區段至行銷自動化平台、數位廣告平台等。
* 定期排程匯出至您偏好目的地的資料。

## 控制{#controls}

[目標工作區](./ui/destinations-workspace.md)中的控制項可讓您：

* 瀏覽可啟動資料的目標平台目錄；
* 建立、編輯、啟用和停用目錄中目的地的資料流；
* 在儲存位置建立帳戶或將平台連結至目標平台中的帳戶；
* 選擇哪些區段應啟動至目標；
* 在啟動區段至電子郵件行銷目標時，選取要匯出的[體驗資料模型(XDM)欄位](../xdm/home.md)。

## 目標類型和類別{#types-and-categories}

有關詳細資訊，請參閱[目標類型和類別概述](./destination-types.md)。

## 目標和訪問控制{#access-controls}

Platform中的目標功能可與Adobe Experience Platform存取控制權限搭配使用。 視使用者的權限層級而定，您可以檢視、管理和啟用目標。 如需個別權限的詳細資訊，請參閱Adobe Experience Platform的[存取控制，並向下捲動至頁面底部。](../access-control/home.md)

有關訪問控制的詳細資訊，請參閱[訪問控制使用手冊](../access-control/ui/overview.md)。

## [!DNL Data Governance] 啟用資料至目的地的限制  {#data-governance}

平台目標的資料控管透過下列方式實施：

* *您可* 在建立目標工作流程中選擇的行銷動作；
* *資料使用* 策略，可限制包含特定使用標籤的資料被啟動至具有特定行銷動作的目的地。

有關[行銷動作](../data-governance/policies/overview.md)和[解決資料原則違規的詳細資訊，請參閱平台檔案中的[!DNL Data Governance]。](../data-governance/enforcement/auto-enforcement.md)

如需在建立目標工作流程中選取行銷動作的詳細資訊，請參閱「平台」中不同目標類型的下列頁面：

* [廣告目的地- Google Ad Manager  ](./catalog/advertising/google-ad-manager.md)
* [廣告目的地- Google Ads](./catalog/advertising/google-ads-destination.md)
* [廣告目的地- Google Display &amp; Video 360  ](./catalog/advertising/google-dv360.md)
* [雲端儲存空間目標](./catalog/cloud-storage/workflow.md)
* [電子郵件行銷目標](./catalog/email-marketing/overview.md)
* [社交目的地](./catalog/social/workflow.md)

如需區段啟動工作流程中違反資料原則的詳細資訊，請參閱[啟用設定檔和區段至目標](./ui/activate-destinations.md#review)中的「檢閱」步驟。
