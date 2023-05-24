---
keywords: profile；即時客戶概要檔案；故障排除；guardrails;guiderines;limit;entity;primary entity;dimension entity;RTCDP;B2B Edition;Real-time Customer Data Platform；即時客戶資料平台；即時cdp;b2b;cdp;
title: Real-time Customer Data PlatformB2B版預設護欄
type: Documentation
description: Adobe Experience Platform 使用與傳統關聯式資料模型不同的高度非標準化混合資料模型。 本文檔提供預設使用和速率限制，幫助您使用Adobe Real-time Customer Data PlatformB2B版為資料建模以獲得最佳系統效能。
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: 6327f5e6cb64a46c502613dd6074d84ed1fdd32b
workflow-type: tm+mt
source-wordcount: '1651'
ht-degree: 2%

---

# Real-time Customer Data PlatformB2B版預設護欄

>[!NOTE]
>
>本文中概述的限制表示Real-time Customer Data PlatformB2B版所啟用的更改。 要獲得Real-Time CDPB2B版預設限制的完整清單，請將這些限制與中概述的一般Adobe Experience Platform限制相結合 [Real-Time Customer Profile資料文檔的護欄](../profile/guardrails.md)。

Real-time Customer Data PlatformB2B版使您能夠以即時客戶配置檔案和客戶配置檔案的形式提供基於行為洞察和客戶屬性的個性化跨渠道體驗。 為支援這種新的輪廓處理方法，Experience Platform使用了與傳統關係資料模型不同的高度不正常的混合資料模型。

本文檔提供預設使用和速率限制，幫助您為資料建模以獲得最佳系統效能。 在查看以下護欄時，假定您已正確建模了資料。 如果您對如何建模資料有疑問，請與客戶服務代表聯繫。

>[!INFO]
>
>大多數客戶未超過這些預設限制。 如果您想瞭解自定義限制，請與您的客戶服務代表聯繫。

## 限制類型

本文檔中有兩種預設限制類型：

* **軟限制：** 可以超出軟限制，但軟限制為系統效能提供了建議的准則。

* **硬限制：** 硬限制提供絕對最大值。

>[!INFO]
>
>本檔案中概述的限制正在不斷改進。 請定期回頭查看更新。 如果您有興趣瞭解自定義限制，請與您的客戶服務代表聯繫。

## 資料模型限制

以下護欄在建模即時客戶配置檔案資料時提供建議的限制。 要瞭解有關主要圖元和尺寸圖元的詳細資訊，請參閱上 [實體類型](#entity-types) 的下界。

### 主要實體護欄

>[!NOTE]
>
>本節中概述的資料模型限制表示Real-time Customer Data PlatformB2B版所啟用的更改。 要獲得Real-Time CDPB2B版預設限制的完整清單，請將這些限制與中概述的一般Adobe Experience Platform限制相結合 [Real-Time Customer Profile資料文檔的護欄](../profile/guardrails.md)。

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| Real-Time CDPB2B版標準XDM類資料集 | 60 | 軟 | 建議最多使用Real-Time CDPB2B版提供的標準體驗資料模型(XDM)類的60個資料集。 有關B2B使用情形的標準XDM類的完整清單，請參閱 [Real-Time CDPB2B版文檔中的架構](schemas/b2b.md)。 <br/><br/>*注：由於Experience Platform的非規範混合資料模型的性質，大多數客戶沒有超過此限制。 有關如何對資料建模的問題，或者如果您想瞭解有關自定義限制的更多資訊，請與您的客戶服務代表聯繫。* |
| 舊式多實體關係 | 20 | 軟 | 建議在主要實體和尺寸實體之間定義最多20個多實體關係。 在刪除或禁用現有關係之前，不應進行其他關係映射。 |
| 每個XDM類的多對一關係 | 2 | 軟 | 建議每個XDM類最多定義2個多對一關係。 在刪除或禁用現有關係之前，不應建立其他關係。 有關如何在兩個架構之間建立關係的步驟，請參閱上的教程 [定義B2B架構關係](../xdm/tutorials/relationship-b2b.md)。 |

### Dimension實體護欄

>[!NOTE]
>
>本節中概述的資料模型限制表示Real-time Customer Data PlatformB2B版所啟用的更改。 要獲得Real-Time CDPB2B版預設限制的完整清單，請將這些限制與中概述的一般Adobe Experience Platform限制相結合 [Real-Time Customer Profile資料文檔的護欄](../profile/guardrails.md)。

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 無嵌套的舊關係 | 0 | 軟 | 您不應在兩個非[!DNL XDM Individual Profile] 架構。 不建議任何不屬於 [!DNL Profile] 聯合架構。 |
| 只有B2B對象可以參與多對一關係 | 0 | 硬 | 系統只支援B2B對象間的多對一關係。 有關多對一關係的詳細資訊，請參閱上的教程 [定義B2B架構關係](../xdm/tutorials/relationship-b2b.md)。 |
| B2B對象之間嵌套關係的最大深度 | 3 | 硬 | B2B對象間嵌套關係的最大深度為3。 這意味著，在高度嵌套的架構中，B2B對象之間不應有深度超過3個級別的嵌套關係。 |

## 資料大小限制

以下護欄參考資料大小，並為可以按預期接收、儲存和查詢的資料提供建議的限制。 要瞭解有關主要圖元和尺寸圖元的詳細資訊，請參閱上 [實體類型](#entity-types) 的下界。

>[!INFO]
>
>資料大小在接收時以JSON中的未壓縮資料度量。

### 主要實體護欄

>[!NOTE]
>
>本節中概述的資料大小限制表示Real-time Customer Data PlatformB2B版所啟用的更改。 要獲得Real-Time CDPB2B版預設限制的完整清單，請將這些限制與中概述的一般Adobe Experience Platform限制相結合 [Real-Time Customer Profile資料文檔的護欄](../profile/guardrails.md)。

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 每天每個XDM類接收的批 | 45 | 軟 | 每個XDM類每天接收的批的總數不應超過45。 接收附加批可能會阻止最佳效能。 |

### Dimension實體護欄

>[!NOTE]
>
>本節中概述的資料大小限制表示Real-time Customer Data PlatformB2B版所啟用的更改。 要獲得Real-Time CDPB2B版預設限制的完整清單，請將這些限制與中概述的一般Adobe Experience Platform限制相結合 [Real-Time Customer Profile資料文檔的護欄](../profile/guardrails.md)。

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 所有維圖元的總大小 | 5 GB   | 軟 | 建議所有維實體的總大小為5GB。 接收大維實體可能會影響系統效能。 例如，不建議嘗試將10GB產品目錄作為維實體載入。 |
| 每維實體架構的資料集 | 5 | 軟 | 建議最多5個與每個維實體模式關聯的資料集。 例如，如果為「products」建立一個模式並添加五個貢獻資料集，則不應建立與產品模式關聯的第六個資料集。 |
| Dimension實體每天接收的批 | 每個實體4個 | 軟 | 建議每天接收的維度實體批的最大數量為每個實體4。 例如，您每天最多可以將更新發送到產品目錄4次。 為同一實體接收附加維實體批可能會影響系統效能。 |

## 分段護欄

本節中概述的護欄是指組織在Experience Platform內可以建立的段的數量和性質，以及將段映射和激活到目標。

>[!NOTE]
>
>本節概述的細分限制表示Real-time Customer Data PlatformB2B版所啟用的更改。 要獲得Real-Time CDPB2B版預設限制的完整清單，請將這些限制與中概述的一般Adobe Experience Platform限制相結合 [Real-Time Customer Profile資料文檔的護欄](../profile/guardrails.md)。

| 瓜德賴爾 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 每個B2B沙箱的段數 | 400 | 軟 | 一個組織總共可以有400多個網段，只要每個B2B沙箱中的網段不到400個。 嘗試建立其他段可能會影響系統效能。 |

## 後續步驟

本文中概述的限制表示Real-time Customer Data PlatformB2B版所啟用的更改。 要獲得Real-Time CDPB2B版預設限制的完整清單，請將這些限制與中概述的一般Adobe Experience Platform限制相結合 [Real-Time Customer Profile資料文檔的護欄](../profile/guardrails.md)。

## 附錄

本節提供本文檔中限制的其他詳細資訊。

### 實體類型

的 [!DNL Profile] 儲存資料模型由兩個核心實體類型組成： [主要實體](#primary-entity) 和 [維實體](#dimension-entity)。

#### 主要實體

主實體或配置檔案實體將資料合併在一起，為個人形成「單一真相源」。 此統一資料使用所謂的「聯合視圖」來表示。 聯合視圖將實現相同類的所有架構的欄位聚合到單個聯合架構中。 的聯合架構 [!DNL Real-Time Customer Profile] 是不正常的混合資料模型，它充當所有配置檔案屬性和行為事件的容器。

與時間無關的屬性（也稱為「記錄資料」）使用 [!DNL XDM Individual Profile]，而時間序列資料（也稱為「事件資料」）則使用 [!DNL XDM ExperienceEvent]。 當記錄和時間序列資料在Adobe Experience Platform被攝入時，它觸發 [!DNL Real-Time Customer Profile] 開始接收已啟用以供使用的資料。 所攝取的交互和細節越多，個體輪廓就變得越強健。

![概述記錄資料與時間序列資料之間差異的資訊圖。](../profile/images/guardrails/profile-entity.png)

#### Dimension實體

雖然配置檔案資料儲存維護配置檔案資料不是關係儲存，但配置檔案允許與小維實體整合，以便以簡化和直觀的方式建立段。 此整合稱為 [多實體分割](../segmentation/multi-entity-segmentation.md)。

您的組織還可以定義XDM類來描述個人以外的事物，如商店、產品或屬性。 這些非[!DNL XDM Individual Profile] 架構稱為「維實體」（也稱為「查找實體」），不包含時間序列資料。 表示維實體的方案通過使用 [架構關係](../xdm/tutorials/relationship-ui.md)。

Dimension實體提供查找資料，該查找資料有助於和簡化多實體段定義，並且必須足夠小，以便分割引擎能夠將整個資料集載入到記憶體中，以便進行最佳處理（快速點查找）。

![一個資訊圖形，顯示配置檔案實體由尺寸實體組成。](../profile/images/guardrails/profile-and-dimension-entities.png)