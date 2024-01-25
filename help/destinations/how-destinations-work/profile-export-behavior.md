---
title: 設定檔匯出行為
description: 瞭解在Experience Platform目的地支援的不同整合模式之間，設定檔匯出行為有何不同。
exl-id: 2be62843-0644-41fa-a860-ccd65472562e
source-git-commit: f9917d6a6de81f98b472cff9b41f1526ea51cdae
workflow-type: tm+mt
source-wordcount: '2931'
ht-degree: 0%

---

# 不同目的地型別的設定檔匯出行為

Experience Platform中有多種目的地型別，如下圖所示。 關於會觸發目的地匯出的內容以及匯出中包含的內容，這些目的地的匯出模式稍有不同，如下節後續所述。

>[!IMPORTANT]
>
>本檔案頁面僅說明圖表底部反白連線的設定檔匯出行為。

![目的地圖表型別](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## 串流目的地中的訊息彙總

在深入研究每個目的地型別的特定資訊之前，請務必瞭解訊息彙總的概念， *串流目的地*.

Experience Platform目的地會將資料匯出至API型整合，做為HTTPS呼叫。 一旦目標服務收到其他上游服務的通知，得知批次擷取、串流擷取、批次細分、串流細分或身分圖表變更導致設定檔已更新，資料就會匯出並傳送至串流目標。

設定檔在傳送到目的地API端點之前，會彙總為HTTPS訊息。

取得 [facebook目的地](/help/destinations/catalog/social/facebook.md) 與 *[可設定的彙總](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* 原則為例 — 資料會以彙總方式傳送，目的地服務會擷取設定檔服務上游的所有傳入資料，並在將資料傳送至Facebook之前依下列其中一個專案彙總：

* 記錄數（最多10,000筆）或
* 時間視窗間隔（300秒）

首次符合上述臨界值的任何一項，都會觸發匯出至Facebook的作業。 因此，在 [!DNL Facebook Custom Audiences] 儀表板，您可能會看到以10,000筆記錄增量從Experience Platform傳入的受眾。 您可能會每2-3分鐘看到10,000筆記錄，因為資料的處理與彙總速度比300秒匯出間隔還快，而且傳送速度也更快，所以在處理所有記錄之前，大約每2-3分鐘就會傳送一次。 如果記錄不足以組成10,000個批次，則符合時間範圍臨界值時將會傳送目前的記錄數，因此您也可能會看到傳送至Facebook的較小批次。

再舉一例，請考慮 [HTTP API目的地](/help/destinations/catalog/streaming/http-destination.md)，具有 *[最大努力彙總](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* 原則，具有 `maxUsersPerRequest: 10`. 這表示在為此目的地觸發HTTP呼叫之前，最多會彙總10個設定檔，但Experience Platform會在目的地服務收到來自上游服務的更新重新評估資訊時，立即嘗試將設定檔分派至目的地。

可設定彙總原則，而目的地開發人員可決定如何設定彙總原則，以最符合下游API端點的速率限制。 深入瞭解 [彙總原則](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) 在Destination SDK檔案中。

## 串流設定檔匯出（企業）目的地 {#streaming-profile-destinations}

>[!IMPORTANT]
>
> 企業目的地僅適用於 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。

此 [企業目的地](/help/destinations/destination-types.md#streaming-profile-export) Experience Platform中有Amazon Kinesis、Azure事件中樞和HTTP API。

Experience Platform會最佳化將設定檔匯出至您企業目的地的行為，以便僅在對象資格或其他重大事件後發生設定檔的相關更新時，將資料匯出至您的API端點。 在下列情況下，設定檔會匯出至您的目的地：

* 設定檔更新是由中的變更所決定 [對象會籍](/help/xdm/field-groups/profile/segmentation.md) 至少有一個對應至目的地的對象。 例如，設定檔已符合對應至目的地的其中一個對象的資格，或已退出對應至目的地的其中一個對象。
* 設定檔更新是由 [身分對應](/help/xdm/field-groups/profile/identitymap.md). 例如，已符合對應至目的地之其中一個對象資格的設定檔，已在身分對應屬性中新增身分。
* 設定檔更新是由對應到目的地的至少一個屬性的變更所決定。 例如，會將對應步驟中對應至目的地的其中一個屬性新增至設定檔。

在上述所有情況下，只有已發生相關更新的設定檔才會匯出至您的目的地。 例如，如果對應至目的地流程的受眾有一百個成員，且有五個新設定檔符合區段的資格，則匯出至您的目的地的作業將以漸進方式進行，且僅包含五個新設定檔。

請注意，無論變更位於何處，所有對映屬性都會匯出為設定檔。 因此，在上述範例中，將會匯出這五個新設定檔的所有對應屬性，即使屬性本身並未變更亦然。

### 決定資料匯出的因素及匯出中包含的因素

針對針對指定設定檔匯出的資料，瞭解以下兩個不同的概念是很重要的 *決定資料匯出至企業目的地的因素* 和 *哪些資料包含在匯出中*.

| 決定目的地匯出的因素 | 目的地匯出包含的內容 |
|---------|----------|
| <ul><li>對應的屬性和受眾可作為目的地匯出的提示。 這表示如果任何對應的對象變更狀態(從 `null` 至 `realized` 或從 `realized` 至 `exiting`)或更新任何對應的屬性，就會開始匯出目的地。</li><li>由於身分目前無法對應至企業目的地，因此特定設定檔上任何身分的變更也會決定目的地匯出專案。</li><li>屬性的變更定義為屬性上的任何更新，無論其是否為相同的值。 這表示即使值本身並未變更，屬性上的覆寫也會視為變更。</li></ul> | <ul><li>此 `segmentMembership` 物件包含啟動資料流中對應的對象，其設定檔的狀態已隨著資格或對象退出事件而變更。 請注意，如果其他未對應對象屬於相同對象，則設定檔符合資格的對象可以屬於目的地匯出的一部分 [合併原則](/help/profile/merge-policies/overview.md) 對象在啟動資料流中的對應方式。 </li><li>中的所有身分 `identityMap` 也包括物件(Experience Platform目前不支援企業目的地中的身分對應)。</li><li>目的地匯出僅包含對應的屬性。</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>將設定檔啟用至目的地時，企業目的地會串流回填資料。 這表示在設定啟用工作流程至目的地後的首次資料匯出將包含符合啟用的對象資格的設定檔，然後再將對象對應至目的地。

>[!BEGINSHADEBOX]

例如，將此資料流視為HTTP目的地，其中在資料流中選取了三個對象，且四個屬性對應至目的地。

![企業目的地資料流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

要判斷匯出至目的地的設定檔是否符合「 」或「 」其中之一， *三個對應的區段*. 不過，在資料匯出中，在 `segmentMembership` 物件，如果特定設定檔為其他未對應對象的成員，且這些對象與觸發匯出的對象共用相同的合併原則，則這些對象可能會出現。 如果設定檔符合 **擁有DeLorean Cars的客戶** 對象，但也是 **觀看「回到未來」的電影** 和 **科幻迷** 區段，則其他這兩個對象也會出現在 `segmentMembership` 匯出的物件，即使這些物件未在資料流中對映，只要它們與共用相同的合併原則 **擁有DeLorean Cars的客戶** 區段。

從設定檔屬性的角度來看，對上述四個對應屬性所做的任何變更將決定目的地匯出，而且設定檔上存在的四個對應屬性中的任何一個都會出現在資料匯出中。

>[!ENDSHADEBOX]

>[!TIP]
>
> 您可在以下連結中檢視匯出至各種企業目的地的資料範例： [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data)， [Azure事件中樞](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data)、和 [HTTP API](/help/destinations/catalog/streaming/http-destination.md#exported-data) 目的地檔案頁面。

## 串流API型目的地 {#streaming-api-based-destinations}

適用於串流目的地(例如Facebook、Trade Desk)和其他以API為基礎的整合，其設定檔匯出行為與前述企業目的地的行為非常類似。

串流目的地的範例為屬於 [社交和廣告類別](/help/destinations/destination-types.md#categories) 在目錄中。

Experience Platform會最佳化將設定檔匯出至串流目的地的行為，以便在對象資格或其他重大事件後發生設定檔的相關更新時，僅將資料匯出至串流API型目的地。 在下列情況下，設定檔會匯出至您的目的地：

* 設定檔更新是由中的變更所決定 [對象會籍](/help/xdm/field-groups/profile/segmentation.md) 至少有一個對應至目的地的對象。 例如，設定檔已符合對應至目的地的其中一個對象的資格，或已退出對應至目的地的其中一個對象。
* 設定檔更新是由 [身分對應](/help/xdm/field-groups/profile/identitymap.md) 適用於標示要匯出給此目的地執行個體的身分名稱空間。 例如，已符合對應至目的地之其中一個對象資格的設定檔，已在身分對應屬性中新增身分。
* 設定檔更新是由對應到目的地的至少一個屬性的變更所決定。 例如，會將對應步驟中對應至目的地的其中一個屬性新增至設定檔。
* 在設定自動同意執行且設定檔選擇退出時，設定檔的同意變更。 自動同意執行會將對象退出事件傳送到目的地，因此設定檔不會包含在目的地的任何目標定位中。

在上述所有情況下，只有已發生相關更新的設定檔才會匯出至您的目的地。 例如，如果對應至目的地流程的受眾有一百個成員，且有五個新設定檔符合區段的資格，則匯出至您的目的地的作業將以漸進方式進行，且僅包含五個新設定檔。

請注意，無論變更位於何處，所有對映屬性都會匯出為設定檔。 因此，在上述範例中，將會匯出這五個新設定檔的所有對應屬性，即使屬性本身並未變更亦然。

### 決定資料匯出的因素及匯出中包含的因素

針對指定設定檔匯出的資料，請務必了解決定匯出至串流API目的地的資料以及匯出中包含哪些資料的兩個不同概念。

| 決定目的地匯出的因素 | 目的地匯出包含的內容 |
|---------|----------|
| <ul><li>對應的屬性和受眾可作為目的地匯出的提示。 這表示如果任何對應的對象變更狀態(從 `null` 至 `realized` 或從 `realized` 至 `exiting`)或更新任何對應的屬性，就會開始匯出目的地。</li><li>身分對應中的變更定義為針對新增/移除的身分 [身分圖表](/help/identity-service/features/identity-graph-viewer.md) ，用於對應以供匯出的身分名稱空間。</li><li>屬性的變更定義為對應到目的地的屬性的任何更新。</li></ul> | <ul><li>已對應至目的地並已變更的受眾將包含在 `segmentMembership` 物件。 在某些情況下，它們可能會使用多個呼叫匯出。 此外，在某些情況下，某些未變更的對象可能也會包含在呼叫中。 在任何情況下，僅會匯出對應的對象。</li><li>名稱空間中所有已對應至目的地身分的身分 `identityMap` 物件也包含在內。</li><li>目的地匯出僅包含對應的屬性。</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>將設定檔啟用至目的地時，串流API目的地會串流回填資料。 這表示在設定啟用工作流程至目的地後的首次資料匯出將包含符合啟用的對象資格的設定檔，然後再將對象對應至目的地。

>[!BEGINSHADEBOX]

例如，將此資料流視為串流目的地，其中在資料流中選取了三個對象。

![串流目的地資料流](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

要判斷匯出至目的地的設定檔是否符合（或退出）三個對應區段之一。 如果設定檔符合 **擁有DeLorean Cars的客戶** 區段，則會觸發匯出。 其他對象(**城市 — 達拉斯** 和 **基本網站使用中**)也可以匯出，以防設定檔有對象以可能狀態之一出現(`realized` 或 `exited`)。 未對應的對象(例如 **科幻迷**)將不會匯出。

從設定檔屬性的角度來看，對上方對應的三個屬性所做的任何變更都會決定匯出目的地。

>[!ENDSHADEBOX]

## 批次（以檔案為基礎）目的地 {#file-based-destinations}

將設定檔匯出至 [檔案型目的地](/help/destinations/destination-types.md#file-based) 在Experience Platform中，有三種排程型別（如下所列）和兩種檔案匯出選項（完整或增量檔案）可供您使用。 所有這些設定都是在對象層級上設定，即使有多個對象對應至單一目的地資料流亦然。

* 排程的匯出：設定目的地、新增一或多個區段、選取是否要匯出完整或增量檔案，以及選取每天設定時間或每天幾次應匯出檔案。 例如，下午5點的匯出時間表示任何符合對象資格的設定檔都會在下午5點匯出。
* 區段評估後：每日對象評估工作執行後會立即觸發匯出。 這表示檔案中匯出的設定檔編號儘可能接近區段的最新評估母體。
* 隨選匯出([立即匯出檔案](/help/destinations/ui/export-file-now.md))：根據最新的對象評估工作，除了定期排程的匯出外，還會匯出完整檔案一次。

在上述任何匯出情況下，匯出的檔案都包含符合匯出條件的設定檔，以及您選取為匯出XDM屬性的欄。

>[!TIP]
>
>當串流對象對應至批次目的地時，匯出檔案中的設定檔數量更有可能接近區段中的使用者數量。 這是因為最新的對象評估在更接近匯出時間執行的可能性較高。

### 增量檔案匯出 {#incremental-file-exports}

並非設定檔的所有更新都符合增量檔案匯出中包含的設定檔資格。 例如，如果將屬性新增到設定檔或從設定檔中移除，則匯出中不包含該設定檔。 僅設定檔的 `segmentMembership` 屬性已變更將會包含在匯出的檔案中。 換言之，只有在設定檔成為對象的一部分或從對象中移除時，才會納入增量檔案匯出中。

同樣地，如果將新的身分識別（新的電子郵件地址、電話號碼、ECID等）新增至 [身分圖表](/help/identity-service/features/identity-graph-viewer.md)，這並不表示有理由將設定檔納入新的增量檔案匯出中。

如果將新對象新增到目的地對應，這不會影響其他區段的資格和匯出。 匯出排程是按對象個別設定，而檔案會按區段個別匯出，即使對象已新增至相同的目的地資料流亦然。

>[!BEGINSHADEBOX]

例如，在下圖所示的匯出設定中，如果對象正在匯出增量檔案更新，請注意以下情況，其中是否在增量檔案匯出中包含設定檔：

![匯出具有數個選定屬性的設定。](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* 當設定檔符合或不符合區段的資格時，該設定檔會包含在增量檔案匯出中。
* 設定檔為 *非* 當新的電話號碼新增到身分圖表時，包含在增量檔案匯出中。
* 設定檔為 *非* 當任何對應的XDM欄位(例如 `xdm: loyalty.points`， `xdm: loyalty.tier`， `xdm: personalEmail.address` 已更新至設定檔上。
* 每當 `segmentMembership.status` XDM欄位會在目的地啟用工作流程中完成對應，退出對象的設定檔也會包含在匯出的增量檔案中，並包含 `exited` 狀態。

>[!ENDSHADEBOX]

### 決定資料匯出的因素及匯出中包含的因素

根據上一節中的資訊，可將設定檔匯出行為摘要至檔案型目的地，如下所述：

**完整檔案匯出**

每天都會匯出對象的完整作用中母體。

| 決定目的地匯出的因素 | 匯出的檔案包含的內容 |
|---------|----------|
| <ul><li>在UI或API中設定的匯出排程和使用者動作(選取 [立即匯出檔案](/help/destinations/ui/export-file-now.md) 在UI中或使用 [臨機啟動API](/help/destinations/api/ad-hoc-activation-api.md))決定目的地匯出的開始。</li></ul> | 在完整檔案匯出作業中，每個檔案匯出作業都會包含區段根據最新對象評估而建立的整個作用中設定檔母體。 為匯出選取的每個XDM屬性的最新值也會包含為每個檔案中的欄。 請注意，處於已退出狀態的設定檔不會包含在檔案匯出中。 |

{style="table-layout:fixed"}

**增量檔案匯出**

在設定啟動工作流程後的第一個檔案匯出中，會匯出對象的整個母體。 在後續的匯出作業中，只會匯出已修改的設定檔。

| 決定目的地匯出的因素 | 匯出的檔案包含的內容 |
|---------|----------|
| <ul><li>在UI或API中設定的匯出排程決定目的地匯出的開始。</li><li>無論設定檔是否符合區段的資格，其對象成員資格的任何變更都會讓設定檔符合納入增量匯出的資格。 設定檔的屬性或身分對應中的變更 *不要* 限定要包含在增量匯出中的設定檔。</li></ul> | <p>對象成員資格已變更的設定檔，以及每個選取匯出之XDM屬性的最新資訊。</p><p>具有已退出狀態的設定檔會包含在目的地匯出中，如果 `segmentMembership.status` 在對應步驟中選取XDM欄位。</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>提醒您，設定檔的屬性值或身分對應中的變更，不符合納入增量檔案匯出的設定檔資格。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在瞭解將設定檔匯出至串流、企業和檔案型目的地的內容。

接下來，您可以閱讀如何 [身分已處理](/help/destinations/how-destinations-work/identity-handling.md) 在啟動工作流程中。
