---
title: 目的地概觀
description: 目的地是預先建立的與目的地平台的整合，可無縫地從Adobe Experience Platform啟用資料。 您可以使用Adobe Experience Platform中的「目的地」，針對跨頻道行銷活動、電子郵件行銷活動、鎖定特定目標的廣告和許多其他使用案例，啟用已知和未知的資料。
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 6dd6190f1b006ffb3346eea6dc917ce52e0aa1c6
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 4%

---

# [!DNL Destinations] 概觀 {#overview}

![目的地概觀橫幅。](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## 目的地和來源 {#destinations-and-sources}

Platform的核心功能之一，就是擷取您的第一方資料，並根據您的業務需求加以啟用。 使用 [來源](../sources/home.md) 將資料內嵌至Platform和目的地，以從Platform匯出資料。

## 目的地步驟 {#steps}

* 從 [自助服務目錄](./catalog/overview.md) Platform中所有可用的目的地。
* 使用目的地將受眾或資料集傳送至行銷自動化平台、數位廣告平台等。
* 排程定期將資料匯出至您偏好的目的地。

## 控制項 {#controls}

中的控制項 [目的地工作區](./ui/destinations-workspace.md) 允許您：

* 瀏覽可啟用資料的目的地平台目錄；
* 建立、編輯、啟用和停用流向目錄中的目的地的資料流；
* 在儲存位置中建立帳戶，或將Platform連結至目的地平台中的帳戶；
* 選取應該對目的地啟用的對象或資料集；
* 選擇哪個 [體驗資料模型(XDM)欄位](../xdm/home.md) 將對象啟用至特定目的地（例如電子郵件行銷目的地、CRM平台、雲端儲存位置等）時，匯出的動作。
* 對目的地啟用不同型別的設定檔和對象 — 人員、帳戶和潛在客戶。

## 目的地型別和類別 {#types-and-categories}

透過Experience Platform，您可以對各種型別的目的地啟用資料，以滿足您的啟用使用案例。 目標範圍從API式整合，到與檔案接收系統、設定檔查詢目的地等的整合。 如需所有可用目的地的詳細資訊，請參閱 [目的地型別和類別概觀](./destination-types.md).

## Adobe建置和合作夥伴建置目的地 {#adobe-and-partner-built-destinations}

Experience Platform目標目錄中的一些聯結器是由Adobe建立和維護的，而其他聯結器是由合作夥伴公司透過以下專案建立和維護的： [Destination SDK](/help/destinations/destination-sdk/overview.md). 若合作夥伴已建立並維護目的地，檔案頁面頂端的備註會指出每個合作夥伴建立的聯結器。 例如， [Amazon S3聯結器](/help/destinations/catalog/cloud-storage/amazon-s3.md) 由Adobe建立，而 [TikTok聯結器](/help/destinations/catalog/social/tiktok.md) 是由TikTok團隊建立及維護。

對於合作夥伴編寫和維護的聯結器，這表示聯結器的問題可能需要由合作夥伴團隊解決（聯絡方法提供在檔案頁面的附註中）。 如需Adobe編寫和維護的聯結器發生問題，請聯絡您的Adobe代表或客戶服務。

## 目的地和存取控制 {#access-controls}

Platform中的目標功能可搭配Adobe Experience Platform存取控制許可權使用。 您可以檢視、管理和啟用目的地，實際取決於您的使用者許可權等級。 如需個別許可權的相關資訊，請前往 [Adobe Experience Platform中的存取控制](../access-control/home.md) 並向下捲動至頁面底部的表格。

下表概述對目的地執行特定動作所需的許可權和許可權組合。

| 許可權層級 | 說明 |
| ---- | ---- |
| **[!UICONTROL 檢視目的地]** | 若要存取Experience PlatformUI中的目的地索引標籤，您需要 **[!UICONTROL 檢視目的地]** [存取控制許可權](/help/access-control/home.md#permissions). |
| **[!UICONTROL 檢視目的地]**， **[!UICONTROL 管理目的地]** | 若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). |
| **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** | 若要對目的地啟用對象，並啟用 [對應步驟](ui/activate-batch-profile-destinations.md#mapping) 的工作流程中，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). |
| **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用沒有對應的區段]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** | 若要在現有資料流中新增或移除對象，而無須存取 [對應步驟](ui/activate-batch-profile-destinations.md#mapping) 的工作流程中，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用沒有對應的區段]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). |
| **[!UICONTROL 檢視目的地]**， **[!UICONTROL 管理和啟用資料集目的地]** | 若要將資料集匯出至目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理和啟用資料集目的地]** [存取控制許可權](/help/access-control/home.md#permissions). |
| **[!UICONTROL 檢視身分圖表]** | 要匯出 *身分* 若要前往目的地，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"} |

{style="table-layout:auto"}

下圖會依據您要在目的地執行的操作，以視覺化方式顯示您需要的許可權。

![此圖表顯示對目的地執行某些動作所需的許可權。](/help/destinations/assets/overview/permissions-diagram.png)

如需有關存取控制的詳細資訊，請參閱 [存取控制使用手冊](../access-control/ui/overview.md).

### 目的地的屬性型存取控制 {#attribute-based-access}

Adobe Experience Platform中基於屬性的存取控制可讓管理員根據屬性控制對特定物件和/或權能的存取。

透過以屬性為基礎的存取控制，您可以將對應設定套用至您有許可權的欄位。 此外，如果您無法存取資料集中的所有欄位，就無法將資料匯出至目的地。

如需有關目的地如何使用屬性型存取控制的詳細資訊，請參閱 [屬性型存取控制概觀](../access-control/abac/overview.md#destinations).

## 目的地監視 {#destinations-monitoring}

在建立與目的地的連線並完成啟動工作流程後，您可以監視匯出至接收系統的資料。 閱讀 [在UI中監控資料流到目的地的指南](/help/dataflows/ui/monitor-destinations.md) 以取得詳細資訊。

![目的地監視頁面範例。](./assets/overview/monitoring-page-example.png)

您也可以驗證資料是否成功到達您的目的地。 目錄中的大多數目的地檔案頁面都有 *驗證資料匯出區段*，會指示您如何從目的地平台簽入資料是否已成功從Experience Platform匯入。 檢視此區段的範例，瞭解 [Amazon Ads目的地](/help/destinations/catalog/advertising/amazon-ads.md#exported-data).

## 啟用目的地的資料治理限制 {#data-governance}

透過以下方式強制執行Platform目的地的資料控管：

* *行銷動作* 在「建立目的地」工作流程中選取的欄位；
* *資料使用原則* 會限制將包含特定使用標籤的資料啟用至具有特定行銷動作的目的地。

如需的詳細資訊，請參閱Platform檔案中的資料控管 [行銷動作](../data-governance/policies/overview.md) 和 [解決資料原則違規](../data-governance/enforcement/auto-enforcement.md).

如需在建立目標工作流程中選取行銷動作的詳細資訊，請參閱Platform中不同目標型別的下列頁面：

* [廣告目的地 — Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Advertising目的地 — Google Ads](./catalog/advertising/google-ads-destination.md)
* [廣告目的地 — Google顯示和影片360](./catalog/advertising/google-dv360.md)
* [雲端儲存空間目的地](./catalog/cloud-storage/overview.md)
* [電子郵件行銷目的地](./catalog/email-marketing/overview.md)
* [社交目的地](./catalog/social/overview.md)

如需對象啟動工作流程中資料原則違規的詳細資訊，請參閱 **[!UICONTROL 檢閱]** 請逐步執行下列指南：

* [啟用受眾資料至串流受眾匯出目的地](./ui/activate-segment-streaming-destinations.md#review)
* [啟用受眾資料至串流設定檔匯出目的地](./ui/activate-streaming-profile-destinations.md#review)
* [啟用對象資料至批次設定檔匯出目的地](./ui/activate-batch-profile-destinations.md#review)
