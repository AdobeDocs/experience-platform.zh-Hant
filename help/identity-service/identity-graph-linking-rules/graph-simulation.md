---
title: 圖表模擬UI指南
description: 瞭解如何在Identity Service UI中使用圖表模擬。
exl-id: 89f0cf6e-c43f-40ec-859a-f3b73a6da8c8
source-git-commit: 28eab3488dccdcc6239b9499e875c31ff132fd48
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 3%

---

# [!DNL Graph Simulation] 使用者介面指南 {#graph-simulation}

>[!CONTEXTUALHELP]
>id="platform_identities_graphsimulation"
>title="圖表模擬"
>abstract="模擬圖表，用於了解身分識別服務如何連結身分，以及身分識別最佳化演算法如何運作。"

[!DNL Graph Simulation]是Identity Service UI中的工具，可用於模擬指定特定身分組合下身分圖表的行為方式，以及設定[身分最佳化演演算法](./identity-optimization-algorithm.md)的方式。

請觀看下列影片，瞭解在Identity Service UI工作區中使用[!DNL Graph Simulation]介面的其他資訊：

>[!VIDEO](https://video.tv.adobe.com/v/3444054/?learn=on&enablevpops&captions=chi_hant)

閱讀本檔案以瞭解如何使用[!DNL Graph Simulation]來更瞭解身分圖表行為以及圖表演演算法如何運作。

## 瞭解[!DNL Graph Simulation]介面 {#interface}

您可以在Adobe Experience Platform UI中存取[!DNL Graph Simulation]。 從左側導覽選取&#x200B;**[!UICONTROL 身分]**，然後從頂端標題選取&#x200B;**[!UICONTROL 圖表模擬]**。

![Adobe Experience Platform UI中的圖表模擬介面。](../images/graph-simulation/graph-simulation.png)

[!DNL Graph Simulation]介面可分成三個區段：

>[!BEGINTABS]

>[!TAB 活動]

事件：使用&#x200B;**[!UICONTROL 事件]**&#x200B;面板新增身分以模擬圖形。 完整身分必須具有身分名稱空間及其對應的身分值。 您必須至少新增兩個身分才能模擬圖形。 您也可以選取&#x200B;**[!UICONTROL 載入範例]**&#x200B;以輸入預先設定的事件和演演算法設定。

![圖表模擬工具的事件面板。](../images/graph-simulation/events.png)

>[!TAB 演演算法組態]

演演算法組態：使用&#x200B;**[!UICONTROL 演演算法組態]**&#x200B;面板為您的名稱空間新增並設定最佳化演演算法。 您可以拖放名稱空間來修改其各自的優先順序排名。 您也可以選取&#x200B;**[!UICONTROL 每個圖表唯一性]**&#x200B;來判斷名稱空間是否為唯一的。

![圖表模擬工具的演演算法設定。](../images/graph-simulation/algorithm-configuration.png)

>[!TAB 模擬的圖表檢視器]

模擬圖形檢視器：模擬圖形檢視器會根據您新增的事件和您設定的演演算法顯示產生的圖形。 兩個身分之間的直線表示已建立連結。 虛線表示連結已移除。

![模擬圖形檢視器面板，包含模擬圖形的範例。](../images/graph-simulation/simulated-graph.png)

>[!ENDTABS]

## 新增事件 {#add-events}

若要開始，請選取&#x200B;**[!UICONTROL 新增事件]**。

![已選取[新增事件]按鈕。](../images/graph-simulation/add-events.png)

[!UICONTROL 事件#1]的快顯視窗會出現。 從這裡，輸入您的身分名稱空間和身分值組合。 您可以使用下拉式選單來選取身分名稱空間。 或者，您可以輸入名稱空間的前幾個字母，然後選取下拉式選單中提供的選項。 選取名稱空間後，請提供與名稱空間對應的身分值。

![具有空白介面的Event #1視窗。](../images/graph-simulation/event-one.png)

>[!TIP]
>
>您在[!DNL Graph Simulation]練習期間輸入的身分值不必是真正的身分值，而且可以是簡單的預留位置。

完成第一個身分識別之後，請選取新增圖示(**`+`**)以新增第二個身分識別。

![ {Email： tom@acme.com}的第一個完整身分識別是在圖表模擬的事件面板中輸入。](../images/graph-simulation/event-one-added.png)

接下來，重複相同的步驟並新增第二個身分。 需要兩個完全合格的身分才能產生身分圖表。 在下列範例中，ECID會新增為名稱空間，且會提供`111`的值。 完成後，選取&#x200B;**[!UICONTROL 儲存]**。

![ {ECID： 111}的第二個身分已新增至事件#1。](../images/graph-simulation/first-event.png)

[!UICONTROL Events]介面會更新以顯示您的第一個事件，在此案例中為： `{Email: tom@acme.com, ECID: 111}`。

![更新的事件介麵包含{Email： tom@acme.com，ECID： 111}。](../images/graph-simulation/add-second-event.png)

接下來，重複相同的步驟以新增第二個事件。 對於事件#2，新增`{Email: summer@acme.com}`作為您的第一個身分，然後新增相同的`{ECID: 111}`作為第二個身分，因此建立第二個事件： `{Email: summer@acme.com}, {ECID: 111}`。 完成後，您應該有兩個事件，一個用於`{Email: tom@acme.com, ECID: 111}`，另一個用於`{Email: summer@acme.com}, {ECID: 111}`。

![更新的事件介麵包含兩個事件。](../images/graph-simulation/two-events.png)

### 載入範例 {#load-example}

選取&#x200B;**[!UICONTROL 載入範例]**&#x200B;以使用預先設定的演演算法和事件組態設定範例圖形。

![已選取載入範例選項。](../images/graph-simulation/load-example.png)

此時會出現一個快顯視窗，提供您可用的圖表情境，供您選擇：

| 範例圖表 | 說明 | 範例 |
| --- | --- | --- |
| 共用裝置 | 共用裝置是指兩個不同使用者登入同一部裝置的情境。 | 夫妻共用一個iPad進行網際網路瀏覽和電子商務。 |
| 無效 (非唯一) 電話 | 無效或非唯一電話是指兩個不同使用者使用相同電話號碼建立帳戶的情況。 | 母親和女兒使用他們共用的家庭電話號碼註冊任何電子商務帳戶。 |
| 「不良」身分識別值 | 「不良」身分值是指身分服務因錯誤實作而產生非唯一IDFA的情況。 | 由於程式碼實作問題，WebSDK會針對每個事件錯誤傳送`user_null`值。 |

![顯示可用預先設定範例的視窗：共用裝置、無效的電話和錯誤的身分值。](../images/graph-simulation/example-options.png)

選取任何選項，以使用預先設定的事件和演演算法載入[!DNL Graph Simulation]。 您仍然可以對任何預先載入的圖表案例範例進行進一步的設定。

![為無效電話設定的事件和演演算法。](../images/graph-simulation/example-loaded.png)

完成後，選取&#x200B;**[!UICONTROL 模擬]**。

![針對無效電話模擬的範例圖表。](../images/graph-simulation/example-simulated.png)

### 使用文字版本 {#use-text-version}

您也可以使用文字模式來設定事件。 若要使用文字模式，請選取設定圖示，然後選取&#x200B;**[!UICONTROL 文字（進階使用者）]**。

![選取的設定圖示。](../images/graph-simulation/settings.png)

您可以使用文字模式手動輸入身分。 請使用冒號(`:`)來區別與您輸入的名稱空間對應的身分值，然後使用逗號(`,`)來分隔您的身分。 若要區分不同的事件，請為每個事件使用新行。

![使用文字模式版本的事件面板。](../images/graph-simulation/text-version.png)

### 編輯事件 {#edit-event}

若要編輯事件，請選取指定事件旁的省略符號(`...`)，然後選取&#x200B;**[!UICONTROL 編輯]**。

![已選取編輯事件圖示。](../images/graph-simulation/edit.png)

### 刪除事件 {#delete-event}

若要刪除事件，請選取指定事件旁的省略符號(`...`)，然後選取&#x200B;**[!UICONTROL 刪除]**。

![已選取刪除事件圖示。](../images/graph-simulation/delete.png)

## 設定演算法 {#configure-algorithm}

>[!IMPORTANT]
>
>您設定的演演算法會指示Identity Service如何處理您在事件中輸入的名稱空間。 您在[!DNL Graph Simulation UI]中組合的任何設定都不會儲存在身分設定中。

新增事件後，您現在可以設定將用來模擬圖表的演演算法。 若要開始，請選取&#x200B;**[!UICONTROL 新增設定]**。

![演演算法設定面板。](../images/graph-simulation/add-config.png)

空白的設定列隨即顯示。 首先，輸入您用於事件的相同名稱空間。 在此情況下，請先輸入電子郵件。 輸入名稱空間後，[!UICONTROL 身分符號]和[!UICONTROL 身分型別]的資料行會自動填入。

![第一個組態專案。](../images/graph-simulation/add-namespace.png)

接下來，重複相同的步驟，並新增第二個名稱空間（在此例中為ECID）。 輸入完所有名稱空間後，您就可以開始設定其優先順序和唯一性。

* **名稱空間優先順序**：名稱空間的優先順序決定它與指定身分圖表中的其他名稱空間相比的相對重要性。 例如，如果您的身分圖表有四個不同的名稱空間：CRMID、ECID、Email和Apple IDFA，您可以設定優先順序來判斷四個名稱空間的重要性順序。
* **唯一的名稱空間**：如果名稱空間被指定為唯一，則身分服務將會產生圖形，並警告只能有一個具有指定唯一名稱空間的身分。 例如，如果電子郵件名稱空間指定為唯一的名稱空間，則圖表只能有一個包含電子郵件的身分。 如果電子郵件名稱空間中有多個身分，則會移除最舊的連結。

若要設定名稱空間優先順序，請選取名稱空間列，並將其拖曳到您想要的優先順序順序，頂端列代表較高的優先順序，底部列代表較低的優先順序。 若要將名稱空間指定為唯一，請選取&#x200B;**[!UICONTROL 每個圖表唯一性]**&#x200B;核取方塊。

完成後，選取&#x200B;**[!UICONTROL 模擬]**。

![已設定所有名稱空間。](../images/graph-simulation/all-namespaces.png)

## 檢視模擬圖形

[!UICONTROL 模擬圖形]區段會顯示根據您新增的事件和您設定的演演算法所產生的身分圖形。

| 圖表圖示 | 說明 |
| --- | --- |
| 實線 | 實線表示兩個身分之間的已建立連結。 |
| 虛線 | 虛線代表兩個身分之間的已移除連結。 |
| 線上號碼 | 某一行上的數字代表產生該指定連結時的時間戳記。 最低數字(1)代表最早建立的連結。 |

在下列範例圖表中，`{Email: tom@acme.com}`和`{ECID: 111}`之間有虛線，原因如下：

* 在演演算法設定步驟中，電子郵件被指定為唯一。 因此，圖形中可能只有一個具有電子郵件名稱空間的身分。
* `{Email: tom@acme.com}`與`{ECID: 111}`之間的連結是第一個建立的身分識別(事件#1)。 這是最舊的連結，因此會被移除。

![模擬圖形檢視器面板，包含模擬圖形的範例。](../images/graph-simulation/simulated-graph.png)

## 後續步驟

閱讀本檔案後，您現在已瞭解如何使用[!DNL Graph Simulation]工具，以更清楚瞭解在指定一組特定規則和設定時，身分資料的處理方式。 如需詳細資訊，請閱讀下列檔案：

* [[!DNL Identity Graph Linking Rules] 概觀](./overview.md)
* [身分識別最佳化演算法](./identity-optimization-algorithm.md)
* [實作指南](./implementation-guide.md)
* [疑難排解和常見問答( FAQ)](./troubleshooting.md)
* [圖表設定範例](./example-configurations.md)
* [命名空間優先順序](./namespace-priority.md)
* [身分設定UI](./identity-settings-ui.md)
