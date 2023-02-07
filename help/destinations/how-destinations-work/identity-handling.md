---
title: 目的地啟動工作流程中的身分處理
description: 了解在啟動工作流程中如何根據目的地類型處理身分匯出
source-git-commit: 372231ab4fc1148c1c2c0c5fdbfd3cd5328b17cc
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 1%

---

# 目的地啟動工作流程中的身分處理

本頁面說明如何將身分匯出至不同目的地類型的特殊性，並說明如何根據目的地尋找可供匯出的身分。

>[!TIP]
>
> 如需身分識別、身分識別命名空間及身分相關詞語定義的詳細資訊，請參閱 [identity服務概述](/help/identity-service/home.md).

中的每個目的地 [目錄](/help/destinations/catalog/overview.md) 稍微不同，因此所有目的地都沒有一刀切的設定。 不過，以下各節會說明一些模式，以引導目的地的設定及其身分需求。

## 檔案型目的地 {#file-based}

針對 [檔案型目的地](/help/destinations/destination-types.md#file-based) (例如 [!DNL Amazon S3]、SFTP、大部分電子郵件行銷目的地，例如 [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud])，則這些目的地中的身分設定皆會開啟，這表示您不需要在 [選擇屬性](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) 批次啟動工作流程的步驟。

如果您選擇將身分新增至檔案匯出，請注意， [身分命名空間](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) 可在匯出中選取。 當您選取要匯出的身分時，系統會自動將其選取為 [強制屬性](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) 和 [去重複化金鑰](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![選作強制屬性和重複資料刪除索引鍵的身分。](/help/destinations/assets/how-destinations-work/selected-identity.png)

若已將身分擷取至Experience Platform作為屬性，您可以將更多身分新增至匯出。 請參閱下方的範例，其中除了身分命名空間外，還選取要匯出的XDM屬性電子郵件地址 `Phone_E.164`.

![選取要匯出的電子郵件地址屬性範例。](/help/destinations/assets/how-destinations-work/email-selected.png)

## 從身分對應匯出身分與將身分匯出為XDM屬性之間的差異 {#identity-map-or-attribute}

匯出的記錄數可能會因您是否從身分對應選取以匯出身分，或是已擷取為屬性的身分識別，而有所不同。 [合併策略](/help/profile/merge-policies/overview.md) 從身分對應中選取身分時，也會在匯出的記錄數中扮演重要角色。

例如，假設您有兩個不同的資料集，且有下列設定檔片段將合併至單一客戶設定檔中：

**設定檔片段一**

| 身分對應 | 「名字」 | 「姓氏」 | 電子郵件屬性 |
|---------|----------|---------|--------|
| email1，忠誠度ID1 | 約翰 | Doe | 電子郵件1 |


**設定檔片段二**

| 身分對應 | 「名字」 | 「姓氏」 | 電子郵件屬性 |
|---------|----------|---------|--------|
| email2，忠誠度ID1 | 約翰 | Doe | 電子郵件2 |

合併的設定檔如下所示：

| 身分對應 | 「名字」 | 「姓氏」 | 電子郵件屬性 |
|---------|----------|---------|--------|
| 電子郵件1、電子郵件2、忠誠度ID1 | 約翰 | Doe | 電子郵件2 |

根據您是否選取 `IdentityMap: Email` 或 `xdm: personalEmail.address` ，以匯出。

如果客戶啟用 `IdentityMap: Email`，則匯出的檔案中會有兩筆記錄，一筆用於email1，另一筆用於email2。

不過，如果客戶啟用 `xdm: personalEmail.address`，記錄中將只會顯示email2，因為email屬性欄位僅包含email2。 這些情況可以解決不同的使用案例，您可能會想要針對客戶的檔案中所有電子郵件地址或針對客戶檔案中最近的電子郵件地址進行啟用。

外觀是，您導出的記錄數取決於您選擇的合併策略，以及您在導出中是否選擇身份或屬性。

## 以API為基礎的串流目的地 {#streaming-destinations}

[以API為基礎的串流目的地](/help/destinations/destination-types.md#streaming-destination) 內建 [Destination SDK](/help/destinations/destination-sdk/overview.md) (例如 [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze]、等)僅支援特定ID以供匯出。 如需可匯出至每個目的地的特定身分的詳細資訊，請參閱 *支援的身分* 區段(例如，請參閱 [支援身分區段](/help/destinations/catalog/advertising/pinterest.md) 在 [!DNL Pinterest] 目的地頁面)。

不過，請注意，您有彈性使用 [專用圖表](/help/profile/merge-policies/overview.md#id-stitching) 或從屬性作為身分。 這表示您可以將XDM屬性對應至目的地所需的身分欄位。 請參閱下方的範例，以取得 [!DNL Pinterest] 目的地，其中XDM屬性 `personalEmail.address` 已對應至必要 [!DNL Pinterest] 身分 `pinterest_audience`.

>[!TIP]
>
>當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，讓Experience Platform在啟動時自動雜湊資料。 深入了解 **[!UICONTROL 套用轉換]** 選項 [串流目的地啟動教學課程](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![對應至Pinterest目的地身分欄位的電子郵件地址屬性範例。](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### 依賴協力廠商Cookie整合的廣告目的地 {#third-party-cookie-destinations}

依賴第三方Cookie的廣告目的地(例如： [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk])不要求客戶在啟用工作流程中選取ID。 針對這些目標，設定啟動工作流程時，Experience Platform會自動尋找由 [[!UICONTROL Experience CloudID服務]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant) 和會匯出可用於設定檔且受目的地支援的所有身分。

這些目的地需要ID同步，才能透過 [!UICONTROL Experience CloudID服務] 或 [!UICONTROL Experience PlatformWeb SDK].

如果您使用 [!UICONTROL Experience PlatformWeb SDK] 和舊 [!UICONTROL Experience CloudID服務] 未在頁面上實作，則您必須確保相關網站的資料流已啟用，以允許第三方ID同步，如 [設定datastream檔案](/help/edge/datastreams/configure.md#create).

如上述連結的檔案所述設定資料流時，您必須確保 **[!UICONTROL 第三方ID同步]** 滑桿已啟用。 大部分客戶會 `container_id` 欄位空白（預設為0）。 只有在舊版Audience Manager實作使用特定容器ID時，您才需要變更此值（但請注意，這將是絕大多數客戶）。

>[!NOTE]
>
>這些廣告目的地大多受Audience Manager支援(這些目的地類型在Audience Manager中稱為以裝置為基礎的目的地。 請參閱 [Audience Manager中所有支援的以裝置為基礎的目的地清單](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=en))。 只有少數幾個列在Experience Platform中。 如需在Experience Platform和Audience Manager之間共用資料的相關資訊，請閱讀 [啟用資料從Experience Platform到Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#enable-aep-to-aam-data). 目前並無計畫支援更多協力廠商Cookie目的地。

## 企業目的地 {#enterprise-destinations}

[企業目的地](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], HTTP API)在資料匯出中不需要特定ID，因為這些ID是針對企業整合使用案例而設計。 不過，您也可以視需要將身分匯出為XDM屬性，或從身分對應匯出。 檢視 [將資料導出到HTTP目標的示例](/help/destinations/catalog/streaming/http-destination.md#exported-data)，其中包含 `personalEmail.address` XDM屬性和身分 `ECID` 和 `email_lc_sha256` （雜湊電子郵件地址）。

## 個人化目的地 {#personalization-destinations}

[個人化（或Edge）目的地](/help/destinations/destination-types.md#edge-personalization-destinations) (例如：Adobe Target, [!DNL Custom Personalization])，因為整合是設定檔查閱，因此在啟用工作流程中不需要任何身分選取。 客戶端([!DNL Target], [!DNL Web SDK]，或其他)查詢 [[!UICONTROL Edge]](/help/collection/home.md#edge) 和會提取其進行站上個人化所需的設定檔資訊。

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何找出個別目的地支援或需要的身分。 您現在也知道身分選擇對於每個目的地類型的運作方式。

接下來，你可以讀到 [匯出設定](/help/destinations/how-destinations-work/destinations-configurations.md) 目的地在各種目的地類型中都很常見，開發人員可在個別目的地層級上設定，而使用者可在啟用工作流程中編輯哪些設定。

您也可以查看 [目錄](/help/destinations/catalog/overview.md).