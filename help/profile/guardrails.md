---
title: 即時客戶設定檔資料和細分的預設護欄
solution: Experience Platform
product: experience platform
type: Documentation
description: 了解輪廓資料和細分的效能和系統強制護欄，確保以最佳方式使用 Real-Time CDP 功能。
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 1150b7726a7cabe6df6bbc7a850fb4d48afa208e
workflow-type: tm+mt
source-wordcount: '2511'
ht-degree: 2%

---

# [!DNL Real-Time Customer Profile]資料和分段的預設護欄

Adobe Experience Platform可讓您根據行為深入分析和客戶屬性，以即時客戶設定檔的形式提供個人化的跨管道體驗。 為了支援這種處理設定檔的新方法，Experience Platform使用與傳統關聯式資料模型不同的高度非標準化混合資料模型。

>[!IMPORTANT]
>
>除了此護欄頁面之外，還請檢查銷售訂單中的授權權益以及實際使用限制的對應[產品說明](https://helpx.adobe.com/legal/product-descriptions.html)。

本檔案提供預設的使用和速率限制，幫助您模型化設定檔資料，以獲得最佳系統效能。 檢閱下列護欄時，系統假設您已正確地模型化資料。 如果您有任何關於如何模型化資料的問題，請聯絡您的客戶服務代表。

>[!NOTE]
>
>大多數客戶不會超過這些預設限制。 如果您想瞭解自訂限制，請聯絡客戶服務代表。

## 快速入門

下列Experience Platform服務參與即時客戶個人檔案資料的模型化：

* [[!DNL Real-Time Customer Profile]](home.md)：使用來自多個來源的資料建立統一的消費者設定檔。
* [身分](../identity-service/home.md)：Bridge身分在擷取到Platform時來自不同的資料來源。
* [結構描述](../xdm/home.md)： Experience Data Model (XDM)結構描述是Platform用來組織客戶體驗資料的標準化架構。
* [對象](../segmentation/home.md)： Platform內的細分引擎是用來根據客戶行為和屬性，從您的客戶設定檔建立對象。

## 限制型別

本檔案有兩種預設限制：

| 護欄型別 | 說明 |
| -------------- | ----------- |
| **效能護欄（軟性限制）** | 效能護欄是與使用案例範圍相關的使用限制。 超過效能護欄時，您可能會遇到效能降低和延遲的問題。 Adobe對這類效能降低不負任何責任。 客戶若持續超過效能護欄，可選擇授權額外的容量，以避免效能降低。 |
| **系統強制的護欄（硬限制）** | Real-Time CDP UI或API會強制執行系統強制的護欄。 這些限制不得超過，因為UI和API會阻止您這樣做或會傳回錯誤。 |

{style="table-layout:auto"}

>[!NOTE]
>
>本檔案中所概述的限制會持續改善。 請定期回來檢視更新。 如果您有興趣瞭解自訂限制，請聯絡客戶服務代表。

## 資料模型限制

以下護欄提供模型化即時客戶設定檔資料時的建議限制。 若要深入瞭解主要實體和維度實體，請參閱附錄中有關[實體型別](#entity-types)的章節。

![顯示Adobe Experience Platform中設定檔資料之不同護欄的圖表。](./images/guardrails/profile-guardrails.png)

### 主要實體護欄

| 護欄 | 限制 | 限制型別 | 說明 |
| --------- | ----- | ---------- | ----------- |
| XDM個別設定檔類別資料集 | 20 | 效能護欄 | 建議最多使用20個運用XDM個別設定檔類別的資料集。 |
| XDM ExperienceEvent類別資料集 | 20 | 效能護欄 | 建議最多使用20個運用XDM ExperienceEvent類別的資料集。 |
| 為設定檔啟用的Adobe Analytics報表套裝資料集 | 1 | 效能護欄 | 設定檔最多應啟用一(1)個Analytics報表套裝資料集。 嘗試為設定檔啟用多個Analytics報表套裝資料集可能會對資料品質產生非預期的結果。 如需詳細資訊，請參閱附錄中有關[Adobe Analytics資料集](#aa-datasets)的章節。 |
| 多實體關係 | 5 | 效能護欄 | 建議在主要實體和尺寸實體之間最多定義5個多實體關係。 在移除或停用現有關聯性之前，不應進行其他關聯性對應。 |
| 用於多實體關係中的ID欄位的JSON深度 | 4 | 效能護欄 | 用於多實體關係中的ID欄位建議的最大JSON深度為4。 這表示在高度巢狀的結構描述中，超過4層深的巢狀欄位不應作為關聯性中的ID欄位。 |
| 設定檔片段中的陣列基數 | &lt;=500 | 效能護欄 | 個人資料片段（與時間無關的資料）中的最佳陣列基數&lt;=500。 |
| ExperienceEvent中的陣列基數 | &lt;=10 | 效能護欄 | ExperienceEvent （時間序列資料）中的最佳陣列基數&lt;=10。 |
| 個別設定檔身分圖表的身分計數 | 50 | 系統強制的護欄 | **個人設定檔的身分圖表最大身分數量為50。**&#x200B;任何具有50個以上身分的設定檔都會從分段、匯出和查詢中排除。 如需詳細資訊，請參閱[瞭解身分刪除邏輯](../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated)上的指南。 |

{style="table-layout:auto"}

### Dimension實體護欄

| 護欄 | 限制 | 限制型別 | 說明 |
| --------- | ----- | ---------- | ----------- |
| 不允許為非[!DNL XDM Individual Profile]實體使用時間序列資料 | 0 | 系統強制的護欄 | 設定檔服務中的非[!DNL XDM Individual Profile]實體不允許使用&#x200B;**時間序列資料。**&#x200B;如果時間序列資料集與非[!DNL XDM Individual Profile] ID相關聯，則不應為[!DNL Profile]啟用該資料集。 |
| 沒有巢狀關聯性 | 0 | 效能護欄 | 您不應該在兩個非[!DNL XDM Individual Profile]結構描述之間建立關係。 不建議將建立關聯性的功能用於任何不屬於[!DNL Profile]聯合結構描述的結構描述。 |
| 主要ID欄位的JSON深度 | 4 | 效能護欄 | 建議的主要ID欄位的最大JSON深度為4。 這表示在高度巢狀結構描述中，如果欄位巢狀超過4層深，則不應選取該欄位作為主要ID。 第4個巢狀層級的欄位可當作主要ID使用。 |

{style="table-layout:auto"}

## 資料大小限制

下列護欄參考資料大小，並根據需要提供建議對可擷取、儲存和查詢的資料加以限制。 若要深入瞭解主要實體和維度實體，請參閱附錄中有關[實體型別](#entity-types)的章節。

>[!NOTE]
>
>資料大小是在內嵌時以JSON的未壓縮資料來測量。

### 主要實體護欄

| 護欄 | 限制 | 限制型別 | 說明 |
| --------- | ----- | ---------- | ----------- |
| ExperienceEvent大小上限 | 10KB | 系統強制的護欄 | **事件大小上限為10KB。**&#x200B;內嵌將會繼續，但是大於10KB的事件將會被捨棄。 |
| 設定檔記錄大小上限 | 100KB | 系統強制的護欄 | **設定檔記錄的大小上限為100KB。**&#x200B;內嵌將繼續，但將捨棄大於100KB的設定檔記錄。 |
| 最大設定檔片段大小 | 50MB | 系統強制的護欄 | **單一設定檔片段的大小上限為50MB。任何大於50MB的[設定檔片段](#profile-fragments)的**&#x200B;分段、匯出和查詢可能會失敗。 |
| 最大設定檔儲存大小 | 50MB | 效能護欄 | **儲存的設定檔大小上限為50MB。**&#x200B;將新的[設定檔片段](#profile-fragments)加入大於50MB的設定檔將會影響系統效能。 例如，設定檔可包含50MB的單一片段，或可包含多個資料集的多個片段，合併總大小為50MB。 嘗試儲存單一片段大於50MB的設定檔，或多個片段合併大小總計超過50MB的設定檔，將會影響系統效能。 |
| 每天擷取的設定檔或ExperienceEvent批次數量 | 90 | 效能護欄 | **每天擷取的Profile或ExperienceEvent批次數量上限為90。**&#x200B;這表示每天擷取的Profile和ExperienceEvent批次總數不能超過90。 擷取其他批次將會影響系統效能。 |
| 每個設定檔記錄的ExperienceEvents數目 | 5000 | 效能護欄 | **每個設定檔記錄的ExperienceEvents數目上限為5000。超過5000個ExperienceEvents的**&#x200B;設定檔&#x200B;**不會**&#x200B;考慮用於分段。 |

{style="table-layout:auto"}

### Dimension實體護欄

| 護欄 | 限制 | 限制型別 | 說明 |
| --------- | ----- | ---------- | ----------- |
| 所有維度實體的總大小 | 5GB   | 效能護欄 | 建議所有維度實體的總大小為5GB。 擷取大型尺寸圖元可能會影響系統效能。 例如，不建議嘗試載入10GB的產品目錄作為維度實體。 |
| 每個維度實體結構描述的資料集 | 5 | 效能護欄 | 建議每個維度實體結構描述最多關聯5個資料集。 例如，如果您為「產品」建立結構描述，並新增五個貢獻資料集，則不應建立與產品結構描述繫結的第六個資料集。 |
| 每日擷取的Dimension實體批次 | 每個實體4個 | 效能護欄 | 建議每天擷取的維度實體批次數量上限為每個實體4個。 例如，您每天最多可以擷取4次產品目錄的更新。 擷取相同實體的其他維度實體批次可能會影響系統效能。 |

{style="table-layout:auto"}

## 分段護欄 {#segmentation-guardrails}

本節中概述的護欄是指組織可以在Experience Platform中建立的對象數量和性質，以及對應和啟用對象到目的地。

| 護欄 | 限制 | 限制型別 | 說明 |
| --------- | ----- | ---------- | ----------- |
| 每個沙箱的受眾 | 4000 | 效能護欄 | 每個沙箱最多可以有4000個&#x200B;**作用中**&#x200B;對象。 只要每個&#x200B;**個別**&#x200B;沙箱少於4000個對象，您每個組織的沙箱就可以超過4000個。 其中包含批次、串流和邊緣對象。 嘗試建立其他對象可能會影響系統效能。 深入瞭解[透過區段產生器建立對象](/help/segmentation/ui/segment-builder.md)。 |
| 每個沙箱的Edge受眾 | 150 | 效能護欄 | 每個沙箱最多可以有150個&#x200B;**使用中**&#x200B;邊緣對象。 只要每個&#x200B;**個別**&#x200B;沙箱中有少於150個邊緣對象，您每個組織就可以有超過150個邊緣對象。 嘗試建立其他邊緣對象可能會影響系統效能。 深入瞭解[邊緣對象](/help/segmentation/methods/edge-segmentation.md)。 |
| 所有沙箱中的Edge輸送量 | 1500 RPS | 效能護欄 | Edge細分支援每秒鐘尖峰值1500個進入Adobe Experience Platform Edge Network的傳入事件。 Edge區段在進入Adobe Experience Platform Edge Network後，最多可能需要350毫秒來處理傳入事件。 深入瞭解[邊緣對象](/help/segmentation/methods/edge-segmentation.md)。 |
| 每個沙箱的串流受眾 | 500 | 效能護欄 | 每個沙箱最多可以有500個&#x200B;**使用中**&#x200B;串流對象。 只要每個&#x200B;**個別**&#x200B;沙箱中的串流對象少於500個，您每個組織就可以有超過500個串流對象。 其中包含串流和邊緣對象。 嘗試建立其他串流對象可能會影響系統效能。 深入瞭解[串流對象](/help/segmentation/methods/streaming-segmentation.md)。 |
| 所有沙箱的串流輸送量 | 1500 RPS | 效能護欄 | 串流細分支援每秒1500個傳入事件的峰值。 串流區段最多可能需要5分鐘，才能讓設定檔符合區段會籍資格。 深入瞭解[串流對象](/help/segmentation/methods/streaming-segmentation.md)。 |
| 每個沙箱的批次對象 | 4000 | 效能護欄 | 每個沙箱最多可以有4000個&#x200B;**作用中**&#x200B;批次對象。 只要每個&#x200B;**個別**&#x200B;沙箱中的批次對象少於4000個，您每個組織可以有超過4000個批次對象。 嘗試建立其他批次對象可能會影響系統效能。 |
| 每個沙箱的帳戶對象 | 50 | 系統強制的護欄 | 您最多可以在沙箱中建立50個帳戶對象。 當您在沙箱中達到50個對象後，嘗試建立新帳戶對象時，**[!UICONTROL 建立對象]**&#x200B;控制項會停用。 深入瞭解[帳戶對象](/help/segmentation/types/account-audiences.md)。 |
| 每個沙箱的已發佈組合 | 10 | 效能護欄 | 一個沙箱中最多可以有10個已發佈的組合。 進一步瞭解UI指南](/help/segmentation/ui/audience-composition.md)中的[對象構成。 |
| 最大對象人數 | 30% | 效能護欄 | 建議的對象最大成員資格為系統中設定檔總數的30%。 您可以建立具有超過30%設定檔的對象為成員，或是多個大型對象，但會影響系統效能。 |

{style="table-layout:auto"}

## 預期的可用性

以下章節概述下游服務(例如Real-Time CDP目的地)中對象和合併原則的&#x200B;**預期**&#x200B;可用性：

| 沙箱類型 | 時間 |
| ------------ | ---- |
| 現有沙箱 | 1 小時 |
| 新沙箱 | 2 小時 |
| 新重設沙箱 | 2 小時 |

{style="table-layout:auto"}

## 附錄

本節提供本檔案中限制的其他詳細資訊。

### 實體型別

[!DNL Profile]存放區資料模型包含兩個核心實體型別：[主要實體](#primary-entity)和[維度實體](#dimension-entity)。

#### 主要實體

主要實體或設定檔實體會將資料合併在一起，為個人形成「單一真實來源」。 此統一資料以所謂的「聯合檢視」表示。 聯合檢視會將實施相同類別的所有結構描述的欄位彙總到單一聯合結構描述中。 [!DNL Real-Time Customer Profile]的聯合結構描述是非正規化混合資料模型，可作為所有設定檔屬性和行為事件的容器。

與時間無關的屬性（也稱為「記錄資料」）是使用[!DNL XDM Individual Profile]建立模型，而時間序列資料（也稱為「事件資料」）是使用[!DNL XDM ExperienceEvent]建立模型。 在Adobe Experience Platform中擷取記錄和時間序列資料時，它會觸發[!DNL Real-Time Customer Profile]開始擷取已啟用以供使用的資料。 內嵌的互動和詳細資訊越多，個別設定檔就越健全。

![說明記錄資料與時間序列資料之間差異的資訊圖表。](images/guardrails/profile-entity.png)

#### Dimension實體

雖然維護設定檔資料的設定檔資料存放區不是關聯式存放區，但設定檔允許與小型維度實體整合，以便以簡化且直覺的方式建立對象。 此整合稱為[多實體分段](../segmentation/tutorials/multi-entity-segmentation.md)。

您的組織也可以定義XDM類別來說明個人以外的專案，例如商店、產品或屬性。 這些非[!DNL XDM Individual Profile]結構描述稱為「維度實體」（也稱為「查詢實體」），不包含時間序列資料。 代表維度實體的結構描述會透過使用[結構描述關係](../xdm/tutorials/relationship-ui.md)連結至設定檔實體。

Dimension實體提供查詢資料，可協助並簡化多實體區段定義，且必須夠小，讓區段引擎可以將整個資料集載入記憶體，以進行最佳處理（快速點查詢）。

![顯示設定檔實體是由維度實體組成的資訊圖。](images/guardrails/profile-and-dimension-entities.png)

### 輪廓片段

在此檔案中，有數個護欄會參照「設定檔片段」。 在Experience Platform中，多個設定檔片段會合併在一起，以形成即時客戶設定檔。 每個片段代表指定資料集中該ID的唯一主要身分和對應的記錄或完整事件資料集。 若要深入瞭解設定檔片段，請參閱[設定檔概述](home.md#profile-fragments-vs-merged-profiles)。

### 合併原則 {#merge-policies}

將來自多個來源的資料彙集在一起時，合併原則是Platform用來判斷資料優先順序的方式以及將會合併哪些資料以建立該統一檢視的規則。 例如，如果客戶跨多個管道與您的品牌互動，則您的組織將會有多個與該單一客戶相關的設定檔片段出現在多個資料集中。 這些片段在擷取至Platform時，會合併在一起，以便為該客戶建立單一設定檔。 當來自多個來源的資料衝突時，合併原則會決定要將哪些資訊包含在個人設定檔中。 每個沙箱最多允許五(5)個使用`_xdm.context.profile`結構描述的合併原則。 若要深入瞭解合併原則，請參閱[合併原則概述](merge-policies/overview.md)。

### Platform中的Adobe Analytics報表套裝資料集 {#aa-datasets}

只要解決所有資料衝突，就可以為設定檔啟用多個報表套裝。 您可以使用「資料準備」功能來解決eVar、清單和Prop之間的資料衝突。 若要進一步瞭解如何使用「資料準備」功能，請參閱[Adobe Analytics聯結器UI指南](../sources/tutorials/ui/create/adobe-applications/analytics.md)。

## 後續步驟

請參閱下列檔案，深入瞭解其他Experience Platform服務護欄、端對端延遲資訊，以及Real-Time CDP產品說明檔案的授權資訊：

* [Real-Time CDP護欄](/help/rtcdp/guardrails/overview.md)
* [各種Experience Platform服務的端對端延遲圖表](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams)。
* [Real-Time Customer Data Platform (B2C版本 — Prime和Ultimate套件)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Prime和Ultimate套件)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Prime和Ultimate套件)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
