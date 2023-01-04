---
keywords: Experience Platform；使用手冊；歸因ai；熱門主題；地區
feature: Attribution AI
title: Attribution AIUI指南
topic-legacy: User guide
description: 本檔案可做為與Intelligent Services使用者介面中的Attribution AI互動的指南。
exl-id: 32e1dd07-31a8-41c4-88df-8893ff773f79
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2960'
ht-degree: 1%

---

# Attribution AIUI指南

Attribution AI是Intelligent Services的一部分，是多管道的演算法歸因服務，可計算客戶互動對指定結果的影響和增量影響。 透過 Attribution AI，行銷人員可經由了解每個客戶在客戶歷程各個階段的互動所產生的影響，來衡量行銷和廣告支出並予以最佳化。

本檔案可做為與Intelligent Services使用者介面中的Attribution AI互動的指南。

## 建立例項

在 [!DNL Adobe Experience Platform] UI, select **[!UICONTROL 服務]** 的下一頁。 此 **[!UICONTROL 服務]** 瀏覽器隨即顯示，並顯示可用的Adobe智慧服務。 在Attribution AI的容器中，選取 **[!UICONTROL 開啟]**.

![存取您的執行個體](./images/user-guide/open_Attribution_ai.png)

Attribution AI服務頁面隨即顯示。 此頁面會列出Attribution AI的服務例項，並顯示其相關資訊，包括例項名稱、轉換事件、執行例項的頻率，以及上次更新的狀態。

您可以找到 **[!UICONTROL 計分的轉換事件總數]** 位於 **[!UICONTROL 建立例項]** 容器。 此量度會追蹤目前日曆年度中，依Attribution AI評分的轉換事件總數，包括所有沙箱環境和任何已刪除的服務例項。

![總計轉換](./images/user-guide/total_conversions.png)

使用UI右側的控制項，即可編輯、複製及刪除服務例項。 若要顯示這些控制項，請從現有的 **[!UICONTROL 服務實例]**. 控制項包含下列資訊：

- **[!UICONTROL 編輯]**:選取 **[!UICONTROL 編輯]** 可讓您修改現有的服務執行個體。 您可以編輯例項的名稱、說明、狀態和計分頻率。
- **[!UICONTROL 原地複製]**:選取 **[!UICONTROL 原地複製]** 複製所選服務實例。 接著，您可以修改工作流程進行微幅調整，並重新命名為新例項。
- **[!UICONTROL 刪除]**:您可以刪除服務例項，包括任何歷史執行。 將從Platform中刪除對應的輸出資料集。 不過，同步至即時客戶設定檔的分數不會刪除。
- **[!UICONTROL 資料來源]**:所使用資料集的連結。 如果Attribution AI使用多個資料集，系統會顯示「多個」，後面接著資料集數量。 選取超連結時，資料集預覽彈出視窗隨即顯示。
- **[!UICONTROL 上次運行詳細資訊]**:唯有執行失敗時，才會顯示此選項。 此處顯示執行失敗原因（例如錯誤代碼）的資訊。

![側窗格](./images/user-guide/multiple-datasets-pane.png)

- **[!UICONTROL 轉換事件]**:快速概述針對此執行個體設定的轉換事件。
- **[!UICONTROL 回顧期間]**:您定義的時間範圍，指出包含轉換事件接觸點前的天數。
- **[!UICONTROL 接觸點]**:建立此例項時定義的所有接觸點的清單。

![](./images/user-guide/side_panel_2.png)

選擇 **[!UICONTROL 建立例項]** 開始。

![建立例項](./images/user-guide/landing_page.png)

接下來，將顯示Attribution AI的設定頁面，您可在其中提供服務執行個體的名稱和可選說明。

![命名例項](./images/user-guide/naming_instance.png)

## 選擇資料 {#select-data}

<!-- https://www.adobe.com/go/aai-select-data -->

根據設計，Attribution AI可以使用Adobe Analytics、體驗事件和消費者體驗事件資料來計算歸因分數。 選取資料集時，僅會列出與Attribution AI相容的資料集。 若要選取資料集，請選取&#x200B;**+**)資料集名稱旁的符號，或選取核取方塊以一次新增多個資料集。 您也可以使用搜尋選項來快速找到您感興趣的資料集。

選取您要使用的資料集後，請選取 **[!UICONTROL 新增]** 按鈕，將資料集新增至資料集預覽窗格。

![選取資料集](./images/user-guide/select-datasets.png)

選取資訊圖示 ![資訊圖示](./images/user-guide/info-icon.png) 資料集旁邊會開啟資料集預覽視窗。

![選取和搜尋資料集](./images/user-guide/dataset-preview.png)

資料集預覽包含上次更新時間、來源結構，以及前10欄的預覽等資料。

選擇 **[!UICONTROL 儲存]** 在工作流程中移動時儲存草稿。 您也可以儲存草稿模型設定，並移至工作流程的下一個步驟。 使用 **[!UICONTROL 保存並繼續]** 在模型配置期間建立和保存草稿。 此功能可讓您建立和儲存模型配置的草稿，當您必須在配置工作流程中定義許多欄位時，此功能特別有用。

![「保存並保存」(Save and Save)和「繼續」(Continue)突出顯示「建立Data Science Services」Attribution AI頁簽的工作流。](./images/user-guide/aai-save-save-&-exit.png)

### 資料集完整性 {#dataset-completeness}

<!-- https://www.adobe.com/go/aai-dataset-completeness -->

在資料集預覽中，資料集的完整性百分比值為。 此值提供資料集中有多少欄為空/空的快速快照。 如果資料集包含許多遺失值，而這些值被擷取到其他位置，強烈建議您加入包含遺失值的資料集。

>[!NOTE]
>
>資料集完整性是使用Attribution AI的最大培訓期間（一年）計算。 這表示顯示資料集完整性值時，不會考慮超過一年的資料。

![資料集完整性](./images/user-guide/dataset-completeness.png)

### 選取身分 {#identity}

您現在可以根據身分對應（欄位），將多個資料集連結在一起。 您必須選取身分類型（也稱為「身分命名空間」），以及該命名空間中的身分值。 如果您已在相同命名空間下將多個欄位指派為架構中的身分，所有指派的身分值都會出現在以命名空間為前置的身分下拉式清單中，例如 `EMAIL (personalEmail.address)` 或 `EMAIL (workEmail.address)`.

>[!IMPORTANT]
>
>您選取的每個資料集都必須使用相同的身分類型（命名空間）。 身分欄中的身分類型旁會出現綠色勾號，指出資料集相容。 例如，使用Phone命名空間時，以及 `mobilePhone.number` 做為識別碼，其餘資料集的所有識別碼都必須包含並使用Phone命名空間。

要選擇標識，請選擇位於標識列中的帶下划線的值。 此時會顯示「選取身分彈出視窗」。

![選擇相同的命名空間](./images/user-guide/aai-identity-map-save-and-exit.png)

如果命名空間中有多個身分可用，請務必為您的使用案例選取正確的身分欄位。 例如，電子郵件命名空間中提供兩個電子郵件身分識別：一個工作電子郵件，另一個是個人電子郵件。 根據使用案例，個人電子郵件更可能填入，且在個別預測中更有用。 這表示您會選取 `EMAIL (personalEmail.address)` 作為您的身份。

![未選擇資料集密鑰](./images/user-guide/aai-identity-namespace.png)

>[!NOTE]
>
> 如果資料集沒有有效的身分類型（命名空間），您必須設定主要身分識別，並使用 [結構編輯器](../../xdm/schema/composition.md#identity). 若要進一步了解命名空間和身分識別，請造訪 [身分識別服務命名空間](../../identity-service/namespaces.md) 檔案。

## 對應媒體頻道和行銷活動欄位 {#aai-mapping}

<!-- https://www.adobe.com/go/aai-mapping -->

選取並新增資料集後， **地圖** 設定步驟隨即顯示。 Attribution AI需要您對應上一步驟中選取之每個資料集的「媒體頻道」欄位。 這是因為若沒有資料集之間的媒體管道對應，衍生自Attribution AI的深入分析可能無法正確顯示，導致分析頁面難以解譯。 雖然只需要媒體管道，但強烈建議您對應一些選用欄位，例如媒體動作、促銷活動名稱、促銷活動群組和促銷活動標籤。 如此可讓Attribution AI提供更清楚的分析和最佳結果。

![映射](./images/user-guide/mapping-save-&-exit.png)

## 定義事件 {#define-events}

<!-- https://www.adobe.com/go/aai-define-events -->

定義事件時使用三種不同類型的輸入資料：

- **轉換事件：** 識別行銷活動影響的業務目標，例如電子商務訂單、店內購買和網站造訪。
- **回顧期間：** 提供時間範圍，指出應包含轉換事件接觸點前的天數。
- **接觸點：** 收件者、個人或cookie層級行銷事件，用於評估轉換的數值或收入型影響。

### 定義轉換事件 {#define-conversion-events}

若要定義轉換事件，您必須為事件指定名稱，並選取事件類型，方法是從 **選取資料集和欄位** 下拉式功能表。

![是下拉式清單](./images/user-guide/define-conversion-events.png)

選取事件後，新的下拉式清單會顯示在其右側。 第二個下拉式清單可透過使用操作，為您的事件提供更多內容。 對於此轉換事件，為預設操作 *存在* 中所有規則的URL區段。

>[!NOTE]
>
>您 *轉換名稱* 會在您定義事件時更新。

![無下拉式清單](./images/user-guide/conversion_event_1.png)

接下來，您可以選取結合的資料集，該資料集是由合併前一個步驟中的所有輸入資料集所產生。 或者，您也可以根據 **選取資料集和欄位** 下拉式功能表。

此 **[!UICONTROL 新增事件]** 和 **[!UICONTROL 新增群組]** 按鈕可用來進一步定義轉換。 視您定義的轉換而定，您可能需要使用 **[!UICONTROL 新增事件]** 和 **[!UICONTROL 新增群組]** 按鈕提供更多內容。

![新增事件](./images/user-guide/add_event.png)

選取 **[!UICONTROL 新增事件]** 會建立其他欄位，使用上述相同的方法來填入。 這樣會在轉換名稱下方的字串定義中新增AND陳述式。 選取 **x** 移除已新增的事件。

![新增事件功能表](./images/user-guide/add_event_result.png)

選取 **[!UICONTROL 新增群組]** 提供可建立與原始欄位不同之其他欄位的選項。 加上組，藍色 *和* 按鈕。 選取 **和** 提供將參數變更為包含「Or」的選項。 「Or」可用來定義多個成功的轉換路徑。 「和」延伸轉換路徑以包含其他條件。

![使用和](./images/user-guide/and_or.png)

如果您需要多個轉換，請選取 **新增轉換** 來建立新的轉換卡。 您可以重複上述程式來定義多個轉換。

![新增轉換](./images/user-guide/add_conversion.png)

### 定義回顧期間 {#lookback-window}

定義完轉換後，您需要確認回顧期間。 使用方向鍵或選取預設值(56)，指定您要加入接觸點的轉換事件前幾天。 接觸點會在下一個步驟中定義。

![回顧](./images/user-guide/lookback_window.png)

### 定義接觸點

定義接觸點會遵循類似的工作流程， [定義轉換](#define-conversion-events). 起初，您需要為接觸點命名，並從 *輸入欄位名稱* 下拉式功能表。 選取後，運算子下拉式清單就會顯示預設值「exists」。 選取下拉式清單以顯示運算子清單。

![運算子](./images/user-guide/operators.png)

為此接觸點的目的，請選取 **等於**.

![步驟1](./images/user-guide/touchpoint_step1.png)

選取接觸點的運算子後， *輸入欄位值* 已可供使用。 的下拉式清單值 *輸入欄位值* 根據您先前選取的運算子和接觸點值填入。 如果值未填入下拉式清單中，您可以手動在中輸入該值。 選取下拉式清單，然後選取 **按一下**.

>[!NOTE]
>
>運算子「exists」和「not exists」沒有與它們相關聯的欄位值。

![接觸點下拉式清單](./images/user-guide/touchpoint_dropdown.png)

此 **新增事件** 和 **新增群組** 按鈕可用來進一步定義接觸點。 由於接觸點的周圍性質複雜，單一接觸點有多個事件和群組的現象並不少見。

若選取， **新增事件** 允許新增其他欄位。 選取 **x** 移除已新增的事件。

![新增事件](./images/user-guide/touchpoint_add_event.png)

選取 **新增群組** 可讓您選擇建立與原始欄位不同的其他欄位。 加上組，藍色 *和* 按鈕。 選擇 **和** 若要變更參數，新參數「Or」可用來定義多個成功路徑。 此特定接觸點只有一個成功路徑，因此不需要「Or」。

![接觸點概觀](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>使用下方的字串 *接觸點名稱* 以取得接觸點的快速概觀。 請注意，字串與接觸點的名稱相符。

![](./images/user-guide/touchpoint_string.png)

您可以選取 **新增接觸點** 並重複上述程式。

![新增接觸點](./images/user-guide/add_touchpoint.png)

定義完所有必要的接觸點後，向上捲動並選取 **下一個** ，以繼續執行最後一個步驟。

![完成定義](./images/user-guide/define_event_save_and_exit.png)

## 高級培訓和評分設定

Attribution AI中的最後一頁是 **[!UICONTROL 進階]** 用於設定訓練和分數的頁面。

![新的頁面集選項](./images/user-guide/advanced_settings_set_options.png)

### 計畫培訓

使用 *排程*，您可以選取要進行分數的一週中的日期和時間。

選取下方的下拉式清單 *計分頻率* 以在每日、每週和每月評分之間進行選擇。 接下來，選擇要進行分數的星期幾。 可選取多天。 再次選取當天會取消選取。

![計畫培訓](./images/user-guide/schedule_training.png)

要更改要進行計分的時間，請選擇時鐘錶徵圖。 在顯示的新覆蓋圖中，輸入要進行計分的時間。 在覆蓋圖外部選取以關閉它。

>[!NOTE]
>
>完成每個計分程式最多需要24小時。

![時鐘錶徵圖](./images/user-guide/time_of_day.png)

### 其他分數資料集欄（選用）

依預設，會為標準結構中的每個服務例項建立分數資料集。 您可以根據「轉換事件」和「接觸點」設定，選擇新增其他欄至計分資料集輸出。 首先，您可以從輸入資料集中選取欄，接著將滑鼠左鍵按住漢堡圖示上方，即可拖放欄以變更順序。

![分數資料集欄加總](./images/user-guide/Add-score-dataset.png)

### 以區域為基礎的模型（可選） {#region-based-modeling-optional}

客戶的行為可能因國家/地區和地理區域而大不相同。 對於全球企業而言，使用國家/地區或地區模型可提高歸因準確度。 新增的每個區域都會使用該區域的資料建立新模型。

要定義新區域，請從選擇 **[!UICONTROL 新增地區]**. 在顯示的容器中，提供地區名稱。 只有一個值(「placeContext.geo.countryCode」)會從 **[!UICONTROL 輸入欄位名稱]** 下拉式清單。 選取此值。

![在中選擇區域](./images/user-guide/select_region_att.png)

接下來，選擇一個運算子。

![區域算子](./images/user-guide/region_operators.png)

最後，在 **[!UICONTROL 輸入欄位值]** 下拉式清單。

>[!NOTE]
>
>國家/地區代碼為兩個字元長。 您可以在此處找到完整清單 [ISO 3166-1alpha-2](https://datahub.io/core/country-list).

![地區](./images/user-guide/region-based.png)

### 培訓窗口 {#training-window}

為了確保您盡可能獲得最精確的模型，請務必使用代表您業務的歷史資料來訓練您的模型。 依預設，模型會使用2個季度（6個月）的轉換事件資料進行訓練。 選取下拉式清單以變更預設值。 您可以選擇使用1到4個季度的資料（3-12個月）進行培訓。

>[!NOTE]
>
>較短的培訓窗口對最近的趨勢更敏感，而較長的培訓窗口則建立更強健的模型，對最近的趨勢更不敏感。

![培訓窗口](./images/user-guide/training_window.png)

選擇培訓窗口後，選擇 **[!UICONTROL 完成]** 在右上角。 讓資料有時間處理。 完成後，畫面會顯示彈出式對話方塊，確認執行個體設定完成。 選擇 **[!UICONTROL 確定]** 被重定向到 **[!UICONTROL 服務實例]** 頁面，您可在其中看到您的服務例項。

![安裝完成](./images/user-guide/instance_setup_complete.png)

## 治理政策

完成工作流程以建立例項並提交模型的設定後， [政策執行](/help/data-governance/enforcement/auto-enforcement.md) 檢查是否有違規。 如果發生策略違規，將顯示一個彈出窗口，指示已違反一個或多個策略。 這是為了確保您的資料操作和Platform中的行銷動作符合資料使用原則。

![顯示違反原則的彈出視窗](./images/user-guide/policy-violation-popover-aai.png)

彈出式視窗會提供違規的特定資訊。 您可以通過策略設定和與配置工作流不直接相關的其他措施來解決這些違規。 例如，您可以變更標籤，讓某些欄位可用於資料科學用途。 或者，您也可以修改模型配置本身，使其不使用帶有標籤的任何內容。 請參閱本檔案，以進一步了解如何設定 [原則](/help/data-governance/policies/overview.md).

## 以屬性為基礎的存取控制

>[!IMPORTANT]
>
>基於屬性的訪問控制當前僅在有限版本中可用。

[基於屬性的訪問控制](../../../help/access-control/abac/overview.md) 是Adobe Experience Platform的功能，可讓管理員根據屬性控制對特定物件和/或功能的存取。 屬性可以是新增至物件的中繼資料，例如新增至架構欄位或區段的標籤。 管理員定義了包括屬性的訪問策略以管理用戶訪問權限。

此功能可讓您以標籤來標示Experience Data Model(XDM)結構欄位，並定義組織或資料使用範圍。 同時，管理員可使用使用者和角色管理介面來定義XDM架構欄位的存取原則，並更妥善地管理指派給使用者或使用者群組（內部、外部或第三方使用者）的存取權。 此外，基於屬性的訪問控制允許管理員管理對特定段的訪問。

透過基於屬性的存取控制，管理員可以控制使用者對所有平台工作流程和資源的敏感個人資料(SPD)和個人識別資訊(PII)的存取權。 管理員可以定義只能存取特定欄位和與這些欄位對應的資料的使用者角色。

由於基於屬性的訪問控制，某些欄位和功能可能具有訪問限制，並且對某些Attribution AI服務實例不可用。 例如「身分」、「分數定義」和「原地複製」。

在Attribution AI工作區頂端 **前瞻分析頁面**，側邊欄中顯示的詳細資料會限制存取。

![Attribution AI工作區，其中會強調顯示限制結構欄位。](./images/user-guide/access-restricted.png)

如果您在 **[!UICONTROL 建立執行個體工作流程]** 頁面上，資料集名稱旁會出現警告符號，並顯示訊息： [!UICONTROL 已排除受限資訊].

![Attribution AI工作區中，已反白顯示限制資料集欄位。](./images/user-guide/restricted-info-excluded.png)

在 **[!UICONTROL 建立執行個體工作流程]** 頁面，警告會通知您 [!UICONTROL 由於存取限制，資料集預覽中不會顯示某些資訊。]

![Attribution AI工作區中，預覽的結構欄位限制會反白顯示結果。](./images/user-guide/restricted-dataset-preview.png)

在您建立具有限制資訊的例項後，請繼續前往 **[!UICONTROL 定義目標]** 步驟中，頂端會顯示警告： [!UICONTROL 由於存取限制，設定中未顯示特定資訊。]

![Attribution AI工作區，其中反白顯示實例結果的限制欄位。](./images/user-guide/information-not-displayed-save-and-exit.png)

## 後續步驟

依照本教學課程，您已成功在Attribution AI中建立服務例項。 執行個體完成計分（最多允許24小時）後，您就可以 [探索Attribution AI分析](./discover-insights.md). 此外，如果您想要下載計分結果，請造訪 [下載分數](./download-scores.md) 檔案。

## 其他資源

以下影片概述在Attribution AI中建立新例項的端對端工作流程。

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)
