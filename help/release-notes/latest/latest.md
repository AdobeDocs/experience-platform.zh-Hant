---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform 2023年5月發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 43f505c6d3871e6ebc7d644aef6ec3b71f9fc2bc
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 4%

---

# Adobe Experience Platform 發行說明

>[!IMPORTANT]
>
>為了因應Audience Portal功能的全面推出，Adobe Experience Platform正在更新系統和檔案內「對象」和「區段」的使用情況。
>
>- **對象**：一組具有共同特徵和行為的人員、帳戶、家庭或其他實體。
>
>- **區段定義**：在Adobe Experience Platform中，用來描述目標對象之關鍵特性或行為的規則。 此辭彙先前稱為「區段」。
>
>- **區段**：將設定檔分隔為對象的動作。 「區段」一詞現在僅用作動詞。
>
>- **細分**：識別並闡明設定檔特徵的動作，這些設定檔將分組在一起以產生一組結果，例如對象。
>
>因此，在Adobe Experience Platform UI中，您會看到「區段」被「對象」取代，以反映建立和管理對象的新路徑。

**發行日期：2023 年 5 月 24 日**

Adobe Experience Platform 現有功能更新：

- [資料彙集](#data-collection)
- [資料治理](#data-governance)
- [資料擷取](#data-ingestion)
- [目的地](#destinations)
- [體驗資料模型(XDM)](#xdm)
- [身份識別服務](#identity-service)
- [查詢服務](#query-service)
- [來源](#sources)


## 資料彙集 {#data-collection}

Adobe Experience Platform提供了一套技術，可讓您收集使用者端客戶體驗資料，並將其傳送至Adobe Experience Platform Edge Network，在那裡可以擴充和轉換資料，並將其分發到Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL Twitter] conversions API擴充功能 | 此 [[!DNL Twitter] 轉換API](../../tags/extensions/server/twitter/overview.md) 事件轉送擴充功能可讓您即時在伺服器端轉送事件資料，以轉換事件。 [!DNL Twitter] 轉換API。 |
| 資料元素路徑協助 | 在中決定資料元素的路徑 [核心擴充功能](../../tags/extensions/client/core/overview.md) 比以往更輕鬆。 此增強功能會提供引導式表單，協助您選取並格式化正確的資料元素路徑。 |

{style="table-layout:auto"}

若要進一步瞭解資料集合，請閱讀 [資料集合概觀](../../tags/home.md).

## 資料治理 {#data-governance}

Adobe Experience Platform資料控管是用於管理客戶資料並確保遵守適用於資料使用的法規、限制和政策的一系列策略與技術。 它在各層級的Experience Platform中發揮關鍵作用，包括編目、資料譜系、資料使用標籤、資料存取原則，以及對行銷動作資料的存取控制。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 資料集欄位層級標籤淘汰 | 將標籤套用至個別欄位的功能已從資料集移至結構描述。 這可讓您集中管理上游的欄位標籤，以進行資料控管、同意和存取控制。 先前套用的資料集欄位標籤將透過Experience PlatformUI暫時獲得支援。 任何現有的資料集欄位標籤，都必須在2024年5月31日之前手動移轉至結構描述欄位標籤。 請閱讀 [資料控管端對端指南](../../data-governance/e2e.md) 以取得標籤移轉的詳細資訊。 |

{style="table-layout:auto"}

若要進一步瞭解資料控管，請閱讀 [資料控管概觀](../../data-governance/home.md).

## 資料擷取 {#data-ingestion}

Adobe Experience Platform提供豐富的功能，可擷取任何型別和任何延遲的資料。 您可以使用Adobe建立的來源、資料整合合作夥伴或Adobe Experience Platform UI，使用批次或串流API來內嵌。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 資料擷取範本的Beta版 | 資料擷取範本為資料架構師和工程師提供標準範本和自動化工具，以加速資料擷取流程，包括架構和資料集建立及對應規則設定。 資料擷取範本目前適用於 [[!DNL Marketo Engage]](../../sources/connectors/adobe-applications/marketo/marketo.md)， [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) 和 [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) 來源。 如需詳細資訊，請閱讀以下指南： [在UI中使用範本](../../sources/tutorials/ui/templates.md). |

若要進一步瞭解資料擷取，請閱讀 [資料擷取概觀](../../ingestion/home.md).

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

**新目的地** {#new-destinations}

| 目的地 | 說明 |
| ----------- | ----------- |
| **[[!UICONTROL Mailchimp興趣類別]](../../destinations/catalog/email-marketing/mailchimp-interest-categories.md)** | **[!UICONTROL Mailchimp]** 是熱門的行銷自動化平台和電子郵件行銷服務，企業用來透過郵寄清單和電子郵件行銷活動管理與聯絡人（客戶、客戶或其他感興趣的當事方）交談。 使用此聯結器可根據連絡人的興趣和偏好來排序連絡人。 |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

| Functionality | Description |
| ----------- | ----------- |
| General availability of attribute-based personalization through the [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) and [Custom personalization](../../destinations/catalog/personalization/custom-personalization.md) destinations. | Leverage profile attributes in real-time to deliver one-to-one web and mobile personalization, via Adobe Target or other custom personalization destinations in Experience Platform. See the [dedicated documentation](../../destinations/ui/activate-edge-personalization-destinations.md) for more details. |
| Destination SDK support for grouping exported audiences based on merge policy. | When building a file-based destination with Destination SDK, you can now configure the grouping of exported audiences into one or multiple files, based on merge policy. <br><br> Additionally, you can now include the merge policy ID and merge policy name in the exported file names, by using the dedicated template macros. <br><br>See the [batch configuration documentation](../../destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md) for more details on how to use the `segmentGroupingEnabled` parameter and the new file name template macros.|

{style="table-layout:auto"}

-->

**修正和增強功能** {#destinations-fixes-and-enhancements}

- 我們已修正（測試版） SFTP雲端儲存空間目的地中的限制，該限制導致使用者無法自訂連線埠引數的值。 現在當您透過設定（測試版） SFTP目的地連線時，可編輯此值 [API](/help/destinations/api/activate-segments-file-based-destinations.md) 或 [UI](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information).

如需有關目的地的詳細一般資訊，請參閱 [目的地概觀](../../destinations/home.md).

## 體驗資料模型(XDM) {#xdm}

XDM是開放原始碼規格，針對帶入Adobe Experience Platform的資料提供通用結構和定義（結構描述）。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**已更新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位群組 | （多個） | 的數個欄位 [選件專案](https://github.com/adobe/xdm/pull/1720/files) 更新以從結構描述中移除雙重階層。 |
| 欄位群組 | [[!UICONTROL XDM個別潛在客戶設定檔]](https://github.com/adobe/xdm/pull/1721/files) | 此 `partnerProspect` 中繼資料標籤的選項已新增至 [!UICONTROL XDM個別潛在客戶設定檔] 類別。 |
| 資料類型 | （多個） | 已為「 」新增多個欄位 [!UICONTROL 媒體詳細資訊] 資料型別。 |
| 資料類型 | [[!UICONTROL 工作階段詳細資訊]](https://github.com/adobe/xdm/pull/1716/files) | 已新增新欄位，以指出是否發生重新導向。 |
| 欄位群組 | [[!UICONTROL MediaAnalytics互動細節]](https://github.com/adobe/xdm/pull/1716/files) | 已新增與媒體報告相關的新欄位。 |

{style="table-layout:auto"}

如需Platform中XDM的詳細資訊，請閱讀 [XDM系統總覽](../../xdm/home.md).

## 身份識別服務 {#identity-service}

Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，藉此全面瞭解客戶及其行為。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援Adobe Experience Cloud應用程式中的合作夥伴ID [!BADGE Beta]{type=Informative} | Identity Service現在提供合作夥伴ID。 合作夥伴ID是資料合作夥伴用來代表人員的識別碼。 在Real-time Customer Data Platform中，合作夥伴ID主要用於擴充受眾啟用和資料擴充。 合作夥伴ID不會儲存在身分圖表中。 如需詳細資訊，請閱讀以下檔案： [身分型別](../../identity-service/namespaces.md#identity-types). |

若要進一步瞭解Identity Service，請閱讀 [Identity Service概觀](../../identity-service/home.md)

## 查詢服務 {#query-service}

查詢服務可讓您使用標準SQL在Adobe Experience Platform中查詢資料 [!DNL data lake]. 您可以聯結Data Lake的任何資料集，並將查詢結果擷取為新資料集，以用於報表、Data Science Workspace或內嵌到即時客戶個人檔案中。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 計算ADLS資料集的資料行層級統計資料 | 此 `ANALYZE TABLE` 命令已擴充為 `COMPUTE STATISTICS` 和 `SHOW STATISTICS` SQL命令。 您現在可以計算ADLS資料集子集或該資料集內特定欄的統計資料。 如需詳細資訊，請閱讀 [資料集統計資料計算指南](../../query-service/essential-concepts/dataset-statistics.md). |

{style="table-layout:auto"}

若要進一步瞭解Query Services，請參閱 [查詢服務總覽](../../query-service/home.md).

## 來源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，並允許您使用Platform服務來建構、加標籤及增強這些資料。 您可以從多種來源擷取資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| API支援來自的串流資料 [!DNL Snowflake] 資料庫 | 您現在可以從以下位置串流資料： [[!DNL Snowflake] source](../../sources/connectors/databases/snowflake-streaming.md) 使用 [!DNL Flow Service] API。 |
| 擴充對草稿模式的API支援 | 您現在可以在使用時暫停並儲存來源工作流程期間的進度 [!DNL Flow Service] API隨時提供。 使用 `mode=draft` 將基礎、來源和目標連線儲存為草稿的狀態。 可稍後重新檢視所有草繪圖元，以便完成。 閱讀指南： [設定您的 [!DNL Flow Service] 圖元變成草稿狀態](../../sources/tutorials/api/draft.md) 以取得詳細資訊。 |
| 全面發行 [!DNL Salesforce Marketing Cloud] source | 此 [[!DNL Salesforce Marketing Cloud source] 現在為GA](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md). 使用此來源將您的 [!DNL Salesforce Marketing Cloud] 要Experience Platform的資料。 |
| [!DNL Google Ads] 驗證更新 | 您現在可以在驗證您的憑證時提供登入客戶ID。 [!DNL Google Ads] 從特定作業客戶擷取報表資料的來源帳戶。 閱讀 [[!DNL Google Ads] 來原始檔](../../sources/connectors/advertising/ads.md) 以取得詳細資訊。 |
| [!DNL Google PubSub] 驗證更新 | 您現在可以為定義存取許可權 [!DNL Google PubSub] 建立新帳戶時的來源。 使用專案型驗證可允許根層級的存取，或使用主題和訂閱型驗證來限制特定主題和訂閱資料流的存取。 閱讀 [[!DNL Google PubSub] 來原始檔](../../sources/connectors/cloud-storage/google-pubsub.md) 以取得詳細資訊。 |
| 的新分頁欄位引數 `type=PAGE` 自助來源（批次SDK） | 您現在可以使用 `initialPageIndex` 和 `endPageIndex` 整合來源時 `type=PAGE` 透過Batch SDK. <ul><li>`initialPageIndex`：此引數可讓您定義分頁開始的頁碼。 </li><li>`endPageIndex`：此引數可讓您建立結束條件並停止分頁。</li></ul> 如需這些新引數的詳細資訊，請參閱 [自助來源批次SDK檔案](../../sources/sources-sdk/config/sourcespec.md#page). |
| 草稿模式的UI支援 | 您現在可以在來源工作流程期間，透過使用者介面暫停並儲存進度。 您可以選取 **[!UICONTROL 另存為草稿]** 在工作流程的資料流詳細資訊、對應和排程步驟期間，將您的資料流儲存為草稿以供稍後完成。 閱讀指南： [在UI中將資料流儲存為草稿](../../sources/tutorials/ui/draft.md) 以取得詳細資訊。 |

{style="table-layout:auto"}

若要進一步瞭解來源，請閱讀 [來源概觀](../../sources/home.md).
