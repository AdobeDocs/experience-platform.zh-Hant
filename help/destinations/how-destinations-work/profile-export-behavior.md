---
title: 配置檔案導出行為
description: 瞭解配置檔案導出行為在Experience Platform目標中支援的不同整合模式之間如何變化。
exl-id: 2be62843-0644-41fa-a860-ccd65472562e
source-git-commit: a0400ab255b3b6a7edb4dcfd5c33a0f9e18b5157
workflow-type: tm+mt
source-wordcount: '2933'
ht-degree: 0%

---

# 不同目標類型的配置檔案導出行為

Experience Platform中有幾種目標類型，如下圖所示。 這些目標的導出模式與觸發目標導出的原因以及導出中包含的內容稍有不同，如下面的更多部分所述。

>[!IMPORTANT]
>
>本文檔頁僅描述圖底部突出顯示的連接的配置檔案導出行為。

![目標圖的類型](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## 微批處理和聚合策略

在根據目標類型深入到特定資訊之前，必須瞭解以下概念： *流目標*。

Experience Platform目標將資料導出到基於API的整合，作為HTTPS調用。 一旦目標服務被其它上游服務通知，概要檔案已經由於批處理接收、流接收、批分段、流分段或身份圖改變而更新，資料就被導出併發送到流目的地。

調用配置檔案在被調度到目標API終結點之前聚合到HTTPS消息的過程 *微批量*。

獲取 [Facebook](/help/destinations/catalog/social/facebook.md) 帶 *[可配置聚合](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* 策略示例 — 資料以聚合方式發送，其中目標服務將從配置檔案服務上游接收的所有傳入資料，並將其聚合，然後將其發送到Facebook:

* 記錄數（最多10.000）或
* 時間窗口間隔（30分鐘）

無論上述閾值是否首次達到，都會引發對Facebook的出口。 所以，在 [!DNL Facebook Custom Audiences] 控制板，您可能會看到以10.000個記錄增量從Experience Platform進入觀眾。 您可能每10-15分鐘看到10.000條記錄，因為資料的處理和聚合速度比30分鐘導出間隔快，發送速度也快，因此大約每10-15分鐘一次，直到所有記錄都得到處理。 如果記錄不足，無法組成10.000批，則當前記錄數將按滿足時間窗口閾值時的方式發送，因此您也可能看到發送到Facebook的較小批。

另外，請考慮 [HTTP API目標](/help/destinations/catalog/streaming/http-destination.md)，其中 *[最佳工作聚合](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* 策略 `maxUsersPerRequest: 10`。 這意味著，在向此目的地觸發HTTP調用之前，最多將聚合十個配置檔案，但當目標服務從上游服務接收到更新的重新評估資訊時，Experience Platform會嘗試將配置檔案派送到目標。

聚合策略是可配置的，目標開發人員可以決定如何配置聚合策略以最好地滿足下游API端點的速率限制。 閱讀有關 [聚合策略](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) Destination SDK文檔。

## 流配置檔案導出（企業）目標 {#streaming-profile-destinations}

>[!IMPORTANT]
>
> 企業目標僅可用於 [Adobe Real-time Customer Data Platform旗艦](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。

的 [企業目標](/help/destinations/destination-types.md#streaming-profile-export) 在Experience Platform中是AmazonKinesis、Azure事件中心和HTTP API。

Experience Platform可優化配置檔案導出行為到企業目標，以便僅在在段鑑定或其他重要事件之後對配置檔案進行相關更新時將資料導出到API終結點。 配置式在以下情況下導出到目標：

* 配置檔案更新由 [段成員](/help/xdm/field-groups/profile/segmentation.md) 至少一個映射到目標的段。 例如，配置檔案已限定映射到目標的段之一或已退出映射到目標的段之一。
* 配置檔案更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md)。 例如，已為映射到目標的段之一限定的配置檔案已在標識映射屬性中添加了新標識。
* 配置檔案更新由映射到目的地的至少一個屬性的屬性的改變確定。 例如，映射步驟中映射到目標的屬性之一被添加到配置檔案。

在上述所有情況下，只將發生相關更新的配置檔案導出到目標。 例如，如果映射到目標流的段有100個成員，並且有5個新配置檔案符合該段的條件，則向目標的導出是增量的，並且只包括5個新配置檔案。

請注意，無論更改位於何處，都會為配置檔案導出所有映射的屬性。 因此，在上面的示例中，即使屬性本身沒有更改，也會導出這五個新配置檔案的所有映射屬性。

### 什麼決定資料導出以及導出中包含的內容

對於為給定配置檔案導出的資料，瞭解以下兩個不同概念非常重要 *決定資料導出到企業目標的因素* 和 *資料包含在導出中*。

| 決定目標導出的因素 | 目標導出中包含的內容 |
|---------|----------|
| <ul><li>映射的屬性和段用作目標導出的提示。 這表示如果任何映射的段更改狀態(從 `null` 至 `realized` 或 `realized` 至 `exiting`)或更新任何映射屬性時，將啟動目標導出。</li><li>由於標識當前無法映射到企業目標，因此給定配置檔案上任何標識的更改也會決定目標導出。</li><li>屬性的更改定義為屬性上的任何更新，無論其值是否相同。 這意味著，即使值本身未更改，屬性上的覆蓋也被視為更改。</li></ul> | <ul><li>的 `segmentMembership` 對象包括在激活資料流中映射的段，在限定或段退出事件後配置檔案的狀態已更改。 請注意，如果配置檔案限定用於的其他未映射段屬於相同的段，則這些段可以是目標導出的一部分 [合併策略](/help/profile/merge-policies/overview.md) 激活資料流中映射的段。 </li><li>中的所有標識 `identityMap` 也包括對象(Experience Platform當前不支援企業目標中的標識映射)。</li><li>目標導出中只包含映射的屬性。</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>在將配置檔案激活到目標時，企業目標流回填資料。 這意味著在將激活工作流配置到目標之後的第一資料導出將包括在段映射到目標之前符合激活段條件的配置檔案。

>[!BEGINSHADEBOX]

例如，將此資料流視為HTTP目標，其中在資料流中選擇了三個段，並將四個屬性映射到目標。

![企業目標資料流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

導出到目標的配置檔案可由符合或退出其中一個配置檔案來確定 *三個映射段*。 但是，在資料導出中，在 `segmentMembership` 對象，如果特定配置檔案是其成員，並且這些配置檔案與觸發導出的段共用相同的合併策略，則可能會出現其他未映射的段。 如果配置檔案符合 **DeLorean汽車的客戶** 部，但亦為 **觀看《回到未來》電影** 和 **科幻迷** 段，則這兩個段也將 `segmentMembership` 資料導出的對象，即使這些對象未在資料流中映射，如果它們與 **DeLorean汽車的客戶** 段。

從配置檔案屬性的視點來看，對上述四個屬性的任何更改都將確定目標導出，並且配置檔案上存在的四個映射屬性中的任何一個都將出現在資料導出中。

>[!ENDSHADEBOX]

>[!TIP]
>
> 您可以在中查看將資料導出到各種企業目標的示例 [AmazonKinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data)。 [Azure事件中心](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data), [HTTP API](/help/destinations/catalog/streaming/http-destination.md#exported-data) 目標文檔頁面。

## 基於流API的目標 {#streaming-api-based-destinations}

流目標(如Facebook、貿易台和其他基於API的整合)的配置檔案導出行為與上述企業目標的行為非常相似。

流目標的示例是屬於 [社會和廣告類別](/help/destinations/destination-types.md#categories) 目錄中。

Experience Platform優化配置檔案導出到流式傳輸目標的行為，以便在經過段限定或其他重要事件之後對配置檔案進行相關更新時，才將資料導出到基於API的流式傳輸目標。 配置式在以下情況下導出到目標：

* 配置檔案更新由 [段成員](/help/xdm/field-groups/profile/segmentation.md) 至少一個映射到目標的段。 例如，配置檔案已限定映射到目標的段之一或已退出映射到目標的段之一。
* 配置檔案更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md) 標識名稱空間，該標識名稱空間標籤為用於導出此目標實例。 例如，已為映射到目標的段之一限定的配置檔案已在標識映射屬性中添加了新標識。
* 配置檔案更新由映射到目的地的至少一個屬性的屬性的改變確定。 例如，映射步驟中映射到目標的屬性之一被添加到配置檔案。
* 配置自動同意強制並選擇配置檔案時配置檔案的同意更改。 自動同意強制將受眾退出事件發送到目標，以便配置檔案不包括在目標位置的任何目標中。

在上述所有情況下，只將發生相關更新的配置檔案導出到目標。 例如，如果映射到目標流的段有100個成員，並且有5個新配置檔案符合該段的條件，則向目標的導出是增量的，並且只包括5個新配置檔案。

請注意，無論更改位於何處，都會為配置檔案導出所有映射的屬性。 因此，在上面的示例中，即使屬性本身沒有更改，也會導出這五個新配置檔案的所有映射屬性。

### 什麼決定資料導出以及導出中包含的內容

關於為給定配置檔案導出的資料，必須瞭解以下兩個不同的概念：決定資料導出到流API目標的是什麼以及導出中包括哪些資料。

| 決定目標導出的因素 | 目標導出中包含的內容 |
|---------|----------|
| <ul><li>映射的屬性和段用作目標導出的提示。 這表示如果任何映射的段更改狀態(從 `null` 至 `realized` 或 `realized` 至 `exiting`)或更新任何映射屬性時，將啟動目標導出。</li><li>標識映射中的更改定義為為 [身份圖](/help/identity-service/ui/identity-graph-viewer.md) 的子目錄。</li><li>屬性的更改定義為屬性上映射到目標的屬性的任何更新。</li></ul> | <ul><li>映射到目標且已更改的段將包括在 `segmentMembership` 的雙曲餘切值。 在某些情況下，它們可能會使用多個調用導出。 此外，在某些情況下，呼叫中可能還包含一些未更改的段。 無論如何，將只導出映射的段。</li><li>映射到中目標的命名空間中的所有標識 `identityMap` 也包括對象。</li><li>目標導出中只包含映射的屬性。</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>在將配置檔案激活到目標時，流API目標流回填資料。 這意味著在將激活工作流配置到目標之後的第一資料導出將包括在段映射到目標之前符合激活段條件的配置檔案。

>[!BEGINSHADEBOX]

例如，將此資料流視為在資料流中選擇三個段的流目標。

![流目標資料流](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

通過限定或退出三個映射段之一的配置檔案，可以確定向目標導出的配置檔案。 如果配置檔案符合 **DeLorean汽車的客戶** 段，這將觸發導出。 其他分部(即&#x200B;**城市 — 達拉斯** 和 **基本站點活動**)可能也會導出，以防配置檔案的段具有可能的狀態之一(`realized` 或 `exited`)。 未映射的段(如 **科幻迷**)。

從配置檔案屬性的視點看，對上述三個屬性的任何更改都將決定目標導出。

>[!ENDSHADEBOX]

## 批處理（基於檔案）目標 {#file-based-destinations}

將配置檔案導出到 [基於檔案的目標](/help/destinations/destination-types.md#file-based) 在Experience Platform中，有三種類型的時間表（下面列出）和兩種檔案導出選項（完整或增量檔案）可供使用。 所有這些設定都在段級別上設定，即使多個段映射到單個目標資料流時也是如此。

* 計畫導出：配置目標、添加一個或多個段、選擇是否要導出完整檔案或增量檔案，並選擇每天或每天應導出檔案的設定時間。 例如，5 PM導出時間意味著任何符合段條件的配置檔案都將在下午5點導出。
* 分部評估後：在每日段評估作業運行後立即觸發導出。 這意味著檔案中導出的配置檔案編號與段的最新評估填充盡可能接近。
* 按需出口([立即導出檔案](/help/destinations/ui/export-file-now.md)):基於最新段評估作業，在定期計畫導出之外一次性導出完整檔案。

在上述任何導出情況下，導出的檔案包括限定用於導出的配置檔案以及您選擇作為XDM屬性進行導出的列。

>[!TIP]
>
>當流段映射到批處理目標時，導出檔案中配置檔案的數量與段中用戶的數量更接近的可能性更大。 這是因為，最新段評估更接近出口時間的可能性更大。

### 增量檔案導出 {#incremental-file-exports}

配置檔案上的所有更新都使配置檔案有資格包含在增量檔案導出中。 例如，如果某個屬性被添加到配置檔案或從配置檔案中刪除，則該屬性在導出中不包括配置檔案。 僅配置檔案 `segmentMembership` 屬性已更改將包含在導出的檔案中。 換句話說，僅當截面梁成為段的一部分或從段中移除時，它才包括在增量檔案導出中。

同樣，如果將新身份（新電子郵件地址、電話號碼、ECID等）添加到 [身份圖](/help/identity-service/ui/identity-graph-viewer.md)，這不表示將配置檔案包括在新增量檔案導出中的原因。

如果將新段添加到目標映射，則不會影響另一個段的資格和導出。 導出計畫按段單獨配置，而檔案則針對每個段單獨導出，即使這些段已添加到同一目標資料流。

>[!BEGINSHADEBOX]

例如，在下面所示的導出設定中，如果段正在導出增量檔案更新，請注意以下情況：配置檔案是否包含在增量檔案導出中：

![導出具有多個選定屬性的設定。](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* 當配置檔案符合或不符合段的條件時，它將包括在增量檔案導出中。
* 配置檔案是 *不* 將新電話號碼添加到標識圖形時包含在增量檔案導出中。
* 配置檔案是 *不* 當任何映射的XDM欄位的值(如 `xdm: loyalty.points`。 `xdm: loyalty.tier`。 `xdm: personalEmail.address` 在配置檔案上更新。
* 只要 `segmentMembership.status` XDM欄位在目標激活工作流中映射，退出段的配置檔案也包含在導出的增量檔案中， `exited` 狀態。

>[!ENDSHADEBOX]

### 什麼決定資料導出以及導出中包含的內容

根據上節中的資訊，可將配置檔案導出到基於檔案的目標的行為總結如下：

**完整檔案導出**

每天導出該段的全部活動人口。

| 決定目標導出的因素 | 導出檔案中包含的內容 |
|---------|----------|
| <ul><li>在UI或API和用戶操作中設定的導出計畫(選擇 [立即導出檔案](/help/destinations/ui/export-file-now.md) 或使用 [點對點激活API](/help/destinations/api/ad-hoc-activation-api.md))確定目標導出的開始。</li></ul> | 在完整檔案導出中，每個檔案導出都包括基於最新段評估的段的整個活動配置檔案填充。 為導出選擇的每個XDM屬性的最新值也作為列包含在每個檔案中。 請注意，檔案導出中不包含處於退出狀態的配置檔案。 |

{style="table-layout:fixed"}

**增量檔案導出**

在設定激活工作流後的第一個檔案導出中，將導出段的全部填充。 在隨後的導出中，僅導出已修改的配置檔案。

| 決定目標導出的因素 | 導出檔案中包含的內容 |
|---------|----------|
| <ul><li>UI或API中設定的導出計畫確定目標導出的開始。</li><li>配置檔案的段成員資格的任何更改（無論其是否符合該段的條件）均可將配置檔案包括在增量導出中。 配置檔案的屬性或身份映射中的更改 *不* 限定要包括在增量導出中的配置檔案。</li></ul> | <p>段成員資格已更改的配置檔案，以及每個選定用於導出的XDM屬性的最新資訊。</p><p>目標導出中包括已退出狀態的配置檔案(如果 `segmentMembership.status` 在映射步驟中選擇XDM欄位。</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>作為提醒，配置檔案的屬性值或標識映射中的更改不會限定配置檔案包含在增量檔案導出中。

## 後續步驟 {#next-steps}

讀完此文檔後，您現在知道在將配置檔案導出到流式、企業和基於檔案的目標時應該看到什麼。

接下來，你可以閱讀 [身份已處理](/help/destinations/how-destinations-work/identity-handling.md) 中。
