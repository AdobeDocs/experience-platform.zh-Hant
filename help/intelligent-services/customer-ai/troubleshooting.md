---
keywords: Experience Platform；快速入門；customer ai；熱門主題；customer ai輸入；customer ai輸出；customer ai疑難排解；customer ai錯誤
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Customer AI錯誤疑難排解
description: 尋找Customer AI中常見錯誤的答案。
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: d88f9691f7a2affc7737e1adab75fc441e3f7e4f
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 1%

---

# Customer AI錯誤疑難排解

當模型訓練、評分和設定失敗時，Customer AI會顯示錯誤。 在 **[!UICONTROL 服務例項]** 區段，欄 **[!UICONTROL 上次執行狀態]** 顯示下列其中一則訊息： **[!UICONTROL 成功]**， **[!UICONTROL 訓練問題]**、和 **[!UICONTROL 已失敗]**.

![上次執行狀態](./images/errors/last-run-status.png)

在 **[!UICONTROL 已失敗]** 或 **[!UICONTROL 訓練問題]** 顯示，您可以選取「執行」狀態以開啟側面板。 側面板包含您的 **[!UICONTROL 上次執行狀態]** 和 **[!UICONTROL 上次執行詳細資料]**. **[!UICONTROL 上次執行詳細資料]** 包含執行失敗原因的資訊。 如果Customer AI無法提供您錯誤的詳細資訊，請聯絡支援人員並提供錯誤代碼。

<img src="./images/errors/last-run-details.png" width="300" /><br />

## 無法無痕存取Chrome中的Customer AI

由於Google Chrome無痕模式安全性設定有所更新，導致Google Chrome無痕模式中的載入錯誤出現。 這個問題正由Chrome積極處理，以讓experience.adobe.com成為信任的網域。

<img src="./images/errors/error.PNG" width="500" /><br />

### 建議的修正

若要解決此問題，您需要將experience.adobe.com新增為可隨時使用Cookie的網站。 首先，瀏覽至 **chrome://settings/cookies**. 接下來，向下捲動至 **自訂行為** 區段，然後選取 **新增** 按鈕（在「可隨時使用Cookie的網站」旁）。 在出現的彈出視窗中，複製並貼上 `[*.]experience.adobe.com` 然後選取 **包含第三方Cookie** [在此網站上]核取方塊。 完成後，選取 **新增** 和重新載入無痕的Customer AI。

![建議的修正](./images/errors/cookies2.gif)

## 模型品質不良

如果您收到錯誤&quot;[!UICONTROL 模型品質不良。 建議您使用修改後的設定來建立新的應用程式]「。 請依照下列建議的步驟進行疑難排解。

<img src="./images/errors/model-quality.png" width="300" /><br />

### 建議的修正

「模型品質不良」表示模型精度不在可接受的範圍內。 Customer AI無法在訓練後建立可靠的模型且AUC （ROC曲線下的區域） &lt; 0.65。 若要修正錯誤，建議您變更其中一個設定引數，然後重新執行訓練。

首先檢查資料的準確性。 您的資料包含預測結果所需的必要欄位非常重要。

- 檢查您的資料集是否有最新日期。 Customer AI一律會假設資料在模型觸發時處於最新狀態。
- 檢查您所定義的預測與適用性視窗中是否有遺漏的資料。 您的資料必須完整無缺。 此外，請確保您的資料集符合 [Customer AI歷史資料需求](./data-requirements.md#data-requirements).
- 在您的結構欄位屬性中，檢查商務、應用程式、網頁和搜尋中是否有缺少的資料。

如果您的資料似乎不是問題，請嘗試變更適用人口條件，將模型限製為特定設定檔(例如， `_experience.analytics.customDimensions.eVars.eVar142` 存在於過去56天內)。 這會限制訓練時段中所使用資料的母體及大小。

如果限制適用人口無效或無法進行，請變更您的預測期間。

- 請嘗試將預測時段變更為7天，並檢視錯誤是否持續發生。 如果錯誤不再發生，表示您可能沒有足夠的資料可供定義的預測時段使用。

### 錯誤

| 錯誤代碼 | 標題 | 訊息範本 | 訊息範例 |
| ---------- | ----- | ---------------- | --------------- |
| 400 | 目標不足 | 使用者太少({{actual_num_samples}} in total) meeting the prediction goal definition from {{outcome_window_start}} to {{outcome_window_end}}. We require at least {{min_num_samples}} 具有合格事件以建立模型的使用者。 <br><br>建議的解決方案： <br><br>1. 檢查資料可用性 <br>2. 減少預測目標時間範圍 <br>3. 修改預測目標定義以包含更多使用者（錯誤碼：VALIDATION-400 NOT_ENOUGH_OBJECTIVE） | 符合2020-04-01到2021-04-01預測目標定義的使用者太少（總共200名）。 我們至少需要500名具有合格活動的使用者來建立模型。 <br><br>建議的解決方案： <br>1. 檢查資料可用性 <br>2. 減少預測目標時間範圍 <br>3. 修改預測目標定義以包含更多使用者。 （錯誤碼：VALIDATION-400 NOT_ENOUGH_OBJECTIVE） |
| 401 | 人口不足 | 符合資格的使用者太少({{actual_num_samples}} in total) from {{eligibility_window_start}} to {{eligibility_window_end}}. We require at least {{min_num_samples}} 符合建立模型的使用者。 <br><br>建議的解決方案： <br>1. 檢查資料可用性 <br>2. 如果提供合格的母體定義，請縮短合格篩選時間範圍3。 如果未提供合格的母體定義，請嘗試新增一個（錯誤代碼：VALIDATION-401 NOT_ENOUGH_POPULATION） | 從2020-04-01到2021-04-01的合格使用者太少（總共200個）。 我們至少需要500名符合資格的使用者才能建立模型。<br><br>建議的解決方案：<br>1. 檢查資料可用性<br>2. 如果提供合格的母體定義，請縮短合格篩選的時間範圍。<br>3.如果未提供合格的母體定義，請嘗試新增一個。 （錯誤碼：VALIDATION-401 NOT_ENOUGH_POPULATION） |
| 402 | 模型錯誤 | 我們無法使用目前的輸入資料集和設定產生高品質的模型。 <br><br>建議包括： <br>1. 修改您的設定以新增合格的母體定義。 <br>2. 使用其他資料來源來改善模型品質 <br>3. 新增自訂事件，在模型中加入更多資料（錯誤碼：VALIDATION-402 BAD_MODEL） | 我們無法使用目前的輸入資料集和設定產生高品質的模型。 <br><br>建議包括： <br>1. 請考慮修改您的設定以新增合格的母體定義。 <br>2. 請考慮使用其他資料來源來改善模型品質。 （錯誤碼：VALIDATION-402 BAD_MODEL） |
| 403 | 不符合資格的分數 | 此分數分佈與預期有太多差異。 <br><br>建議包括： <br>1. 請確認模型已使用最新資料進行訓練，否則請考慮重新訓練您的模型。 <br>2. 請確定評分任務中沒有資料問題（例如遺失資料/資料延遲）。 （錯誤碼：VALIDATION-403 INELIGIBLE_SCORES） | 此分數分佈與預期有太多差異。 <br><br>建議包括： <br>1. 請確認模型已使用最新資料進行訓練，否則請考慮重新訓練您的模型。 <br>2. 請確定評分任務中沒有資料問題（例如遺失資料/資料延遲）。 （錯誤碼：VALIDATION-403 INELIGIBLE_SCORES） |
| 405 | 無評分資料 | 沒有可用於評分的使用者行為或設定檔資料 {{eligibility_window_start}} to {{eligibility_window_end}}請檢查資料，以確保定期更新。 （錯誤碼：VALIDATION-405 NO_SCORING_DATA） | 從2020-04-01到2021-04-01沒有可用於評分的使用者行為或設定檔資料。 請檢查資料，以確保定期更新。 （錯誤碼：VALIDATION-405 NO_SCORING_DATA） |
| 407 | 歷史事件資料不足 | 沒有足夠的資料可建置模型。 從2020-04-01到2021-04-01，只有90天的資料。 <br><br>我們需要120天的最新資料。 如需詳細資訊，請參閱資料需求檔案。 <br><br>建議的解決方案： <br>1. 檢查資料可用性 <br>2. 減少預測目標時間範圍 <br>3. 如果提供合格的母體定義，請縮短合格篩選的時間範圍 <br>4. 如果未提供合格的母體定義，請嘗試新增一個（錯誤代碼：VALIDATION-407 NOT_ENOUGH_HISTORICAL_EVENT_DATA） | 沒有足夠的資料可建置模型。 從2020-04-01到2021-04-01，只有90天的資料。<br><br>我們需要120天的最新資料。 如需詳細資訊，請參閱資料需求檔案。<br><br>建議的解決方案：<br>1. 檢查資料可用性。<br>2. 縮短預測目標時間範圍。<br>3.如果提供合格的母體定義，請縮短合格篩選的時間範圍。<br>4.如果未提供合格的母體定義，請嘗試新增一個。 （錯誤碼：VALIDATION-407 NOT_ENOUGH_HISTORICAL_EVENT_DATA） |
| 408 | 沒有符合資格的最近資料 | 中沒有符合資格的使用者的使用者行為資料。 {{data_days}} days prior to {{etl_window_end}}. 請檢查資料集，確保會定期更新。 （錯誤碼：VALIDATION-408 NO_RECENT_DATA_FOR_ELIGIBLE_POPULATION） | 2021-04-01之前60天內沒有符合資格的使用者的使用者行為資料。 請檢查資料集，確保會定期更新。 （錯誤碼：VALIDATION-408 NO_RECENT_DATA_FOR_ELIGIBLE_POPULATION） |
| 409 | 無目標 | 沒有符合來自的預測目標定義的使用者 {{outcome_window_start}} to {{outcome_window_end}}. We require at least {{min_num_samples}} 具有合格事件以建立模型的使用者。 <br><br>建議的解決方案： <br>1. 檢查資料可用性 <br>2. 修改預測目標定義（錯誤碼：VALIDATION-409 NO_OBJECTIVE） | 2020-04-01到2021-04-01期間沒有符合預測目標定義的使用者。 我們至少需要500名具有合格活動的使用者來建立模型。 <br><br>建議的解決方案：<br>1. 檢查資料可用性。<br>2. 修改預測目標定義。 （錯誤碼：VALIDATION-409 NO_OBJECTIVE） |
| 410 | 無母體 | 沒有符合資格的使用者來自 {{eligibility_window_start}} to {{eligibility_window_end}}. We require at least {{min_num_samples}} 符合建立模型的使用者。 <br><br>建議的解決方案： <br>1. 檢查資料可用性 <br>2. 若提供合格的母體定義，請修改條件或增加合格篩選的時間範圍（錯誤代碼：VALIDATION-410 NO_POPULATION） | 2020-04-01到2021-04-01沒有符合資格的使用者。 我們至少需要500名符合資格的使用者才能建立模型。 <br><br>建議的解決方案：<br>1. 檢查資料可用性。 <br> 2. 如果提供合格母體定義，請修改條件或增加合格篩選的時間範圍。 （錯誤碼：VALIDATION-410 NO_POPULATION） |
| 411 | ETL之後沒有輸入資料 | 模型沒有可供之間使用的使用者行為或設定檔資料 {{etl_start_date}} and {{etl_end_date}}. 請確定資料集有足夠的資料。 （錯誤碼：VALIDATION-411 NO_INPUT_DATA_AFTER_ETL） | 在2020-04-01和2021-04-01之間沒有可供模型使用的使用者行為或設定檔資料。 請確定資料集有足夠的資料。 （錯誤碼：VALIDATION-411 NO_INPUT_DATA_AFTER_ETL） |
| 412 | ETL之後沒有事件 | 模型沒有可供之間使用的使用者行為資料 {{etl_start_date}} and {{etl_end_date}}. 請確定資料集有足夠的資料。 | 在2020-04-01和2021-04-01之間沒有模型可用的使用者行為資料。 請確定資料集有足夠的資料。 （錯誤碼：VALIDATION-412 NO_EVENT_DATA_AFTER_ETL） |
| 413 | 目標中的單一值 | CustomerAI要求資料集必須同時具有符合及不符合預測目標定義的事件。 輸入資料集只包含符合以下條件的事件： {{etl_window_start}} and {{etl_window_end}}. <br><br>建議的解決方案： <br>1. 修改預測目標定義 <br>2. 驗證資料完整性，或使用包含預測目標之不合格事件範例的其他專案（錯誤代碼：VALIDATION-413 SINGLE_VALUE_IN_OBJECTIVE） | CustomerAI要求資料集必須同時具有符合及不符合預測目標定義的事件。 輸入資料集只包含介於2020-04-01和2021-04-01之間的合格事件。<br><br>建議的解決方案：<br>1. 修改預測目標定義。<br>2. 驗證資料完整度或使用包含預測目標之不合格事件範例的不同專案。 （錯誤碼：VALIDATION-413 SINGLE_VALUE_IN_OBJECTIVE） |
| 414 | 無影響因素 | 影響因子模型產生非預期的輸出。 建議您使用修改後的設定來建立新的應用程式。 （錯誤碼：VALIDATION-414 NO_INFLUENCE_FACTORS） | 影響因子模型產生非預期的輸出。 建議您使用修改後的設定來建立新的應用程式。 （錯誤碼：VALIDATION-414 NO_INFLUENCE_FACTORS） |