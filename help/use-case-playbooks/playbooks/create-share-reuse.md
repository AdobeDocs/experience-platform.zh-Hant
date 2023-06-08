---
solution: Experience Platform
title: 建立、共用和重複使用教戰手冊例項
description: 瞭解如何建立、共用及重複使用Playbook例項，以完成您的行銷使用案例。
badgeBeta: label="Beta" type="Informative"
source-git-commit: 51e4a77472ccb560dbfa5f56011ce50932d87b64
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---


# （測試版）建立、共用及重複使用教戰手冊例項

>[!AVAILABILITY]
>
>此功能目前為測試版，並未開放所有使用者使用。 文件和功能可能會有所變更。

若要使用教戰手冊，請導覽至 **[!UICONTROL 使用案例教戰手冊] > [!UICONTROL 教戰手冊]**. 瀏覽並使用頁面上的各種搜尋和篩選選項，以選取並開始使用特定教戰手冊。

## 建立Playbook例項 {#create-playbook-instance}

在建立教戰手冊例項之前，請先探索可用的教戰手冊，以 [探索適合您的行動手冊](/help/use-case-playbooks/playbooks/discover.md). 當您準備好繼續使用教戰手冊並建立例項時，請選取「 」 **[!UICONTROL 建立執行個體]** 以繼續使用教戰手冊並產生技術資產。

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

閱讀本指南及探索適合您的行動手冊的指南後，您現在知道如何解讀行動手冊的各個區段，以及如何使用在您建立行動手冊例項後產生的資產。

接下來，您可以瀏覽教戰手冊目錄，找到適合您使用案例的教戰手冊，並閱讀 [疑難排解指南](/help/use-case-playbooks/playbooks/troubleshooting.md) 如果您遇到任何問題。