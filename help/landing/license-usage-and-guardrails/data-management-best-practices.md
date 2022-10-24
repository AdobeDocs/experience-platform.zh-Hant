---
keywords: Experience Platform；首頁；熱門主題；資料管理；授權；授權；最佳作法
title: 資料管理許可證權限最佳做法
description: 了解可用來更好地管理 Adobe Experience Platform 授權權益的最佳實務及工具。
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '2529'
ht-degree: 2%

---

# 資料管理許可證權限最佳實踐

Adobe Experience Platform是一個開放系統，可將您的資料轉換為可即時更新的健全客戶設定檔，並使用AI導向的深入分析來協助您跨每個管道提供合適的體驗。 您可以使用來源將各種類型、卷和歷史記錄的資料輸入到Experience Platform中，然後滿足這些資料的使用需求，從細分和個人化到分析和機器學習。

Platform提供的授權可建立您可建立的設定檔數量，以及可匯入的資料量。 由於能夠帶入任何資料源、卷或歷史記錄，因此，隨著資料量的增長，您的許可權限可能會超過您的權限。

本文件會概述可遵循的最佳做法以及可用來將 Adobe Experience Platform 的授權權益管理得更好的工具。

## 了解Adobe Experience Platform資料儲存

Experience Platform主要由兩個資料存放庫組成：the [!DNL Data Lake] 和設定檔存放區。

此 **[!DNL Data Lake]** 主要用途如下：

* 充當將資料上線至Experience Platform的中繼區域；
* 充當所有Experience Platform資料的長期資料儲存；
* 啟用資料分析和資料科學等使用案例。

此 **設定檔存放區** 是建立客戶設定檔的位置，主要用於下列用途：

* 可作為用於支援即時體驗之設定檔的資料儲存；
* 啟用分段、啟用和個人化等使用案例。

>[!NOTE]
>
>您對 [!DNL Data Lake] 取決於您購買的產品SKU。 如需產品SKU的詳細資訊，請洽詢您的Adobe代表。

## 授權使用情況 {#license-usage}

當您Experience Platform授權時，我們會提供您的授權使用權限，這些權限會依SKU而有所不同：

**[!DNL Addressable Audience]** -Experience Platform中合約允許的客戶設定檔總數，包括已知和假名的設定檔。

**[!DNL Profile Richness]** -Experience Platform中設定檔資料的平均大小。 您可以增加 [!DNL Profile Richness] 購買豐富的套件即可享有此優惠。

此 [!DNL Profile Richness] 量度會根據您購買的授權而有所不同。 有兩種計算方式 [!DNL Profile Richness] 可用：

* Adobe Real-time Customer Data Platform中儲存的所有生產資料（即Profile Service和Identity Service）在任何時間點的總和，除以 [!DNL Addressable Audience];
* Platform中儲存的所有資料的總和(包括但不限於 [!DNL Data Lake]、設定檔服務和Identity Service)，以及過去12個月中透過（而非儲存在）Platform串流的任何資料，除以 [!DNL Addressable Audience].

這些量度的可用性和每個量度的特定定義會因貴組織已購買的授權而異。

## 授權使用控制面板

Adobe Experience Platform UI提供控制面板，您可透過該控制面板檢視貴組織Platform授權相關資料的快照。 控制面板中的資料與拍攝快照時在特定時間點顯示的資料完全相同。 快照既不是近似值，也不是資料的樣本，控制面板不會即時更新。

如需詳細資訊，請參閱 [在Platform UI上使用授權使用控制面板](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## 資料管理最佳實務

以下小節概述可遵循的最佳實務，以便更妥善地管理您的資料。

### 了解您的資料

並非所有資料在Adobe Experience Platform中都一樣。 有些資料可能是密集的，但價值較低，而有些資料可能是稀疏的，但價值較高。 有些資料一產生就可能失去價值，而有些資料可能會在數月乃至數年內失去價值。

了解資料的值時，需考慮三個維度：

| 維度 | 說明 | 範例 |
| --- | --- | --- |
| 卷 | 代表擷取的資料量和總數。 | 網頁點按次數 — 大量增加，且保真度適度。 價值可能會迅速消失。 |
| 時間盤 | 代表擷取的資料持續有價值的時間長度。 | 離線購買 — 量和保真度適中，但可能在長時間內很有價值。 |
| 富達 | 代表資料的資訊豐富程度。 | 客戶帳戶 — 數量低，但保真度高。 在客戶的有限期內都很有價值。 |

### 資料管理工具 {#data-management-tools}

在確保您的資料使用量維持在授權限制內時，有兩個主要案例需要考量：

### 要將哪些資料帶入Platform?

資料可擷取至Platform中的一或多個系統，即 [!DNL Data Lake] 和/或設定檔存放區。 這表示針對不同的使用案例，兩個系統中都可能存在不同的資料。 例如，您可能想要將歷史資料保留在 [!DNL Data Lake]，但設定檔存放區中不會。 您可以啟用資料集以擷取設定檔，借此選取要將哪些資料傳送至設定檔存放區。

>[!NOTE]
>
>您對 [!DNL Data Lake] 取決於您購買的產品SKU。 如需產品SKU的詳細資訊，請洽詢您的Adobe代表。

### 要保留哪些資料？

您可以同時套用資料擷取篩選器和到期規則（也稱為存留時間「TTL」），以移除已因您的使用案例而過時的資料。 通常，行為資料（例如Analytics資料）的儲存空間會比記錄資料（例如CRM資料）大很多。 例如，與記錄資料相比，許多Platform使用者單獨以行為資料填入的設定檔高達90%。 因此，管理您的行為資料對於確保許可權限內的合規性至關重要。

您可以利用許多工具來保留在授權使用權限內：

* [擷取篩選器](#ingestion-filters)
* [設定檔服務TTL](#profile-service)

### 擷取篩選器 {#ingestion-filters}

內嵌篩選器可讓您僅內嵌使用案例所需的資料，並篩選掉所有非必要的事件。

| 擷取篩選器 | 說明 |
| --- | --- |
| Adobe Audience Manager來源篩選 | 建立Adobe Audience Manager來源連線時，您可以挑選要帶入的區段和特徵 [!DNL Data Lake] 和設定檔服務，而非擷取Audience Manager資料的整體。 請參閱 [建立Audience Manager源連接](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 以取得更多資訊。 |
| Adobe Analytics資料準備 | 您可以使用 [!DNL Data Prep] 建立Analytics來源連線以篩選出您使用案例不需要的資料時的功能。 通過 [!DNL Data Prep]，您可以定義需要發佈至設定檔的屬性/欄。 您也可以提供條件陳述式，通知Platform資料應發佈至設定檔，或僅發佈至 [!DNL Data Lake]. 請參閱 [建立Analytics來源連線](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 以取得更多資訊。 |
| 支援啟用/停用設定檔資料集 | 若要將資料內嵌至設定檔服務，您必須啟用資料集才能在設定檔存放區中使用。 這麼做會增加您的 [!DNL Addressable Audience] 和 [!DNL Profile Richness] 權益。 客戶設定檔使用案例不再需要資料集後，您可以停用該資料集與設定檔的整合，確保資料符合授權規範。 請參閱 [啟用和停用設定檔的資料集](../../catalog/datasets/enable-for-profile.md) 以取得更多資訊。 |
| Web SDK與行動SDK資料排除 | Web和Mobile SDK收集的資料類型有兩種：自動收集的資料和開發人員明確收集的資料。 若要更妥善地管理授權規範，您可以透過內容設定，在SDK設定中停用自動資料收集。 您的開發人員也可以移除或不設定自訂資料。 請參閱 [配置SDK基礎知識](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) 以取得更多資訊。 |
| 伺服器端轉送資料排除 | 如果您使用伺服器端轉送將資料傳送至Platform，您可以移除規則動作中的對應以在所有事件中排除它，或將條件新增至規則，讓資料只針對特定事件而觸發，來排除所傳送的資料。 請參閱 [事件與條件](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if)) 以取得更多資訊。 |

{style=&quot;table-layout:auto&quot;}

### 設定檔服務 {#profile-service}

「設定檔服務TTL」（存留時間）功能可讓您對設定檔存放區中的資料套用TTL。 這樣可讓系統自動移除隨著時間而價值降低的資料。

設定檔存放區由下列元件組成：

| 設定檔存放區元件 | 說明 |
| --- | --- |
| 設定檔片段 | 每個客戶設定檔由多個 **設定檔片段** 已合併，以形成該客戶的單一檢視。 例如，如果客戶透過數個管道與您的品牌互動，則您的組織會有多個管道 **設定檔片段** 與出現在多個資料集中的單一客戶相關。 將這些片段擷取至Platform時，會使用身分圖表來匯整在一起，為該客戶建立單一設定檔。 **設定檔片段** 由身份命名空間組成，作為標識符，與相關的記錄資料和/或時間序列資料。 |
| 記錄資料（屬性） | 設定檔是由許多 **屬性** (也稱為 **記錄資料**)。 例如，產品的設定檔可能包含SKU和說明，而人員的設定檔則包含名字、姓氏和電子郵件地址等資訊。 **記錄資料** 通常數較低/適中，但長時間有用。 |
| 時間序列資料（行為） | **時間序列資料** 提供使用者行為的相關資訊。 由標準結構類別Experience Data Model(XDM)表示 [!DNL ExperienceEvent]，時間序列資料可說明新增至購物車的項目、點按的連結，以及檢視的影片等事件。 行為的價值可能隨著時間的流逝而減少。 |
| 身分命名空間（身分） | 當客戶資料匯整在一起時，會透過使用 **身分識別命名空間**，以及當使用者的相關資訊越來越多時，將這些身分結合在一起的能力。 請參閱 [身分識別命名空間概述](../../identity-service/namespaces.md) 以取得更多資訊。 |

{style=&quot;table-layout:auto&quot;}

#### 設定檔存放區組成報表

有許多報表可協助您了解設定檔存放區的組成。 這些報表可協助您決定設定檔TTL的設定方式與位置，以更妥善地最佳化您的授權使用情形：

* **資料集重疊報表API**:顯示對可定址對象貢獻最多的資料集。 您可以使用此報告來識別 [!DNL ExperienceEvent] 為設定TTL的資料集。 請參閱 [產生資料集重疊報表](../../profile/tutorials/dataset-overlap-report.md) 以取得更多資訊。
* **身分重疊報表API**:公開對可定址對象貢獻最大的身分命名空間。 請參閱 [產生身分重疊報表](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) 以取得更多資訊。
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous TTL for different time thresholds. You can use this report to identify which pseudonymous TTL threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### [!DNL ExperienceEvent] 資料集TTL {#dataset-ttl}

您可以將TTL套用至已啟用設定檔的資料集，以移除「設定檔存放區」中不再對您使用案例有價值的行為資料。 TTL套用至啟用設定檔的資料集後，Platform就會透過兩步驟程式自動移除不再需要的資料：

* 所有後續新資料擷取時都會套用TTL有效期值；
* 所有現有資料都會在一次性回填系統作業中套用TTL過期值。

您可以預期每個事件的TTL值都來自事件時間戳記。 系統工作執行時，所有超過TTL有效期值的事件都會立即被捨棄。 當其他所有事件接近事件時間戳記中指定的TTL到期值時，就會將其捨棄。

請參閱下列範例，協助您了解 [!DNL ExperienceEvent] 資料集TTL。

如果您在5月15日套用30天的TTL值，則：

* 所有新事件傳入時，其TTL都會套用30天；
* 時間戳記早於4月15日的所有現有事件都會立即被系統作業刪除。;
* 在4月15日之後具有時間戳記的事件，其事件時間戳記+ TTL天數會到期。 因此，4月18日時間戳記的事件，將在5月15日後三天下降。

>[!IMPORTANT]
>
>套用TTL後，任何超過所選TTL天數的資料都會 **永久** 已刪除，無法還原。

套用TTL之前，您必須確保在TTL界限內保留任何區段的回顧期間。 否則，套用TTL後，區段結果可能會不正確。 例如，如果您對Adobe Analytics資料套用TTL 30天，對於店內交易資料套用TTL 365天，則下列區段會產生不正確的結果：

* 在過去60天內檢視「產品頁面」後，即進行店內購買；
* 新增至購物車，接著在過去60天內沒有購買。

反之，下列項目仍會產生正確的結果：

* 在過去14天內檢視過「產品頁面」，之後又進行店內購買；
* 過去30天內線上檢視了特定說明頁面；
* 過去120天內離線購買產品；
* 新增至購物車，接著在過去14天內購買。

>[!TIP]
>
>為方便起見，您可以保留所有資料集的相同TTL，如此您就不必擔心分段邏輯中資料集的TTL影響。

如需將TTL套用至設定檔資料的詳細資訊，請參閱 [設定檔服務TTL](../../profile/apply-ttl.md).

## 符合許可證使用規範的最佳做法摘要 {#best-practices}

以下是一些建議的最佳實務清單，您可以遵循這些作法，以確保更符合您的授權使用權限：

* 使用 [授權使用控制面板](../../dashboards/guides/license-usage.md) 追蹤及監控客戶使用趨勢。 這可讓您搶在任何可能發生的超額之前處理。
* 設定 [內嵌篩選器](#ingestion-filters) 識別您的細分和個人化使用案例所需的事件。 這可讓您只傳送使用案例所需的重要事件。
* 請確定您只有 [啟用設定檔資料集](#ingestion-filters) 區段和個人化使用案例所需的項目。
* 設定 [[!DNL ExperienceEvent] 資料集TTL](#dataset-ttl) 適用於高頻率資料，例如網頁資料。
* 定期檢查 [設定檔組成報表](#profile-store-composition-reports) 來了解您的設定檔存放區構成。 這可讓您了解對授權使用量貢獻最大的資料來源。

## 功能摘要和可用性 {#feature-summary}

本檔案中概述的最佳實務和工具可協助您在Adobe Experience Platform中更妥善地管理授權使用情形。 本檔案將隨著發行其他功能而更新，以協助為所有Experience Platform客戶提供可見性和控制。

下表概述您目前可使用的功能清單，以便更妥善地管理您的授權使用權限。

| 功能 | 說明 |
| --- | --- |
| [啟用/停用設定檔的資料集](../../catalog/datasets/user-guide.md) | 啟用或停用將資料集內嵌至設定檔服務 |
| [!DNL ExperienceEvent] 資料集TTL | 對設定檔存放區中的行為資料集套用TTL過期。 請連絡您的Adobe支援代表。 |
| [Adobe Analytics資料準備篩選器](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | 套用 [!DNL Kafka] 從擷取中排除不必要資料的篩選器 |
| [Adobe Audience Manager來源連接器篩選器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | 套用Audience Manager來源連線篩選器，以排除不必要的資料不擷取 |
| [Alloy SDK資料篩選器](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) | 套用合金篩選器以排除不必要的資料不擷取 |
| [事件轉送資料篩選器](../../tags/ui/event-forwarding/overview.md) | 套用伺服器端 [!DNL Kafka] 篩選器，以排除不必要的資料而不擷取。  請參閱 [標籤規則](../../tags/ui/managing-resources/rules.md) 以取得其他資訊。 |
| [授權使用控制面板UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | 查看貴組織與許可證相關的資料的快照以進行Experience Platform |
| [資料集重疊報表API](../../profile/tutorials/dataset-overlap-report.md) | 輸出對可定址對象貢獻最大的資料集 |
| [身分重疊報表API](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | 輸出對可定址對象貢獻最大的身分命名空間 |

{style=&quot;table-layout:auto&quot;}
