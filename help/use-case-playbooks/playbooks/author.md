---
solution: Experience Platform
title: 使用案例的AI助理 — 編寫並分享您自己的教戰手冊。
description: 如何編寫和分享您自己的使用案例教戰手冊。
role: User
source-git-commit: f813db7599409a8fc048480f7803ed86c9f397fe
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---


# 撰寫並分享您自己的教戰手冊

由Adobe的AI Assistant支援的&#x200B;**教戰手冊編寫架構**&#x200B;可讓您在Adobe Experience Platform中有效率地建立、管理和共用教戰手冊。

此架構遵循三個步驟的流程：

1. **中繼資料擷取**：使用AI助理或[網頁表單]來擷取Playbook中繼資料。

2. **技術關聯**：將歷程或受眾等特定技術資產新增至行動手冊。 您可以完整控制開發沙箱中的Playbook建立流程，確保與您的結構描述和其他獨特的資料結構一致。

3. **行動手冊發佈**：跨不同組織共用行動手冊。 例如，ACME的德國Martech Center of Excellence可以建立「黃金」行動手冊，並分發給泰國、澳洲等地的區域組織。 協助標準化行銷使用案例。

## 使用Adobe的AI助理建立教戰手冊

### 教戰手冊概述

您可以透過兩種方式建立行動手冊：使用Adobe的AI助理或手動。

請依照下列步驟，使用Adobe的AI Assistant建立行動手冊：

1. 在左側導覽窗格中，選取&#x200B;**教戰手冊**。

在UI的左側導覽窗格中反白顯示![「教戰手冊」。](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

1. 選取&#x200B;**新行動手冊**，然後選取&#x200B;**使用AI助理產生行動手冊**。

![選取[新行動手冊]按鈕。](/help/use-case-playbooks/assets/playbooks/authoring/new-playbook.png)

![選取「使用AI助理產生行動手冊」按鈕強調顯示。](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

1. 在提示欄位中，說明使用案例。

**範例**：「與瀏覽跑步鞋但未完成購買的ACME客戶互動。」

![選取[使用AI助理產生行動手冊]按鈕。](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

1. 選取&#x200B;**產生**&#x200B;以建立Playbook中繼資料。

![提示區域的「產生」Playbook按鈕反白顯示。](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

1. 產生後，選取&#x200B;**[!UICONTROL 編輯]**&#x200B;以視需要修改產生的標題、說明和中繼資料。

![產生的Playbook中反白顯示「編輯」按鈕。](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

為確保資料工程師擁有設定使用案例所需的所有詳細資訊，請填寫&#x200B;**[!UICONTROL 行動手冊詳細資訊]**&#x200B;區段。 雖然這些欄位可供選用，但有助於擷取重要資訊，讓您更輕鬆地連線正確的技術元件。 選取&#x200B;**[!UICONTROL 編輯]**&#x200B;以新增值至下列欄位：

* **產業**
* **目標客群**
* **行銷管道**

![標示「編輯」按鈕的Playbook詳細資訊區段。](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

中繼資料產生後，請選取&#x200B;**編輯歷程圖**&#x200B;按鈕，以視需要調整歷程圖中的步驟。

![編輯歷程地圖按鈕。](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![擷取行動手冊中繼資料後，請編輯歷程地圖。](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

然後繼續將教戰手冊與技術資產建立關聯。

若要手動建立行動手冊，請選取&#x200B;**手動建立行動手冊**。

![手動建立行動手冊](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

空白的Playbook範本隨即出現。 填寫&#x200B;**標題**&#x200B;和&#x200B;**描述**&#x200B;等詳細資料。 您也可以編輯歷程圖，以視需要新增事件和接觸點。

## 將行動手冊與技術資產建立關聯

無論您是以手動方式還是使用AI助理建立行動手冊，您都必須將其與所需的技術資產建立關聯。 導覽至&#x200B;**[!UICONTROL 技術Assets]**&#x200B;標籤，然後選取所需的產品。 在此範例中，請選擇&#x200B;**[!UICONTROL Journey Optimizer]**。

>[!NOTE]
>
> 未來版本將新增對Real-Time Customer Data Platform的支援。

![「技術資產」索引標籤和「新增必要產品」按鈕強調顯示。](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

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

![範例1提示](/help/use-case-playbooks/assets/playbooks/authoring/example-prompt.png)

**範例2：**

「專案名稱：時尚電子報
背景： （主動式或解決問題的方式）：旨在傳送時尚電子報給已訂閱電子報通訊的ACME客戶的歷程。
目標：傳送時尚電子報電子郵件給訂閱通訊的ACME客戶。
促銷詳細資料：客戶每週都會透過電子郵件頻道收到時尚新聞。 電子郵件應該根據性別、語言和市場進行個人化和內容變化。
專案管道/接觸點：電子郵件
目標對象：已訂閱ACME時尚電子報通訊的客戶。
目標KPI/參與量度/ROI：1. 增加產品的收入。 2.提升客戶忠誠度。」

![範例2提示](/help/use-case-playbooks/assets/playbooks/authoring/example-2-prompt.png)

**範例3：**

「在持續進行的產品促銷活動期間，引導購物者購買產品。
透過透過電子郵件、簡訊或推播通知傳送適當的通訊來購買產品，在持續促銷期間與購物者互動。 在他們24小時未參與促銷活動後，傳送提醒電子郵件給他們。」

![範例3提示](/help/use-case-playbooks/assets/playbooks/authoring/example-3-prompt.png)

**範例4：**

「賣鞋給高中玩家。」

![範例4提示](/help/use-case-playbooks/assets/playbooks/authoring/example-4-prompt.png)

AI助理會移除所有不必要的詳細資料，例如「專案名稱」或「背景」。 它會擷取「目標對象」、「行銷活動目標」及「行銷管道」等關鍵元素，並搭配任何輸入樣式使用。

這些範例示範AI如何從使用者提示中縮小並擷取重要細節。

>[!NOTE]
>
> 在撰寫提示時避免使用任何PII或明確的字詞。

## 內容指導方針與管制

建立教戰手冊時，請留意您包含的語言和內容。 教戰手冊在整個組織中皆可見，且使用者可標籤任何冒犯性或不適當的內容。

### 標幟和檢閱程式

如果行動手冊被標籤為不適當或冒犯性的內容，則會自動向Adobe報告以供稽核。 Adobe接著會稽核標幟的內容，如果認為不適當，則會通知客戶，並移除Playbook。

## 後續步驟

現在您已瞭解如何使用Adobe的AI Assistant建立和發佈教戰手冊，瞭解如何開始使用可用的教戰手冊，並從[教戰手冊清單](/help/use-case-playbooks/playbooks/choose.md)為您的使用案例選擇正確的教戰手冊。
