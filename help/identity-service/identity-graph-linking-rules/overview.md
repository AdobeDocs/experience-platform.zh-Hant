---
title: 身分圖表連結規則
description: 瞭解Identity Service中的身分圖表連結規則。
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 38d331bd9265f25a3aebdcbd20ae5fc30a93e960
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 7%

---

# [!DNL Identity Graph Linking Rules] 概觀 {#identity-graph-linking-rules-overview}

>[!CONTEXTUALHELP]
>id="platform_identities_linkingrules_overview"
>title="身分識別圖連結規則"
>abstract="為避免這些不想要的合併，您可以使用透過身分圖表連結規則提供的設定，並允許使用者進行精確的個人化。"

>[!IMPORTANT]
>
>[!DNL Identity Graph Linking Rules]現已正式可用。 如果您有現有的沙箱，在啟用身分設定後，需要取消收合的圖形（「已修正」），請聯絡您的Adobe帳戶團隊或Adobe支援。

透過Adobe Experience Platform Identity Service和即時客戶設定檔，很容易假設您的資料已完全內嵌，而且所有合併的設定檔透過個人識別碼（例如CRMID）代表單一個人。 但是，在某些情況下，某些資料可能會嘗試將多個不同的設定檔合併為單一設定檔（「圖表摺疊」）。 若要防止這些不想要的合併，您可以使用透過[!DNL Identity Graph Linking Rules]提供的設定，並允許使用者進行精確的個人化。

## 快速入門

下列檔案是瞭解[!DNL Identity Graph Linking Rules]的必要條件。

* [身分最佳化演演算法](./identity-optimization-algorithm.md)
* [實作指南](./implementation-guide.md)
* [圖表設定範例](./example-configurations.md)
* [疑難排解和常見問答( FAQ)](./troubleshooting.md)
* [命名空間優先順序](./namespace-priority.md)
* [圖表模擬UI](./graph-simulation.md)
* [身分設定UI](./identity-settings-ui.md)

## 視訊程式庫

觀看以下影片，瞭解身分圖表連結規則的一些基本層面。

<!-- CARDS
{target = _blank}
* https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/identities/graph-linking-rules/overview
* https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation 

    {description = Learn how to use the graph simulator to test out identity graph linking rules.}

* https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings
    {description = Learn how to enable and configure identity graph linking rules to build accurate customer profiles}
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules overview">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" title="身分識別圖連結規則概觀" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3448250/?format=jpeg&nocache=1747851655227" alt="身分識別圖連結規則概觀"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" target="_blank" rel="referrer" title="身分識別圖連結規則概觀">身分識別圖連結規則概觀</a>
                    </p>
                    <p class="is-size-6">概略了解身分識別圖連結規則如何協助資料架構者維護準確的客戶設定檔，並防止圖表崩潰。</p>
                </div>
                <a href="https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">觀看</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules - Graph Simulation">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" title="身分圖表連結規則 — 圖表模擬" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3444032/?format=jpeg&nocache=1747851655237" alt="身分圖表連結規則 — 圖表模擬"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" target="_blank" rel="referrer" title="身分圖表連結規則 — 圖表模擬">身分識別圖連結規則 - 圖表模擬</a>
                    </p>
                    <p class="is-size-6">瞭解如何使用圖表模擬器來測試身分圖表連結規則。</p>
                </div>
                <a href="https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">觀看</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules - Identity settings">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" title="身分圖表連結規則 — 身分設定" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3458487/?format=jpeg&nocache=1747851655218" alt="身分圖表連結規則 — 身分設定"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" target="_blank" rel="referrer" title="身分圖表連結規則 — 身分設定">身分圖表連結規則 — 身分設定</a>
                    </p>
                    <p class="is-size-6">瞭解如何啟用及設定身分圖表連結規則，以建置準確的客戶設定檔</p>
                </div>
                <a href="https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">觀看</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


## 圖表收合案例 {#graph-collapse-scenarios}

>[!CONTEXTUALHELP]
>id="platform_identities_graphcollapsescenarios"
>title="圖表收合案例"
>abstract="圖表可能「收合」或代表多人實體的原因有很多。"

本節概述設定[!DNL Identity Graph Linking Rules]時可考慮的範例情境。

### 共用裝置

在單一裝置上可能發生多次登入的例項：

| 共用裝置 | 說明 |
| --- | --- |
| 家用電腦和平板電腦 | 丈夫和妻子都登入各自的銀行帳戶。 |
| 公用資訊站 | 在機場登入的旅行者，會使用他們的忠誠度身份證來登記行李和列印登機牌。 |
| 呼叫中心 | 客服中心人員代表客戶致電客戶支援以解決問題，登入單一裝置。 |

![一些常用共用裝置的圖表。](../images/identity-settings/shared-devices.png "某些共用裝置的圖表。"){zoomable="yes"}

在這些情況下，從圖表觀點來看，未啟用任何限制，單一ECID會連結至多個CRMID。

透過[!DNL Identity Graph Linking Rules]，您可以：

* 設定用於登入的ID作為唯一識別碼。 例如，您可以限制圖表僅儲存一個具有CRMID名稱空間的身分識別，然後將CRMID定義為共用裝置的唯一識別碼。
   * 這麼做可確保ECID不會合併CRMID。

### 無效的電子郵件/電話案例

註冊時也會有使用者提供虛假值做為電話號碼和/或電子郵件地址的例項。 在這些情況下，如果未啟用限制，則電話/電子郵件相關的身分最終將會連結到多個不同的CRMID。

![代表無效電子郵件或電話情況的圖表。](../images/identity-settings/invalid-email-phone.png "代表無效電子郵件或電話情況的圖表。"){zoomable="yes"}

透過[!DNL Identity Graph Linking Rules]，您可以：

* 將CRMID、電話號碼或電子郵件地址設定為唯一識別碼，因此將一個人限製為只能有一個與其帳戶相關聯的CRMID、電話號碼和/或電子郵件地址。

### 錯誤或錯誤的身分值

在某些情況下，無論名稱空間為何，都會在系統中擷取非唯一、錯誤的身分值。 例如：

* 身分值為「user_null」的IDFA名稱空間。
   * IDFA身分值應該有36個字元： 32個英數字元和4個連字型大小。
* 身分值為「未指定」的電話號碼名稱空間。
   * 電話號碼不應有任何字母字元。

這些身分可能會導致以下圖表，其中多個CRMID與「不良」身分合併在一起：

![具有錯誤或錯誤身分值的身分資料圖表範例。](../images/identity-settings/bad-data.png "具有錯誤或錯誤身分值的身分資料圖形範例。"){zoomable="yes"}

透過[!DNL Identity Graph Linking Rules]，您可以將CRMID設定為唯一識別碼，以防止由於此型別的資料而造成不需要的設定檔摺疊。

## [!DNL Identity Graph Linking Rules] {#identity-graph-linking-rules}

透過[!DNL Identity Graph Linking Rules]，您可以：

* 透過設定唯一的名稱空間，為每個使用者建立單一身分圖表/合併的設定檔，以防止兩個不同的個人識別碼合併到一個身分圖表中。
* 透過設定優先順序來關聯線上、已驗證的事件與人員

### 術語 {#terminology}

| 術語 | 說明 |
| --- | --- |
| 唯一命名空間 | 唯一名稱空間是身分識別名稱空間，在身分識別圖形的上下文中已設定為不同。 您可以使用UI將名稱空間設定為唯一。 一旦名稱空間定義為唯一，圖表就只能有一個包含該名稱空間的身分。 |
| 命名空間優先順序 | 名稱空間優先順序是指名稱空間彼此相比的相對重要性。 名稱空間優先順序可透過UI設定。 您可以在指定的身分圖表中排列名稱空間。 啟用後，名稱優先順序將用於各種情境，例如身分最佳化演演算法的輸入以及判斷體驗事件片段的主要身分。 |
| 身分最佳化演演算法 | 身分最佳化演演算法可確保透過設定唯一名稱空間和名稱空間優先順序所建立的准則，在指定的身分圖形中強制執行。 |

### 唯一命名空間 {#unique-namespace}

您可以使用身分設定UI工作區將名稱空間設定為唯一。 如此一來，會通知身分最佳化演演算法，指定圖表可能只有一個包含該唯一名稱空間的身分。 這可防止將兩個不同的人員識別碼合併到同一個圖表中。

請考量下列情況：

* Scott使用平板電腦並開啟Google Chrome瀏覽器，前往acme<span>.com，在此登入並瀏覽新籃球鞋。
   * 在幕後，此情境會記錄下列身分：
      * 代表使用瀏覽器的ECID名稱空間和值
      * 代表已驗證使用者（Scott以他的使用者名稱和密碼組合登入）的CRMID名稱空間和值。
* 他的兒子Peter接著使用相同的平板電腦，並使用Google Chrome前往acme<span>.com，以自己的帳戶登入以瀏覽足球裝備。
   * 在幕後，此情境會記錄下列身分：
      * 代表瀏覽器的相同ECID名稱空間和值。
      * 代表已驗證使用者的新CRMID名稱空間和值。

如果將CRMID設定為唯一的名稱空間，則身分最佳化演演算法會將CRMID分割成兩個個別的身分圖表，而不是將其合併在一起。

如果您未設定唯一的名稱空間，您最後可能會遇到不想要的圖表合併，例如具有相同CRMID名稱空間但不同身分值（這類情況通常代表同一圖表中的兩個不同個人實體）的兩個身分實體。

您必須設定唯一的名稱空間，以通知身分最佳化演演算法強制限制擷取到指定身分圖表的身分資料。

### 命名空間優先順序 {#namespace-priority}

名稱空間優先順序是指名稱空間彼此相比的相對重要性。 名稱空間優先順序可透過UI設定，並且您可以在指定的身分圖表中排行名稱空間。

使用名稱空間優先順序的一種方式，是判斷即時客戶設定檔中體驗事件片段（使用者行為）的主要身分。 如果已設定優先順序設定，則網路SDK上的主要身分設定將不再用來決定要儲存哪些設定檔片段。

唯一的名稱空間和名稱空間優先順序都可在身分設定UI工作區中設定。 不過，其設定的效果會有所不同：

| | 身分識別服務 | 即時客戶輪廓 |
| --- | --- | --- |
| 唯一命名空間 | 在Identity Service中，身分最佳化演演算法會參考唯一的名稱空間，以判斷要內嵌至指定身分圖表的身分資料。 | 不重複名稱空間不會影響即時客戶個人檔案。 |
| 命名空間優先順序 | 在Identity Service中，對於擁有多個圖層的圖形，名稱空間優先順序將決定適當的連結是否已移除。 | 在設定檔中擷取體驗事件時，具有最高優先順序的名稱空間會成為設定檔片段的主要身分。 |

* 當達到每個圖表50個身分的限制時，名稱空間優先順序不會影響圖表行為。
* **名稱空間優先順序是指派給名稱空間的數值**，表示其相對重要性。 這是名稱空間的屬性。
* **主要身分是針對**&#x200B;儲存設定檔片段的身分。 設定檔片段是儲存特定使用者相關資訊的資料記錄：屬性（通常透過CRM記錄擷取）或事件（通常從體驗事件或線上資料擷取）。
* 名稱空間優先順序決定體驗事件片段的主要身分。
   * 對於設定檔記錄，您可以使用Experience Platform UI中的結構描述工作區來定義身分欄位，包括主要身分。 如需詳細資訊，請參閱[在UI](../../xdm/ui/fields/identity.md)中定義身分欄位的指南。
* 如果體驗事件在identityMap中具有兩個或多個最高名稱空間優先順序的身分，該事件將會因為會被視為「錯誤資料」而遭到拒絕的擷取。 例如，如果identityMap包含`{ECID: 111, CRMID: John, CRMID: Jane}`，則整個事件將會被拒絕為錯誤資料，因為它表示該事件同時與`CRMID: John`和`CRMID: Jane`相關聯。

如需詳細資訊，請閱讀[名稱空間優先順序](./namespace-priority.md)的指南。

## 後續步驟

如需[!DNL Identity Graph Linking Rules]的詳細資訊，請閱讀下列檔案：

* [身分最佳化演演算法](./identity-optimization-algorithm.md)
* [實作指南](./implementation-guide.md)
* [圖表設定範例](./example-configurations.md)
* [疑難排解和常見問答( FAQ)](./troubleshooting.md)
* [命名空間優先順序](./namespace-priority.md)
* [圖表模擬UI](./graph-simulation.md)
* [身分設定UI](./identity-settings-ui.md)