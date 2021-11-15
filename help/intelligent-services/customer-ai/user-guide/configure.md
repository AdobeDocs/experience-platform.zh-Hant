---
keywords: Experience Platform；使用手冊；customer ai；熱門主題；設定例項；建立例項；
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: 設定Customer AI例項
topic-legacy: Instance creation
description: Intelligent Services將Customer AI提供為簡單易用的Adobe Sensei服務，可針對不同使用案例進行設定。 以下各節提供設定Customer AI例項的步驟。
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
source-git-commit: 899ea8502c80fa520df55ce63255e95cb5ad436d
workflow-type: tm+mt
source-wordcount: '2299'
ht-degree: 0%

---

# 設定Customer AI例項

Customer AI是Intelligent Services的一部分，可讓您產生自訂傾向分數，而無須擔心機器學習。

Intelligent Services將Customer AI提供為簡單易用的Adobe Sensei服務，可針對不同使用案例進行設定。 以下各節提供設定Customer AI例項的步驟。

## 設定您的執行個體 {#set-up-your-instance}

在平台UI中，選取 **[!UICONTROL 服務]** 的下一頁。 此 **[!UICONTROL 服務]** 瀏覽器隨即顯示，並顯示您自己擁有的所有可用服務。 在Customer AI的容器中，選取 **[!UICONTROL 開啟]**.

![](../images/user-guide/navigate-to-service.png)

此 **Customer AI** UI隨即顯示，並顯示您的所有服務執行個體。

- 您可以找到 **[!UICONTROL 計分的設定檔總數]** 位於 **[!UICONTROL 建立例項]** 容器。 此量度會追蹤Customer AI在目前日曆年度中得分的設定檔總數，包括所有沙箱環境和任何已刪除的服務例項。

![](../images/user-guide/total-profiles.png)

使用UI右側的控制項，即可編輯、複製及刪除服務例項。 若要顯示這些控制項，請從現有的 **[!UICONTROL 服務實例]**. 控制項包含下列項目：

- **[!UICONTROL 編輯]**:選取 **[!UICONTROL 編輯]** 可讓您修改現有的服務執行個體。 您可以編輯例項的名稱、說明和計分頻率。
- **[!UICONTROL 原地複製]**:選取 **[!UICONTROL 原地複製]** 複製當前選擇的服務實例設定。 接著，您可以修改工作流程進行微幅調整，並重新命名為新例項。
- **[!UICONTROL 刪除]**:您可以刪除服務例項，包括任何歷史執行。
- **[!UICONTROL 資料來源]**:此例項所使用資料集的連結。 如果使用多個資料集，選取超連結文字會開啟資料集預覽彈出視窗。
- **[!UICONTROL 上次運行詳細資訊]**:唯有執行失敗時，才會顯示此選項。 此處顯示了執行失敗的原因，例如錯誤代碼。
- **[!UICONTROL 分數定義]**:快速概述您為此執行個體設定的目標。

![](../images/user-guide/service-instance-panel.png)

若要建立新例項，請選取 **[!UICONTROL 建立例項]**.

![](../images/user-guide/dashboard.png)

## 設定

執行個體建立工作流程隨即顯示，從 **[!UICONTROL 設定]** 步驟。

以下是您必須為執行個體提供之值的重要資訊：

- **[!UICONTROL 名稱]:** 在顯示Customer AI分數的所有位置中，都會使用例項的名稱。 因此，名稱應該描述預測分數的代表。 例如「取消雜誌訂閱的可能性」。

- **[!UICONTROL 說明]:** 說明您要預測的內容。

- **[!UICONTROL 傾向類型]:** 傾向類型決定分數和量度極性的目的。 您可以選擇 **[!UICONTROL 流失率]** 或 **[!UICONTROL 轉換]**. 請參閱 [計分摘要](./discover-insights.md#scoring-summary) 深入了解傾向類型對您執行個體有何影響的詳細資訊。

![設定畫面](../images/user-guide/create-instance.png)

提供所需值，然後選取 **[!UICONTROL 下一個]** 繼續。

## 選擇資料 {#select-data}

Customer AI根據設計使用Adobe Analytics、Adobe Audience Manager、體驗事件和消費者體驗事件資料來計算傾向分數。 選取資料集時，僅會列出與Customer AI相容的資料集。 若要選取資料集，請選取&#x200B;**+**)資料集名稱旁的符號，或選取核取方塊以一次新增多個資料集。 使用搜尋選項快速找到您感興趣的資料集。

![選取和搜尋資料集](../images/user-guide/configure-dataset-page.png)

選取您要使用的資料集後，請選取 **[!UICONTROL 新增]** 按鈕，將資料集新增至資料集預覽窗格。

![選取資料集](../images/user-guide/select-datasets.png)

選取資訊圖示 ![資訊圖示](../images/user-guide/info-icon.png) 資料集旁邊會開啟資料集預覽視窗。

![選取和搜尋資料集](../images/user-guide/dataset-info.png)

資料集預覽包含上次更新時間、來源結構，以及前10欄的預覽等資料。

### 資料集完整性 {#dataset-completeness}

資料集預覽中有資料集完整性百分比值。 此值提供資料集中有多少欄為空/空的快速快照。 如果資料集包含許多遺失值，而這些值被擷取到其他位置，強烈建議您加入包含遺失值的資料集。 在此範例中，人員ID為空，但人員ID會擷取至可包含的個別資料集中。

>[!NOTE]
>
>使用Customer AI（一年）的最大培訓期間，即可計算資料集完整性。 這表示顯示資料集完整性值時，不會考慮超過一年的資料。

![資料集完整性](../images/user-guide/dataset-info-2.png)

### 選取身分 {#identity}

若要讓多個資料集彼此連結，您必須選取身分類型（也稱為「身分命名空間」），以及該命名空間中的身分值。 如果您已在相同命名空間下將多個欄位指派為架構中的身分，所有指派的身分值都會出現在以命名空間為前置的身分下拉式清單中，例如 `EMAIL (personalEmail.address)` 或 `EMAIL (workEmail.address)`.

>[!IMPORTANT]
>
>您選取的每個資料集都必須使用相同的身分類型（命名空間）。 身分欄中的身分類型旁會出現綠色勾號，指出資料集相容。 例如，使用Phone命名空間時，以及 `mobilePhone.number` 做為識別碼，其餘資料集的所有識別碼都必須包含並使用Phone命名空間。

要選擇標識，請選擇位於標識列中的帶下划線的值。 此時會顯示「選取身分彈出視窗」。

![選擇相同的命名空間](../images/user-guide/identity-type.png)

如果命名空間中有多個身分可用，請務必為您的使用案例選取正確的身分欄位。 例如，電子郵件命名空間中提供兩個電子郵件身分識別：一個工作電子郵件，另一個是個人電子郵件。 根據使用案例，個人電子郵件更可能填入，且在個別預測中更有用。 這表示 `EMAIL (personalEmail.address)` 會被選為身分。

![未選擇資料集密鑰](../images/user-guide/select-identity.png)

>[!NOTE]
>
> 如果資料集沒有有效的身分類型（命名空間），您必須設定主要身分識別，並使用 [結構編輯器](../../../xdm/schema/composition.md#identity). 若要進一步了解命名空間和身分識別，請造訪 [身分識別服務命名空間](../../../identity-service/namespaces.md) 檔案。

## 定義目標 {#define-a-goal}

<!-- https://www.adobe.com/go/cai-define-a-goal -->

此 **[!UICONTROL 定義目標]** 步驟隨即顯示，提供互動式環境，供您以視覺化方式定義預測目標。 目標由一或多個事件組成，其中每個事件的發生取決於其保留的條件。 Customer AI例項的目標是決定在指定時間範圍內達成其目標的可能性。

若要建立目標，請選取 **[!UICONTROL 輸入欄位名稱]** 後接下拉式清單中的欄位。 選取第二個輸入、事件條件的子句，然後選擇性地提供目標值以完成事件。 您可以選取 **[!UICONTROL 新增事件]**. 最後，應用預測時間範圍以天數完成目標，然後選擇 **[!UICONTROL 下一個]**.

![](../images/user-guide/define-a-goal.png)

### 將發生且不會發生

定義目標時，您有選取的選項 **[!UICONTROL 將會發生]** 或 **[!UICONTROL 不會發生]**. 選取 **[!UICONTROL 將會發生]** 表示您定義的事件條件必須符合，才能將客戶的事件資料納入前瞻分析UI中。

例如，如果您想要設定應用程式以預測客戶是否要進行購買，您可以選取 **[!UICONTROL 將會發生]** 後跟 **[!UICONTROL 全部]** 然後輸入 **commerce.purchases.id** （或類似欄位）和 **[!UICONTROL 存在]** 作為運算子。

![將發生](../images/user-guide/occur.png)

不過，在某些情況下，您可能會想要預測某個事件是否會在特定時間範圍內發生。 若要使用此選項設定目標，請選取 **[!UICONTROL 不會發生]** 從頂層下拉式清單中。

例如，如果您想要預測哪些客戶的參與度會降低，則不要在下個月造訪您的帳戶登入頁面。 選擇 **[!UICONTROL 不會發生]** 後跟 **[!UICONTROL 全部]** 然後輸入 **web.webInteraction.URL** （或類似欄位）和 **[!UICONTROL 等於]** 作為運算元，搭配 **account-login** 作為值。

![不會發生](../images/user-guide/not-occur.png)

### 所有及任何

在某些情況下，您可能想要預測事件的組合是否會發生，而在其他情況下，您可能想要預測來自預先定義之集的任何事件的發生。 若要預測客戶是否會有事件組合，請選取 **[!UICONTROL 全部]** 選項(位於 **[!UICONTROL 定義目標]** 頁面。

例如，您可能想要預測客戶是否購買特定產品。 此預測目標由兩個條件定義：a `commerce.order.purchaseID` **存在** 和 `productListItems.SKU` **等於** 某些特定值。

![所有範例](../images/user-guide/all-of.png)

為了預測客戶是否會有來自指定集的任何事件，您可以使用 **[!UICONTROL 任何]** 選項。

例如，您可能想要預測客戶是否造訪特定URL或具有特定名稱的網頁。 此預測目標由兩個條件定義： `web.webPageDetails.URL` **開頭為** 特定值與 `web.webPageDetails.name` **開頭為** 特定值。

![任何範例](../images/user-guide/any-of.png)

### 合格人口 *（可選）*

依預設，除非指定合格母體，否則會為所有設定檔產生傾向分數。 您可以定義條件，根據事件包含或排除設定檔，以指定符合條件的母體。

![合格人口](../images/user-guide/eligible-population.png)

### 自訂事件(*可選*) {#custom-events}

如果您除了 [標準事件欄位](../input-output.md#standard-events) 由Customer AI用來產生傾向分數，會提供自訂事件選項。 使用此選項可讓您新增您認為有影響力的其他事件，這可能會改善模型品質，並有助於提供更精確的結果。 如果您選取的資料集包含結構中定義的自訂事件，您可以將其新增至執行個體。

![事件功能](../images/user-guide/event-feature.png)

若要新增自訂事件，請選取 **[!UICONTROL 新增自訂事件]**. 接下來，輸入自訂事件名稱，然後將其對應至您結構中的事件欄位。 查看影響因素和其他深入分析時，會顯示自訂事件名稱，取代欄位值。 這表示使用者ID、保留ID、裝置資訊和其他自訂值會以自訂事件名稱列出，而非事件的ID/值。 Customer AI會使用這些額外的自訂事件來改善模型品質，並提供更精確的結果。

![自訂事件欄位](../images/user-guide/custom-event.png)

接下來，從「可用運算子」下拉式清單中選取您要使用的運算子。 僅列出與事件相容的運算子。

![自訂事件運算子](../images/user-guide/custom-operator.png)

最後，如果選取的運算子需要一個，請輸入欄位值。 在此範例中，我們只需要查看酒店或餐廳是否存在預訂。 不過，如果想要更精確，可以使用等於運算子，並在值提示中輸入確切的值。

![自訂事件欄位值](../images/user-guide/custom-value.png)

完成後，選取 **[!UICONTROL 下一個]** 在右上角繼續。

### 自訂設定檔屬性(*可選*)

除了 [標準事件欄位](../input-output.md#standard-events) 供客戶AI用來產生傾向分數。 使用此選項可讓您新增您認為有影響的其他設定檔屬性，這可能會改善模型品質，並提供更精確的結果。 此外，新增自訂設定檔屬性可讓客戶AI更妥善地展示特定設定檔在傾向貯體中的結果。

>[!NOTE]
>
>新增自訂設定檔屬性的工作流程與新增自訂事件相同。

![新增自訂設定檔屬性](../images/user-guide/profile-attributes.png)

### 設定排程 *（可選）* {#configure-a-schedule}

此 **[!UICONTROL 進階]** 步驟。 此選用步驟可讓您設定排程以自動執行預測、定義預測排除以篩選特定事件或選取 **[!UICONTROL 完成]** 如果不需要。

通過配置 **[!UICONTROL 計分頻率]**. 可排程每週或每月執行自動預測執行。

![](../images/user-guide/schedule.png)

### 預測排除

如果您的資料集包含任何新增為測試資料的欄，您可以選取 **新增排除項目** 接著輸入您要排除的欄位。 這可防止在產生分數時評估符合特定條件的事件。 此功能可用來篩選掉無關的資料輸入或特定促銷活動。

若要排除事件，請選取 **[!UICONTROL 新增排除項目]** 和定義事件。 若要移除排除項目，請選取點(**[!UICONTROL ...]**)，然後選取「 」 **[!UICONTROL 移除容器]**.

![](../images/user-guide/exclusion.png)

### 設定檔切換

「設定檔」切換可讓Customer AI將計分結果匯出至「即時客戶設定檔」。 禁用此切換可防止將模型評分結果添加到「配置檔案」中。 停用此功能後，仍可使用Customer AI評分結果。

首次使用Customer AI時，應將此功能關閉，直到您對模型輸出結果滿意為止。 這可防止您上傳多個計分資料集至「即時客戶設定檔」，同時微調您的模型。

![設定檔切換](../images/user-guide/advanced-workflow.png)

設定計分排程、納入預測排除後，以及切換您想要其所在位置的設定檔，請選取 **[!UICONTROL 完成]** ，以建立您的Customer AI例項。

如果成功建立例項，則會立即觸發預測執行，並根據您定義的排程執行後續執行。

>[!NOTE]
>
>根據輸入資料的大小，預測執行最多可能需要24小時才能完成。

依照本節所述，您已設定Customer AI的例項並執行預測執行。 當執行成功完成時，如果設定檔切換已啟用，則分數的深入分析會自動填入預測的分數。 請等候最多24小時，再繼續進行本教學課程的下一節。

## 後續步驟 {#next-steps}

依照本教學課程，您已成功設定Customer AI例項並產生傾向分數。 您現在可以選擇使用區段產生器，以 [建立預測分數的客戶區段](./create-segment.md) 或 [透過Customer AI探索見解](./discover-insights.md).

## 其他資源

以下影片旨在協助您了解Customer AI的設定工作流程。 此外，也提供最佳實務和使用案例範例。

>[!IMPORTANT]
>
> 以下視訊已過期。 如需最新資訊，請參閱本檔案。

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
