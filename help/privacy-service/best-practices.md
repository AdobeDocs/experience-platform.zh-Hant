---
title: Privacy Service的最佳實務
description: 瞭解如何遵循這些最佳使用准則，以減少處理時間以及完成隱私權請求時組織產生的成本。
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Privacy Service的最佳實務

當客戶希望從您的資料存放區存取或刪除其個人資料時，請使用Privacy Service自動遵守資料隱私權法規。 為了滿足這些不斷變化的業務需求，Privacy Service提供RESTful API和UI，以便在整個Adobe Experience Cloud應用程式中提交客戶資料的存取和刪除請求。

本指南概述在管理客戶資料請求時，有效處理隱私權請求及最佳化完成回應時間的最佳實務。

## 快速入門 {#getting-started}

本指南需要您實際瞭解 [Privacy Service](./home.md) 以及它如何讓您管理來自Adobe Experience Cloud應用程式中資料主體（客戶）的存取和刪除請求。 建議您也閱讀以下指南： [在UI中建立隱私權工作請求](./ui/user-guide.md#create-a-new-privacy-job-request) 或 [API](./api/overview.md)，並瞭解如何以程式設計方式執行這些操作。

## 先決條件 {#prerequisites}

Adobe Experience Platform Privacy Service的存取權可透過Adobe Admin Console中精細的角色型許可權加以控制。 您需要產品設定檔中的相關許可權，才能使用Privacy Service UI和API中的特定功能。 如果您需要其他許可權，請聯絡系統管理員。

管理員可參考指南，網址為 [管理Privacy Service的許可權](./permissions.md) 以取得詳細資訊。

## 隱私權工作建立指導方針 {#creation-guidelines}

若要簡化請求處理流程並縮短回應時間，在建立隱私權工作時，請考量下列准則。 這同時適用於API和UI方法。

1. **最大化的每個請求資料主體：** 包括儘可能多的資料主體，每個請求最多1000個。
2. **群組ID以提升效率：** 為每個要求中的單一資料主體將多個ID分組（最多九個）。 此 **ID可來自相同請求中的不同Adobe服務**.
3. **結合存取與刪除工作：** 如果資料主體有需要，可在單一請求中加入「存取」和「刪除」工作型別。
4. **僅包含必要的產品：** 僅包含所需或授權的產品。 其他產品可能會延長處理時間並增加成本。

## 監視隱私權工作狀態 {#monitor-status}

為了有效監視隱私權工作並檢查其狀態，Privacy Service提供了三種方法。 為了監控效率和生產力，以下列出可用的方法。 每種方法都包含改善您體驗的最佳實務准則，隨後是結合所有方法的理想案例範例。

### 接收即時通知 {#real-time-notifications}

**I/O事件** 透過狀態事件提供近乎即時的狀態監控。 這是最有效率的方法，因為它不需要實作輪詢機制並產生額外的API流量。

**Recommendations：**

- **Webhook設定：** 設定webhook以便在已提交工作的狀態發生變更時接收推播通知。 這有助於即時監視。
- **通知：** 在工作與產品層級使用通知來協助監控要求的進度。

請參閱以下檔案： [訂閱Privacy Service事件](./privacy-events.md) 以取得有關設定Privacy Service通知的事件註冊，以及如何解譯通知裝載的說明。

### 根據篩選器擷取所有工作 {#retrieve-filtered-responses-for-all-jobs}

若要根據任何指定的篩選器擷取您的所有隱私權工作資料， **執行GET要求給 `/jobs` 端點**. 此API呼叫有助於提供大型工作ID集之目前工作狀態的高層級檢視，且只有單一請求。 它確實缺乏詳細的產品回應，但可使用以下網址找到： [`/jobs/{jobID}` 端點](#retrieve-detailed-responses-for-specific-jobs).

向傳送的GET要求 `/jobs` 端點最適合用來收集或比較大量工作ID的狀態資料，但 **非** 用於定期輪詢型別活動。

**Recommendations：**

- **查詢引數：** 使用特定篩選器來縮小結果的範圍，例如：資料範圍、法規型別和狀態（處理、完成等）。

您可以透過Privacy ServiceUI檢視貴組織中所有目前隱私權工作的清單。 請參閱 [管理UI檔案中的隱私權工作](./ui/user-guide.md#job-requests) 有關如何篩選工作請求清單的資訊。 或者，請參閱以下檔案： [在Privacy ServiceAPI中使用/job端點](./api/privacy-jobs.md).

Privacy Service API檔案包含有關以下專案的詳細資訊： [可用的查詢引數篩選器](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### 擷取單一作業的詳細回應 {#retrieve-detailed-responses-for-specific-jobs}

若要擷取單一作業的詳細回應， **對/jobs/執行GET要求{jobID} 端點**. 此方法旨在進行更深入的資訊收集，例如產品專屬回應和成功訊息。 呼叫此端點是檢視哪些產品已回應以及哪些產品仍在等候處理（儘管仍在等候處理）的最佳方式 **非** 用於定期輪詢活動。

請參閱 `/jobs/{JOB_ID}` 端點檔案，以瞭解詳細資訊 [如何檢查特定工作的狀態](./api/privacy-jobs.md#check-status).

### 理想案例範例 {#ideal-scenario}

使用webhook，系統就能自動更新記錄，並在請求的ID群組完成時提供報表或警報。 如果工作仍未完成，系統會向Privacy Service API發出GET要求，擷取這些工作狀態 `/jobs` 端點，並提供清單的高層級更新。

如果特定工作仍在擱置中，或已傳回錯誤，您可以向擷取包含GET請求的詳細回應 `/job/{jobId}` 端點。

## 存取要求資料 {#access-request-data}

請求資料主體資訊時，每個服務都會以與其儲存和使用資料方式一致的格式傳回資料。 所有服務都完成要求後，工作詳細資料中會提供.ZIP封存檔案URL，以便下載此資料。 請參閱疑難排解指南，瞭解有關的資訊 [如何下載隱私權工作結果](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=en#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F).

以下是與資料封存管理相關的重要備註專案：

- 30天後，所有封存檔案都會從Experience Platform伺服器刪除。 您無法查詢超過30天的客戶資料。
- 封存檔案的結構包括請求中所包含每個產品的資料夾以及其中包含的資料檔案。 如果找不到指定ID的資料，封存檔案或資料夾可能會是空的。
- 先前建立之工作的資料僅可在完成日期後30天記憶體取。 在這之後，資料會從系統中移除，且必須提出新請求。

**Recommendations：**

- **Protect資料封存：** URL和.ZIP檔案都應該受到保護，因為它們可能包含資料主體的個人識別資訊(PII)。

## 技術考量 {#technical-considerations}

完成Privacy Service請求時，應注意某些技術考量事項：

- **資料保留期：** 任何工作群組的最大回顧期間為60天，而查詢的最大時間範圍為30天（起始/終止日期）。
- **閘道逾時：** 請注意，如果您的要求超過60秒，系統可能會從閘道捨棄該要求。
- **錯誤處理：** 徹底檢閱錯誤訊息，並在適當時重新提交請求。 Privacy Service不會在錯誤後自動重新處理工作。
- **瞭解HTTP 429錯誤：** 請熟悉HTTP 429錯誤訊息和緩解問題的必要步驟。 HTTP 429錯誤是「太多請求」的結果。 請參閱 [常見錯誤訊息](./troubleshooting-guide.md#common-error-messages) 疑難排解指南的區段，以取得如何解決問題的詳細資訊。

## 後續步驟

閱讀本檔案後，您現在已具備有效率且有效地使用Privacy Service的必要知識和實務。 接下來，檢視 [疑難排解指南](./troubleshooting-guide.md) 以取得有關Privacy Service常見問題的解答，以及API中常見錯誤的資訊。
