---
title: 即時客戶設定檔資料和細分的預設護欄
solution: Experience Platform
product: experience platform
type: Documentation
description: 了解設定檔資料和細分的效能和系統強制護欄，確保以最佳方式使用 Real-Time CDP 功能。
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: c7537959b1cc53998acafbccaa2f39686afd9f15
workflow-type: tm+mt
source-wordcount: '2282'
ht-degree: 2%

---

# 預設護欄 [!DNL Real-Time Customer Profile] 資料與細分

Adobe Experience Platform可讓您根據行為深入分析和客戶屬性，以即時客戶設定檔的形式提供個人化的跨管道體驗。 為了支援這種處理設定檔的新方法，Experience Platform使用與傳統關聯式資料模型不同的高度非標準化混合資料模型。

本檔案提供預設的使用和速率限制，幫助您模型化設定檔資料，以獲得最佳系統效能。 檢閱下列護欄時，系統假設您已正確地模型化資料。 如果您有任何關於如何模型化資料的問題，請聯絡您的客戶服務代表。

>[!NOTE]
>
>大多數客戶不會超過這些預設限制。 如果您想瞭解自訂限制，請聯絡客戶服務代表。

## 快速入門

下列Experience Platform服務與即時客戶個人檔案資料的模型化有關：

* [[!DNL Real-Time Customer Profile]](home.md)：使用來自多個來源的資料建立統一的消費者設定檔。
* [身分](../identity-service/home.md)：橋接擷取到Platform中的不同資料來源身分。
* [方案](../xdm/home.md)：Experience Data Model (XDM)結構描述是Platform用來組織客戶體驗資料的標準化架構。
* [受眾](../segmentation/home.md)：Platform內的細分引擎是用來根據客戶行為和屬性，從您的客戶設定檔建立對象。

## 限制型別

本檔案有兩種預設限制：

| 護欄型別 | 說明 |
|----------|---------|
| **效能護欄（軟性限制）** | 效能護欄是與使用案例範圍相關的使用限制。 超過效能護欄時，您可能會遇到效能降低和延遲的問題。 Adobe對這類效能降級概不負責。 客戶若持續超過效能護欄，可選擇授權額外的容量，以避免效能降低。 |
| **系統強制的護欄（硬限制）** | Real-Time CDP UI或API會強制執行系統強制的護欄。 這些限制不得超過，因為UI和API會阻止您這樣做或會傳回錯誤。 |

{style="table-layout:auto"}

>[!NOTE]
>
>本檔案中所概述的限制會持續改善。 請定期回來檢視更新。 如果您有興趣瞭解自訂限制，請聯絡客戶服務代表。

## 資料模型限制

以下護欄提供模型化即時客戶設定檔資料時的建議限制。 若要深入瞭解主要實體和維度實體，請參閱以下章節： [實體型別](#entity-types) 在附錄中。

![此圖表顯示Adobe Experience Platform中設定檔資料的不同護欄。](./images/guardrails/profile-guardrails.png)

### 主要實體護欄

| 護欄 | 限制 | 限制型別 | 說明 |
| --- | --- | --- | --- |
| XDM個別設定檔類別資料集 | 20 | 效能護欄 | 建議最多使用20個運用XDM個別設定檔類別的資料集。 |
| XDM ExperienceEvent類別資料集 | 20 | 效能護欄 | 建議最多使用20個運用XDM ExperienceEvent類別的資料集。 |
| 為設定檔啟用的Adobe Analytics報表套裝資料集 | 1 | 效能護欄 | 設定檔最多應啟用一(1)個Analytics報表套裝資料集。 嘗試為設定檔啟用多個Analytics報表套裝資料集可能會對資料品質產生非預期的結果。 如需詳細資訊，請參閱以下章節： [Adobe Analytics資料集](#aa-datasets) 在附錄中。 |
| 多實體關係 | 5 | 效能護欄 | 建議在主要實體和尺寸實體之間最多定義5個多實體關係。 在移除或停用現有關聯性之前，不應進行其他關聯性對應。 |
| 用於多實體關係中的ID欄位的JSON深度 | 4 | 效能護欄 | 用於多實體關係中的ID欄位建議的最大JSON深度為4。 這表示在高度巢狀的結構描述中，超過4層深的巢狀欄位不應作為關聯性中的ID欄位。 |
| 設定檔片段中的陣列基數 | &lt;=500 | 效能護欄 | 個人資料片段（與時間無關的資料）中的最佳陣列基數&lt;=500。 |
| ExperienceEvent中的陣列基數 | &lt;=10 | 效能護欄 | ExperienceEvent （時間序列資料）中的最佳陣列基數&lt;=10。 |
| 個別設定檔身分圖表的身分計數 | 50 | 系統強制的護欄 | **在身分圖表中，個別設定檔的身分數量上限為50。** 任何具有超過50個身分的設定檔都會從分段、匯出和查詢中排除。 |

{style="table-layout:auto"}

### Dimension實體護欄

| 護欄 | 限制 | 限制型別 | 說明 |
| --- | --- | --- | --- |
| 不允許將時間序列資料用於[!DNL XDM Individual Profile] 實體 | 0 | 系統強制的護欄 | **時間序列資料不允許用於非[!DNL XDM Individual Profile] 設定檔服務中的實體。** 如果時間序列資料集與非關聯[!DNL XDM Individual Profile] ID，此資料集不應啟用 [!DNL Profile]. |
| 沒有巢狀關聯性 | 0 | 效能護欄 | 您不應在兩個非關聯式之間建立[!DNL XDM Individual Profile] 結構描述。 不建議將建立關係的功能用於不屬於的任何結構描述 [!DNL Profile] 聯合結構描述。 |
| 主要ID欄位的JSON深度 | 4 | 效能護欄 | 建議的主要ID欄位的最大JSON深度為4。 這表示在高度巢狀結構描述中，如果欄位巢狀超過4層深，則不應選取該欄位作為主要ID。 第4個巢狀層級的欄位可當作主要ID使用。 |

{style="table-layout:auto"}

## 資料大小限制

下列護欄參考資料大小，並根據需要提供建議對可擷取、儲存和查詢的資料加以限制。 若要深入瞭解主要實體和維度實體，請參閱以下章節： [實體型別](#entity-types) 在附錄中。

>[!NOTE]
>
>資料大小是在內嵌時以JSON的未壓縮資料來測量。

### 主要實體護欄

| 護欄 | 限制 | 限制型別 | 說明 |
| --- | --- | --- | --- |
| ExperienceEvent大小上限 | 10KB | 系統強制的護欄 | **事件的大小上限為10KB。** 內嵌將會繼續，但大於10KB的事件將會捨棄。 |
| 設定檔記錄大小上限 | 100KB | 系統強制的護欄 | **設定檔記錄的大小上限為100KB。** 內嵌將會繼續，但將捨棄大於100KB的設定檔記錄。 |
| 最大設定檔片段大小 | 50MB | 系統強制的護欄 | **單一設定檔片段的大小上限為50MB。** 任何專案的分段、匯出和查詢都可能失敗 [設定檔片段](#profile-fragments) 大於50MB。 |
| 最大設定檔儲存大小 | 50MB | 效能護欄 | **已儲存設定檔的大小上限為50MB。** 新增 [設定檔片段](#profile-fragments) 到大於50MB的設定檔將會影響系統效能。 例如，設定檔可包含50MB的單一片段，或可包含多個資料集的多個片段，合併總大小為50MB。 嘗試儲存單一片段大於50MB的設定檔，或多個片段合併大小總計超過50MB的設定檔，將會影響系統效能。 |
| 每天擷取的設定檔或ExperienceEvent批次數量 | 90 | 效能護欄 | **每天最多可擷取90個Profile或ExperienceEvent批次。** 這表示每天擷取的Profile和ExperienceEvent批次總數不能超過90。 擷取其他批次將會影響系統效能。 |
| 每個設定檔記錄的ExperienceEvents數目 | 5000 | 效能護欄 | **每個設定檔記錄的ExperienceEvents數量上限為5000。** 具有超過5000個ExperienceEvents的設定檔將 **非** 視為分段。 |

{style="table-layout:auto"}

### Dimension實體護欄

| 護欄 | 限制 | 限制型別 | 說明 |
| --- | --- | --- | --- |
| 所有維度實體的總大小 | 5GB   | 效能護欄 | 建議所有維度實體的總大小為5GB。 擷取大型尺寸圖元可能會影響系統效能。 例如，不建議嘗試載入10GB的產品目錄作為維度實體。 |
| 每個維度實體結構描述的資料集 | 5 | 效能護欄 | 建議每個維度實體結構描述最多關聯5個資料集。 例如，如果您為「產品」建立結構描述，並新增五個貢獻資料集，則不應建立與產品結構描述繫結的第六個資料集。 |
| 每日擷取的Dimension實體批次 | 每個實體4個 | 效能護欄 | 建議每天擷取的維度實體批次數量上限為每個實體4個。 例如，您每天最多可以擷取4次產品目錄的更新。 擷取相同實體的其他維度實體批次可能會影響系統效能。 |

{style="table-layout:auto"}

## 分段護欄 {#segmentation-guardrails}

本節中概述的護欄是指組織可在Experience Platform中建立的對象數量和性質，以及對應及啟用對象至目的地。

| 護欄 | 限制 | 限制型別 | 說明 |
| --- | --- | --- | --- |
| 每個沙箱的受眾 | 4000 | 效能護欄 | 一個組織總共可以有超過4000個對象，但前提是每個個別沙箱中的對象少於4000個。 嘗試建立其他對象可能會影響系統效能。 深入瞭解 [建立對象](/help/segmentation/ui/segment-builder.md) 區段產生器的連結。 |
| 每個沙箱的Edge對象 | 150 | 效能護欄 | 只要每個個別沙箱中的邊緣對象少於150個，組織就可以總共擁有超過150個邊緣對象。 嘗試建立其他邊緣對象可能會影響系統效能。 深入瞭解 [邊緣對象](/help/segmentation/ui/edge-segmentation.md). |
| 每個沙箱的串流受眾 | 500 | 效能護欄 | 只要每個個別沙箱中的串流對象少於500個，組織就可以總共超過500個串流對象。 嘗試建立其他串流對象可能會影響系統效能。 深入瞭解 [串流對象](/help/segmentation/ui/streaming-segmentation.md). |
| 每個沙箱的批次對象 | 4000 | 效能護欄 | 一個組織總共可以有超過4000個批次對象，只要每個個別沙箱中有少於4000個批次對象即可。 嘗試建立其他批次對象可能會影響系統效能。 |
| 每個沙箱的帳戶對象 | 50 | 系統強制的護欄 | 您最多可以在沙箱中建立50個帳戶對象。 當您在沙箱中達到50個對象後， **[!UICONTROL 建立對象]** 嘗試建立新帳戶對象時，控制項會停用。 深入瞭解 [帳戶對象](/help/segmentation/ui/account-audiences.md). |
| 每個沙箱的已發佈組合 | 10 | 效能護欄 | 一個沙箱中最多可以有10個已發佈的組合。 深入瞭解 [UI指南中的對象構成](/help/segmentation/ui/audience-composition.md). |
| 最大對象人數 | 30% | 效能護欄 | 建議的對象最大成員資格為系統中設定檔總數的30%。 您可以建立具有超過30%設定檔的對象為成員，或是多個大型對象，但會影響系統效能。 |

{style="table-layout:auto"}

## 附錄

本節提供本檔案中限制的其他詳細資訊。

### 實體型別

此 [!DNL Profile] 存放區資料模型包含兩種核心實體型別： [主要實體](#primary-entity) 和 [維度圖元](#dimension-entity).

#### 主要實體

主要實體或設定檔實體會將資料合併在一起，為個人形成「單一真實來源」。 此統一資料以所謂的「聯合檢視」表示。 聯合檢視會將實施相同類別的所有結構描述的欄位彙總到單一聯合結構描述中。 的聯合結構描述 [!DNL Real-Time Customer Profile] 是一個非正規化的混合資料模型，可作為所有設定檔屬性和行為事件的容器。

獨立於時間的屬性（也稱為「記錄資料」）是使用 [!DNL XDM Individual Profile]，而時間序列資料（也稱為「事件資料」）則使用進行模型化 [!DNL XDM ExperienceEvent]. 當在Adobe Experience Platform中擷取記錄和時間序列資料時，就會觸發 [!DNL Real-Time Customer Profile] 以開始擷取已啟用的資料。 內嵌的互動和詳細資訊越多，個別設定檔就越健全。

![概述記錄資料與時間序列資料之間差異的資訊圖。](images/guardrails/profile-entity.png)

#### Dimension實體

雖然維護設定檔資料的設定檔資料存放區不是關聯式存放區，但設定檔允許與小型維度實體整合，以便以簡化且直覺的方式建立對象。 這項整合稱為 [多實體分段](../segmentation/multi-entity-segmentation.md).

您的組織也可以定義XDM類別來說明個人以外的專案，例如商店、產品或屬性。 這些非[!DNL XDM Individual Profile] 結構描述稱為「維度實體」（也稱為「查詢實體」），不包含時間序列資料。 代表維度實體的結構描述會透過使用連結至設定檔實體。 [綱要關係](../xdm/tutorials/relationship-ui.md).

Dimension實體提供查閱資料，可協助並簡化多實體區段定義，且必須夠小，讓區段引擎可以將整個資料集載入記憶體，以進行最佳處理（快速點查閱）。

![顯示輪廓圖元由尺寸圖元組成的資訊圖。](images/guardrails/profile-and-dimension-entities.png)

### 設定檔片段

在此檔案中，有數個護欄會參照「設定檔片段」。 在Experience Platform中，多個設定檔片段會合併在一起，以形成即時客戶設定檔。 每個片段代表指定資料集中該ID的唯一主要身分和對應的記錄或完整事件資料集。 若要瞭解有關設定檔片段的詳細資訊，請參閱 [設定檔概述](home.md#profile-fragments-vs-merged-profiles).

### 合併政策 {#merge-policies}

將來自多個來源的資料彙集在一起時，合併原則是Platform用來判斷資料優先順序的方式以及將會合併哪些資料以建立該統一檢視的規則。 例如，如果客戶跨多個管道與您的品牌互動，則您的組織將會有多個與該單一客戶相關的設定檔片段出現在多個資料集中。 這些片段在擷取至Platform時，會合併在一起，以便為該客戶建立單一設定檔。 當來自多個來源的資料衝突時，合併原則會決定要將哪些資訊包含在個人設定檔中。 每個組織最多允許五(5)個合併原則。 若要深入瞭解合併原則，請參閱 [合併原則概觀](merge-policies/overview.md).

### Platform中的Adobe Analytics報表套裝資料集 {#aa-datasets}

只要解決所有資料衝突，就可以為設定檔啟用多個報表套裝。 您可以使用「資料準備」功能來解決eVar、清單和Prop之間的資料衝突。 若要進一步瞭解如何使用「資料準備」功能，請參閱 [Adobe Analytics聯結器UI指南](../sources/tutorials/ui/create/adobe-applications/analytics.md).

## 後續步驟

請參閱下列檔案，深入瞭解其他Experience Platform服務護欄、端對端延遲資訊，以及Real-Time CDP產品說明檔案的授權資訊：

* [Real-Time CDP護欄](/help/rtcdp/guardrails/overview.md)
* [端對端延遲圖](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) 用於各種Experience Platform服務。
* [Real-time Customer Data Platform （B2C版本 — Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2P - Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2B - Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
