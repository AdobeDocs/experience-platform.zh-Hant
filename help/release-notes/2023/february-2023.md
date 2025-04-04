---
title: Adobe Experience Platform 發行說明 (2023 年 2 月)
description: Adobe Experience Platform 2023 年 2 月版發行說明。
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 91%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 2 月 22 日**

Adobe Experience Platform 現有功能的更新：

- [資料集合](#data-collection)
- [[!DNL Destinations]](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [查詢服務](#query-service)
- [Real-Time Customer Data Platform B2B 版本](#b2b)
- [來源](#sources)

## 資料集合 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目標。

### Assurance {#assurance}

Adobe Assurance 可讓您檢查、校訂、模擬和驗證您在行動應用程式中收集資料或服務體驗的方式。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 公用 API | Adobe Assurance APIs 現已推出。Assurance API 是 API 的集合，可讓使用者在配備了包含 Mobile SDK 的 Adob&#x200B;&#x200B;e Assurance 擴充功能時，能夠測試自己的 Web 和行動應用程式並進行偵錯。若要了解 Assurance API 的詳細資訊，請閱讀 [Assurance API 概觀](https://developer.adobe.com/adobe-assurance-public-apis/)。 |

{style="table-layout:auto"}

如需有關 Assurance 的詳細資訊，請閱讀 [Assurance 文件](https://developer.adobe.com/client-sdks/documentation/platform-assurance/)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新功能或更新功能** {#destinations-new-updated-features}

| 功能 | 說明 |
| ----------- | ----------- |
| [「同意政策」擴充](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement)以用於和[檔案型 (批次) 目的地](/help/destinations/destination-types.md#file-based)的整合 | <p> 當輪廓不再符合同意政策的條件時，Experience Platform 現在會主動向檔案型目的地傳達其政策退場的訊息。這是 [2023 年 2 月版](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality)的要求，該版本包含了串流目的地的相同功能。 </p> <p> <b>注意事項</b>：此功能僅適用於 **[!UICONTROL Privacy and Security Shield]** 以及 **[!UICONTROL Healthcare Shield]** 的客戶。 </p> |

{style="table-layout:auto"}

**新文件或更新的文件** {#destinations-new-updated-documentation}

| 文件 | 說明 |
| ----------- | ----------- |
| 目的地運作方式的文件 | <p>我們根據使用者的常見問題發佈了三篇新的文章，闡述目的地如何運作：</p> <p><ul><li>[目的地中可設定的常用匯出設定](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[不同目的地類型的輪廓匯出行為](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[目的地啟動工作流程中的身分識別處理](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| UI 中的欄位汰除 | 您現在可以[在擷取資料後汰除結構描述中的欄位](../../xdm/tutorials/field-deprecation-ui.md)。XDM 欄位汰除讓您可從 UI 檢視中移除欄位，同時予以保留以供使用。如有需要，您可以再次顯示已汰除的欄位，而參照這些欄位的任何區段、查詢或下游解決方案都會照常執行。 |

{style="table-layout:auto"}

**新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類別 | [[!UICONTROL XDM 個別潛在客戶輪廓]](https://github.com/adobe/xdm/pull/1669/files) | 此「XDM 個別潛在客戶輪廓」類別引進了合作夥伴提供的 ID。 |

{style="table-layout:auto"}

**已更新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位群組 | [!UICONTROL 頻率上限限制] | 此「[!UICONTROL 頻率上限限制]」欄位群組已[更新，以支援重複和自訂事件](https://github.com/adobe/xdm/pull/1641/files)。 |
| 資料類型 | [!UICONTROL Web 反向連結] | Web 反向連結屬性已[更新為包括 `xdm:linkName` 和 `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files)。在前一頁面上分別選取了 HTML 元素的名稱和區域。 |
| 欄位群組 | [!UICONTROL Adobe CJM 體驗事件 - 訊息互動的詳細資料] | [該[!UICONTROL 追蹤器 URL] 欄位已新增](https://github.com/adobe/xdm/pull/1665/files)至 [!UICONTROL Adobe CJM 體驗事件]。此追蹤器會提供使用者所選取的 URL。 |
| 欄位群組 | [!UICONTROL Adobe CJM 體驗事件 - 訊息互動的詳細資料] | [空白的`meta:enum`屬性會](https://github.com/adobe/xdm/pull/1668/files)從 URL [!UICONTROL 追蹤類型]欄位移除。 |
| 資料類型 | [!UICONTROL 媒體資訊] | [已移除 `videoSegment` 屬性 (在[!UICONTROL 媒體資訊]資料類型中) 的規則運算式模式](https://github.com/adobe/xdm/pull/1667/files)。 |

{style="table-layout:auto"}

如需Experience Platform中XDM的詳細資訊，請閱讀[XDM系統總覽](../../xdm/home.md)&#x200B;。

## 查詢服務 {#query-service}

查詢服務可讓您使用標準的 SQL 查詢 Adobe Experience Platform 中的資料[!DNL Data Lake]。您可以加入任何資料湖的資料集，並將查詢結果擷取為新資料集，以用於報表、資料科學工作區或擷取至即時客戶輪廓。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 使用 SQL 啟用輪廓的資料集 | [在 CTAS 查詢中使用 LABEL 使資料集「啟用輪廓」](../../query-service/sql/syntax.md#create-table-as-select)，或使用 ALTER 以更新要為輪廓啟用的現有資料集。您可以使用此擴充的SQL建構，針對即時客戶個人檔案業務使用案例的衍生資料集提供順暢的支援。 如需詳細資訊，請參閱衍生資料集檔案](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md)的[無縫SQL流程。 |
| 監視已排程查詢 | 使用[「已排程查詢」索引標籤](../../query-service/ui/monitor-queries.md)找到有關查詢執行的重要資訊並訂閱警示。監視查詢以獲取排程詳細資料、狀態，並在萬一查詢失敗時獲取錯誤訊息/代碼。 |
| 切換自動完成功能 | 消除特定的中繼資料命令並[切換查詢編輯器自動完成功能](../../query-service/ui/user-guide.md#auto-complete)以縮短處理時間。本功能會在您編寫查詢時自動建議可能的 SQL 關鍵字和表格的詳細資料。 |
| 資料集範例 | 指定查詢中的抽樣率並[使用資料集範例建立統一的隨機採樣](../../query-service/key-concepts/dataset-samples.md)，或根據特定標準建立條件式範例。 |

{style="table-layout:auto"}

如需有關查詢服務的詳細資訊，請參閱[查詢服務概觀](../../query-service/home.md)。


## Real-Time Customer Data Platform B2B 版本 {#b2b}

在 Real-Time Customer Data Platform (Real-Time CDP) 上建置的 Real-Time CDP B2B 版本是專為採用企業對企業服務模式操作的行銷人員所建置的。它將來自多個來源的資料集中在一起，並將其合併成包含人員和帳戶輪廓的單一檢視。這種統一的資料讓行銷人員可以精確地以特定客群為目標，並在所有可用的管道中和這些客群互動。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 啟用相關的帳戶服務 | 新的切換功能可讓您在您的帳戶上啟用相關的帳戶服務。如需詳細資訊，請至「[啟用相關的帳戶服務](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable)」詳閱指南。 |

{style="table-layout:auto"}

若要了解 Real-Time CDP B2B 版本的詳細資訊，請閱讀 [Real-Time CDP B2B 版本概觀](../../rtcdp/overview.md)。

## 來源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，並允許您使用Experience Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 使用 [!DNL Google PubSub] 指定訂閱層級的存取權 | 現在提供驗證時的訂閱 ID，即可定義使用 [!DNL Google PubSub] 來源時對特定主題訂閱的存取權。如需詳細資訊，請使用Flow Service API](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md)或[Experience Platform UI](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md)閱讀[!DNL Google PubSub]驗證教學課程[。 |
| 從 [!DNL Marketo] 擷取自訂活動資料 | 您現在可以將自訂活動資料從您的 [!DNL Marketo] 執行個體帶到 Experience Platform。若要擷取自訂活動資料，您必須在 B2B 活動結構描述中設定自訂活動欄位並使用活動資料集建立資料流。資料流完成後，擷取的資料集即會同時包含您的 [!DNL Marketo] 執行個體中的標準和自訂活動。然後，您可以使用[查詢服務](../../query-service/home.md)來存取您在Experience Platform上的自訂活動記錄。 如需詳細資訊，請至「[建立自訂活動資料的資料流](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md)」詳閱指南。 |
| 從 [!DNL Marketo] 排除無人申請的帳戶 | 您現在可以設定在建立公司資料的資料流時是否要從擷取中排除或包含無人申請的帳戶。如需詳細資訊，請至「[建立  [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md) 的來源連線和資料流」詳閱指南。 |

{style="table-layout:auto"}

若要了解有關來源的詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
