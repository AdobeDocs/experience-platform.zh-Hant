---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields;schemas;Schemas;identityMap;Identity map;Schema design;map;Map；事件建模；最佳做法；event;event;
solution: Experience Platform
title: XDM ExperienceEvent類別
topic-legacy: overview
description: 本檔案概述XDM ExperienceEvent類別，以及事件資料模型的最佳實務。
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 4f1fe7ca5f09bb1e8e1b913d1dee1cff347d6a24
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] 是標準的「體驗資料模型」(XDM)類別，可讓您在發生特定事件或達到特定條件集時，建立系統的時間戳記快照。

「體驗事件」是所發生事件的事實記錄，包括相關個人的時間點和身分。 事件可以是顯式（直接可觀察的人類行為）或隱式（在沒有直接人類行為的情況下提出），並且記錄時不進行匯總或解釋。 有關在平台生態系統中使用此類的更高級別資訊，請參閱[XDM概述](../home.md#data-behaviors)。

[!DNL XDM ExperienceEvent]類本身為方案提供了多個與時間序列相關的欄位。 在收錄資料時，會自動填入其中某些欄位的值：

![](../images/classes/experienceevent/structure.png)

| 屬性 | 說明 |
| --- | --- |
| `_id` | 事件的唯一字串識別碼。 此欄位可用來追蹤個別事件的唯一性、防止資料重複，並在下游服務中尋找該事件。<br><br>在某些情況下， `_id` 可以是 [通用唯一識別碼(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全域唯一識別碼(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)。在「Adobe Experience Platform資料準備」中，可使用[`uuid`或`guid`映射函式](../../data-prep/functions.md#special-operations)生成此值。<br><br>如果您是從來源連線串流資料或直接從Parce檔案擷取資料，您應串連特定的組合欄位，讓這些欄位變得唯一，例如主要ID、時間戳記、事件類型等，以產生此值。<br><br>請務必指出，此 **欄位不代表與個人相關的身分**，而是資料本身的記錄。與人有關的身份資料應被降級到由相容混音提供的[身份欄位](../schema/composition.md#identity)。 |
| `eventMergeId` | 如果使用[Adobe Experience Platform網頁SDK](../../edge/home.md)來收錄資料，這表示導致建立記錄的收錄批次的ID。 系統會在擷取資料時自動填入此欄位。 不支援在Web SDK實作之外使用此欄位。 |
| `eventType` | 指示事件類型或類別的字串。 如果您想要區分相同架構和資料集內的不同事件類型，例如區分產品檢視事件與零售公司的新增至購物車事件，則可使用此欄位。<br><br>此屬性的標準值在附錄部分 [中提供](#eventType)，包括其預期使用案例的說明。此欄位是可擴充的列舉，這表示您也可以使用您自己的事件類型字串來分類您追蹤的事件。 |
| `producedBy` | 描述事件產生者或來源的字串值。 若需要，此欄位可用來篩選特定事件產生者，以用於分段。<br><br>此屬性的一些建議值在附錄部分 [中提供](#producedBy)。此欄位是可擴充的列舉，這表示您也可以使用自己的字串來代表不同的事件產生者。 |
| `identityMap` | 映射欄位，包含事件所應用的個人的一組命名空間標識。 系統會在擷取身分資料時自動更新此欄位。 為了將此欄位正確用於[即時客戶概要檔案](../../profile/home.md)，請勿嘗試手動更新資料操作中的欄位內容。<br /><br />如需其使用案例的詳細資訊，請參 [閱架構構](../schema/composition.md#identityMap) 成基礎中有關身分映射的章節。 |
| `timestamp` | 事件發生時的ISO 8601時間戳記，格式為[RFC 3339第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6)。 此時間戳記必須發生在過去。 請參閱[時間戳記](#timestamps)上的下節，瞭解使用此欄位的最佳實務。 |

## 事件建模的最佳做法

以下各節介紹在Adobe Experience Platform設計事件型體驗資料模型(XDM)架構的最佳範例。

### 時間戳記 {#timestamps}

事件模式的根`timestamp`欄位只能&#x200B;****&#x200B;表示事件本身的觀察，且必須發生在過去。 如果您的分段使用案例需要使用日後可能發生的時間戳記，這些值必須限制在您的「體驗事件」結構中的其他位置。

例如，如果旅行和接待服務業的企業正在為航班預訂事件建模，則班級`timestamp`欄位表示預訂事件被觀察到的時間。 與事件相關的其他時間戳記（例如旅行訂房的開始日期），應在標準或自訂混音所提供的個別欄位中擷取。

![](../images/classes/experienceevent/timestamps.png)

透過在事件結構描述中將類別層級時間戳記與其他相關日期時間值分開，您可以實作有彈性的分段使用案例，同時保留體驗應用程式中客戶歷程的時間戳記帳戶。

### 使用計算欄位

您的體驗應用程式中的某些互動可能會產生多個相關事件，這些事件在技術上會共用相同的事件時間戳記，因此可以表示為單一事件記錄。 例如，如果客戶在您的網站上檢視產品，則可能導致事件記錄同時包含「產品檢視」屬性以及某些重疊的一般「頁面檢視」屬性。 在這些情況下，當記錄中擷取多個事件時，您可以使用計算欄位來擷取最重要的屬性。

[Adobe Experience Platform數](../../data-prep/home.md) 據預準備允許您映射、轉換和驗證與XDM之間的資料。使用服務提供的可用[映射函式](../../data-prep/functions.md)，可以調用邏輯運算子，以在將多事件記錄的資料引入Experience Platform時對資料進行優先順序排序、轉換和／或合併。

如果您要透過UI手動將資料擷取至平台，請參閱[將CSV檔案對應至XDM](../../ingestion/tutorials/map-a-csv-file.md)的指南，以取得如何建立計算欄位的特定步驟。

如果您使用來源連線將資料串流至平台，則可以設定來源以改用計算欄位。 有關如何在配置連接時實施計算欄位的說明，請參閱特定源的[文檔。](../../sources/home.md)

## 相容模式欄位組{#field-groups}

>[!NOTE]
>
>數個欄位群組的名稱已變更。 如需詳細資訊，請參閱[欄位群組名稱updates](../field-groups/name-updates.md)上的檔案。

Adobe提供多個標準欄位組，用於[!DNL XDM ExperienceEvent]類。 以下是類中一些常用欄位組的清單：

* [[!UICONTROL 用戶ID詳細資訊]](../field-groups/event/enduserids.md)
* [[!UICONTROL 環境詳細資訊]](../field-groups/event/environment-details.md)

## 附錄

下節包含有關[!UICONTROL XDM ExperienceEvent]類別的其他資訊。

### `eventType`的接受值 {#eventType}

下表概述`eventType`的接受值及其定義：

| 值 | 定義 |
| --- | --- |
| `advertising.completes` | 已觀看逾時媒體資產完成。 這不一定表示檢視者已觀看整個視訊，因為檢視者可能已跳過。 |
| `advertising.timePlayed` | 說明使用者在特定定時媒體資產上逗留的時間。 |
| `advertising.federated` | 指出是否透過資料聯盟建立體驗事件（客戶之間的資料共用）。 |
| `advertising.clicks` | 按一下廣告上的動作。 |
| `advertising.conversions` | 由客戶執行的預先定義動作，觸發事件進行效能評估。 |
| `advertising.firstQuartiles` | 數位視訊廣告以正常速度播放了25%的時間。 |
| `advertising.impressions` | 對有可能被檢視之客戶的廣告印象。 |
| `advertising.midpoints` | 數位視訊廣告以正常速度播放了50%的時間。 |
| `advertising.starts` | 數位視訊廣告已開始播放。 |
| `advertising.thirdQuartiles` | 數位視訊廣告以正常速度播放了75%的時間。 |
| `web.webpagedetails.pageViews` | 網頁已收到一或多個檢視。 |
| `web.webinteraction.linkClicks` | 連結已選取一或多次。 |
| `commerce.checkouts` | 產品清單已發生結帳事件。 如果結帳程式中有多個步驟，則可能會有多個結帳事件。 如果有多個步驟，則會使用每個事件的時間戳記和參考頁面／體驗來識別依順序呈現的每個個別事件（步驟）。 |
| `commerce.productListAdds` | 產品已新增至產品清單或購物車。 |
| `commerce.productListOpens` | 已初始化或建立新的產品清單（購物車）。 |
| `commerce.productListRemovals` | 一個或多個產品項目已從產品清單或購物車中移除。 |
| `commerce.productListReopens` | 客戶已重新啟動不再存取（放棄）的產品清單（購物車），例如透過再行銷活動。 |
| `commerce.productListViews` | 產品清單或購物車已收到一或多個檢視。 |
| `commerce.productViews` | 產品已收到一或多個檢視。 |
| `commerce.purchases` | 已接受命令。 這是商務轉換中唯一必要的動作。 購買事件必須有參考的產品清單。 |
| `commerce.saveForLaters` | 產品清單已儲存以供日後使用，例如產品願望清單。 |
| `delivery.feedback` | 傳送的意見回應事件，例如電子郵件傳送。 |
| `message.feedback` | 傳送給客戶之訊息的回饋事件，例如傳送／彈回／錯誤。 |
| `message.tracking` | 追蹤傳送給客戶之訊息的開啟／點按／自訂動作等事件。 |

### `producedBy`的建議值 {#producedBy}

下表概述了`producedBy`的一些接受值：

| 值 | 定義 |
| --- | --- |
| `self` | Self |
| `system` | 系統 |
| `salesRef` | 銷售代表 |
| `customerRep` | 客戶代表 |
