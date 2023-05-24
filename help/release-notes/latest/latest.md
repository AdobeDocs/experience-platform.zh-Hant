---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform 2023年5月發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 85401e3abfd7d5d1d84e082d20a1a064760c4e19
workflow-type: tm+mt
source-wordcount: '1071'
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
| 擴充對草稿模式的API支援 | 您現在可以在使用時暫停並儲存來源工作流程期間的進度 [!DNL Flow Service] API隨時提供。 使用 `mode=draft` 將基礎、來源和目標連線儲存為草稿的狀態。 可稍後重新檢視所有草繪圖元，以便完成。 閱讀指南： [設定您的 [!DNL Flow Service] 圖元變成草稿狀態](../../sources/tutorials/api/draft.md) 以取得詳細資訊。 |
| 全面發行 [!DNL Salesforce Marketing Cloud] source | 此 [[!DNL Salesforce Marketing Cloud source] 現在為GA](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md). 使用此來源將您的 [!DNL Salesforce Marketing Cloud] 要Experience Platform的資料。 |
| [!DNL Google Ads] 驗證更新 | 您現在可以在驗證您的憑證時提供登入客戶ID。 [!DNL Google Ads] 從特定作業客戶擷取報表資料的來源帳戶。 閱讀 [[!DNL Google Ads] 來原始檔](../../sources/connectors/advertising/ads.md) 以取得詳細資訊。 |
| [!DNL Google PubSub] 驗證更新 | 您現在可以為定義存取許可權 [!DNL Google PubSub] 建立新帳戶時的來源。 使用專案型驗證可允許根層級的存取，或使用主題和訂閱型驗證來限制特定主題和訂閱資料流的存取。 閱讀 [[!DNL Google PubSub] 來原始檔](../../sources/connectors/cloud-storage/google-pubsub.md) 以取得詳細資訊。 |
| 的新分頁欄位引數 `type=PAGE` 自助來源（批次SDK） | 您現在可以使用 `initialPageIndex` 和 `endPageIndex` 整合來源時 `type=PAGE` 透過Batch SDK. <ul><li>`initialPageIndex`：此引數可讓您定義分頁開始的頁碼。 </li><li>`endPageIndex`：此引數可讓您建立結束條件並停止分頁。</li></ul> 如需這些新引數的詳細資訊，請參閱 [自助來源批次SDK檔案](../../sources/sources-sdk/config/sourcespec.md#page). |
| 草稿模式的UI支援 | 您現在可以在來源工作流程期間，透過使用者介面暫停並儲存進度。 您可以選取 **[!UICONTROL 另存為草稿]** 在工作流程的資料流詳細資訊、對應和排程步驟期間，將您的資料流儲存為草稿以供稍後完成。 閱讀指南： [在UI中將資料流儲存為草稿](../../sources/tutorials/ui/draft.md) 以取得詳細資訊。 |

{style="table-layout:auto"}

若要進一步瞭解來源，請閱讀 [來源概觀](../../sources/home.md).

<!-- | API support for streaming data from a [!DNL Snowflake] database | You can now stream data from a [[!DNL Snowflake] source](../../sources/connectors/databases/snowflake.md) using the [!DNL Flow Service] API. | -->