---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform
title: 設定客戶AI例項
topic: Instance creation
translation-type: tm+mt
source-git-commit: f7c59ef097c00073fbf9f6522b6e70ed24cc8bf1

---


# 設定客戶AI例項

客戶人工智慧(Customer AI)是智慧型服務的一部分，可讓您產生自訂傾向分數，而不必擔心機器學習。

智慧型服務提供客戶人工智慧，提供簡單易用的Adobe Sensei服務，可針對不同使用案例進行設定。 以下各節提供設定客戶AI例項的步驟。

## 設定您的例項 {#set-up-your-instance}

在「平台UI」中，按一下 **[!UICONTROL Services]** 左側導覽中的。 瀏覽 **[!UICONTROL Services]** 器隨即出現，並顯示您可使用的所有服務。 在「客戶AI」的容器中，按一下 **[!UICONTROL Open]**。

![](../images/user-guide/navigate-to-service.png)

「客 *戶AI* 」畫面會顯示所有現有的客戶AI例項。 按一下「**[!UICONTROL Create instance]**」。

![](../images/user-guide/dashboard.png)

此時將顯示實例建立工作流，從「設定」( *Setup* )步驟開始。

以下是您必須為實例提供的值的重要資訊：

* 在顯示客戶AI分數的所有位置都會使用實例的名稱。 因此，名稱應該描述預測分數代表什麼，例如「取消雜誌訂閱的可能性」。

* 傾向類型會決定分數和量度極性的意圖。 您可以選擇 **[!UICONTROL Churn]** 或 **[!UICONTROL Conversion]**。 如需傾向類型如何影 [響您的例項的詳細資訊](./discover-insights.md#scoring-summary) ，請參閱發現見解檔案中得分摘要下方的附註。

* 資料來源是資料所在位置。 資料集是用來預測分數的輸入資料集。 根據設計，客戶人工智慧會使用消費者體驗事件資料來計算傾向分數。 從下拉式選取器選取資料集時，只會列出與客戶AI相容的資料集。

* 依預設，會為所有描述檔產生傾向分數，除非指定合格人口。 您可以定義條件，根據事件加入或排除描述檔，以指定合格人口。

提供所需值，然後按一下 **[!UICONTROL Next]**。

![](../images/user-guide/setup.png)

### 定義目標 {#define-a-goal}

「定 *義目標* 」(Define goal)步驟隨即出現，它提供互動式環境供您以視覺化方式定義目標。 目標由一個或多個事件組成，每個事件的發生基於事件所保持的條件。 客戶AI實例的目標是確定在給定時間範圍內實現其目標的可能性。

按一 **[!UICONTROL Enter Field Name]** 下並從下拉式清單中選取欄位。 按一下第二個輸入，並為事件條件選擇一個子句，然後提供目標值以完成事件。 按一下即可設定其他事件 **[!UICONTROL Add event]**。 最後，套用預測時間範圍（天數），然後按一下，以完成目標 **[!UICONTROL Next]**。

![](../images/user-guide/goal.png)

### 設定排程 *（選用）*{#configure-a-schedule}

將出 *現高級* 步驟。 此可選步驟可讓您設定排程以自動執行預測、定義預測排除以篩選特定事件，或在不需要時 **[!UICONTROL Finish]** 按一下。

設定計分頻率，以設定計 *分排程*。 自動預測執行可排程每週或每月執行。

![](../images/user-guide/schedule.png)

在排程設定下方，您可以定義預測排除，以防止在產生分數時評估符合特定條件的事件。 此功能可用來篩選不相關的資料輸入。

若要排除某些事件，請按 **[!UICONTROL Add exclusion]** 一下並定義事件，其方式與定義目標的方式相同。 若要移除排除，請按一下事件容器&#x200B;**[!UICONTROL ...]**&#x200B;右上方的省略號()，然後按一下 **[!UICONTROL Remove Container]**。

![](../images/user-guide/exclusion.png)

視需要排除事件，然後按一 **[!UICONTROL Finish]** 下以建立例項。

![](../images/user-guide/advanced.png)

如果成功建立例項，則會立即觸發預測執行，並根據您定義的排程執行後續執行。

>[!NOTE] 根據輸入資料的大小，預測執行最多需要24小時才能完成。

依照本節內容，您已設定客戶AI的例項，並執行預測執行。 在執行成功完成後，計分見解會自動填入預測分數的個人檔案。 請等候最多24小時，再繼續本教學課程的下一節。

## 下一步 {#next-steps}

透過本教學課程，您已成功設定客戶AI的例項並產生傾向分數。 您現在可以選擇使用「區段產生器」來建立具 [有預測分數的客戶區段](./create-segment.md) ，或 [透過客戶人工智慧發掘見解](./discover-insights.md)。

