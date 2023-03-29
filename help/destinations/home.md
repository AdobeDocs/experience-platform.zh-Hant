---
keywords: 目的地；adobe experience platform；平台；目的地概述；啟動資料；啟動；
title: 目的地概觀
description: 目的地是預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用Adobe Experience Platform中的目的地，針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# [!DNL Destinations] 概覽 {#overview}

![目的地概述橫幅](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## 目的地和來源 {#destinations-and-sources}

Platform的其中一項核心功能是擷取您的第一方資料，並根據您的業務需求加以啟用。 使用 [來源](../sources/home.md) 將資料內嵌至Platform和目的地，以便從Platform匯出資料。

## 目的地步驟 {#steps}

* 從 [自助式目錄](./catalog/overview.md) Platform中可用的所有目的地。
* 使用目的地將設定檔或區段傳送至行銷自動化平台、數位廣告平台等。
* 定期排程匯出至您偏好目的地的資料。

## 控制項 {#controls}

中的控制項 [目的地工作區](./ui/destinations-workspace.md) 允許您：

* 瀏覽可啟用資料的目的地平台目錄；
* 建立、編輯、啟用和停用流向目錄中目的地的資料流；
* 在儲存位置中建立帳戶，或將Platform連結至目標平台中的帳戶；
* 選取應將哪些區段啟動至目的地；
* 選取 [Experience Data Model(XDM)欄位](../xdm/home.md) 若要在啟用區段至電子郵件行銷目的地時匯出。

## 目的地類型和類別 {#types-and-categories}

透過Experience Platform，您可以針對各種類型的目的地啟用資料，以符合您的啟用使用案例。 目的地範圍包括API型整合、與檔案接收系統的整合、設定檔查詢目的地等。 如需所有可用目的地的詳細資訊，請參閱 [目的地類型與類別概觀](./destination-types.md).

## 目的地和存取控制 {#access-controls}

Platform中的目的地功能可與Adobe Experience Platform存取控制權限搭配使用。 您可以檢視、管理和啟用目的地，視使用者的權限層級而定。 如需個別權限的相關資訊，請參閱 [Adobe Experience Platform中的存取控制](../access-control/home.md) 並向下捲動至頁面底部。

下表概述在目的地執行特定動作所需的權限和權限組合：

| 權限層級 | 說明 |
| ---- | ----|
| **[!UICONTROL 管理目的地]** | 若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). |
| **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** | 若要啟用目的地的區段並啟用 [對應步驟](ui/activate-batch-profile-destinations.md#mapping) 工作流程中，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). |
| **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 啟用區段而不進行對應]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** | 若要啟用目的地的區段並隱藏 [對應步驟](ui/activate-batch-profile-destinations.md#mapping) 工作流程中，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 啟用區段而不進行對應]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). |

{style="table-layout:auto"}

如需存取控制的詳細資訊，請參閱 [存取控制使用手冊](../access-control/ui/overview.md).

### 目的地的基於屬性的存取控制 {#attribute-based-access}

Adobe Experience Platform中以屬性為基礎的存取控制可讓管理員根據屬性來控制特定物件和/或功能的存取。

使用基於屬性的訪問控制，您可以將映射配置應用到您有權限的欄位。 此外，如果您沒有資料集中所有欄位的存取權，則無法將資料匯出至目的地。

如需目標如何搭配屬性型存取控制運作的詳細資訊，請參閱 [基於屬性的訪問控制概述](../access-control/abac/overview.md#destinations).

## 目標監視 {#destinations-monitoring}

建立與目的地的連線並完成啟動工作流程後，您可以監控匯出至您接收系統的資料。 閱讀 [在UI中監控資料流到目的地的指南](/help/dataflows/ui/monitor-destinations.md) 以取得更多資訊。

您也可以驗證資料是否成功傳入您的目的地。 目錄中的大部分目的地檔案頁面都有 *驗證資料匯出區段*，指出如何在目標平台中檢查資料是否正從Experience Platform成功傳入。

## 針對將資料啟用至目的地的資料控管限制 {#data-governance}

Platform目的地的資料控管會透過下列方式強制執行：

* *行銷動作* （在「建立目標」工作流程中選取）;
* *資料使用原則* 限制包含特定使用標籤的資料啟動至具有特定行銷動作的目的地。

如需詳細資訊，請參閱Platform中的資料控管檔案 [行銷動作](../data-governance/policies/overview.md) 和 [解決資料策略違規](../data-governance/enforcement/auto-enforcement.md).

如需在建立目標工作流程中選取行銷動作的詳細資訊，請參閱下列頁面，了解Platform中不同目標類型的資訊：

* [廣告目的地 — Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [廣告目的地 — Google Ads](./catalog/advertising/google-ads-destination.md)
* [廣告目的地 — Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [雲端儲存目的地](./catalog/cloud-storage/overview.md)
* [電子郵件行銷目的地](./catalog/email-marketing/overview.md)
* [社交目的地](./catalog/social/overview.md)

如需區段啟動工作流程中違反資料原則的詳細資訊，請參閱 **[!UICONTROL 檢閱]** 步驟：

* [對串流區段匯出目的地啟用受眾資料](./ui/activate-segment-streaming-destinations.md#review)
* [對串流設定檔匯出目的地啟用受眾資料](./ui/activate-streaming-profile-destinations.md#review)
* [啟用受眾資料以批次設定檔匯出目的地](./ui/activate-batch-profile-destinations.md#review)
