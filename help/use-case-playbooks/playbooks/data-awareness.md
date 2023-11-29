---
solution: Experience Platform
title: 使用案例教戰手冊中的資料感知概觀
description: 瞭解如何透過將最終啟髮型沙箱中產生的資產複製到其他沙箱，以加快實現價值的時間。
badgeBeta: label="Beta" type="Informative"
source-git-commit: 5b6b69d69a088f58d10f41debde859294285360d
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---


# 使用案例教戰手冊中的資料感知概觀

使用案例教戰手冊是行銷範本，設計用於產生資產，例如常見行銷使用案例的對象、結構或歷程。 在Adobe Experience Platform中，這些範本會參考數個標準欄位和欄位群組。 但是，在某些情況下，您可能已經設定自己的結構描述、欄位和欄位群組。 這可能會使使用案例範本產生的部分資產（例如歷程）與您的資料不相容。 閱讀本教學課程，瞭解如何使用資料感知功能，讓產生的資產與現有資產更妥善地配對和互補。

## 先決條件 {#prerequisites}

閱讀本教學課程前，請先瀏覽 [可用的使用案例教戰手冊範本](/help/use-case-playbooks/playbooks/discover.md#search-and-filter) 和 [建立執行個體](/help/use-case-playbooks/playbooks/create-share-reuse.md) 屬於偏好的行動手冊。

建立例項會在勵志沙箱中產生一組資產，例如歷程、區段、方案和訊息。 請閱讀下文，瞭解如何將這些資產複製到其他沙箱。

### 建立及發佈套件 {#create-publish-package}

1. 若要將物件從啟發性的沙箱匯入另一個沙箱，請瀏覽至使用案例行動手冊的所需執行個體，然後選取「 」 **[!UICONTROL 發佈到不同的沙箱]** 將成品匯出為封裝。

   ![顯示不同使用案例執行個體的GIF](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. 一旦您選取 **[!UICONTROL 發佈到不同的沙箱]** 按鈕，強制回應視窗隨即顯示。 填寫名稱和可選的說明，然後選取 **[!UICONTROL 建立]**. 此步驟將產生的資產整合到一個套件中，可將其匯入不同的沙箱中。

   ![建立套件的強制回應視窗](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. 導覽至 **沙箱** 頁面左側導覽並選取 **封裝** 索引標籤中，尋找您的封裝並發佈。 若要發佈處於草稿狀態的套件，請依照 [沙箱工具](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish) 檔案。

   ![處於草稿或未發佈狀態的套件](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![發佈套件](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. 發佈成功後，在套件瀏覽頁面上，您應該會看到 **+** 名稱旁邊的按鈕已啟用。

   ![「沙箱」頁面中的「套件」標籤](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > 當套件仍處於草稿模式時無法匯入它，因此請開啟套件詳細資訊頁面並發佈套件。

5. 選取 **+** 啟動工作流程的控制項，以將使用案例行動手冊產生的資產匯入 **[!UICONTROL Target沙箱]**. 選取目標沙箱，並使用下拉式清單確認您要匯入的套件名稱。 在繼續下一步之前，新增工作詳細資訊，例如工作名稱和工作說明。

   ![啟動匯入工作流程、選取目標、確認封裝、新增工作詳細資料。](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

   >[!NOTE]
   >
   > 您只能將套件匯入其他開發沙箱。 生產沙箱已針對這類匯入停用。

6. 在 **[!UICONTROL 檢視相依性]** 步驟，您可以對應結構描述，並將其他資產從啟發性的沙箱複製到目標沙箱。 此 **[!UICONTROL 完成]** 在您對應每個結構描述之前，按鈕都會停用。

   ![在「檢視相依性」步驟中對應結構描述，啟用「完成」按鈕。](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### 對應結構描述 {#map-schemas}

1. 對應第一個結構描述。 綱要對應對話方塊會顯示一個下拉式清單，用來選取目標綱要。 如果來源結構描述是設定檔結構描述，則除了 [個別聯合設定檔結構描述](/help/xdm/classes/individual-profile.md). 第一次顯示頁面時，您可以看到來源資料與目標欄位之間自動產生的對應建議。 您可以選取目標欄位，然後選取新欄位來編輯對應。 如果您對建議的對映進行變更，請使用 **驗證** 按鈕以驗證新對應並顯示任何可能連結至新對應的錯誤。 選取 **儲存** 當對應完成後。

   ![結構描述對應對話方塊，內含可選取目標結構描述的下拉式清單。](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. 繼續對應結構描述中的所有欄位。 如果結構描述是 [事件結構描述](/help/xdm/classes/experienceevent.md)，對話方塊會顯示一個下拉式清單，您可在其中檢視target沙箱中的所有事件結構。

   ![從下拉式清單中選取目標結構描述](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. 從中的可用結構描述中選取結構描述 **Target沙箱**.

   ![選取結構描述](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. 完成對應並選取 **儲存**.

   ![儲存對應](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. 對應完結構描述中的所有欄位後，請選取 **完成** 以完成匯入工作流程。

   ![完成流程](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > 您無法對結構描述以外的任何資產執行動作，因為這是啟發性的沙箱，但因其為套件的相依性而顯示。

### 匯入狀態 {#import-status}

1. 系統會自動將您重新導向至 [**匯入**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) 您可以在此頁面檢視匯入進度。

   ![顯示匯入進度的頁面](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. 匯入套件時，會在目標沙箱中建立套件的資產。 完成後，它們將會參考您剛在匯入程式中對應的欄位。 此程式現已完成，而來自勵志沙箱的資產現在也出現在您的目標沙箱中，供您測試。

   ![在目標沙箱中產生的資產](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## 後續步驟

閱讀本指南後，您現在已清楚瞭解如何運用使用案例教戰手冊以及 [沙箱工具](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) 以建立參考您結構描述的可執行檔歷程。 進一步瞭解常見問題 [Real-Time CDP使用案例](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).