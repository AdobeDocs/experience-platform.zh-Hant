---
title: 資料管理許可證權利最佳實踐
description: 了解可用來更好地管理 Adobe Experience Platform 授權權益的最佳實務及工具。
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 225fee7e2addf5067cb13da11615f6acff62ed72
workflow-type: tm+mt
source-wordcount: '2203'
ht-degree: 2%

---

# 資料管理許可證權利最佳實踐

Adobe Experience Platform是一個開放系統，可將您的資料轉換為即時更新的強健客戶配置檔案，並使用人工智慧驅動的洞察力幫助您跨所有渠道提供正確的體驗。 您可以使用源將各種類型、卷和歷史記錄的資料導入到Experience Platform中，然後滿足這些資料的使用需求，從分段和個性化到分析和機器學習。

平台提供許可證，用於確定可建立的配置檔案數和可導入的資料量。 由於能夠引入任何資料源、卷或歷史記錄，因此隨著資料卷的增長，可能會超出您的許可權限。

本文件會概述可遵循的最佳做法以及可用來將 Adobe Experience Platform 的授權權益管理得更好的工具。

## 瞭解Adobe Experience Platform資料儲存

Experience Platform主要由兩個資料儲存庫組成：這樣 [!DNL data lake] 和Profile儲存。

的 **[!DNL data lake]** 主要用於以下目的：

* 充當將資料登錄到Experience Platform的中轉區；
* 充當所有Experience Platform資料的長期資料儲存；
* 啟用資料分析和資料科學等使用案例。

的 **配置檔案儲存** 是建立客戶配置檔案的地點，主要用於以下目的：

* 充當用於支援即時體驗的配置檔案的資料儲存；
* 啟用分段、激活和個性化等使用案例。

>[!NOTE]
>
>訪問 [!DNL data lake] 取決於您購買的產品SKU。 有關產品SKU的詳細資訊，請與您的Adobe代表聯繫。

## 授權使用情況 {#license-usage}

當您進行許可Experience Platform時，您將獲得許可使用權，這些權利因SKU而異：

**[!DNL Addressable Audience]**  — 合同允許Experience Platform的客戶配置檔案總數，包括已知和假名配置檔案。

**[!DNL Profile Richness]**  — 配置檔案資料在Experience Platform中的平均大小。 你可以 [!DNL Profile Richness] 購買豐富的包。

的 [!DNL Profile Richness] 度量因您購買的許可而異。 有兩種計算 [!DNL Profile Richness] 可用：

* 在任何時間點儲存在Adobe Real-time Customer Data Platform（即即時客戶配置檔案和身份服務）內的所有生產資料的總和，除以 [!DNL Addressable Audience];
* 平台內儲存的所有資料(包括但不限於 [!DNL data lake]、即時客戶配置檔案和身份服務)以及過去12個月中通過平台（而不是儲存在平台內）流過的任何資料，除以 [!DNL Addressable Audience]。

這些指標的可用性以及這些指標的具體定義會因貴組織購買的許可而有所不同。

## 許可證使用儀表板

Adobe Experience PlatformUI提供了一個儀表板，通過它可以查看貴組織與許可證相關的平台資料的快照。 儀表板中的資料與拍攝快照時在特定時間點顯示的資料完全相同。 快照既不是近似資料，也不是資料的示例，並且儀表板不會即時更新。

有關詳細資訊，請參閱上的指南 [在平台UI上使用許可證使用儀表板](../../dashboards/guides/license-usage.md#license-usage-dashboard-data)。

## 資料管理最佳做法

以下各節概述了為更好地管理資料而遵循的最佳做法。

### 瞭解您的資料

並非所有資料都在Adobe Experience Platform。 有些資料可能是密集的，但值較低，而另一些資料可能是稀疏的，但值較高。 一些資料一旦產生就可能會失去價值，而另一些資料可能會在數月甚至數年內都有價值。

瞭解資料的價值需要考慮三個方面：

| 維度 | 說明 | 範例 |
| --- | --- | --- |
| 卷 | 表示所接收的資料量和總量。 | Web點擊量高，保真度適中。 價值可能會迅速下降。 |
| 時間盤 | 表示所攝取的資料持續保持有價值的時間長度。 | 離線購買 — 數量和保真度都適中，但可能在很長時間內很有價值。 |
| 保真度 | 表示資料對資訊的豐富程度。 | 客戶帳戶 — 數量低，但保真度高。 在客戶的整個生命週期之外都有價值。 |

### 資料管理工具 {#data-management-tools}

在確保資料使用量保持在許可證權限範圍內時，需要考慮以下兩種主要情形：

### 要將哪些資料引入平台？

資料可以被測試到平台中的一個或多個系統，即 [!DNL data lake] 和/或配置檔案儲存。 這意味著，兩個系統中都可以存在不同的資料，用於不同的使用情形。 例如，您可能希望在 [!DNL data lake]，但不在配置檔案儲存中。 通過啟用資料集以接收配置檔案，可以選擇要發送到配置檔案儲存的資料。

>[!NOTE]
>
>訪問 [!DNL data lake] 取決於您購買的產品SKU。 有關產品SKU的詳細資訊，請與您的Adobe代表聯繫。

### 要保留哪些資料？

您可以同時應用資料攝取過濾器和過期規則，以刪除已因使用情形而過時的資料。 通常，行為資料（如分析資料）消耗的儲存量比記錄資料（如CRM資料）消耗的儲存量要大得多。 例如，與記錄資料相比，許多平台用戶最多有90%的配置檔案是單獨由行為資料填充的。 因此，管理行為資料對於確保許可證權利中的合規性至關重要。

您可以利用多種工具來保留許可證使用權限：

* [攝取過濾器](#ingestion-filters)
* [配置檔案儲存](#profile-service)

### 攝取過濾器 {#ingestion-filters}

「攝取」過濾器允許您只導入使用案例所需的資料，並過濾掉不需要的所有事件。

| 攝取過濾器 | 說明 |
| --- | --- |
| Adobe Audience Manager源過濾 | 建立Adobe Audience Manager源連接時，可以選擇要引入到 [!DNL data lake] 和Real-Time Customer Profile ，而不是整個接收Audience Manager資料。 請參閱上的指南 [建立Audience Manager源連接](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 的子菜單。 |
| Adobe Analytics資料準備 | 您可以使用 [!DNL Data Prep] 建立分析源連接以過濾您的使用案例不需要的資料時的功能。 通過 [!DNL Data Prep]，您可以定義哪些屬性/列需要發佈到配置檔案。 您還可以提供條件語句，以通知平台資料應發佈到配置檔案，還是僅發佈到 [!DNL data lake]。 請參閱上的指南 [建立分析源連接](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 的子菜單。 |
| 支援啟用/禁用配置檔案的資料集 | 要將資料插入Real-Time Customer Profile中，必須啟用資料集以便在Profile儲存中使用。 這樣，您 [!DNL Addressable Audience] 和 [!DNL Profile Richness] 權利。 一旦客戶配置檔案使用案例不再需要資料集，您就可以禁用該資料集與配置檔案的整合，以確保您的資料保持許可證合規性。 請參閱上的指南 [啟用和禁用配置檔案的資料集](../../catalog/datasets/enable-for-profile.md) 的子菜單。 |
| Web SDK和Mobile SDK資料排除 | Web和Mobile SDK收集的資料有兩種：自動收集的資料和開發人員顯式收集的資料。 為了更好地管理許可證合規性，您可以通過上下文設定在SDK配置中禁用自動資料收集。 您的開發人員也可以刪除或不設定自定義資料。 請參閱上的指南 [配置SDK基礎](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) 的子菜單。 |
| 伺服器端轉發資料排除 | 如果您使用伺服器端轉發將資料發送到平台，則可以通過刪除規則操作中的映射以在所有事件中排除該映射，或向規則添加條件以使某些事件只觸發資料來排除發送的資料。 請參閱 [事件和條件](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if)) 的子菜單。 |
| 在源級別篩選資料 | 在建立連接並將資料接收到Experience Platform之前，可以使用邏輯運算子和比較運算子來過濾源中的行級資料。 有關詳細資訊，請閱讀上的指南 [使用 [!DNL Flow Service] API](../../sources/tutorials/api/filter.md)。 |

{style="table-layout:auto"}

### 配置檔案儲存 {#profile-service}

配置檔案儲存由以下元件組成：

| 配置檔案儲存元件 | 說明 |
| --- | --- |
| 配置檔案片段 | 每個客戶配置檔案由多個 **配置檔案片段** 已合併，形成該客戶的單一視圖。 例如，如果客戶通過多個渠道與您的品牌進行交互，您的組織將具有多個 **配置檔案片段** 與出現在多個資料集中的單個客戶相關。 當這些片段被放入平台中時，它們會使用身份圖拼合在一起，為該客戶建立單個配置檔案。 **配置檔案片段** 由標識名稱空間作為標識符，與關聯的記錄資料和/或時間序列資料一起構成。 |
| 記錄資料（屬性） | 配置檔案是由許多組成的主題、組織或個人的表示 **屬性** (也稱為 **記錄資料**)。 例如，產品的配置檔案可能包括SKU和說明，而人員的配置檔案則包含諸如名、姓和電子郵件地址等資訊。 **記錄資料** 通常體積較低/中等，但在較長的時間內很有價值。 |
| 時間序列資料（行為） | **時間序列資料** 提供有關用戶行為的資訊。 由標準架構類體驗資料模型(XDM)表示 [!DNL ExperienceEvent]，時間序列資料可描述事件，如添加到購物車的項目、按一下的連結和查看的視頻。 行為的價值可能會隨著時間推移而下降。 |
| 標識名稱空間（標識） | 當客戶資料匯集在一起時，通過使用 **標識命名空間**，以及隨著更多關於用戶的資訊逐漸為人所知而將這些身份粘在一起的能力。 查看 [標識命名空間概述](../../identity-service/namespaces.md) 的子菜單。 |

{style="table-layout:auto"}

#### 配置檔案儲存合成報告

有許多報告可幫助您瞭解配置檔案儲存的組成。 這些報告可幫助您做出關於如何設定「體驗事件」過期時間以及如何設定以更好地優化許可證使用的明智決策：

* **資料集重疊報表API**:公開對可定址受眾貢獻最大的資料集。 您可以使用此報表來確定 [!DNL ExperienceEvent] 設定到期的資料集。 請參閱上的教程 [生成資料集重疊報告](../../profile/tutorials/dataset-overlap-report.md) 的子菜單。
* **標識重疊報表API**:顯示對可定址受眾貢獻最大的身份命名空間。 請參閱上的教程 [生成身份重疊報告](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) 的子菜單。
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### 假名配置檔案資料過期 {#pseudonymous-profile-expirations}

此功能允許您自動從配置檔案儲存中刪除過時的假名配置檔案。 有關此功能的詳細資訊，請閱讀 [假名配置檔案資料過期概述](../../profile/pseudonymous-profiles.md)。

#### 體驗事件過期 {#event-expirations}

此功能允許您自動從啟用配置檔案的資料集中刪除對您的使用案例不再有價值的行為資料。 請參閱 [體驗事件過期](../../profile/event-expirations.md) 有關在為資料集啟用此進程後如何工作的詳細資訊。

## 許可證使用合規性的最佳做法摘要 {#best-practices}

以下是一些建議的最佳做法的清單，您可以遵循這些做法來確保更好地遵守許可證使用權利：

* 使用 [許可證使用儀表板](../../dashboards/guides/license-usage.md) 跟蹤和監控客戶使用趨勢。 這樣，您就可以提前發現任何可能發生的超額。
* 配置 [攝食過濾器](#ingestion-filters) 通過確定分割和個性化使用案例所需的事件。 這允許您僅發送使用案例所需的重要事件。
* 確保您只 [已啟用配置檔案資料集](#ingestion-filters) 分段和個性化使用案例所必需的。
* 配置 [體驗事件過期](#event-expirations) 和 [假名配置檔案資料過期](#pseudonymous-profile-expirations) 用於Web資料等高頻資料。
* 定期檢查 [配置檔案組成報告](#profile-store-composition-reports) 瞭解您的檔案庫組成。 這使您能夠瞭解對許可證使用量貢獻最大的資料源。

## 功能摘要和可用性 {#feature-summary}

本文檔中概述的最佳做法和工具將幫助您更好地管理Adobe Experience Platform的許可證權利使用。 隨著其他功能的發佈，本文檔將更新，以幫助向所有Experience Platform客戶提供可見性和控制。

下表概述了您當前可用的功能清單，以便更好地管理許可證使用權限。

| 功能 | 說明 |
| --- | --- |
| [啟用/禁用配置檔案的資料集](../../catalog/datasets/user-guide.md) | 啟用或禁用資料集攝取到即時客戶配置檔案中。 |
| [體驗事件過期](../../profile/event-expirations.md) | 對接收到啟用配置檔案的資料集中的所有事件應用過期時間。 請聯繫您的Adobe客戶團隊或客戶服務以啟用此功能。 |
| [Adobe Analytics資料準備篩選器](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | 應用 [!DNL Kafka] 從攝取中排除不必要資料的過濾器 |
| [Adobe Audience Manager源連接器過濾器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | 應用Audience Manager源連接篩選器以從攝取中排除不必要的資料 |
| [合金SDK資料篩選器](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) | 應用合金濾鏡以從攝取中排除不必要的資料 |
| [事件轉發資料篩選器](../../tags/ui/event-forwarding/overview.md) | 應用伺服器端 [!DNL Kafka] 過濾器，以從攝取中排除不必要的資料。  請參閱 [標籤規則](../../tags/ui/managing-resources/rules.md) 的雙曲餘切值。 |
| [許可證使用儀表板UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | 查看組織與許可證相關資料的快照以進行Experience Platform |
| [資料集重疊報表API](../../profile/tutorials/dataset-overlap-report.md) | 輸出對可定址受眾貢獻最大的資料集 |
| [標識重疊報表API](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | 輸出對可定址受眾貢獻最大的身份命名空間 |

{style="table-layout:auto"}
