---
keywords: 目的地；adobe體驗平台；平台；目標概述；激活資料；activate;
title: 目的地概觀
description: 目的地是預先構建的與目標平台的整合，這些平台允許從Adobe Experience Platform無縫激活資料。 您可以使用Adobe Experience Platform的目標來激活您已知的和未知的資料，以用於跨渠道營銷活動、電子郵件活動、目標廣告和許多其他使用案例。
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# [!DNL Destinations] 概覽 {#overview}

![目標概述標題](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## 目標和來源 {#destinations-and-sources}

平台的一個核心功能是接收您的第一方資料，並根據您的業務需要激活它。 使用 [來源](../sources/home.md) 將資料導入平台和目標，以從平台導出資料。

## 目標步驟 {#steps}

* 從 [自助目錄](./catalog/overview.md) 平台中所有可用目的地。
* 使用目標向營銷自動化平台、數字廣告平台等發送配置檔案或段。
* 計畫定期向首選目標導出資料。

## 控制項 {#controls}

中的控制項 [目標工作區](./ui/destinations-workspace.md) 允許您：

* 瀏覽可激活資料的目標平台目錄；
* 建立、編輯、激活和禁用流向目錄中目標的資料流；
* 在儲存位置建立帳戶或將平台連結到目標平台中的帳戶；
* 選擇應激活到目標的段；
* 選擇 [體驗資料模型(XDM)欄位](../xdm/home.md) 在將段激活到電子郵件營銷目標時導出。

## 目標類型和類別 {#types-and-categories}

通過Experience Platform，您可以將資料激活到各種類型的目標，以滿足您的激活使用案例。 目標範圍從基於API的整合到與檔案接收系統的整合、配置檔案查找目標等。 有關所有可用目標的詳細資訊，請參閱 [目標類型和類別概述](./destination-types.md)。

## 目標和訪問控制 {#access-controls}

平台中的目標功能與Adobe Experience Platform訪問控制權限配合使用。 根據用戶的權限級別，您可以查看、管理和激活目標。 有關單個權限的資訊，請參見 [Adobe Experience Platform的訪問控制](../access-control/home.md) 向下滾動到頁面底部。

下表概述了在目標上執行某些操作所需的權限和權限組合：

| 權限級別 | 說明 |
| ---- | ----|
| **[!UICONTROL 管理目標]** | 要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 |
| **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** | 將段激活到目標並啟用 [映射步驟](ui/activate-batch-profile-destinations.md#mapping) 工作流中，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 |
| **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 激活段而不映射]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** | 將段激活到目標並隱藏 [映射步驟](ui/activate-batch-profile-destinations.md#mapping) 工作流中，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 激活段而不映射]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 |

{style="table-layout:auto"}

有關訪問控制的詳細資訊，請參見 [訪問控制使用手冊](../access-control/ui/overview.md)。

### 目標的基於屬性的訪問控制 {#attribute-based-access}

Adobe Experience Platform基於屬性的訪問控制允許管理員基於屬性控制對特定對象和/或權能的訪問。

使用基於屬性的訪問控制，您可以將映射配置應用到您具有權限的欄位。 此外，如果您沒有訪問資料集中所有欄位的權限，則無法將資料導出到目標。

有關目標如何使用基於屬性的訪問控制的詳細資訊，請閱讀 [基於屬性的訪問控制概述](../access-control/abac/overview.md#destinations)。

## 目標監視 {#destinations-monitoring}

在建立到目標的連接並完成激活工作流後，您可以監視導出到接收系統的資料。 閱讀 [有關監視資料流到UI中目標的指南](/help/dataflows/ui/monitor-destinations.md) 的子菜單。

您還可以驗證資料是否成功傳遞到目標。 目錄中的大多數目標文檔頁面 *驗證資料導出部分*，指示如何簽入目標平台，以便從Experience Platform成功導入資料。

## 將資料激活到目標的資料治理限制 {#data-governance}

通過以下方式為平台目標強制實施資料治理：

* *市場營銷操作* 可在建立目標工作流中選擇；
* *資料使用策略* 限制包含某些使用標籤的資料被激活到具有某些市場營銷操作的目標。

有關更多資訊，請參閱平台中的資料治理文檔 [營銷活動](../data-governance/policies/overview.md) 和 [解決資料策略違規](../data-governance/enforcement/auto-enforcement.md)。

有關在建立目標工作流中選擇市場營銷操作的詳細資訊，請參閱以下有關平台中不同目標類型的頁面：

* [廣告目的地 — Google廣告經理 ](./catalog/advertising/google-ad-manager.md)
* [廣告目的地 — Google廣告](./catalog/advertising/google-ads-destination.md)
* [廣告目的地 — GoogleDisplay &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [雲儲存目標](./catalog/cloud-storage/overview.md)
* [電子郵件營銷目標](./catalog/email-marketing/overview.md)
* [社會目的地](./catalog/social/overview.md)

有關段激活工作流中違反資料策略的詳細資訊，請參見 **[!UICONTROL 審閱]** 的下界：

* [將受眾資料激活到流段導出目標](./ui/activate-segment-streaming-destinations.md#review)
* [激活受眾資料以流式處理配置檔案導出目標](./ui/activate-streaming-profile-destinations.md#review)
* [將受眾資料激活到批配置檔案導出目標](./ui/activate-batch-profile-destinations.md#review)
