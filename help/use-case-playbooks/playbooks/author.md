---
solution: Experience Platform
title: 瞭解如何使用AI助理撰寫和分享您自己的教戰手冊。
description: 如何編寫和分享您自己的使用案例教戰手冊。
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: a910c922e9a51b60e276b0aac7e81e35d0a378fd
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 0%

---


# 撰寫並分享您自己的教戰手冊(Beta)

[!DNL Playbook Authoring Framework]由Adobe Experience Platform中的AI Assistant提供技術支援，可讓您在Adobe Experience Platform中有效率地建立、管理和共用教戰手冊。

此架構遵循三個步驟的流程：

1. **中繼資料擷取**：使用AI助理或網頁表單來擷取Playbook中繼資料。

2. **技術關聯**：將歷程或受眾等特定技術資產新增至行動手冊。 您可以完整控制開發沙箱中的Playbook建立流程，確保與您的結構描述和其他獨特的資料結構一致。

3. **行動手冊發佈**：跨不同組織共用行動手冊。 例如，ACME的德國Martech Center of Excellence可以建立「黃金」行動手冊，並分發給泰國、澳洲等地的區域組織。 協助標準化行銷使用案例。

## 建立行動手冊

您可以使用兩種方式建立行動手冊：使用AI助理或手動。 請閱讀以下章節，瞭解如何使用AI Assistant建立行動手冊。

### 教戰手冊概述

請依照下列步驟，使用AI Assistant建立行動手冊：

在左側導覽面板中，選取&#x200B;**[!UICONTROL 教戰手冊]**。

在UI的左側導覽窗格中反白顯示![「教戰手冊」。](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

選取&#x200B;**[!UICONTROL 新行動手冊]**，然後選取&#x200B;**使用AI助理產生行動手冊**。

![已選取「使用AI助理產生行動手冊」的行動手冊介面。](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

使用提示欄位來說明使用案例。 例如：

「與瀏覽跑步鞋但未完成購買的ACME客戶互動。」

![反白顯示網頁表單區域的Playbook介面。](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

選取&#x200B;**[!UICONTROL 產生]**&#x200B;以建立Playbook中繼資料。

![提示區域的「產生」Playbook按鈕反白顯示。](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

產生後，選取&#x200B;**[!UICONTROL 編輯]**&#x200B;以視需要修改產生的標題、說明和中繼資料。

![產生的Playbook中反白顯示「編輯」按鈕。](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

為確保資料工程師擁有設定使用案例所需的所有詳細資訊，請填寫&#x200B;**[!UICONTROL 行動手冊詳細資訊]**&#x200B;區段。 雖然這些欄位可供選用，但有助於擷取重要資訊，讓您更輕鬆地連線正確的技術元件。 選取&#x200B;**[!UICONTROL 編輯]**&#x200B;以新增值至下列欄位：

* **產業**
* **目標客群**
* **行銷管道**

![標示「編輯」按鈕的行動手冊詳細資訊區段。](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

中繼資料產生後，選取&#x200B;**[!UICONTROL 編輯歷程圖]**&#x200B;以視需要調整歷程圖中的步驟。

![編輯歷程地圖按鈕。](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![擷取行動手冊中繼資料後，請編輯歷程地圖。](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

接著，繼續將行動手冊與技術資產建立關聯。 若要手動建立行動手冊，請選取&#x200B;**[!UICONTROL 手動建立行動手冊]**。

![手動建立行動手冊](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

空白的Playbook範本隨即出現。 填寫&#x200B;**標題**&#x200B;和&#x200B;**描述**&#x200B;等詳細資料。 您也可以編輯歷程圖，以視需要新增事件和接觸點。

## 將行動手冊與技術資產建立關聯

無論您是以手動方式還是使用AI助理建立行動手冊，您都必須將其與所需的技術資產建立關聯。 導覽至&#x200B;**[!UICONTROL 技術Assets]**&#x200B;標籤，然後選取所需的產品。 在此範例中，選取&#x200B;**[!UICONTROL Journey Optimizer]**。

>[!NOTE]
>
> 未來版本將新增對Real-Time CDP的支援。

![ 「技術資產」索引標籤和「新增必要產品」按鈕已反白顯示。](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

選擇&#x200B;**[!UICONTROL 選取資產]**&#x200B;以將此行動手冊與歷程建立關聯，如下圖所示。 然後選取&#x200B;**發佈行動手冊**&#x200B;以完成行動手冊。

在「技術資產」索引標籤](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)上反白顯示![「選取資產」按鈕

![選取歷程](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

發佈後，行動手冊會自動擷取並關聯歷程的結構描述和受眾詳細資訊。

![已發佈的行動手冊](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

所有已建立的教戰手冊，都可在&#x200B;**您的教戰手冊**&#x200B;索引標籤中使用。

![「您的教戰手冊」索引標籤](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

您可以從目錄中選取任何教戰手冊，以建立重複使用的例項。 請參閱檔案，以便[瞭解如何建立執行個體](/help/use-case-playbooks/playbooks/create-share-reuse.md)。

選取行動手冊後，「行動手冊概述」索引標籤中會反白顯示![「建立執行個體」選項。](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> 行動手冊一經發佈，便無法編輯。 若要進行變更，請刪除行動手冊，然後重新開始。

## 提示範例

AI助理可以處理各種提示結構並擷取關鍵詳細資訊，同時篩選掉不必要的資訊。 以下是一些使用者提示的範例，以及系統如何解譯這些提示：

**範例1：**

建立標題為「完成外觀」的行銷活動，以增加銷售和CLV。 此行銷活動鼓勵客戶購買廚具或傢俱，透過與購買相關的個人化建議和優惠完成補充購買。 首先傳送訊息給有產品建議的客戶。 如果他們沒有在7天內進行任何購買，他們會收到第二則訊息，其中包含產品建議和選件。 使用推播通知和電子郵件聯絡客戶。 鎖定在過去7天內在廚具或傢俱類別中購買過，且在過去30天內未成為目標的客戶。 在行銷活動中，我們要測量KPI，例如點按數（電子郵件、應用程式、簡訊、推播）、CTR、電子錢包CTR、AOV轉換。CLV收入、總購買事件（店內、數位、客服中心）。」

![在文字輸入方塊中顯示長提示的範例](/help/use-case-playbooks/assets/playbooks/authoring/long-prompt.png)

**範例2：**

「專案名稱：時尚電子報
背景： （主動式或解決問題的方式）：旨在傳送時尚電子報給已訂閱電子報通訊的ACME客戶的歷程。
目標：傳送時尚電子報電子郵件給訂閱通訊的ACME客戶。
促銷詳細資料：客戶每週都會透過電子郵件頻道收到時尚新聞。 電子郵件應該根據性別、語言和市場進行個人化和內容變化。
專案管道/接觸點：電子郵件
目標對象：已訂閱ACME時尚電子報通訊的客戶。
目標KPI/參與量度/ROI：1. 增加產品的收入。 2.提升客戶忠誠度。」

![在文字輸入方塊中顯示有組織的提示的範例](/help/use-case-playbooks/assets/playbooks/authoring/organized-list-prompt.png)

**範例3：**

「在持續進行的產品促銷活動期間，引導購物者購買產品。
透過透過電子郵件、簡訊或推播通知傳送適當的通訊來購買產品，在持續促銷期間與購物者互動。 在他們24小時未參與促銷活動後，傳送提醒電子郵件給他們。」

![在文字輸入方塊中顯示精簡提示的範例](/help/use-case-playbooks/assets/playbooks/authoring/concise-prompt.png)

**範例4：**

「賣鞋給高中玩家。」

![顯示單一提示字元的範例](/help/use-case-playbooks/assets/playbooks/authoring/one-liner-prompt.png)

AI助理會移除所有不必要的詳細資料，例如「專案名稱」或「背景」。 它會擷取「目標對象」、「行銷活動目標」及「行銷管道」等關鍵元素，並搭配任何輸入樣式使用。

這些範例示範AI如何從使用者提示中縮小並擷取重要細節。

>[!NOTE]
>
> 在撰寫提示時避免使用任何PII或明確的字詞。

## 內容指導方針與管制

建立教戰手冊時，請留意您包含的語言和內容。 教戰手冊在整個組織中皆可見，且使用者可標籤任何冒犯性或不適當的內容。

### 標幟和檢閱程式

如果行動手冊被標籤為不適當或冒犯性的內容，則會自動向Adobe報告以供稽核。 Adobe接著會稽核標幟的內容，如果認為不適當，則會通知客戶，並移除Playbook。

## 在沙箱間共用教戰手冊 {#sharing-playbooks-sandboxes}

如果您的組織包含多個沙箱，您不需要手動在這些沙箱之間共用教戰手冊。 在單一沙箱中建立並發佈Playbook後，即可在該組織的所有沙箱中使用。 然後您可以在任何其他沙箱中建立該行動手冊的執行個體。

如果行動手冊參照的欄位在另一個沙箱的聯合結構描述中無法使用，則嘗試建立執行個體時可能會看到錯誤訊息。 該訊息會呼叫缺少的欄位，因此您可以根據需要更新結構。

>[!IMPORTANT]
>
>不支援傳遞行動手冊共用。 如果您將行動手冊從一個組織分享到另一個組織，然後匯入它，則它無法再次從接收組織分享到第三個組織。

## 跨組織共用您的教戰手冊 {#sharing-playbooks-organizations}

若要在不同組織之間分享行動手冊，請遵循下列步驟：

* **登入來源組織**：從&#x200B;**[!UICONTROL 您的行動手冊]**&#x200B;索引標籤，瀏覽至包含您已建立且要共用的行動手冊的組織。
* **發佈行動手冊**：如果行動手冊尚未發佈，您必須先發佈再分享。

>[!NOTE]
>
>來源和目標組織之間必須建立合作關係，才能啟用行動手冊共用。 瞭解如何[建立組織夥伴關係請求](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/ui/sharing-packages-across-orgs)。

* **啟動共用**：一旦行動手冊發佈並建立合作關係，請選取&#x200B;**[!UICONTROL 共用行動手冊]**。
* **選取目標組織**：選擇您要在系統提示時與其共用行動手冊的組織。
* **確認並共用**：確認您的選擇。 您將會收到指示成功共用的確認訊息。
* ***驗證目標組織**：登入目標組織以驗證行動手冊是否可用。
* **匯入行動手冊**：選取「**[!UICONTROL 匯入]**」，將行動手冊匯入目標組織。 您可以在&#x200B;**教戰手冊**&#x200B;索引標籤中檢視它。

如果聯合結構描述中缺少任何欄位，在匯入期間將會顯示一個對話方塊，反白顯示它們。

匯入程式期間所列的聯合結構描述中缺少![欄位](/help/use-case-playbooks/assets/playbooks/authoring/missing-fields.png)

如果行動手冊未出現，請確保已發佈且組織夥伴關係有效。

## 必要權限

若要存取沙箱及使用此功能，您需要下列許可權：

* **沙箱許可權**：

存取功能所在的沙箱環境需要這些許可權：

* **管理沙箱**
* **檢視沙箱**

* **封裝共用許可權**：

內部共用功能需要下列許可權：

* [**管理封裝**](/help/sandboxes/ui/sandbox-tooling.md)
* [**共用封裝**](/help/sandboxes/ui/sharing-packages-across-orgs.md)

這些許可權可讓您：

* 輸入沙箱環境
* 存取沙箱中的功能
* 視需要管理和共用套件

這些許可權位於許可權清單的&#x200B;**[!UICONTROL 沙箱]**&#x200B;區段中。

![標示相關許可權的許可權清單。](/help/use-case-playbooks/assets/playbooks/authoring/permissions.png)

### 歷程和相關物件 — 許可權

當建置使用教戰手冊的歷程時，您可能會參考其他物件，例如&#x200B;**管道**、**對象**&#x200B;和其他實體。 每個檔案都有其專屬的許可權集。

這些是Journey相關動作的主要許可權，例如：

* **檢視歷程**
* **管理歷程**
* 和「對象」和「管道」等物件相關的許可權

您還需要下列對象許可權：

* **區段讀取**
* **已讀取的設定檔**
* **資料集讀取**

由於歷程非常靈活，而且可能涉及許多互連的物件，因此其[完整許可權](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/privacy/high-low-permissions)會單獨記錄，並可能因您的特定使用案例而有所不同。

## 後續步驟

現在您已瞭解如何使用AI Assistant建立、發佈和分享教戰手冊，瞭解如何開始使用可用的教戰手冊，並從[教戰手冊清單](/help/use-case-playbooks/playbooks/choose.md)為您的使用案例選擇正確的教戰手冊。