---
title: 資料管理授權權益最佳實務
description: 了解可以更有效管理 Adobe Experience Platform 授權權益的最佳實務及工具。
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 1b8fd7671146519fa66768aab3fe081adb0bd6c6
workflow-type: tm+mt
source-wordcount: '2145'
ht-degree: 3%

---

# 資料管理授權權益最佳實務

Adobe Experience Platform是一個開放系統，可將您的資料轉換為健全的客戶設定檔，並即時更新，使用AI驅動的深入分析來協助您跨每個管道提供適當的體驗。 您可以內嵌不同型別、磁碟區和歷史的資料，以使用來源Experience Platform，然後迎合從細分和個人化到分析和機器學習等使用案例的資料。

Platform提供可建立設定檔數量及可匯入資料量的授權。 因為有引入任何資料來源、數量或歷史記錄的容量，所以可能會隨著資料數量的增加而超過您的授權權利。

本文件會概述可遵循的最佳做法以及可用來將 Adobe Experience Platform 的授權權益管理得更好的工具。

## 瞭解Adobe Experience Platform資料儲存

Experience Platform主要由兩個資料存放庫組成： [!DNL data lake]和設定檔存放區。

**[!DNL data lake]**&#x200B;主要用途如下：

* 充當將資料上線到Experience Platform中的中繼區域；
* 充當所有Experience Platform資料的長期資料儲存體；
* 啟用資料分析和資料科學等使用案例。

**設定檔存放區**&#x200B;是建立客戶設定檔的位置，主要用途如下：

* 充當用來支援即時體驗之設定檔的資料儲存空間；
* 啟用分段、啟用和個人化等使用案例。

>[!NOTE]
>
>您對[!DNL data lake]的存取權取決於您購買的產品SKU。 如需產品SKU的詳細資訊，請洽詢您的Adobe代表。

## 授權使用情況 {#license-usage}

當您授權Experience Platform時，會根據SKU提供您不同的授權使用權益：

**[!DNL Addressable Audience]** — 合約允許在Experience Platform中使用的客戶設定檔總數，包括已知和假名設定檔。

**[!DNL Total Data Volume]** — 可在參與工作流程中使用的Adobe Experience Platform設定檔服務資料總數。

這些量度的可用性，以及每個量度的特定定義，會因貴組織已購買的授權而有所不同。

## 授權使用量儀表板

Adobe Experience Platform UI提供控制面板，讓您檢視貴組織適用於Platform的授權相關資料快照。 儀表板中的資料與快照拍攝時的特定時間點顯示的資料完全相同。 快照既不是近似值，也不是資料範例，而且儀表板不會即時更新。

如需詳細資訊，請參閱[在Platform UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data)上使用授權使用儀表板的指南。

## 資料管理最佳實務

以下章節概述要遵循的最佳實務，以便更妥善管理您的資料。

### 瞭解您的資料

Adobe Experience Platform並非所有資料都是相同的。 有些資料可能密集，但數值偏低，而其他資料可能稀疏，但數值偏高。 有些資料一產生就可能失去價值，而其他資料可能有幾個月（如果不是幾年的話）的價值。

在瞭解資料的值時，有三個需要考量的維度：

| 維度 | 說明 | 範例 |
| --- | --- | --- |
| 卷 | 代表擷取的資料數量和總數。 | 網頁點按 — 高音量和中等逼真度。 值可能會快速減少。 |
| 時間跨度 | 代表內嵌資料繼續保持有價值的時間長度。 | 離線購買 — 在數量和保真度上較為適中，但可能在很長一段時間內都有價值。 |
| 逼真度 | 代表資料含有的資訊有多豐富。 | 客戶帳戶 — 數量低但保真度高。 在客戶的生命週期後仍可發揮寶貴價值。 |

### 資料管理工具 {#data-management-tools}

在確保您的資料使用量維持在授權權益限制內時，請考慮以下兩種主要情況：

### 要將哪些資料帶入Platform？

資料可以擷取到Platform的一或多個系統中，即[!DNL data lake]和/或設定檔存放區。 這表示在不同的使用案例中，兩個系統中都可以存在不同的資料。 例如，您可能想要在[!DNL data lake]中保留歷史資料，但不想在設定檔存放區中保留。 您可以啟用設定檔擷取的資料集，以選取要傳送至設定檔存放區的資料。

>[!NOTE]
>
>您對[!DNL data lake]的存取權取決於您購買的產品SKU。 如需產品SKU的詳細資訊，請洽詢您的Adobe代表。

### 要保留哪些資料？

您可以同時套用資料擷取篩選器和到期規則，以移除已因使用案例而過時的資料。 通常，行為資料（例如Analytics資料）使用的儲存空間遠高於記錄資料（例如CRM資料）。 例如，相較於記錄資料，許多Platform使用者有超過90%的設定檔僅由行為資料填入。 因此，管理您的行為資料對於確保授權權益的合規性至關重要。

您可善用許多工具以符合授權使用權益：

* [內嵌篩選器](#ingestion-filters)
* [設定檔存放區](#profile-service)

### 身分識別服務和可定址的受眾 {#identity-service}

身分圖表不會計入可定址對象權利總數，因為可定址對象會參照客戶設定檔總數。

不過，身分圖表限制可能會因為分割身分而影響可定址的受眾。 例如，如果從圖表移除最舊的ECID，ECID將以假名設定檔的形式繼續存在於即時客戶設定檔中。 您可以設定[假名設定檔資料有效期](../../profile/pseudonymous-profiles.md)以規避此行為。 若要了解更多資訊，請閱讀[身分識別服務資料的護欄](../../identity-service/guardrails.md)。

### 內嵌篩選器 {#ingestion-filters}

內嵌篩選器可讓您僅匯入使用案例所需的資料，並篩選掉所有不需要的事件。

| 擷取篩選器 | 說明 |
| --- | --- |
| Adobe Audience Manager來源篩選 | 建立Adobe Audience Manager來源連線時，您可以挑選要帶入[!DNL data lake]和即時客戶個人檔案的區段和特徵，而不是擷取完整的Audience Manager資料。 如需詳細資訊，請參閱[建立Audience Manager來源連線](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)的指南。 |
| Adobe Analytics資料準備 | 建立Analytics來源連線時，您可以使用[!DNL Data Prep]功能來篩選出使用案例不需要的資料。 透過[!DNL Data Prep]，您可以定義哪些屬性/欄需要發佈到設定檔。 您也可以提供條件陳述式，通知Platform資料應該發佈到設定檔，還是隻發佈到[!DNL data lake]。 如需詳細資訊，請參閱[建立Analytics來源連線](../../sources/tutorials/ui/create/adobe-applications/analytics.md)的指南。 |
| 支援為設定檔啟用/停用資料集 | 若要將資料擷取至即時客戶個人檔案，您必須啟用資料集以用於個人檔案存放區。 如此一來，新增至您的[!DNL Addressable Audience]和[!DNL Total Data Volume]權益。 客戶設定檔使用案例不再需要資料集後，您可以停用該資料集與設定檔的整合，以確保您的資料符合授權規範。 如需詳細資訊，請參閱[啟用和停用設定檔](../../catalog/datasets/enable-for-profile.md)的資料集指南。 |
| Web SDK和Mobile SDK資料排除 | Web和Mobile SDK收集的資料有兩種型別：自動收集的資料以及開發人員明確收集的資料。 若要更妥善地管理授權法規遵循，您可以透過內容設定，在SDK的組態中停用自動資料收集。 您的開發人員也可以移除或設定自訂資料。 |
| 伺服器端轉送資料排除 | 如果您使用伺服器端轉送將資料傳送至Platform，您可以移除規則動作中的對應以在所有事件中排除資料，或是將條件新增至規則，讓資料僅針對特定事件引發，藉此排除傳送的資料。 如需詳細資訊，請參閱有關[事件和條件](/help/tags/ui/managing-resources/rules.md#events-and-conditions-if)的檔案。 |
| 在來源層級篩選資料 | 您可以使用邏輯和比較運運算元，在建立連線並將資料擷取到Experience Platform之前，先篩選來源中的列層級資料。 如需詳細資訊，請參閱[使用 [!DNL Flow Service] API](../../sources/tutorials/api/filter.md)篩選來源之資料列層級資料的指南。 |

{style="table-layout:auto"}

### 設定檔存放區 {#profile-service}

設定檔存放區由下列元件組成：

| 設定檔存放區元件 | 說明 |
| --- | --- |
| 輪廓片段 | 每個客戶設定檔都由多個&#x200B;**設定檔片段**&#x200B;組成，這些片段已合併以形成該客戶的單一檢視。 例如，如果客戶跨多個管道與您的品牌互動，您的組織將有多個與該單一客戶相關的&#x200B;**設定檔片段**&#x200B;出現在多個資料集中。 將這些片段內嵌至Platform時，會使用身分圖表將它們彙整在一起，以為該客戶建立單一設定檔。 **設定檔片段**&#x200B;包含身分名稱空間做為識別碼，以及關聯的記錄資料和/或時間序列資料。 |
| 記錄資料（屬性） | 設定檔是主旨、組織或個人的表示法，由許多&#x200B;**屬性** （也稱為&#x200B;**記錄資料**）組成。 例如，產品的設定檔可能包含SKU和說明，而人員的設定檔包含名字、姓氏和電子郵件地址等資訊。 **記錄資料**&#x200B;的磁碟區通常為低/中等，但長時間都有價值。 |
| 時間序列資料（行為） | **時間序列資料**&#x200B;提供有關使用者行為的資訊。 以標準結構描述類別Experience Data Model (XDM) [!DNL ExperienceEvent]表示，時間序列資料可說明新增至購物車的專案、點按連結及檢視影片等事件。 行為的價值可能會隨著時間而降低。 |
| 身分名稱空間（身分） | 當客戶資料彙整在一起時，會透過使用&#x200B;**身分識別名稱空間**&#x200B;將其合併到單一設定檔中，並可在更多使用者相關資訊時將這些身分識別貼在一起。 如需詳細資訊，請參閱[身分識別名稱空間概觀](../../identity-service/features/namespaces.md)。 |

{style="table-layout:auto"}

#### 設定檔存放區構成報表

有許多報表可協助您瞭解設定檔存放區的組成。 這些報表可協助您針對如何以及在何處設定體驗事件有效期，做出明智的決策，以便更佳地最佳化您的授權使用情況：

* **資料集重疊報表API**：公開對可定址對象貢獻最大的資料集。 您可以使用此報告來識別要設定到期日的[!DNL ExperienceEvent]個資料集。 如需詳細資訊，請參閱有關[產生資料集重疊報表](../../profile/tutorials/dataset-overlap-report.md)的教學課程。
* **身分重疊報表API**：公開對可定址對象貢獻最大的身分名稱空間。 如需詳細資訊，請參閱有關[產生身分重疊報表](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report)的教學課程。
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### 假名設定檔資料有效期 {#pseudonymous-profile-expirations}

此功能可讓您從設定檔存放區中自動移除過時的假名設定檔。 如需有關此功能的詳細資訊，請閱讀[假名設定檔資料到期總覽](../../profile/pseudonymous-profiles.md)。

#### 體驗事件有效期 {#event-expirations}

此功能可讓您從已啟用設定檔的資料集中自動移除行為資料，該資料不再對您的使用案例有用。 如需此程式在資料集啟用後如何運作的詳細資訊，請參閱[體驗事件有效期](../../profile/event-expirations.md)的概觀。

## 授權使用合規性最佳實務摘要 {#best-practices}

以下是您可以遵循的一些建議最佳實務清單，以確保更符合您的授權使用權益：

* 使用[授權使用量儀表板](../../dashboards/guides/license-usage.md)追蹤及監控客戶使用趨勢。 這可讓您搶先掌握可能出現的使用過量。
* 識別細分和個人化使用案例所需的事件，以設定[擷取篩選器](#ingestion-filters)。 這可讓您僅傳送使用案例所需的重要事件。
* 確保您只有區段和個人化使用案例所需的設定檔](#ingestion-filters)的[已啟用資料集。
* 設定[體驗事件有效期](#event-expirations)和[假名設定檔資料有效期](#pseudonymous-profile-expirations)，以取得高頻資料，例如Web資料。
* 請定期檢查[設定檔組合報告](#profile-store-composition-reports)，以瞭解您的設定檔存放區組合。 這可讓您瞭解對授權使用量消耗貢獻最大的資料來源。

## 功能摘要和可用性 {#feature-summary}

本檔案概述的最佳實務和工具可協助您更妥善管理Adobe Experience Platform中的授權權益使用情況。 此檔案將會隨著其他功能的發行而更新，以協助向所有Experience Platform客戶提供可見度和控制力。

下表概述您目前可使用的功能清單，以便更妥善管理您的授權使用權益。

| 功能 | 說明 |
| --- | --- |
| [啟用/停用設定檔](../../catalog/datasets/user-guide.md)的資料集 | 啟用或停用將資料集擷取至Real-Time Customer Profile。 |
| [體驗活動有效期](../../profile/event-expirations.md) | 為擷取到啟用設定檔的資料集中的所有事件套用到期時間。 請聯絡您的Adobe客戶團隊或客戶服務，以啟用此功能。 |
| [Adobe Analytics資料準備篩選器](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | 套用[!DNL Kafka]篩選器以從擷取中排除不必要的資料 |
| [Adobe Audience Manager來源聯結器篩選器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | 套用Audience Manager來源連線篩選條件，從擷取中排除不必要的資料 |
| [事件轉寄資料篩選器](../../tags/ui/event-forwarding/overview.md) | 套用伺服器端[!DNL Kafka]篩選器以從擷取中排除不必要的資料。  如需其他資訊，請參閱[標籤規則](../../tags/ui/managing-resources/rules.md)的相關檔案。 |
| [授權使用儀表板UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | 檢視貴組織授權相關資料的快照，以供Experience Platform |
| [資料集重疊報告API](../../profile/tutorials/dataset-overlap-report.md) | 輸出對可定址對象貢獻最大的資料集 |
| [身分重疊報表API](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | 輸出對可定址對象貢獻最大的身分名稱空間 |

{style="table-layout:auto"}
