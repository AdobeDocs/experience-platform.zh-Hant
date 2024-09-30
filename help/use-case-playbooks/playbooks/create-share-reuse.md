---
solution: Experience Platform
title: 建立、共用和重複使用教戰手冊執行個體
description: 了解如何建立、共用和重複使用教戰手冊執行個體以完成您的行銷使用案例。
role: User, Developer
exl-id: b06d8186-c41f-4150-bac4-69c616151ef9
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 81%

---

# 建立、共用和重複使用教戰手冊執行個體

若要使用教戰手冊，請瀏覽至&#x200B;**[!UICONTROL 使用案例] > [!UICONTROL 教戰手冊]**。瀏覽並使用頁面上的各種搜尋和篩選選項以選取並開始使用特定的教戰手冊。

## 建立教戰手冊實例 {#create-playbook-instance}

>[!CONTEXTUALHELP]
>id="platform_playbooks_create"
>title="建立實例"
>abstract="產生資產清單 (例如旅程、客群、結構描述或目的地) 以在旅程或啟動情境中使用。"

在建立教戰手冊執行個體之前，請先探索可用的教戰手冊，以[選擇正確的教戰手冊](/help/use-case-playbooks/playbooks/choose.md)。 當您準備好繼續使用教戰手冊並建立執行個體時，請選取&#x200B;**[!UICONTROL 建立執行個體]**&#x200B;以繼續使用教戰手冊並產生技術資產。

![建立教戰手冊的執行個體。](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

此動作會產生幾個資產供您用於實現教戰手冊中說明的使用案例。

![啟用後產生之資產的教戰手冊檢視。](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### 使用設定控制編輯執行個體名稱和說明 {#edit-instance-metadata}

根據教戰手冊建立執行個體後，您可以將該執行個體個人化，以和其他使用相同教戰手冊建立之執行個體有所區別。選取設定控制，如下所示。編輯名稱、說明和註釋，並在完成時選取&#x200B;**[!UICONTROL 儲存]**。

![編輯執行個體的名稱和說明。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### 了解產生的資產 {#understand-assets}

>[!IMPORTANT]
>
>無須擔憂！這是一個安全的實驗空間，您不會造成任何破壞。目前還沒有和您建立的任何資產相關聯的資料。您必須先擷取資料才能實現此使用案例。

重要的是要了解產生的資產會依據您啟用的使用案例而有所不同：

* 不同類型的教戰手冊會產生不同的資產。這些資產是專門為了透過教戰手冊實現的使用案例所建立的。例如，行動手冊會產生結構、受眾、歷程和訊息。 另一個教戰手冊產生要為其啟用資料的結構描述、受眾和目的地。
* 不同教戰手冊之間的資產本身有所不同。例如，若為「**[!UICONTROL 傳送生日訊息給來賓]**」教戰手冊，所建立的客群會具有規則 `birthday=today AND year=any`。

以範例說明，若為「**[!UICONTROL 捨棄的購物車：商品]**」教戰手冊，您可以看到建立了一個特定的歷程，其中會包括為此使用案例所建立的訊息。

![根據使用案例教戰手冊建立的歷程。](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### 使用和編輯產生的資產 {#use-and-edit-assets}

當您探索在您建立教戰手冊的執行個體後產生的資產時，您可以編輯所建立的任何資產。

如果您或您團隊中的某人建立了教戰手冊的另一個執行個體，則將保留已編輯的資產，並為教戰手冊的新執行個體建立新資產。

上述行為適用於已建立的所有資產 (綱要除外)。至於綱要，建立教戰手冊的新執行個體時並不會建立新的綱要，因此您會在新建立的執行個體中使用來自教戰手冊的另一個執行個體的已編輯綱要。

>[!TIP]
>
>在開發沙箱中進行測試，準備就緒後即可移動到生產環境。
>
>物件產生後，只要新增資料，即可在開發沙箱中繼續測試。只要您想在開發沙箱中測試資產，就可以在準備就緒時，在生產沙箱中複製資產邏輯（對象定義、歷程、結構描述等）。 您可以使用[資料感知功能](/help/use-case-playbooks/playbooks/data-awareness.md)，先移至開發沙箱，然後再移至生產沙箱。

## 重複使用教戰手冊 {#reuse-playbooks}

建立相同教戰手冊的多個執行個體，您即可在稍後實作相同的使用案例，而無需修改先前使用案例實作的詳細資料。

## 和其他團隊成員共用教戰手冊以及所產生的資產 {#share-playbook}

您可以和其他團隊成員共用產生的執行個體和資產。若要這麼做，請從瀏覽器複製 URL 連結並和您的團隊共用，提供他們對產生的資產的概觀。

![在使用案例教戰手冊檢視中反白顯示的 URL。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## 端對端行動手冊程式的影片逐步解說

觀看此影片瞭解如何從端對端探索、建立、發佈使用案例行動手冊並對執行個體進行疑難排解，以及如何將行動手冊產生的資產複製到組織中設定的其他沙箱中。

>[!VIDEO](https://video.tv.adobe.com/v/3427058/?learn=on)

## 後續步驟 {#next-steps}

由於閱讀過本指南以及有關探索適合您的教戰手冊的指南，您現在了解如何解譯教戰手冊的各個章節以及如何使用您建立教戰手冊的執行個體後所產生的資產。

接下來，您可以瀏覽教戰手冊目錄，找到適合您的使用案例的教戰手冊，如果遇到任何問題，則可閱讀[疑難排解指南](/help/use-case-playbooks/playbooks/troubleshooting.md)。
