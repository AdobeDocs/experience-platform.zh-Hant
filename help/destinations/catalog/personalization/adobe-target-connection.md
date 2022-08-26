---
keywords: 目標個性化；目的地；體驗平台目標；adobe目標目標；
title: Adobe Target
description: Adobe Target是一個應用程式，在跨網站、移動應用等的所有入站客戶交互中提供基於人工智慧的即時個性化和實驗功能。
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 769d3f14e858ed69c6bb50360da90e4e0816a377
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 1%

---

# Adobe Target {#adobe-target-connection}

## 目標更改日誌 {#changelog}

>[!IMPORTANT]
>
>通過增強的Adobe TargetV2目標連接器的beta版本，您可能在目標目錄中看到兩個Adobe Target卡。
>Adobe TargetV2目標連接器目前處於測試版，只適用於特定數量的客戶。 除了AdobeV1卡提供的功能外，目標V2連接器還 [映射步驟](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) 激活工作流，它允許您將配置檔案屬性映射到Adobe Target，從而啟用基於屬性的同頁和下一頁個性化。

![兩張Adobe Target目的卡並排顯示的影像。](/help/destinations/assets/catalog/personalization/adobe-target-connection/adobe-target-side-by-side-view.png)

## 總覽 {#overview}

Adobe Target是一個應用程式，在跨網站、移動應用等的所有入站客戶交互中提供基於人工智慧的即時個性化和實驗功能。

Adobe Target是Adobe Experience Platform目的地目錄中的個性化連接。

## 先決條件 {#prerequisites}

### 資料流ID {#datastream-id}

將Adobe Target連接配置為 [使用資料流ID](#parameters)，您必須 [Adobe Experience PlatformWeb SDK](../../../edge/home.md) 執行。

在不使用資料流ID的情況下配置Adobe Target連接不需要您實現Web SDK。

>[!IMPORTANT]
>
>在建立 [!DNL Adobe Target] 連接，閱讀有關如何 [為同一頁和下一頁個性化設定配置個性化目標](../../ui/configure-personalization-destinations.md)。 本指南將引導您跨多個Experience Platform元件完成同一頁和下一頁個性化使用案例所需的配置步驟。 同頁和下一頁個性化要求您在配置Adobe Target連接時使用資料流ID。

### Adobe Target的先決條件 {#prerequisites-in-adobe-target}

在Adobe Target，確保您的用戶：

* 訪問 [預設工作區](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#default-workspace);
* 的 **批准者** [角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#roles-and-permissions)。

閱讀有關授予權限的詳細資訊 [目標高級](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=en#section_8C425E43E5DD4111BBFC734A2B7ABC80) 和 [目標標準](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=en#roles-permissions)。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!DNL Profile request]** | 您正在請求在Adobe Target目標中映射的所有段以獲得單個配置檔案。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style=&quot;table-layout:auto&quot;}

## 使用案例 {#use-cases}

**個性化首頁標題**

一家房屋租賃和銷售公司希望根據Adobe Experience Platform的客戶細分資格，在自己的首頁上打出一個標語，個性化自己的首頁。 公司可以選擇哪些受眾應該獲得個性化體驗，並將這些體驗作為目標服務的目標標準發送給Adobe Target。

## 連接到目標 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="關於資料流ID"
>abstract="此選項確定將包含段的資料收集資料流的位置。 下拉菜單僅顯示啟用了目標配置的資料流。 要使用邊緣分割，必須選擇資料流ID。 選擇「無」(None)將禁用使用邊分割的所有使用情形。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="瞭解有關選擇資料流的詳細資訊"

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

Adobe Experience Platform自動連接到您公司的Adobe Target實例。 不需要身份驗證。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **名稱**:填寫此目標的首選名稱。
* **說明**:輸入目標的說明。 例如，您可以提及您為此目標使用的市場活動。 此欄位為可選欄位。
* **資料流ID**:這確定將包含段的資料收集資料流的位置。 下拉菜單僅顯示已啟用目標目標的資料流。 請參閱 [配置資料流](../../../edge/datastreams/overview.md#target) 有關如何為Adobe Target配置資料流的詳細資訊。
   * **[!UICONTROL 無]**:如果需要配置Adobe Target個性化設定，但無法實施 [Experience PlatformWeb SDK](../../../edge/home.md)。 使用此選項時，從Experience Platform導出到目標的段僅支援下一會話個性化，並且會禁用邊緣分割。 有關詳細資訊，請參閱下表。

| 未選擇任何資料流 | 已選擇資料流 |
|---|---|
| <ul><li>[邊緣分割](../../../segmentation/ui/edge-segmentation.md) 不支援。</li><li>[同頁和下頁個性化](../../ui/configure-personalization-destinations.md) 不支援。</li><li>您只能為生產沙盒共用段到Adobe Target連接。</li><li>要配置下一會話個性化而不使用資料流ID，請使用 [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en)。</li></ul> | <ul><li>邊緣分割按預期工作。</li><li>[同頁和下頁個性化](../../ui/configure-personalization-destinations.md) 。</li><li>其他沙箱支援段共用。</li></ul> |

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以配置請求目標](../../ui/activate-profile-request-destinations.md) 有關激活此目標受眾段的說明。

## 導出的資料 {#exported-data}

Adobe Target從Adobe Experience Platform邊緣網路讀取配置檔案資料，因此不會導出任何資料。

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)。
