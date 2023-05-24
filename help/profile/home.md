---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API；統一配置檔案；統一配置檔案；配置檔案；rtcp;XDM圖形
title: 即時客戶概要資訊概述
description: 即時客戶配置檔案合併來自各種來源的資料，並以單個客戶配置檔案和相關時間系列事件的形式提供對這些資料的訪問。 此功能使營銷人員能夠跨多個渠道與其受眾進行協調、一致和相關的體驗。
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] 概覽

Adobe Experience Platform使您能夠為您的客戶提供協調、一致和相關的體驗，無論客戶在何處或何時與您的品牌進行交互。 與 [!DNL Real-Time Customer Profile]，通過組合來自多個渠道（包括線上、離線、CRM和第三方）的資料，您可以看到每個客戶的整體視圖。 [!DNL Profile] 允許您將客戶資料整合到一個統一視圖中，為每次客戶交互提供一個可操作且時間戳記的帳戶。 本概述將幫助您瞭解 [!DNL Real-Time Customer Profile] 在 [!DNL Experience Platform]。

## [!DNL Profile] Experience Platform

Real-Time Customer Profile與Experience Platform內其他服務之間的關係在以下圖中突出顯示：

![Real-Time Customer Profile與Adobe Experience Platform其他服務之間的關係。 此圖表顯示Profile是Adobe Experience Platform的核心元件之一。](images/profile-overview/profile-in-platform.png)

## 瞭解配置檔案

[!DNL Real-Time Customer Profile] 合併來自各種企業系統的資料，然後以客戶配置檔案的形式提供對該資料的訪問，並顯示相關的時間系列事件。 此功能使營銷人員能夠跨多個渠道與其受眾進行協調、一致和相關的體驗。 以下各節重點介紹一些必須瞭解的核心概念，以便在平台內有效地構建和維護配置檔案。

### 配置檔案實體組合

即時客戶配置檔案由主實體組成，稱為 **主實體**&#x200B;以及各種配套實體。 在Experience Platform上下文中，主實體通常是 **配置檔案實體**&#x200B;由個人的特徵，行為和分會員構成。 其它實體允許分割引擎利用輪廓的主實體之外的資料，並包括：

- **維實體**:用於簡化資料建模過程的實體，用於在事件或配置檔案記錄之間共用資訊。 這也稱為查找實體或分類實體。
- **B2B實體**:描述配置檔案與業務對業務客戶和機會關係的實體。

![說明配置檔案圖元組成的圖。](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>由於維實體和B2B實體僅存在於主實體之外，因此它們僅用於批分割。

維實體和B2B實體通過 **架構關係**。 有關詳細資訊，請參閱以下文檔：

- [為查找實體建立一對一架構關係](../xdm/tutorials/relationship-ui.md)
- [為B2B實體建立多對一模式關係](../xdm/tutorials/relationship-b2b.md)

### 配置檔案資料儲存

儘管 [!DNL Real-Time Customer Profile] 處理所測資料和使用Adobe Experience Platform [!DNL Identity Service] 通過身份映射來合併相關資料，在中維護自己的資料 [!DNL Profile] 資料儲存。 的 [!DNL Profile] 儲存與資料湖中的目錄資料分離， [!DNL Identity Service] 標識圖中的資料。

配置檔案儲存使用MicrosoftAzure Cosmos DB基礎架構，平台資料湖使用MicrosoftAzure資料湖儲存。

### 輪廓護欄

Experience Platform提供一系列護欄，幫助您避免建立 [體驗資料模型(XDM)架構](../xdm/home.md) Real-Time Customer Profile不能支援。 這包括導致效能降低的軟限制，以及導致錯誤和系統中斷的硬限制。 有關詳細資訊，包括指南和示例使用案例清單，請閱讀 [輪廓護欄](guardrails.md) 文檔。

### 配置檔案儀表板 {#profile-dashboard}

Experience PlatformUI提供了一個儀表板，您可以通過該儀表板查看有關即時客戶配置檔案資料的重要資訊，這些資訊在每日快照中捕獲。 瞭解如何訪問和使用 [!DNL Profile] UI中的儀表板，以及有關儀表板中顯示的度量的詳細資訊，請參閱 [配置檔案儀表板UI指南](ui/profile-dashboard.md)。

### 配置檔案片段與合併的配置檔案 {#profile-fragments-vs-merged-profiles}

每個單獨的客戶配置檔案由多個配置檔案片段組成，這些片段已合併以形成該客戶的單個視圖。 例如，如果客戶通過多個渠道與您的品牌進行交互，您的組織將具有多個與該單個客戶相關的配置檔案片段，這些配置檔案片段出現在多個資料集中。 當這些片段被放入平台中時，它們會合併在一起，以便為該客戶建立單個配置檔案。

換句話說，簡檔片段表示唯一的主身份和相應的 [記錄](#record-data) 或 [事件](#time-series-events) 給定資料集中該ID的資料。

當來自多個資料集的資料發生衝突時（例如，一個片段將客戶列為「單一」，而另一個片段將客戶列為「已婚」） [合併策略](#merge-policies) 確定要排定優先順序並包含在個人配置檔案中的資訊。 因此，平台內配置檔案片段的總數可能總是高於合併配置檔案的總數，因為每個配置檔案通常由多個資料集中的多個片段組成。

### 記錄資料 {#record-data}

配置檔案是由許多屬性（也稱為記錄資料）組成的主題、組織或個人的表示。 例如，產品的配置檔案可能包括SKU和說明，而人員的配置檔案則包含諸如名、姓和電子郵件地址等資訊。 使用 [!DNL Experience Platform]，您可以自定義配置檔案以使用與業務相關的特定資料。 標準 [!DNL Experience Data Model] (XDM)類， [!DNL XDM Individual Profile]，是描述客戶記錄資料時構建模式的首選類，並為平台服務之間的許多交互提供資料。 有關使用中的架構的詳細資訊 [!DNL Experience Platform]，請從閱讀 [XDM系統概述](../xdm/home.md)。

### 時間系列事件 {#time-series-events}

時間序列資料提供了對象直接或間接執行操作時系統的快照，以及詳細描述事件本身的資料。 由標準架構類XDM ExperienceEvent表示，時間序列資料可以描述事件，如添加到購物車的項目、按一下的連結和查看的視頻。 時間序列資料可用於基於分段規則，並且事件可在概要檔案的上下文中單獨訪問。

### 身分

每家企業都希望以一種感覺私人的方式與客戶溝通。 然而，向客戶提供相關數字型驗的一個挑戰是瞭解如何將其斷開連接的資料聯繫起來，這種資料通常分佈在不同的數字渠道，如平板電腦、行動電話和筆記型電腦。 [!DNL Identity Service] 通過連結來自多個渠道的身份並為每個客戶建立身份圖表，您可以將客戶的完整圖片拼湊在一起。 訪問 [Identity Service概述](../identity-service/home.md) 的子菜單。

### 合併策略

將來自多個源的資料片段合併在一起並合併這些片段以便查看每個客戶的完整視圖時，合併策略是 [!DNL Platform] 用於確定資料的優先順序以及將使用哪些資料建立客戶配置檔案。

當來自多個資料集的資料發生衝突時，合併策略將確定應如何處理該資料以及應使用哪個值。 通過REST風格的API或用戶介面，您可以建立新的合併策略、管理現有策略以及為組織設定預設的合併策略。

要瞭解有關合併策略及其在Experience Platform中的角色的詳細資訊，請首先閱讀 [合併策略概述](merge-policies/overview.md)。

### 聯合架構 {#profile-fragments-and-union-schemas}

C.C.C.C.C. [!DNL Real-Time Customer Profile] 是統一多通道資料的能力。 當 [!DNL Real-Time Customer Profile] 用於訪問實體，它可為您提供跨資料集的該實體的所有配置檔案片段的合併視圖，稱為「聯合視圖」，並通過稱為聯合架構的內容實現。

要瞭解有關聯合架構的詳細資訊，包括如何訪問UI中的聯合架構，請訪問 [聯合架構UI指南](ui/union-schema.md)。

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## 配置檔案和段

Adobe Experience Platform [!DNL Segmentation Service] 為您的個別客戶提供強大體驗所需的受眾。 建立受眾段時，該段的ID將添加到所有合格配置檔案的段成員資格清單中。 段規則生成並應用於 [!DNL Real-Time Customer Profile] 使用REST風格的API和段生成器用戶介面的資料。 要瞭解有關分段的詳細資訊，請首先閱讀 [分段服務概述](../segmentation/home.md)。

### 流攝入和流分割

通過稱為流式接收的過程使即時輸入成為可能。 在接收資料和時間序列資料時， [!DNL Real-Time Customer Profile] 在將資料與現有資料合併並更新聯合視圖之前，自動決定通過稱為流分段的持續過程將資料包括或排除在資料段中。 因此，您可以即時執行計算並做出決策，在客戶與您的品牌進行交互時向客戶提供增強的個性化體驗。 在攝取資料的同時，還進行驗證以確保正確攝取資料並且符合資料集所基於的模式。 有關在接收期間執行的驗證操作的詳細資訊，請首先閱讀 [資料接收質量概述](../ingestion/quality/overview.md)。

## 邊緣投影

為了在多個渠道中為客戶提供協調、一致和個性化的即時體驗，需要隨時提供適當的資料並在發生更改時不斷更新。 Adobe Experience Platform通過使用所謂的邊緣實現對資料的即時訪問。 邊緣是位於地理位置的伺服器，它儲存資料，並使應用程式能夠方便地訪問資料。 例如，Adobe應用程式(如Adobe Target和Adobe Campaign)使用邊緣，以便即時提供個性化的客戶體驗。 資料通過投影被路由到邊緣，投影目的地定義要向其發送資料的邊緣，投影配置定義將在邊緣上提供的特定資訊。 要瞭解更多資訊，並使用 [!DNL Real-Time Customer Profile] API，請參閱 [邊緣投影端點導引](api/edge-projections.md)。

## 將資料插入 [!DNL Profile]

[!DNL Platform] 可以配置為將記錄和時間序列資料發送到 [!DNL Profile]支援即時流攝入和批量攝入。 有關詳細資訊，請參閱概述如何 [將資料添加到即時客戶配置檔案](tutorials/add-profile-data.md)。

>[!NOTE]
>
>通過Adobe解決方案收集的資料，包括 [!DNL Analytics Cloud]。 [!DNL Marketing Cloud], [!DNL Advertising Cloud]，流入 [!DNL Experience Platform] 被攝入 [!DNL Profile]。

### 配置檔案接收度量

Oncebrity Insights允許您公開Adobe Experience Platform的關鍵指標。 除 [!DNL Experience Platform] 使用統計和績效指標 [!DNL Platform] 功能，有特定的與配置檔案相關的度量，使您能夠深入瞭解傳入請求速率、成功攝取速率、攝取的記錄大小等。 要瞭解更多資訊，請從閱讀 [可觀性透視API概述](../observability/api/overview.md)，有關即時客戶配置檔案度量的完整清單，請參閱 [可用度量](../observability/api/metrics.md#available-metrics)。

## 更新配置檔案儲存資料

有時可能需要更新組織的配置檔案儲存中的資料。 例如，您可能需要更正記錄或更改屬性值。 這可以通過批處理接收來完成，並且需要使用upsert標籤配置啟用配置檔案的資料集。 有關如何配置資料集以進行屬性更新的詳細資訊，請參閱本教程以瞭解 [為配置檔案和upsert啟用資料集](../catalog/datasets/enable-upsert.md)。

## 資料治理和 [!DNL Privacy]

資料治理是用於管理客戶資料和確保遵守適用於資料使用的法規、限制和策略的一系列策略和技術。

由於資料存取相關，資料治理在 [!DNL Experience Platform] 各級：

- 資料使用標籤
- 資料存取策略
- 對市場營銷活動資料的訪問控制

資料治理在幾個點進行管理。 這些包括確定所攝取的資料 [!DNL Platform] 以及在接收特定營銷活動後可以訪問哪些資料。 有關詳細資訊，請首先閱讀 [資料治理概述](../data-governance/home.md)。

### 處理選擇退出和資料隱私請求

[!DNL Experience Platform] 使您的客戶能夠發送與其資料在以下位置的使用和儲存相關的退出請求 [!DNL Real-Time Customer Profile]。 有關如何處理選擇退出請求的詳細資訊，請參閱 [處理選擇退出請求](../segmentation/consents.md)。

## 後續步驟和其他資源

要瞭解有關使用Experience PlatformUI或配置檔案API處理即時客戶配置檔案資料的更多資訊，請從閱讀 [配置檔案UI指南](ui/user-guide.md) 或 [API開發人員指南](api/overview.md)的下界。
