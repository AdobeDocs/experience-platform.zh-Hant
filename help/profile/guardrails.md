---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；疑難解答；guardrails;guiderines;limit;entity;primary entity;dimension entity;
title: 即時客戶配置檔案資料的預設護欄
solution: Experience Platform
product: experience platform
type: Documentation
description: 'Adobe Experience Platform 使用與傳統關聯式資料模型不同的高度非標準化混合資料模型。 本文件提供預設的使用和速率限制，幫助您模型化設定檔資料，以獲得最佳系統效能。 '
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 8a343ad275dcfc33eb304e3fc19d375b81277448
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 5%

---

# 預設的護欄 [!DNL Real-time Customer Profile] 資料

Adobe Experience Platform使您能夠以即時客戶概要資訊的形式提供基於行為洞察和客戶屬性的個性化跨渠道體驗。 為支援這種新的輪廓處理方法，Experience Platform使用了與傳統關係資料模型不同的高度不正常的混合資料模型。

本文件提供預設的使用和速率限制，幫助您模型化設定檔資料，以獲得最佳系統效能。在查看以下護欄時，假定您已正確建模了資料。 如果您對如何建模資料有疑問，請與客戶服務代表聯繫。

>[!NOTE]
>
>大多數客戶未超過這些預設限制。 如果您想瞭解自定義限制，請與您的客戶服務代表聯繫。

## 快速入門

以下Experience Platform服務涉及對即時客戶配置檔案資料建模：

* [[!DNL Real-time Customer Profile]](home.md):使用來自多個源的資料建立統一的使用者配置檔案。
* [身份](../identity-service/home.md):將不同資料源的標識插入平台時進行橋接。
* [架構](../xdm/home.md):體驗資料模型(XDM)模式是平台組織客戶體驗資料的標準化框架。
* [段](../segmentation/home.md):平台內的細分引擎用於根據客戶行為和屬性從客戶配置檔案建立細分。

## 限制類型

本文檔中有兩種預設限制類型：

* **軟限制：** 可以超出軟限制，但軟限制為系統效能提供了建議的准則。

* **硬限制：** 硬限制提供絕對最大值。

>[!NOTE]
>
>本檔案中概述的限制正在不斷改進。 請定期回頭查看更新。 如果您有興趣瞭解自定義限制，請與您的客戶服務代表聯繫。

## 資料模型限制

以下護欄在建模即時客戶配置檔案資料時提供建議的限制。 要瞭解有關主要圖元和尺寸圖元的詳細資訊，請參閱上 [實體類型](#entity-types) 的下界。

### 主要實體護欄

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| XDM Individual Profile類資料集 | 20 | 軟 | 建議最多使用20個XDM Individual Profile類的資料集。 |
| XDM ExperienceEvent類資料集 | 20 | 軟 | 建議最多使用20個XDM ExperienceEvent類的資料集。 |
| Adobe Analytics為配置檔案啟用的報告套件資料集 | 1 | 軟 | 最多應為配置檔案啟用一(1)個分析報告套件資料集。 嘗試為配置檔案啟用多個分析報告套件資料集可能會對資料質量產生意外影響。 有關詳細資訊，請參閱 [Adobe Analytics資料集](#aa-datasets) 的下界。 |
| 多實體關係 | 5 | 軟 | 建議在主要實體和尺寸實體之間定義最多5個多實體關係。 在刪除或禁用現有關係之前，不應進行其他關係映射。 |
| 用於多實體關係的ID欄位的JSON深度 | 4 | 軟 | 在多實體關係中使用的ID欄位的建議最大JSON深度為4。 這意味著，在高度嵌套的架構中，深度超過4級的欄位不應用作關係中的ID欄位。 |
| 配置檔案片段中的陣列基數 | &lt;=500 | 軟 | 配置檔案片段（與時間無關的資料）中的最佳陣列基數為&lt;=500。 |
| ExperienceEvent中的陣列基數 | &lt;=10 | 軟 | ExperienceEvent（時間序列資料）中的最佳陣列基數為&lt;=10。 |
| 單個配置檔案標識圖的標識計數 | 50 | 硬 | **單個配置檔案的標識圖中的標識的最大數量為50。** 任何具有50個以上身份的配置檔案都不包括在分段、導出和查找中。 |

{style=&quot;table-layout:auto&quot;}

### Dimension實體護欄

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 不允許非[!DNL XDM Individual Profile] 實體 | 0 | 硬 | **不允許對非[!DNL XDM Individual Profile] 配置檔案服務中的實體。** 如果時間序列資料集與非[!DNL XDM Individual Profile] ID，不應為 [!DNL Profile]。 |
| 無嵌套關係 | 0 | 軟 | 您不應在兩個非[!DNL XDM Individual Profile] 架構。 不建議任何不屬於 [!DNL Profile] 聯合架構。 |
| 主ID欄位的JSON深度 | 4 | 軟 | 主ID欄位的建議最大JSON深度為4。 這意味著，在高度嵌套的架構中，如果欄位的嵌套深度超過4個級別，則不應選擇它作為主ID。 位於第4個嵌套級別的欄位可用作主ID。 |

{style=&quot;table-layout:auto&quot;&quot;

## 資料大小限制

以下護欄參考資料大小，並為可以按預期接收、儲存和查詢的資料提供建議的限制。 要瞭解有關主要圖元和尺寸圖元的詳細資訊，請參閱上 [實體類型](#entity-types) 的下界。

>[!NOTE]
>
>資料大小在接收時以JSON中的未壓縮資料度量。

### 主要實體護欄

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| ExperienceEvent最大大小 | 10 KB | 硬 | **事件的最大大小為10KB。** 攝取將繼續，但任何大於10KB的事件都將被丟棄。 |
| 最大配置檔案記錄大小 | 100 KB | 硬 | **配置檔案記錄的最大大小為100KB。** 將繼續攝取，但將丟棄大於100KB的配置檔案記錄。 |
| 最大配置檔案片段大小 | 50MB | 硬 | **單個配置檔案片段的最大大小為50MB。** 分段、導出和查找可能對任何 [配置檔案片段](#profile-fragments) 大於50MB。 |
| 最大配置檔案儲存大小 | 50MB | 軟 | **儲存的配置檔案的最大大小為50MB。** 添加新 [配置檔案片段](#profile-fragments) 大於50MB的配置檔案會影響系統效能。 例如，配置檔案可能包含一個50MB的片段，或者它可能包含跨多個資料集的多個片段，其總大小為50MB。 嘗試儲存單個片段大於50MB的配置檔案，或多個片段的總大小超過50MB，將影響系統效能。 |
| 每天接收的Profile或ExperienceEvent批數 | 90 | 軟 | **每天接收的Profile或ExperienceEvent批的最大數量為90。** 這意味著每天接收的Profile和ExperienceEvent批的合計不能超過90。 接收附加批將影響系統效能。 |

{style=&quot;table-layout:auto&quot;&quot;

### Dimension實體護欄

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 所有維圖元的總大小 | 5 GB   | 軟 | 建議所有維實體的總大小為5GB。 接收大維實體可能會影響系統效能。 例如，不建議嘗試將10GB產品目錄作為維實體載入。 |
| 每維實體架構的資料集 | 5 | 軟 | 建議最多5個與每個維實體模式關聯的資料集。 例如，如果為「products」建立一個模式並添加五個貢獻資料集，則不應建立與產品模式關聯的第六個資料集。 |
| Dimension實體每天接收的批 | 每個實體4個 | 軟 | 建議每天接收的維度實體批的最大數量為每個實體4。 例如，您每天最多可以將更新發送到產品目錄4次。 為同一實體接收附加維實體批可能會影響系統效能。 |

{style=&quot;table-layout:auto&quot;&quot;

## 分段護欄

本節中概述的護欄是指組織在Experience Platform內可以建立的段的數量和性質，以及將段映射和激活到目標。

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 每個沙盒的段數 | 1萬 | 軟 | 一個組織總共可以有10,000個以上的網段，只要每個沙箱中的網段不到10,000個。 嘗試建立其他段可能會影響系統效能。 |
| 每個沙箱的流資料段 | 500 | 軟 | 一個組織總共可以有500多個流資料段，只要每個沙箱中的流資料段少於500個。 嘗試建立附加流段可能會影響系統效能。 |
| 每個沙盒的批處理段 | 1萬 | 軟 | 一個組織可以具有總數超過10,000個批段，只要每個沙箱中的批段數少於10,000個。 嘗試建立附加批處理段可能會影響系統效能。 |

{style=&quot;table-layout:auto&quot;&quot;

## 附錄

本節提供本文檔中限制的其他詳細資訊。

### 實體類型

的 [!DNL Profile] 儲存資料模型由兩個核心實體類型組成：

* **主要實體：** 主實體或配置檔案實體將資料合併在一起，為個人形成「單一真相源」。 此統一資料使用所謂的「聯合視圖」來表示。 聯合視圖將實現相同類的所有架構的欄位聚合到單個聯合架構中。 的聯合架構 [!DNL Real-time Customer Profile] 是不正常的混合資料模型，它充當所有配置檔案屬性和行為事件的容器。

   與時間無關的屬性（也稱為「記錄資料」）使用 [!DNL XDM Individual Profile]，而時間序列資料（也稱為「事件資料」）則使用 [!DNL XDM ExperienceEvent]。 當記錄和時間序列資料在Adobe Experience Platform被攝入時，它觸發 [!DNL Real-time Customer Profile] 開始接收已啟用以供使用的資料。 所攝取的交互和細節越多，個體輪廓就變得越強健。

   ![](images/guardrails/profile-entity.png)

* **Dimension實體：** 雖然配置檔案資料儲存維護配置檔案資料不是關係儲存，但配置檔案允許與小維實體整合，以便以簡化和直觀的方式建立段。 此整合稱為 [多實體分割](../segmentation/multi-entity-segmentation.md)。 您的組織還可以定義XDM類來描述個人以外的事物，如商店、產品或屬性。 這些非[!DNL XDM Individual Profile] 架構稱為「維實體」，不包含時間序列資料。 Dimension實體提供查找資料，該查找資料有助於和簡化多實體段定義，並且必須足夠小，以便分割引擎能夠將整個資料集載入到記憶體中，以便進行最佳處理（快速點查找）。

   ![](images/guardrails/profile-and-dimension-entities.png)

### 配置檔案片段

在本文檔中，有幾個護欄提到「配置檔案片段」。 在Experience Platform中，將多個配置檔案片段合併在一起以形成即時客戶配置檔案。 每個片段表示給定資料集內該ID的唯一主標識和相應的記錄或事件資料。 要瞭解有關配置檔案片段的詳細資訊，請參閱 [概要檔案概述](home.md#profile-fragments-vs-merged-profiles)。

### 合併策略 {#merge-policies}

當將來自多個源的資料匯集在一起時，合併策略是平台用來確定資料優先順序以及將哪些資料合併以建立該統一視圖的規則。 例如，如果客戶通過多個渠道與您的品牌進行交互，您的組織將具有多個與該單個客戶相關的配置檔案片段，這些配置檔案片段出現在多個資料集中。 當這些片段被放入平台中時，它們會合併在一起，以便為該客戶建立單個配置檔案。 當來自多個源的資料衝突時，合併策略將確定要包含在個人配置檔案中的資訊。 要瞭解有關合併策略的詳細資訊，請從 [合併策略概述](merge-policies/overview.md)。

### Adobe Analytics平台中的報告套件資料集 {#aa-datasets}

最多應為配置檔案啟用一(1)個Adobe Analytics報告套件資料集。 這是一個軟限制，表示您能夠為配置檔案啟用多個分析資料集，但不建議這樣做，因為它可能會對您的資料產生意外的後果。 這是由於經驗資料模型(XDM)模式之間的差異，它為Experience Platform中的資料提供語義結構並允許資料解釋的一致性，以及Adobe Analytics中eVars和轉換變數的可定製性。

例如，在Adobe Analytics，單個組織可能具有多個報告套件。 如果報表套件A將eVar4指定為「內部搜索術語」，而報表套件B將eVar4指定為「引用域」，則這些值將同時被引入配置檔案中的同一欄位中，導致混淆並降低資料質量。
