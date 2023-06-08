---
solution: Experience Platform
title: 教戰手冊UI指南
description: 瞭解如何使用Experience PlatformUI來檢視和啟用教戰手冊。
badgeBeta: label="Beta" type="Informative"
source-git-commit: 63ea852ca9f9a45d1c071fd1033cbd44cbb427c6
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 1%

---


# （測試版）如何啟用和重複使用教戰手冊

>[!AVAILABILITY]
>
>此功能目前為測試版，並未開放所有使用者使用。 文件和功能可能會有所變更。

若要使用教戰手冊，請導覽至 **[!UICONTROL 使用案例教戰手冊] > [!UICONTROL 教戰手冊]**. 瀏覽並使用頁面上的各種搜尋和篩選選項，以選取並開始使用特定教戰手冊。

## 搜尋和篩選 {#search-and-filter}

使用頁面上可用的搜尋視窗和篩選器，為您的使用案例尋找合適的劇本。

例如，您可以根據行銷漏斗中您要鎖定的階段（轉換、參與或保留），篩選可以使用的教戰手冊。 您也可以依您所在的產業或您可存取的產品權益(Adobe Journey Optimizer或Real-time CDP)來篩選顯示的教戰手冊。

![依行銷漏斗、產業或產品篩選教戰手冊](/help/use-case-playbooks/assets/playbooks/ui-guide/filter-by-funnel-industry-product.gif)

您也可以使用搜尋功能來尋找適合您的行動手冊。 請參閱下面的範例，瞭解如何尋找可幫助您與可能已放棄購物車的使用者互動的行動手冊。

![與可能已放棄購物車的使用者互動。](/help/use-case-playbooks/assets/playbooks/ui-guide/engage-abandoned-cart.gif)

或者，您可以按照您計畫用來聯絡客戶的管道，篩選可用的教戰手冊，如下所示：

![依管道篩選](/help/use-case-playbooks/assets/playbooks/ui-guide/channel-select-filter.gif)

嘗試使用篩選器和搜尋選項，找出適合您的劇本。

## 檢視教戰手冊並產生資產 {#view-playbook-generate-assets}

在您決定使用教戰手冊並建立其例項之前，您應該先檢查教戰手冊以確定其符合您的需求。 為協助您更清楚瞭解其涵蓋的使用案例，所有教戰手冊皆包含下列章節。 當您準備好繼續並產生資產時，請選取 **[!UICONTROL 建立執行個體]**.

### 思維導圖 {#mindmap}

使用教戰手冊中的心智圖區段來了解教戰手冊可協助您解決的工作流程步驟。 從使用案例中鎖定的角色的角度來看，以視覺效果呈現所有產生物件如何協助您達成使用案例的流程。

心智圖從定義使用者歷程中可觸及的人開始，並在每個步驟描述透過Adobe傳遞某些內容（例如新訊息或提醒），或是目標角色所做的事物觸發了下一個訊息或事件。

![強調行動手冊思維導圖。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-mindmap.png)


### 摘要 {#summary}

Inspect的「摘要」區段，以瞭解當您從Playbook建立例項後會產生哪些資產。 為每個教戰手冊產生的資產會根據教戰手冊啟用的使用案例量身打造。 取得以下摘要區段中所有專案的詳細資訊。

| 項目 | 說明 |
---------|----------|
| **[!UICONTROL 目標對象]** | 說明您透過此使用案例行動手冊希望觸及的角色。 |
| **[!UICONTROL 行銷頻道]** | 說明用於觸及教戰手冊中鎖定之角色的管道。 |
| **[!UICONTROL 技術資產]** | 建立行動手冊例項後產生的技術資產清單。 產生的資產會因教戰手冊而異，視使用案例而定。 有些教戰手冊可能會產生結構描述、區段和歷程。 其他人可能會產生目的地。 請參閱 [瞭解產生的資產](#understand-assets) 區段，以取得有關如何使用和重複使用產生的資產的詳細資訊。 |

{style="table-layout:auto"}

![強調的行動手冊摘要](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-summary.png)

### 實例 {#instances}

向下捲動至例項區段，以取得您或您的團隊成員已建立的本Playbook例項概觀。 您可以使用各種控制項來排序和篩選顯示的例證，例如只檢視您建立的例證。 您也可以看到有關每個執行個體的各種資訊，如下所列。

| 項目 | 說明 |
|---------|----------|
| **[!UICONTROL 名稱]** | 根據教戰手冊的執行個體名稱。 您可以自訂執行個體的名稱和描述。 閱讀以下章節： [如何編輯執行個體中繼資料](#edit-instance-metadata) 以取得詳細資訊。 |
| **[!UICONTROL 狀態]** | 指示執行個體的狀態。 A **[!UICONTROL 已提交]** 執行個體已可供使用。 |
| **[!UICONTROL 已建立]** | 表示執行個體的建立時間。 |
| **[!UICONTROL 建立者]** | 指出建立執行個體的使用者。 |
| **[!UICONTROL 上次修改日期]** | 表示上次修改執行個體的時間。 |

{style="table-layout:auto"}

![反白顯示Playbook執行個體。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-instances.png)

## 啟用教戰手冊 {#enable-playbook}

當您準備好繼續使用教戰手冊並建立例項時，請選取「 」 **[!UICONTROL 建立執行個體]** 以繼續使用教戰手冊並產生技術資產。

![建立教戰手冊的執行個體。](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

此動作會產生數個資產，供您用於達成教戰手冊所述的使用案例。

![啟用後所產生資產的Playbook檢視。](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### 使用組態控制項來編輯執行處理名稱和說明 {#edit-instance-metadata}

根據教戰手冊建立執行個體後，您可以對其進行個人化，以將其與從相同教戰手冊建立的其他執行個體區分開來。 選取設定控制項，如下所示。 編輯名稱、說明和附註，然後選取 **[!UICONTROL 儲存]** 完成時。

![編輯執行個體的名稱和描述。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### 瞭解產生的資產 {#understand-assets}

>[!IMPORTANT]
>
>無需擔心！ 這是安全的實驗空間，您無法破壞任何內容。 目前還沒有與您建立的任何資產相關聯的資料。 您必須先內嵌資料，才能達成使用案例。

請務必瞭解，產生的資產會因您啟用的使用案例而異：

* 不同型別的教戰手冊會產生不同的資產。 這些資產是專為透過行動手冊達成的使用案例而建立。 例如，行動手冊會產生結構、區段、歷程和訊息。 另一個行動手冊產生要為其啟用資料的結構描述、區段和目的地。
* 資產本身因教戰手冊而異。 例如，對於 **[!UICONTROL 傳送生日訊息給來賓]** playbook，建立的對象擁有規則 `birthday=today AND year=any`.

舉例來說，對於 **[!UICONTROL 捨棄的購物車：商品]** playbook，您會看到已建立特定歷程，其中包含針對此使用案例建立的訊息。

![從使用案例劇本建立的歷程。](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### 使用和編輯產生的資產 {#use-and-edit-assets}

當您探索建立行動手冊例項後產生的資產時，可以編輯任何已建立的資產。

如果您或您團隊中的某人建立另一個行動手冊例項，則會保留編輯後的資產，並為行動手冊的新例項建立新資產。

上述行為適用於所有已建立的資產，但結構描述除外。 在使用結構描述的情況下，建立行動手冊的新執行個體時不會建立新結構描述，因此您將使用來自新建立的執行個體中行動手冊另一個執行個體的已編輯結構描述。

>[!TIP]
>
>在開發沙箱中測試，並在準備就緒後移至生產環境。
>
>產生物件後，您可以新增資料，繼續於開發沙箱中測試。 只要您想在開發沙箱中測試資產，就可以在準備就緒後，在生產沙箱中複製資產邏輯（區段定義、歷程、結構描述等）。

### 重複使用教戰手冊 {#reuse-playbooks}

透過建立同一行動手冊的多個執行個體，您可以稍後實施相同的使用案例，而不需修改先前實施使用案例的詳細資訊。

### 與其他團隊成員共用行動手冊和產生的資產 {#share-playbook}

您可以與其他團隊成員共用產生的執行個體和資產。 若要這麼做，請從瀏覽器複製URL連結，然後與您的團隊共用，讓他們大致瞭解產生的資產。

![使用案例行動手冊檢視中醒目提示的URL。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## 後續步驟 {#next-steps}

閱讀本UI指南後，您現在瞭解如何解譯行動手冊的各個區段，以及如何使用在您建立行動手冊例項後產生的資產。 接下來，您可以瀏覽教戰手冊目錄，以尋找適合您使用案例的教戰手冊，並在遇到任何錯誤時閱讀疑難排解指南。