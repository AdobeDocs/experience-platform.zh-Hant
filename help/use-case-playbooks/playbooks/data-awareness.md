---
solution: Experience Platform
title: 使用案例教戰手冊中的資料感知概觀
description: 瞭解如何透過將最終啟髮型沙箱中產生的資產複製到其他沙箱，以加快實現價值的時間。
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# 將Publish playbook產生的資產移至其他沙箱 {#publish-to-other-sandboxes}

使用案例教戰手冊是行銷範本，旨在針對常見行銷使用案例產生對象、結構或歷程等資產。 您可以在啟發性的沙箱中測試教戰手冊建立的資產，當您準備好時，您可以將資產匯入其他開發沙箱，以使用這些沙箱中提供的資料進行進一步測試。 對測試感到滿意後，您就可以將資產從開發沙箱移至生產沙箱。

但是，在某些情況下，您可能已經在其他開發沙箱中設定自己的結構描述、欄位和欄位群組。 這可能會使使用案例範本產生的部分資產（例如歷程）與您的資料不相容。 若要瞭解如何使用資料感知功能，以便讓產生的資產更符合併完善您的現有資產，請閱讀本教學課程。

## 先決條件 {#prerequisites}

閱讀本教學課程之前，請先瀏覽[可用的使用案例行動手冊範本](/help/use-case-playbooks/playbooks/choose.md#search-and-filter)並[建立慣用行動手冊的執行個體](/help/use-case-playbooks/playbooks/create-share-reuse.md)。

建立例項會在勵志沙箱中產生一組資產，例如歷程、區段、方案和訊息。 請閱讀下文，瞭解如何將這些資產複製到其他沙箱。

### 建立及發佈套件 {#create-publish-package}

>[!NOTE]
>
> 您只能將套件匯入其他開發沙箱。 完成所有必要的變更或更新後，您就可以從這些開發沙箱將資產或套件匯入生產環境。 您無法直接從使用案例教戰手冊沙箱匯入到生產環境。

1. 若要將物件從啟發性的沙箱匯入另一個沙箱，請瀏覽至使用案例行動手冊的所需執行個體，然後選取&#x200B;**[!UICONTROL Publish至另一個沙箱]**，將成品匯出為套件。

   ![顯示不同使用案例執行個體的GIF](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. 選取&#x200B;**[!UICONTROL Publish至其他沙箱]**&#x200B;按鈕後，強制回應視窗會出現。 填寫名稱和選擇性說明，然後選取&#x200B;**[!UICONTROL 建立]**。 此步驟將產生的資產整合到一個套件中，可將其匯入不同的沙箱中。

   ![建立封裝的強制回應視窗](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. 導覽至左側導覽的「**沙箱**」頁面，然後選取「**套件**」標籤、尋找您的套件並發佈。 若要發佈處於草稿狀態的套件，請依照[沙箱工具](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish)檔案中的步驟操作。

   ![封裝處於草稿或未發佈狀態](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![正在發佈封裝](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. 發佈成功後，在套件瀏覽頁面上，您應該會看到名稱旁邊有&#x200B;**+**&#x200B;按鈕已啟用。

   沙箱頁面中的![封裝標籤](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > 當套件仍處於草稿模式時無法匯入它，因此請開啟套件詳細資訊頁面並發佈套件。

5. 選取&#x200B;**+**&#x200B;控制項並啟動工作流程，以將使用案例行動手冊產生的資產匯入&#x200B;**[!UICONTROL Target沙箱]**。 選取目標沙箱，並使用下拉式清單確認您要匯入的套件名稱。 在繼續下一步之前，新增工作詳細資訊，例如工作名稱和工作說明。

   ![啟動匯入工作流程、選取目標、確認封裝、新增工作詳細資料。](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. 在&#x200B;**[!UICONTROL 檢視相依性]**&#x200B;步驟中，您可以對應結構描述，並將其他資產從勵志沙箱複製到目標沙箱。 在您對應每個結構描述之前，**[!UICONTROL 完成]**&#x200B;按鈕是停用的。

   ![在[檢視相依性]步驟中對應結構描述，啟用[完成]按鈕。](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### 對應結構描述 {#map-schemas}

1. 對應第一個結構描述。 綱要對應對話方塊會顯示一個下拉式清單，用來選取目標綱要。 如果來源結構描述是設定檔結構描述，則除了[個別聯合設定檔結構描述](/help/xdm/classes/individual-profile.md)之外，沒有其他目標結構描述選項。 第一次顯示頁面時，您可以在Source資料和目標欄位之間檢視自動產生的對應建議。 您可以選取目標欄位，然後選取新欄位來編輯對應。 如果您修改建議的對應，請使用&#x200B;**驗證**&#x200B;按鈕來驗證新對應，並顯示任何可能連結到新對應的錯誤。 完成對應後，選取&#x200B;**儲存**。

   ![具有下拉式清單的結構描述對應對話方塊，以選取目標結構描述。](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. 繼續對應結構描述中的所有欄位。 如果結構描述是[事件結構描述](/help/xdm/classes/experienceevent.md)，對話方塊會顯示一個下拉式清單，您可以在其中檢視目標沙箱中的所有事件結構描述。

   ![從下拉式清單中選取目標結構描述](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. 從&#x200B;**Target沙箱**&#x200B;中的可用結構描述中選取結構描述。

   ![選取結構描述](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. 完成對應並選取&#x200B;**儲存**。

   ![儲存對應](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. 完成對應結構描述中的所有欄位後，請選取&#x200B;**完成**&#x200B;以完成匯入工作流程。

   ![完成流程](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > 您無法修改任何資產，除了結構描述，因為這是啟發性的沙箱，但它們確實顯示，因為它們是套件的相依性。

### 匯入狀態 {#import-status}

1. 系統會自動將您重新導向至&#x200B;[**匯入**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details)&#x200B;頁面，您可以在其中檢視匯入進度。

   顯示匯入進度的![頁面](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. 匯入套件時，會在目標沙箱中建立套件的資產。 完成後，它們會參照您在匯入過程中對應的欄位。 此程式現已完成，而來自勵志沙箱的資產現在也出現在您的目標沙箱中，供您測試。

   ![在目標沙箱中產生的資產](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## 後續步驟

閱讀本指南後，您現在更瞭解如何運用使用案例教戰手冊及[沙箱工具](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details)，建立參考您結構描述的可執行檔歷程。 深入瞭解常見的[Real-Time CDP使用案例](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)。
