---
title: 目標激活工作流中的身份處理
description: 瞭解如何根據目標類型在激活工作流中處理身份導出
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 1%

---

# 目標激活工作流中的身份處理

本頁介紹如何將標識導出到不同的目標類型，並教您如何根據目標查找哪些標識可供導出。

>[!TIP]
>
> 有關身份、身份命名空間和身份相關術語定義的詳細資訊，請閱讀 [身份服務概述](/help/identity-service/home.md)。

中的每個目標 [目錄](/help/destinations/catalog/overview.md) 略有不同，因此所有目標上都沒有一刀切的設定。 但是，有一些模式可指導目標的設定及其身份要求，如下面各節所述。

## 基於檔案的目標 {#file-based}

對於 [基於檔案的目標](/help/destinations/destination-types.md#file-based) (例如 [!DNL Amazon S3], SFTP，大多數電子郵件營銷目標，如 [!DNL Adobe Campaign]。 [!DNL Oracle Eloqua]。 [!DNL Salesforce Marketing Cloud])，這些目標中的大多數標識設定是開啟的，這意味著您不需要在 [選擇屬性](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) 批處理激活工作流的步驟。

如果選擇將標識添加到檔案導出中，請注意， [標識命名空間](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) 可在導出中選擇。 選擇要導出的標識時，將自動將其選為 [必備屬性](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) 和 [重複資料消除密鑰](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys)。

![選作強制屬性和重複資料消除密鑰的標識。](/help/destinations/assets/how-destinations-work/selected-identity.png)

作為解決方法，如果這些標識已作為屬性被引入Experience Platform中，則可以將更多標識添加到導出中。 請參見下面的示例，其中除了標識命名空間外，還選擇了XDM屬性電子郵件地址進行導出 `Phone_E.164`。

![選擇導出的電子郵件地址屬性示例。](/help/destinations/assets/how-destinations-work/email-selected.png)

## 從身份映射導出身份與將身份導出為XDM屬性 — 差異 {#identity-map-or-attribute}

導出的記錄數可能不同，具體取決於您是從身份映射中選擇導出身份，還是將作為屬性被攝取到Experience Platform中的身份。 [合併策略](/help/profile/merge-policies/overview.md) 在從身份映射中選擇身份時導出的記錄數中，還扮演著重要角色。

例如，請考慮從兩個不同的資料集中，您有以下配置檔案片段將合併到單個客戶配置檔案中：

**配置檔案片段1**

| 身份映射 | 「名字」 | 「姓氏」 | 電子郵件屬性 |
|---------|----------|---------|--------|
| email1，會員ID1 | 約翰 | 多伊 | 電子郵件1 |


**配置檔案片段2**

| 身份映射 | 「名字」 | 「姓氏」 | 電子郵件屬性 |
|---------|----------|---------|--------|
| email2，會員ID1 | 約翰 | 多伊 | 電子郵件2 |

合併的配置檔案如下所示：

| 身份映射 | 「名字」 | 「姓氏」 | 電子郵件屬性 |
|---------|----------|---------|--------|
| 電子郵件1，電子郵件2，會員ID1 | 約翰 | 多伊 | 電子郵件2 |

導出行為因是否選擇 `IdentityMap: Email` 或 `xdm: personalEmail.address` 的下界。

如果客戶激活 `IdentityMap: Email`，導出檔案中將有兩條記錄，一條用於email1，另一條用於email2。

但是，如果客戶激活 `xdm: personalEmail.address`，只有email2會出現在記錄中，因為email屬性欄位只包括email2。 這些情況可以解決不同的使用情形：您可能希望激活客戶檔案中的所有電子郵件地址，或者只激活客戶檔案中最近的電子郵件地址。

其結論是，導出的記錄數取決於您選擇的合併策略以及您是否在導出中選擇標識或屬性。

## 基於API的流目標 {#streaming-destinations}

[基於API的流目標](/help/destinations/destination-types.md#streaming-destination) 內置 [Destination SDK](/help/destinations/destination-sdk/overview.md) (例如 [!DNL Facebook]。 [!DNL Google Customer Match]。 [!DNL Pinterest]。 [!DNL Braze]、等)僅支援特定ID以進行導出。 有關可導出到每個目標的特定標識的詳細資訊，請閱讀 *支援的身份* 每個目標文檔頁中的部分(例如，請參見 [支援的標識部分](/help/destinations/catalog/advertising/pinterest.md) 的 [!DNL Pinterest] 目標頁)。

但請注意，您可以靈活地使用 [私有圖](/help/profile/merge-policies/overview.md#id-stitching) 或從屬性中作為身份。 這意味著您可以將XDM屬性映射到目標所需的標識欄位。 請參閱下面的示例 [!DNL Pinterest] 目標，其中XDM屬性 `personalEmail.address` 映射到必需 [!DNL Pinterest] 身份 `pinterest_audience`。

>[!TIP]
>
>如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項，使Experience Platform在激活時自動對資料進行散列。 閱讀有關 **[!UICONTROL 應用轉換]** 的上界 [流式目標激活教程](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation)。

![映射到Pinterest目標的標識欄位的電子郵件地址屬性示例。](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### 依賴第三方Cookie整合的廣告目標 {#third-party-cookie-destinations}

依賴第三方Cookie的廣告目標(例如： [!DNL Google Ads]。 [!DNL Google Ad Manager]。 [!DNL Google DV360]。 [!DNL Bing]。 [!DNL The Trade Desk])不要求客戶在激活工作流中選擇ID。 對於這些目標，在設定激活工作流時，Experience Platform會自動查找由 [[!UICONTROL Experience CloudID服務]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant) 並導出可用於配置檔案且受目標支援的所有標識。

這些目標需要通過以下任一ID同步 [!UICONTROL Experience CloudID服務] 或 [!UICONTROL Experience PlatformWeb SDK]。

如果您使用 [!UICONTROL Experience PlatformWeb SDK] 和遺產 [!UICONTROL Experience CloudID服務] 未在頁面上實現，則您需要確保相關網站的資料流已啟用以允許第三方ID同步，如 [配置datastream文檔](/help/edge/datastreams/configure.md#create)。

在配置資料流時，您需要確保 **[!UICONTROL 第三方ID同步]** 已啟用滑塊。 大多數客戶將 `container_id` 欄位為空（預設為0）。 只有在舊式Audience Manager實施使用特定容器ID時，您才需要更改此值（但請注意，這將是絕大多數客戶的情況）。

>[!NOTE]
>
>這些廣告目的地大多受Audience Manager支援(這些目標類型在Audience Manager中稱為基於設備的目的地。 查看 [Audience Manager中所有支援的基於設備的目標清單](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=en))。 只有少數列在Experience Platform。 有關在Experience Platform和Audience Manager之間共用資料的資訊，請閱讀 [啟用資料共用從Experience Platform到Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#enable-aep-to-aam-data)。 目前，沒有計畫支援更多第三方Cookie目標。

## 企業目標 {#enterprise-destinations}

[企業目標](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis]。 [!DNL Azure Event Hubs], HTTP API)在資料導出中不需要特定ID，因為這些ID是針對企業整合使用情形設計的。 但是，如果需要，可以將標識導出為XDM屬性或從標識映射中導出。 查看 [將資料導出到HTTP目標的示例](/help/destinations/catalog/streaming/http-destination.md#exported-data)，包括 `personalEmail.address` XDM屬性和標識 `ECID` 和 `email_lc_sha256` （散列電子郵件地址）。

## 個性化目標 {#personalization-destinations}

[個性化（或邊緣）目標](/help/destinations/destination-types.md#edge-personalization-destinations) (例如：Adobe Target, [!DNL Custom Personalization])不需要在激活工作流中選擇任何身份，因為整合是配置檔案查找。 客戶端([!DNL Target]。 [!DNL Web SDK]、或其他)查詢 [[!UICONTROL 邊緣]](/help/collection/home.md#edge) 並提取現場個性化所需的配置檔案資訊。

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## 後續步驟 {#next-steps}

閱讀此文檔後，您現在知道如何確定各個目標支援或需要哪些身份。 您現在還知道每個目標類型的身份選擇工作原理。

接下來，你可以閱讀 [導出設定](/help/destinations/how-destinations-work/destinations-configurations.md) 對於目標，在目標類型之間是通用的，這些類型可由開發人員在單個目標級別上配置，以及哪些設定可由激活工作流中的用戶編輯。

您還可以在 [目錄](/help/destinations/catalog/overview.md)。
