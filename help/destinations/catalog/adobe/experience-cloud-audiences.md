---
title: (Beta)Experience Cloud受眾
description: 瞭解如何共用從Experience Platform到各種Experience Platform解決方案的細分市場。
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 2%

---

# (Beta) [!UICONTROL Experience Cloud觀眾] 連接

此目標允許您共用從Experience Platform到各種Experience Cloud解決方案的段，如Audience Manager、分析、Advertising Cloud、Adobe Campaign、目標或Marketo。

![Experience Cloud受眾目標，在目標目錄中突出顯示。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* 此目標將替換 [傳統段共用整合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) 從Experience Platform到各種Experience Cloud。
>* 此目標當前處於Beta中。 文檔和功能可能會更改。


## 使用案例和優勢 {#use-cases}

幫助您更好地瞭解您應如何以及何時使用 [!UICONTROL Experience Cloud觀眾] 目的地，以下是Adobe Experience Platform客戶可通過使用此目的地解決的示例使用案例。

### 啟用資料管理平台使用案例 {#dmp-use-cases}

在Audience Manager中，可以將Experience Platform段用於資料管理平台使用案例，例如：

* 添加 [第三方資料](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) 你的部門；
* [演算法塑型](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* 將段激活到Experience Platform目標目錄中尚不支援的基於cookie的目標。

### 導出段的粒度控制 {#segments-control}

通過Experience Cloud受眾目標使用新的自助服務段共用整合，以選擇要導出到Audience Manager及以外的段。 這允許您確定要與其他Experience Cloud解決方案共用的段以及要獨佔Experience Platform的段。

舊段共用整合不允許細粒度控制哪些段應導出到Audience Manager和更遠的區域。

### 共用Experience Platform分部及進一步Experience Cloud解決方案 {#share-segments-with-other-solutions}

除了與Audience Manager共用段外，Experience Platform受眾目標卡還允許您與您預配的任何其他Experience Cloud解決方案共用段，包括：

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share segments to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
> * 此目標可用於 [Adobe Real-time Customer Data PlatformPrime和Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。
> * 您需要Audience Manager許可證才能啟用 [資料管理平台使用案例](#dmp-use-cases) 上文。
> * 你 *不需要* 與Adobe Advertising Cloud、Adobe Target、Marketo和其他Experience Cloud解決方案共用Experience Platform分部的Audience Manager許可證。 [上](#share-segments-with-other-solutions)。


### 對於使用傳統段共用解決方案的客戶

如果您已通過以下方式共用了從Experience Platform到Audience Manager和其他Experience Cloud解決方案的段： [傳統段共用整合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam)，您必須聯繫「客戶服務」或您的Adobe客戶團隊以禁用舊式整合。 客戶關懷和Adobe帳戶團隊必須提交Jira票證(請參AAM閱模板票證–52354)才能禁用整合。

解決測試版客戶取消置備票證的週轉時間為6個工作日或更短。 禁用現有舊式整合後，您可以繼續 [建立連接](#connect) 自助目的卡。

>[!IMPORTANT]
>
>在Jira票證解析到通過目標卡建立新連接之間的時間內，將停止從Experience Platform導出到其他解決方案的段。 關閉Jira票證後，即可通過目標卡建立連接，從而最大限度地減少停機時間。

## 已知限制和註解 {#known-limitations}

請注意「Experience Cloud觀眾」卡的beta版中的以下已知限制和重要標注：

* [資料流監視](/help/dataflows/ui/monitor-destinations.md) 不支援。
* 連接到目標時，您可以看到一個選項 [啟用資料流警報](#enable-alerts)。 儘管在UI中可見， **不支援啟用警報選項** 測試版。
* **不支援回填**。 第一個向Audience Manager或其他Experience Cloud出口解決方案不包括這些分部的歷史人口。
* 在測試版中，您可以建立 **到Experience Cloud受眾目標的單個目標連接**，位於屬於您的Experience Platform組織的所有沙箱中。
* 有 **4小時延遲** 資料在Experience Platform中激活的時間與資料準備在Audience Manager和其他Experience Cloud解決方案中使用的時間之間。

## 支援的身份 {#supported-identities}

導出到的配置檔案 [!UICONTROL Experience Cloud觀眾] 目標映射到下表中描述的標識。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| ECID | Experience Cloud ID | 表示ECID的命名空間。 以下別名也可以引用此命名空間：&quot;Adobe Marketing CloudID&quot;,&quot;Adobe Experience CloudID&quot;,&quot;Adobe Experience PlatformID&quot; 請參閱以下文檔 [ECID](/help/identity-service/ecid.md) 的子菜單。 |
| GAID | Google廣告ID | 以Google廣告ID(GAID)的主要身份導入Experience Platform中的配置檔案可以導出到此目標。 |
| IDFA | Apple廣告商ID | 以AppleID(Dablocise Id)的主身份被引入Experience Platform中的配置檔案可以導出到此目標。 |
| email_lc_sha256 | 使用SHA256算法散列的電子郵件地址 | 將以散列電子郵件地址的主標識被Experience Platform的配置檔案導出到此目標。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，這些成員與上面一節中列出的標識相關聯。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

>[!IMPORTANT]
> 
>在Beta版本中，您可以跨屬於您的Experience Cloud組織的所有沙箱建立到Experience Platform觀眾目標的單個目標連接。

### 驗證到目標 {#authenticate}

要驗證到目標，請選擇 **[!UICONTROL 設定]** 在目錄中的目標卡視圖中，然後選擇 **[!UICONTROL 連接到目標]**。

![「連接到目標」選項的「Experience Cloud受眾」目標的視圖。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

![配置新目標螢幕，顯示連接到Experience Cloud受眾目標所需的和可選的設定。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。


## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。 注意否 [映射步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 必需，否 [調度步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 可用於此目標。

## 驗證資料導出 {#exported-data}

要驗證資料導出是否成功，您可以檢查資料段是否已成功傳送到所需的Experience Cloud解決方案。

### 驗證Audience Manager中的資料

您的Experience Platform段在Audience Manager中顯示為 [信號](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals)。 [性狀](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits), [段](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments)。 您可以在Audience Manager中驗證資料是否如上文檔連結中所述出現。

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料治理概述](/help/data-governance/home.md)。

Experience Platform中的資料治理由兩者實施 [資料使用標籤](/help/data-governance/labels/reference.md) 和營銷行動。
資料使用標籤將傳輸到應用程式，但市場營銷操作將不會。 這意味著，一旦它們降落在Audience Manager中，Experience Platform中的片段就可以輸出到任何可用目的地。 在Audience Manager中，您可以 [資料導出控制項](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) 阻止段導出到某些目標。

### Audience Manager中的權限管理

Audience Manager中的片段和特徵 [基於角色的訪問控制](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=zh-Hant) (RBAC)。

從Experience Platform導出的段被分配給Audience Manager中的特定資料源 **[!UICONTROL Experience Platform段]**。

要僅允許某些用戶訪問資料段，可以對屬於資料源的資料段應用訪問控制。 必須在Audience Manager中為這些段和從Experience Platform段建立的特徵設定新的訪問控制權限。
