---
title: 設定檔匯出行為
description: 了解設定檔匯出行為如何因Experience Platform目的地支援的不同整合路徑而有所不同。
source-git-commit: 90964189396b3b89f35a96eb4c04e248dc34b9b4
workflow-type: tm+mt
source-wordcount: '2954'
ht-degree: 0%

---

# 不同目的地類型的設定檔匯出行為

Experience Platform中有數種目的地類型，如下圖所示。 這些目的地的匯出模式與觸發目的地匯出的因素，以及匯出中包含的項目略有不同，如下節所述。

>[!IMPORTANT]
>
>本檔案頁面僅說明圖表底部醒目顯示之連線的設定檔匯出行為。

![目的地圖表類型](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## 微批處理和聚合策略

在深入了解每個目的地類型的特定資訊之前，請務必了解以下概念： *串流目的地*.

Experience Platform目的地會以HTTPS呼叫的形式，將資料匯出至API型整合。 當其他上游服務通知目的地服務，說明設定檔已因批次內嵌、串流內嵌、批次分段、串流分段或身分圖變更而更新後，資料會匯出並傳送至串流目的地。

在將設定檔發送至目的地API端點之前，先匯總為HTTPS訊息的程式稱為 *微量分批*.

取用 [Facebook目的地](/help/destinations/catalog/social/facebook.md) 帶 *[可配置聚合](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation)* 原則為範例 — 資料會以匯總方式傳送，其中目的地服務會擷取設定檔服務上游的所有傳入資料，並依下列其中一項匯總，再將其發送至Facebook:

* 記錄數（最多10.000）或
* 時間窗口間隔（30分鐘）

以上任一臨界值首次符合時，就會觸發匯出至Facebook。 所以，在 [!DNL Facebook Custom Audiences] 控制面板，您可能會看到以10.000記錄增量從Experience Platform傳入的對象。 您可能每10-15分鐘會看到10.000筆記錄，因為資料的處理和匯總速度比30分鐘匯出間隔快，而且傳送速度也快，因此大約每10-15分鐘就會看到一次，直到所有記錄都處理完畢。 如果記錄不足，無法組成10.000批，則當前記錄數將如符合時間窗口閾值時一樣發送，因此您可能也會看到傳送到Facebook的較小批。

另外，請考量 [HTTP API目的地](/help/destinations/catalog/streaming/http-destination.md)，其中 *[最佳成果匯總](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation)* 政策， `maxUsersPerRequest: 10`. 這表示在向此目的地觸發HTTP呼叫之前，最多會匯總10個設定檔，但當目標服務收到來自上游服務的更新重新評估資訊時，Experience Platform會嘗試將設定檔分派至目的地。

聚合策略是可配置的，目標開發人員可以決定如何配置聚合策略以最好地滿足下游API端點的速率限制。 深入了解 [聚合策略](/help/destinations/destination-sdk/destination-configuration.md#aggregation) 在Destination SDK檔案中。

## 串流設定檔匯出（企業）目的地 {#streaming-profile-destinations}

>[!IMPORTANT]
>
> 企業目標僅適用於 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。

此 [企業目的地](/help/destinations/destination-types.md#streaming-profile-export) Experience Platform中有Amazon Kinesis、Azure事件中心和HTTP API。

Experience Platform會最佳化設定檔匯出行為至您的企業目的地，以僅在區段資格或其他重大事件後發生設定檔的相關更新時，將資料匯出至API端點。 設定檔會在下列情況下匯出至您的目的地：

* 設定檔更新是由 [區段成員資格](/help/xdm/field-groups/profile/segmentation.md) 至少一個區段對應至目的地。 例如，設定檔已符合對應至目的地的其中一個區段資格，或已退出對應至目的地的其中一個區段。
* 設定檔更新是由 [身分圖](/help/xdm/field-groups/profile/identitymap.md). 例如，已符合其中一個對應至目的地區段資格的設定檔，已在「身分對應」屬性中新增身分識別。
* 配置檔案更新由至少一個映射到目標的屬性的屬性的屬性變化確定。 例如，對應步驟中對應至目的地的其中一個屬性會新增至設定檔。

在上述所有情況中，只有發生相關更新的設定檔會匯出至您的目的地。 例如，如果對應至目的地流程的區段有100個成員，且有5個新設定檔符合該區段的資格，則匯出至目的地的作業會是增量的，且僅包含5個新設定檔。

請注意，無論變更在何處，所有對應屬性都會匯出至設定檔。 因此，在上述範例中，即使屬性本身未變更，這五個新設定檔的所有對應屬性也會匯出。

### 決定資料匯出的項目，以及匯出中包含的項目

對於針對指定設定檔匯出的資料，請務必了解 *決定要匯出至企業目的地的資料的因素* 和 *匯出中包含的資料*.

| 決定目標匯出的因素 | 目的地匯出包含的項目 |
|---------|----------|
| <ul><li>對應的屬性和區段可作為目的地匯出的提示。 這表示，如果任何映射的段更改狀態（從null更改為已實現或從已實現/現有更新為正在退出）或任何映射的屬性被更新，則將啟動目標導出。</li><li>由於身分目前無法對應至企業目的地，因此指定設定檔上任何身分的變更也會決定目的地匯出。</li><li>屬性的更改定義為對屬性的任何更新，無論其是否為相同值。 這表示即使值本身未變更，屬性的覆寫仍視為變更。</li></ul> | <ul><li>此 `segmentMembership` 對象包括在激活資料流中映射的段，在資格鑑定或段退出事件後，配置檔案的狀態已更改。 請注意，如果設定檔符合資格的其他未對應區段屬於相同區段，則這些區段可能是目的地匯出的一部分 [合併策略](/help/profile/merge-policies/overview.md) 作為激活資料流中映射的段。 </li><li>中的所有身分 `identityMap` 也包含物件(Experience Platform目前不支援企業目標中的身分對應)。</li><li>目標匯出中僅包含對應的屬性。</li></ul> |

{style=&quot;table-layout:fixed&quot;}

>[!IMPORTANT]
>
>在將設定檔啟用至目的地時，企業目的地會串流回填資料。 這表示在設定啟動工作流程至目的地後，第一個匯出資料將包含在區段對應至目的地前符合啟動區段資格的設定檔。

>[!BEGINSHADEBOX]

例如，將此資料流視為HTTP目標，其中資料流中選擇了三個段，四個屬性映射到目標。

![企業目標資料流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

匯出至目的地的設定檔可由符合以下條件之一或退出該條件的設定檔來決定 *三個已對應區段*. 不過，在資料匯出中， `segmentMembership` 對象中，如果該特定配置檔案是其成員，並且這些配置檔案與觸發導出的段共用相同的合併策略，則可能會顯示其他未映射的段。 如果設定檔符合 **DeLorean汽車的客戶** 區段，但亦為 **觀看《回到未來》電影** 和 **科幻迷** 區段，則另外兩個區段也會出現在 `segmentMembership` 資料導出的對象，即使這些對象未映射到資料流中，如果這些對象與共用相同的合併策略 **DeLorean汽車的客戶** 區段。

從設定檔屬性的觀點來看，對上述四個屬性所做的任何變更將決定目的地匯出，而設定檔上呈現的四個對應屬性中的任何一個將出現在資料匯出中。

>[!ENDSHADEBOX]

>[!TIP]
>
> 您可以在 [AmazonKinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data), [Azure事件中心](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data)，和 [HTTP API](/help/destinations/catalog/streaming/http-destination.md#exported-data) 目的地檔案頁面。

## 以API為基礎的串流目的地 {#streaming-api-based-destinations}

串流目的地(例如Facebook、交易台和其他API型整合)的設定檔匯出行為與上述企業目的地的行為非常類似。

串流目的地的範例是屬於 [社交和廣告類別](/help/destinations/destination-types.md#categories) 在目錄中。

Experience Platform會最佳化設定檔匯出行為至您的串流目的地，以便只有在符合區段資格或其他重大事件後，當設定檔發生相關更新時，才能將資料匯出至以API為基礎的串流目的地。 設定檔會在下列情況下匯出至您的目的地：

* 設定檔更新是由 [區段成員資格](/help/xdm/field-groups/profile/segmentation.md) 至少一個區段對應至目的地。 例如，設定檔已符合對應至目的地的其中一個區段資格，或已退出對應至目的地的其中一個區段。
* 設定檔更新是由 [身分圖](/help/xdm/field-groups/profile/identitymap.md) ，標籤為要導出此目標實例的標識命名空間。 例如，已符合其中一個對應至目的地區段資格的設定檔，已在「身分對應」屬性中新增身分識別。
* 配置檔案更新由至少一個映射到目標的屬性的屬性的屬性變化確定。 例如，對應步驟中對應至目的地的其中一個屬性會新增至設定檔。
* 設定自動同意強制時，設定檔的同意變更，且設定檔會選擇退出。 自動同意強制會將對象退出事件傳送至目的地，這樣設定檔就不會包含在目的地的任何定位中。

在上述所有情況中，只有發生相關更新的設定檔會匯出至您的目的地。 例如，如果對應至目的地流程的區段有100個成員，且有5個新設定檔符合該區段的資格，則匯出至目的地的作業會是增量的，且僅包含5個新設定檔。

請注意，無論變更在何處，所有對應屬性都會匯出至設定檔。 因此，在上述範例中，即使屬性本身未變更，這五個新設定檔的所有對應屬性也會匯出。

### 決定資料匯出的項目，以及匯出中包含的項目

關於針對指定設定檔匯出的資料，請務必了解決定要匯出至串流API目的地的資料，以及匯出中包含哪些資料的兩個不同概念。

| 決定目標匯出的因素 | 目的地匯出包含的項目 |
|---------|----------|
| <ul><li>對應的屬性和區段可作為目的地匯出的提示。 這表示，如果任何映射的段更改狀態（從null更改為已實現或從已實現/現有更新為正在退出）或任何映射的屬性被更新，則將啟動目標導出。</li><li>身分對應中的變更定義為針對 [身分圖](/help/identity-service/ui/identity-graph-viewer.md) 的，適用於對應以匯出的身分識別命名空間。</li><li>屬性的變更定義為對映至目的地之屬性的屬性的任何更新。</li></ul> | <ul><li>對應至目的地且已變更的區段將包含在 `segmentMembership` 物件。 在某些情況下，可能會使用多個呼叫匯出。 此外，在某些情況下，某些未變更的區段也可能包含在呼叫中。 無論如何，只會匯出對應的區段。</li><li>來自命名空間且對應至中目的地的所有身分識別 `identityMap` 也包含物件。</li><li>目標匯出中僅包含對應的屬性。</li></ul> |

{style=&quot;table-layout:fixed&quot;}

>[!IMPORTANT]
>
>在將設定檔啟用至目的地時，串流API目的地會串流回填資料。 這表示在設定啟動工作流程至目的地後，第一個匯出資料將包含在區段對應至目的地前符合啟動區段資格的設定檔。

>[!BEGINSHADEBOX]

例如，將此資料流視為資料流中選擇了三個段的流目標。

![流目標資料流](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

匯出至目的地的設定檔，可由符合三個對應區段其中之一或退出該三個對應區段的設定檔來決定。 如果設定檔符合 **DeLorean汽車的客戶** 區段，則會觸發匯出。 其他區段(**城市 — 達拉斯** 和 **基本站點活動**)也可匯出，以備設定檔中有該區段顯示其中一種可能狀態(`realized`, `existing`, `exited`)。 未對應的區段(例如 **科幻迷**)無法匯出。

從設定檔屬性的檢視點，對上述三個屬性所進行的任何變更都將決定目的地匯出。

>[!ENDSHADEBOX]

## 批次（檔案型）目的地 {#file-based-destinations}

將設定檔匯出至 [檔案型目的地](/help/destinations/destination-types.md#file-based) 在Experience Platform中，有三種排程類型（如下所列）和兩種檔案匯出選項（完整或增量檔案）可供您使用。 所有這些設定都設定在段級別上，即使多個段映射到單個目標資料流。

* 排程匯出：設定目標、新增一或多個區段、選取是否要匯出完整或增量檔案，並選取每天設定的時間或每天應匯出檔案的數次。 例如，下午5點匯出時間表示任何符合區段資格的設定檔將於下午5點匯出。
* 分段評估後：匯出會在每日區段評估工作執行後立即觸發。 這表示檔案中匯出的設定檔編號會盡可能接近區段的最新評估母體。
* 按需導出([立即匯出檔案](/help/destinations/ui/export-file-now.md)):根據最新的區段評估工作，除了定期排程的匯出外，還會一次匯出完整檔案。

在上述任何匯出情況中，匯出的檔案會包含符合匯出資格的設定檔，以及您選為要匯出的XDM屬性的欄。

>[!TIP]
>
>將串流區段對應至批次目的地時，匯出檔案中的設定檔數量與區段中的使用者數量較接近的可能性較大。 這是因為，最新區段評估更有可能更接近匯出時間。

### 增量檔案導出 {#incremental-file-exports}

並非配置檔案上的所有更新都允許配置檔案包含在增量檔案導出中。 例如，如果屬性已新增至設定檔或從中移除，則匯出中不會包含設定檔。 僅限 `segmentMembership` 已變更的屬性將包含在匯出的檔案中。 換言之，只有當設定檔成為區段的一部分或從區段中移除時，它才會包含在增量檔案匯出中。

同樣地，如果新的身分（新電子郵件地址、電話號碼、ECID等）已新增至 [身分圖](/help/identity-service/ui/identity-graph-viewer.md)，這不代表將設定檔納入新的增量檔案匯出中的原因。

如果將新區段新增至目的地對應，則不會影響其他區段的資格和匯出。 匯出排程會依每個區段個別設定，而檔案會針對每個區段個別匯出，即使區段已新增至相同的目的地資料流亦然。

>[!BEGINSHADEBOX]

例如，在下圖所示的導出設定中，如果區段正在導出增量檔案更新，請注意以下情況：配置檔案是否包含在增量檔案導出中：

![匯出設定，包含數個選取的屬性。](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* 當設定檔符合或取消符合區段的資格時，該設定檔會包含在增量檔案匯出中。
* 設定檔是 *not* 新增電話號碼至身分圖表時，包含在增量檔案匯出中。
* 設定檔是 *not* 當任何已對應XDM欄位的值(如 `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` 會在設定檔上更新。
* 每當 `segmentMembership.status` XDM欄位已對應至目標啟動工作流程，退出區段的設定檔也會包含在匯出的增量檔案中，並帶有 `exited` 狀態。

>[!ENDSHADEBOX]

### 決定資料匯出的項目，以及匯出中包含的項目

根據上節中的資訊，設定檔匯出至檔案式目的地的行為可匯總如下：

**完整檔案匯出**

區段的完整作用中母體會每天匯出。

| 決定目標匯出的因素 | 匯出的檔案中包含的內容 |
|---------|----------|
| <ul><li>UI或API中設定的匯出排程和使用者動作(選取 [立即匯出檔案](/help/destinations/ui/export-file-now.md) 或使用 [臨機啟動API](/help/destinations/api/ad-hoc-activation-api.md))決定目的地匯出的開始。</li></ul> | 在完整檔案匯出中，根據最新區段評估，每個檔案匯出都會包含區段的整個作用中設定檔母體。 選取要匯出的每個XDM屬性的最新值也會納入為每個檔案中的欄。 請注意，處於退出狀態的設定檔不會包含在檔案匯出中。 |

{style=&quot;table-layout:fixed&quot;}

**增量檔案導出**

在設定啟動工作流程後的第一個檔案匯出中，會匯出區段的整個母體。 在後續的匯出中，只會匯出修改的設定檔。

| 決定目標匯出的因素 | 匯出的檔案中包含的內容 |
|---------|----------|
| <ul><li>UI或API中設定的匯出排程會決定目的地匯出的開始。</li><li>設定檔的區段成員資格變更（無論是否符合區段資格或取消資格）都可讓設定檔納入增量匯出。 設定檔屬性或身分對應中的變更 *不* 允許將配置檔案包含在增量導出中。</li></ul> | <p>區段成員資格已變更的設定檔，以及每個選取要匯出之XDM屬性的最新資訊。</p><p>具有退出狀態的設定檔會包含在目的地匯出中(如果 `segmentMembership.status` 已在對應步驟中選取XDM欄位。</p> |

{style=&quot;table-layout:fixed&quot;}

>[!TIP]
>
>提醒您，設定檔屬性值或身分對映中的變更，不會讓設定檔納入增量檔案匯出。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道在將描述檔匯出至串流、企業和檔案型目的地時會看到什麼。

接下來，你可以閱讀 [身分識別已處理](/help/destinations/how-destinations-work/identity-handling.md) 在啟動工作流程中。
