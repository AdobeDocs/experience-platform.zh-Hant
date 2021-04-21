---
keywords: Experience Platform；使用手冊；客戶ai；熱門主題；配置實例；建立實例；
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 設定客戶AI例項
topic-legacy: Instance creation
description: 智慧型服務提供客戶人工智慧，以簡單易用的Adobe Sensei服務形式提供，可針對不同使用案例進行設定。 以下各節提供設定客戶AI例項的步驟。
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 0%

---

# 設定客戶AI例項

客戶人工智慧(Customer AI)是智慧型服務的一部分，可讓您產生自訂傾向分數，而不必擔心機器學習。

智慧型服務提供客戶人工智慧，以簡單易用的Adobe Sensei服務形式提供，可針對不同使用案例進行設定。 以下各節提供設定客戶AI例項的步驟。

## 設定您的例項{#set-up-your-instance}

在平台UI中，選擇左側導覽中的&#x200B;**[!UICONTROL Services]**。 出現&#x200B;**[!UICONTROL Services]**&#x200B;瀏覽器，並顯示您可使用的所有可用服務。 在客戶AI的容器中，選擇&#x200B;**[!UICONTROL Open]**。

![](../images/user-guide/navigate-to-service.png)

出現&#x200B;**Customer AI** UI，並顯示您的所有服務實例。

- 您可以在&#x200B;**[!UICONTROL Create instance]**&#x200B;容器的右下側找到&#x200B;**[!UICONTROL Total profiles scored]**&#x200B;量度。 此量度會追蹤客戶AI在目前日曆年度（包括所有沙盒環境和任何已刪除的服務例項）計分的設定檔總數。

![](../images/user-guide/total-profiles.png)

使用UI右側的控制項，即可編輯、複製和刪除服務例項。 若要顯示這些控制項，請從您現有的&#x200B;**[!UICONTROL Service instances]**&#x200B;中選取例項。 控制項包含下列項目：

- **[!UICONTROL Edit]**:選擇 **[!UICONTROL Edit]** 允許修改現有服務實例。您可以編輯實例的名稱、說明和計分頻率。
- **[!UICONTROL Clone]**:選擇 **[!UICONTROL Clone]** 將複製當前選定的服務實例設定。然後，您可以修改工作流程，進行微調，並將其重新命名為新例項。
- **[!UICONTROL Delete]**:您可以刪除包含任何歷史執行的服務例項。
- **[!UICONTROL Data source]**:此例項所使用之資料集的連結。
- **[!UICONTROL Last run details]**:只有當執行失敗時，才會顯示此項。此處會顯示執行失敗原因的資訊，例如錯誤代碼。
- **[!UICONTROL Score definition]**:快速概述您為此例項設定的目標。

![](../images/user-guide/service-instance-panel.png)

要建立新實例，請選擇&#x200B;**[!UICONTROL Create instance]**。

![](../images/user-guide/dashboard.png)

將出現實例建立工作流，從&#x200B;**[!UICONTROL Setup]**&#x200B;步驟開始。

以下是您必須為實例提供的值的重要資訊：

- 在顯示客戶AI分數的所有位置都會使用實例的名稱。 因此，名稱應該描述預測分數代表什麼，例如「取消雜誌訂閱的可能性」。

- 傾向類型會決定分數和量度極性的意圖。 您可以選擇&#x200B;**[!UICONTROL Churn]**&#x200B;或&#x200B;**[!UICONTROL Conversion]**。 如需傾向類型如何影響您的例項的詳細資訊，請參閱發現深入解析檔案中[計分摘要](./discover-insights.md#scoring-summary)下的附註。

- 資料來源是資料所在位置。 資料集是用來預測分數的輸入資料集。 根據設計，客戶AI會使用消費者體驗事件、Adobe Analytics和Adobe Audience Manager資料來計算傾向分數。 從下拉式選取器選取資料集時，只會列出與客戶AI相容的資料集。

- 依預設，會為所有描述檔產生傾向分數，除非指定合格人口。 您可以定義條件，根據事件加入或排除描述檔，以指定合格人口。

提供所需值，然後選擇&#x200B;**[!UICONTROL Next]**。

![](../images/user-guide/setup.png)

### 定義目標{#define-a-goal}

出現&#x200B;**[!UICONTROL Define goal]**&#x200B;步驟，它提供互動環境供您以視覺化方式定義預測目標。 目標由一個或多個事件組成，每個事件的發生基於事件所保持的條件。 客戶AI實例的目標是確定在給定時間範圍內實現其目標的可能性。

要建立目標，請選擇&#x200B;**[!UICONTROL Enter Field Name]**&#x200B;並從下拉清單中選擇一個欄位。 選擇第二個輸入並為事件條件選擇一個子句，然後提供目標值以完成事件。 您可以選擇&#x200B;**[!UICONTROL Add event]**&#x200B;來設定其他事件。 最後，套用以天數為單位的預測時間範圍，完成目標，然後選取&#x200B;**[!UICONTROL Next]**。

![](../images/user-guide/goal.png)

#### 將發生且不會發生

定義目標時，您可以選擇&#x200B;**[!UICONTROL Will occur]**&#x200B;或&#x200B;**[!UICONTROL Will not occur]**。 選擇&#x200B;**[!UICONTROL Will occur]**&#x200B;表示您定義的事件條件必須符合，才能將客戶的事件資料納入前瞻分析UI。

例如，如果您想要設定應用程式來預測客戶是否要進行購買，您可以選取&#x200B;**[!UICONTROL Will occur]**&#x200B;後接&#x200B;**[!UICONTROL All of]**，然後輸入&#x200B;**commerce.purchases.id**&#x200B;和&#x200B;**exists**&#x200B;作為運算元。

![將會發生](../images/user-guide/occur.png)

不過，您可能有興趣預測某個事件是否會在特定時間範圍內發生。 若要使用此選項設定目標，請從頂層下拉式清單中選取&#x200B;**[!UICONTROL Will not occur]**。

例如，如果您想預測哪些客戶的參與度降低，且不要在下個月造訪您的帳戶登入頁面。 選擇&#x200B;**[!UICONTROL Will not occur]**&#x200B;後跟&#x200B;**[!UICONTROL All of]**，然後輸入&#x200B;**web.webInteraction.URL**&#x200B;和&#x200B;**[!UICONTROL equals]**&#x200B;作為運算子，並輸入&#x200B;**account-login**&#x200B;作為值。

![不會發生](../images/user-guide/not-occur.png)

#### 所有及任何

在某些情況下，您可能想要預測事件組合是否會發生，而在其他情況下，您可能想預測來自預先定義集合的任何事件的發生。 為了預測客戶是否將擁有事件組合，請從&#x200B;**[!UICONTROL Define Goal]**&#x200B;頁面的第二層下拉式清單中選擇&#x200B;**[!UICONTROL All of]**&#x200B;選項。

例如，您可能想要預測客戶是否購買特定產品。 此預測目標由兩個條件定義：a `commerce.order.purchaseID` **exists**&#x200B;和`productListItems.SKU` **等於**&#x200B;某些特定值。

![所有範例](../images/user-guide/all-of.png)

為了預測客戶是否將擁有給定集合中的任何事件，可以使用&#x200B;**[!UICONTROL Any of]**&#x200B;選項。

例如，您可能想要預測客戶是否瀏覽特定URL或具有特定名稱的網頁。 此預測目標由兩個條件定義：`web.webPageDetails.URL` **開頭為**&#x200B;特定值，`web.webPageDetails.name` **開頭為**&#x200B;特定值。

![任何範例](../images/user-guide/any-of.png)

### 配置計畫&#x200B;*（可選）* {#configure-a-schedule}

出現&#x200B;**[!UICONTROL Advanced]**&#x200B;步驟。 此可選步驟可讓您設定排程以自動執行預測、定義預測排除以篩選特定事件，或選取&#x200B;**[!UICONTROL Finish]**（如果不需要）。

通過配置&#x200B;**[!UICONTROL Scoring Frequency]**&#x200B;設定計分計畫。 自動預測執行可排程每週或每月執行。

![](../images/user-guide/schedule.png)

在排程設定下方，您可以定義預測排除，以防止在產生分數時評估符合特定條件的事件。 此功能可用來篩選不相關的資料輸入。

若要排除某些事件，請選取&#x200B;**[!UICONTROL Add exclusion]**，並以定義目標的方式定義事件。 若要移除排除，請選取事件容器右上角的省略號(**[!UICONTROL ...]**)，然後選取&#x200B;**[!UICONTROL Remove Container]**。

![](../images/user-guide/exclusion.png)

視需要排除事件，然後選取&#x200B;**[!UICONTROL Finish]**&#x200B;以建立例項。

![](../images/user-guide/advanced.png)

如果成功建立例項，則會立即觸發預測執行，並根據您定義的排程執行後續執行。

>[!NOTE]
>
>根據輸入資料的大小，預測執行最多需要24小時才能完成。

依照本節內容，您已設定客戶AI的例項，並執行預測執行。 在執行成功完成後，計分見解會自動填入預測分數的個人檔案。 請等候最多24小時，再繼續本教學課程的下一節。

## 下一步 {#next-steps}

透過本教學課程，您已成功設定客戶AI的例項並產生傾向分數。 您現在可以選擇使用「區段產生器」，以[建立預測分數](./create-segment.md)或[的客戶區段，並透過「客戶AI」(a3/)探索見解。](./discover-insights.md)

## 其他資源

以下視訊旨在協助您瞭解客戶AI的設定工作流程。 此外，還提供最佳實務和使用案例範例。

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
