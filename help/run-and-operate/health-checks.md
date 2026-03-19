---
title: 健康情況檢查
description: 瞭解如何使用Adobe Experience Platform中的健康情況檢查，在結構描述和身分設定問題影響您的資料作業之前，主動偵測這些問題。
solution: Experience Platform
type: Documentation
role: Admin, User
hide: true
source-git-commit: ab2420b898dc38d19187cee627b5c44e7fb44a6c
workflow-type: tm+mt
source-wordcount: '1590'
ht-degree: 1%

---

# 健康情況檢查

健康情況檢查會掃描您在沙箱中使用的結構描述和身分，並提供問題摘要，以便您探索和疑難排解[!UICONTROL AI Assistant]。 未來可以掃描更多物件，以取得更完整的報告。

不良的結構描述和身分設定會導致嚴重的下游問題，包括不正確的設定檔建立、失敗的區段資格和不準確的啟用。 這些問題很難偵測，通常需要專業知識才能診斷。 健康狀態檢查將您的方式從被動式疑難排解轉變為主動預防性維護。

透過健康狀態檢查，您可以：

* **及早偵測設定問題**：找出遺漏的最佳實務、設定錯誤和模式，導致個人化、啟動等作業效率低下。
* **接收引導式修正**：取得每個問題的明確指引，以及處理該問題的方式。
* **持續監視**：在這個時候，健康情況檢查會執行每日自動掃描，以便在問題變成嚴重失敗之前找出問題。 未來版本可能會變更排程。

## 先決條件 {#prerequisites}

若要存取健康情況檢查，您需要&#x200B;**[!UICONTROL View Health Checks]** [存取控制許可權](/help/access-control/home.md#permissions)。 請聯絡您的系統管理員，以確保您擁有適當的許可權。

## 存取健康狀態檢查 {#access-health-checks}

若要從[!UICONTROL Experience Platform] UI存取健康情況檢查：

1. 從左側導覽中選取&#x200B;**[!UICONTROL Run and Operate]**。
1. 選擇「**[!UICONTROL Health Checks]**」。

健康情況檢查儀表板會顯示您最近掃描結果的摘要。

![健康情況檢查儀表板，顯示已評估的物件、掃描結果和已識別的問題](assets/health-checks/dashboard.png)

## 瞭解儀表板 {#understanding-dashboard}

健康情況檢查儀表板提供三個方面的資訊來協助您評估實作的狀態。

### 物件已評估 {#objects-evaluated}

**[!UICONTROL Objects evaluated]**&#x200B;區段顯示已掃描的結構描述和身分識別名稱空間總數，以及每個類別找到多少問題。 這可讓您快速檢視沙箱中設定問題的範圍和嚴重性。

### 掃描結果 {#scan-results}

**[!UICONTROL Scan results]**&#x200B;區段顯示失敗的檢查數目。 失敗的檢查表示一或多個健康狀態檢查偵測到需要注意的組態問題。 上次於&#x200B;**時間戳記完成之**&#x200B;每日健康情況掃描會顯示最近一次掃描的執行時間。

### 已識別的問題 {#identified-issues}

**[!UICONTROL Identified issues]**&#x200B;區段會顯示每個健康狀態檢查的卡片。 每個卡片都會顯示：

* 健康情況檢查名稱和問題的簡短說明。
* 發現的問題數，或不存在問題的確認。
* 顯示檢查通過或需要注意的狀態指示器。

選取任一卡片以探索該健康狀態檢查的詳細資訊。

## 可用的健康狀態檢查 {#available-health-checks}

健康狀態檢查目前會評估架構和身分設定的五個基本區域。 這些檢查會針對整個平台中最具影響力的資料模型問題。

### 身分欄位驗證 {#identity-field-validation}

掃描以確保識別欄位具有最小和最大長度限制，以及資料整合的規則運算式模式規則。

| 詳細資料 | 說明 |
| --- | --- |
| **問題** | 標籤為身分的欄位缺少最小/最大長度或模式驗證。 |
| **影響** | 若未驗證，記憶體值可以輸入[!UICONTROL Identity Service]。 例如「0」、「Guest」或大小寫不符的值（例如「xyz123」與「XYZ123」）會損害分段與啟用期間所組裝之設定檔的完整性。 |
| **修正** | 在標籤為身分的自訂欄位上設定最小/最大長度和模式限制。 使用規則運算式可強制實施僅數字、大寫或小寫或特定字元組合等規則。 |

選取&#x200B;**[!UICONTROL Identity Field Validation]**&#x200B;卡片時，右側會開啟詳細資料面板。 面板會顯示：

* **[!UICONTROL Description]**：掃描以確保身分識別欄位具有最小/最大長度，以及資料完整性規則運算式模式規則。 列出受影響的方案和欄位。
* **[!UICONTROL Impact]**：如果結構描述中的身分欄位沒有設定上下限長度和模式驗證，可能會導致資料不一致，進而影響資料的完整性和品質。
* **[!UICONTROL General areas of impact]**： [!UICONTROL Identity Service]中的低品質識別碼；不可靠的彙整。
* **[!UICONTROL Experience League Documentation]**：資料模型最佳作法的連結。
* **[!UICONTROL Affected Schemas]**：受影響的結構描述清單，每個結構描述都有一個擴充功能，可檢視更多詳細資料和開啟結構描述的連結。

![身分欄位驗證詳細資訊面板，顯示說明、影響和受影響的結構描述](assets/health-checks/identity-field-validation-detail.png)

如需詳細資訊，請參閱結構描述最佳實務檔案中的[資料完整性提示](/help/xdm/schema/best-practices.md#data-integrity-tips)。

### 身分識別圖連結規則 {#identity-graph-linking-rules}

驗證身分圖表連結規則是否已針對沙箱進行設定，以防止摺疊的設定檔。

| 詳細資料 | 說明 |
| --- | --- |
| **問題** | 未針對此沙箱設定身分圖表連結規則。 |
| **影響** | 如果沒有連結規則，多個不同的設定檔可以合併為單一設定檔（圖表收合）。 來自共用裝置或非唯一身分的特定資料可能會觸發不需要的合併，導致不正確的個人化。 |
| **修正** | 導覽至&#x200B;**[!UICONTROL Identities]**&#x200B;功能表，選取&#x200B;**[!UICONTROL Settings]**，然後選取每個圖形的至少一個唯一識別。 如此可啟用身分圖表連結規則，並防止設定檔摺疊。 |

選取&#x200B;**[!UICONTROL Identity Graph Linking Rules]**&#x200B;卡片時，右側會開啟詳細資料面板。 面板會顯示：

* **[!UICONTROL Description]**：驗證是否已設定適當的連結規則，以防止摺疊的設定檔。 它會顯示目前的規則狀態和每個圖表的不重複身分。
* **[!UICONTROL Impact]**：如果未設定身分圖表連結規則，某些資料可能會嘗試將多個不同的設定檔合併為單一設定檔。 若要防止不想要的合併，應使用透過身分圖表連結規則提供的設定。
* **[!UICONTROL General areas of impact]**：摺疊或合併的設定檔。
* **[!UICONTROL Experience League Documentation]**：身分圖表連結規則總覽的連結，以取得詳細資訊。
* **[!UICONTROL Configure linking rules]**：檢查失敗時，會出現一個按鈕，讓您可直接從面板設定連結規則。

![身分圖表連結規則詳細資訊面板，顯示說明、影響和設定連結規則按鈕](assets/health-checks/identity-graph-linking-detail.png)

如需詳細資訊，請參閱[身分圖表連結規則總覽](/help/identity-service/identity-graph-linking-rules/overview.md)和[實作指南](/help/identity-service/identity-graph-linking-rules/implementation-guide.md)。

### 人員與非人員身分設定 {#people-non-people-identity}

驗證結構描述類別中人員與非人員身分型別的正確使用。

| 詳細資料 | 說明 |
| --- | --- |
| **問題** | 非人員識別碼用於個人設定檔或體驗事件類別結構描述，或人員識別碼用於查詢結構描述。 |
| **影響** | 個人資料結構描述上的非人員識別碼不參與身分圖表，這會導致不完整的身分解析。 查閱結構描述上的人員識別碼會使設定檔計數膨脹，使資料不符合查閱使用案例的資格。 這兩個案例都可能讓未來的產品增強功能破壞您的實作。 |
| **修正** | 檢閱已標幟的結構描述並更正身分型別指派。 儘可能從個人設定檔結構描述中移除非個人識別碼。 對於資料集已使用的結構描述，請參閱[結構描述演化規則](/help/xdm/schema/composition.md#evolution)。 |

選取&#x200B;**[!UICONTROL People & Non-People Identity Config]**&#x200B;卡片時，右側會開啟詳細資料面板。 面板會顯示：

* **[!UICONTROL Description]**：驗證跨結構描述類別正確使用了身分型別。 列出設定錯誤的結構描述，並醒目提示錯誤的指派。
* **[!UICONTROL Impact]**：如果非個人實體獲得個人身分，將誇大設定檔計數，並使此資料不符合查閱資格。 如果以非個人身分識別個人實體，資料將無法用於串流或邊緣劃分。
* **[!UICONTROL General areas of impact]**：不完整的身分圖表；膨脹的設定檔計數；查詢誤用。
* **[!UICONTROL Affected Schemas]**：有問題的結構描述清單。 展開結構描述列，以檢視每個設定錯誤的路徑、身分名稱和結構描述型別。 使用連結圖示開啟方案。

![人員與非人員身分設定詳細資料面板，顯示說明、影響以及包含可擴充列的受影響結構描述](assets/health-checks/people-non-people-identity-detail.png)

如需詳細資訊，請參閱[身分型別檔案](/help/identity-service/features/namespaces.md#identity-type)和[結構描述最佳實務](/help/xdm/schema/best-practices.md)。

### 自訂身分名稱空間說明 {#namespace-missing-description}

掃描以確保自訂身分名稱空間中繼資料和說明完整。

| 詳細資料 | 說明 |
| --- | --- |
| **問題** | 自訂身分名稱空間缺少其說明欄位。 |
| **影響** | 缺少說明可能會在使用和偵錯期間導致混淆。 |
| **修正** | 填寫說明欄位以記錄每個自訂名稱空間。 包括驗證條件（最小/最大長度、模式）和識別外部來源系統建立這些身分的生命週期資訊。 |

選取&#x200B;**[!UICONTROL Custom Identity Namespace Description]**&#x200B;卡片時，右側會開啟詳細資料面板。 面板會顯示：

* **[!UICONTROL Description]**：掃描以確保名稱空間中繼資料和說明完整。 顯示具有空白說明欄位的名稱空間和擁有者。
* **[!UICONTROL Impact]**：在自訂身分名稱空間上設定說明，可提供每個名稱空間用途的內容，進而提高清晰度。 這有助於團隊成員和利害關係人快速瞭解每個名稱空間的功能，而不會混淆。
* **[!UICONTROL General areas of impact]**：偵錯或使用方式混淆；不清楚的驗證意圖。
* **[!UICONTROL Experience League Documentation]**：建立自訂名稱空間的連結，以取得進一步資訊。
* **[!UICONTROL Affected namespaces]**：遺失說明的自訂身分名稱空間清單。 使用每個名稱空間旁的連結圖示來檢視或編輯。

![自訂身分名稱空間描述詳細資訊面板，顯示描述、影響和受影響的名稱空間清單](assets/health-checks/custom-namespace-description-detail.png)

如需詳細資訊，請參閱有關[建立自訂名稱空間](/help/identity-service/features/namespaces.md#create-namespaces)的檔案。

### 已棄用的身分名稱空間 {#deprecated-namespace}

偵測應標示為要清理的過時或未使用的身分名稱空間。

| 詳細資料 | 說明 |
| --- | --- |
| **問題** | 過時的身分名稱空間不會標示為已過時。 |
| **影響** | 未使用或過時的名稱空間會造成使用中內容的混淆，並會增加身分欄位錯誤標籤的風險。 |
| **修正** | 重新命名未使用的名稱空間以包含「不要使用」前置詞（例如「不要使用 — [原始名稱]」）。 Adobe Experience Platform目前不支援名稱空間刪除，因此建議重新命名。 |

選取&#x200B;**[!UICONTROL Deprecated Identity Namespace]**&#x200B;卡片時，右側會開啟詳細資料面板。 面板會顯示：

* **[!UICONTROL Description]**：偵測過時或未使用的身分名稱空間以進行清除。 列出具有上次使用時間戳記或結構描述參考的未使用名稱空間。
* **[!UICONTROL Impact]**：未在任何結構描述中使用的身分名稱空間應該標示為要移除，方法是在其名稱中新增「DEPRECATED」或「DO NOT USE」標籤。 目前不支援刪除身分名稱空間。
* **[!UICONTROL General areas of impact]**：混淆和標籤錯誤的風險。
* **[!UICONTROL Experience League Documentation]**：舊版身分識別名稱空間的連結，以取得進一步檔案。
* **[!UICONTROL Affected namespaces]**：過時或未使用的身分名稱空間清單。 使用每個名稱空間旁的連結圖示來檢視或管理名稱空間。

![已棄用的身分名稱空間詳細資料面板，顯示說明、影響和受影響的名稱空間清單](assets/health-checks/deprecated-namespace-detail.png)

如需詳細資訊，請參閱有關過時名稱空間的[Experience Cloud知識庫文章](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-18155){target="_blank"}。

## 後續步驟 {#next-steps}

檢閱完健康情況檢查結果後，請探索下列資源，以加深您的瞭解：

* 瞭解設計可靠資料模型的[結構描述最佳做法](/help/xdm/schema/best-practices.md)。
* 瞭解[身分圖表連結規則](/help/identity-service/identity-graph-linking-rules/overview.md)以防止設定檔摺疊。
* 檢閱[身分識別名稱空間檔案](/help/identity-service/features/namespaces.md)，以取得名稱空間管理的最佳實務。
* 探索其他[執行及操作工具](/help/run-and-operate/overview.md) （包括[[!UICONTROL Job Schedules]](/help/run-and-operate/job-schedules.md)）以取得批次作業可見度。
