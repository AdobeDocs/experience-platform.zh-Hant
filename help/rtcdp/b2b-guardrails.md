---
keywords: 設定檔；即時客戶設定檔；疑難排解；護欄；准則；限制；實體；主要實體；維度實體； RTCDP; CDP;B2B Edition;Real-time Customer Data Platform；即時客戶資料平台；即時cdp;b2b;cdp;
title: Real-time Customer Data Platform B2B版的預設護欄
type: Documentation
description: Adobe Experience Platform 使用與傳統關聯式資料模型不同的高度非標準化混合資料模型。 本檔案提供預設的使用和比率限制，協助您使用Adobe Real-time Customer Data Platform B2B版來建模資料，以獲得最佳的系統效能。
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: 6327f5e6cb64a46c502613dd6074d84ed1fdd32b
workflow-type: tm+mt
source-wordcount: '1651'
ht-degree: 2%

---

# Real-time Customer Data Platform B2B版的預設護欄

>[!NOTE]
>
>本檔案中概述的限制代表Real-time Customer Data Platform B2B版所啟用的變更。 如需Real-Time CDP B2B版的完整預設限制清單，請將這些限制與 [即時客戶個人檔案資料檔案的護欄](../profile/guardrails.md).

Real-time Customer Data Platform B2B Edition可讓您以即時客戶設定檔和帳戶設定檔的形式，根據行為分析和客戶屬性提供個人化的跨管道體驗。 為了支援這種新的設定檔方法，Experience Platform使用與傳統關係資料模型不同的高度非正常化混合資料模型。

本文檔提供預設的使用和費率限制，以幫助您為資料建模以獲得最佳系統效能。 檢閱下列護欄時，會假設您已正確模型化資料。 若您對如何建立資料模型有任何疑問，請連絡您的客戶服務代表。

>[!INFO]
>
>大部分客戶未超過這些預設限制。 若您想了解自訂限制，請聯絡客戶服務代表。

## 限制類型

本文檔中有兩種預設限制類型：

* **軟限制：** 可能超出軟限制，但軟限制為系統效能提供建議的准則。

* **硬限制：** 硬限制提供絕對最大值。

>[!INFO]
>
>本檔案中概述的限制正在不斷改進。 請定期回來查看更新。 如果您想了解自訂限制，請聯絡客戶服務代表。

## 資料模型限制

以下護欄在建模即時客戶設定檔資料時提供建議的限制。 要進一步了解主要圖元和維圖元，請參閱 [實體類型](#entity-types) 在附錄中。

### 主實體護欄

>[!NOTE]
>
>本節中概述的資料模型限制代表Real-time Customer Data Platform B2B版所啟用的變更。 如需Real-Time CDP B2B版的完整預設限制清單，請將這些限制與 [即時客戶個人檔案資料檔案的護欄](../profile/guardrails.md).

| 瓜德拉伊 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| Real-Time CDP B2B Edition標準XDM類別資料集 | 60 | 軟 | 建議最多使用60個資料集，這些資料集皆採用Real-Time CDP B2B Edition提供的標準Experience Data Model(XDM)類別。 如需B2B使用案例的標準XDM類別完整清單，請參閱 [Real-Time CDP B2B版檔案的綱要](schemas/b2b.md). <br/><br/>*注意：由於Experience Platform的非正常混合資料模型的性質，大多數客戶沒有超過此限制。 若對如何建立資料模型或想進一步了解自訂限制有任何疑問，請連絡您的客戶服務代表。* |
| 舊式多實體關係 | 20 | 軟 | 建議在主實體和維實體之間定義最多20個多實體關係。 在刪除或禁用現有關係之前，不應進行其他關係映射。 |
| 每個XDM類別的多對一關係 | 2 | 軟 | 建議每個XDM類別最多定義2個多對一關係。 在刪除或禁用現有關係之前，不應建立其他關係。 如需如何建立兩個結構間關係的步驟，請參閱 [定義B2B架構關係](../xdm/tutorials/relationship-b2b.md). |

### Dimension實體護欄

>[!NOTE]
>
>本節中概述的資料模型限制代表Real-time Customer Data Platform B2B版所啟用的變更。 如需Real-Time CDP B2B版的完整預設限制清單，請將這些限制與 [即時客戶個人檔案資料檔案的護欄](../profile/guardrails.md).

| 瓜德拉伊 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 無嵌套的舊關係 | 0 | 軟 | 您不應在兩個非[!DNL XDM Individual Profile] 結構。 對於不屬於 [!DNL Profile] 聯合架構。 |
| 只有B2B對象可以參與多對一關係 | 0 | 硬 | 系統僅支援B2B物件之間的多對一關係。 如需多對一關係的詳細資訊，請參閱 [定義B2B架構關係](../xdm/tutorials/relationship-b2b.md). |
| B2B對象之間嵌套關係的最大深度 | 3 | 硬 | B2B物件之間巢狀關係的深度上限為3。 這表示在高度巢狀的架構中，巢狀內嵌的B2B物件之間不應有深度超過3個層級的關係。 |

## 資料大小限制

以下護欄是指資料大小，並針對可如預期擷取、儲存和查詢的資料提供建議的限制。 要進一步了解主要圖元和維圖元，請參閱 [實體類型](#entity-types) 在附錄中。

>[!INFO]
>
>擷取時，資料大小會在JSON中以解壓縮資料的形式測量。

### 主實體護欄

>[!NOTE]
>
>本節中概述的資料大小限制代表Real-time Customer Data Platform B2B Edition所啟用的變更。 如需Real-Time CDP B2B版的完整預設限制清單，請將這些限制與 [即時客戶個人檔案資料檔案的護欄](../profile/guardrails.md).

| 瓜德拉伊 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 每日根據XDM類別批次擷取 | 45 | 軟 | 每個XDM類別每天擷取的批次總數不應超過45個。 接收額外的批次可能會阻止最佳效能。 |

### Dimension實體護欄

>[!NOTE]
>
>本節中概述的資料大小限制代表Real-time Customer Data Platform B2B Edition所啟用的變更。 如需Real-Time CDP B2B版的完整預設限制清單，請將這些限制與 [即時客戶個人檔案資料檔案的護欄](../profile/guardrails.md).

| 瓜德拉伊 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 所有維圖元的總大小 | 5 GB   | 軟 | 所有維度實體的建議總大小為5GB。 擷取大型維度實體可能會影響系統效能。 例如，不建議您嘗試將10GB產品目錄載入為維度實體。 |
| 每維實體結構的資料集 | 5 | 軟 | 建議最多使用5個與每個維度實體結構相關的資料集。 例如，如果您為「產品」建立結構，並新增五個貢獻資料集，則不應建立與產品結構相連結的第六個資料集。 |
| Dimension實體每天擷取批次 | 每個實體4 | 軟 | 建議每天擷取的維度實體批次數上限為每個實體4個。 例如，您每天最多可以擷取4次產品目錄的更新。 為同一實體獲取其他維實體批可能會影響系統效能。 |

## 分段護欄

本節中概述的護欄是指組織可在Experience Platform內建立的區段數量和性質，以及將區段對應和啟用至目的地。

>[!NOTE]
>
>本節中概述的分段限制代表Real-time Customer Data Platform B2B版本所啟用的變更。 如需Real-Time CDP B2B版的完整預設限制清單，請將這些限制與 [即時客戶個人檔案資料檔案的護欄](../profile/guardrails.md).

| 瓜德拉伊 | 限制 | 限制類型 | 說明 |
| --- | --- | --- | --- |
| 每個B2B沙箱的區段 | 400 | 軟 | 只要每個B2B沙箱中的區段少於400個，組織總共可以有超過400個區段。 嘗試建立其他段可能會影響系統效能。 |

## 後續步驟

本檔案中概述的限制代表Real-time Customer Data Platform B2B版所啟用的變更。 如需Real-Time CDP B2B版的完整預設限制清單，請將這些限制與 [即時客戶個人檔案資料檔案的護欄](../profile/guardrails.md).

## 附錄

本節提供本文檔中限制的其他詳細資訊。

### 實體類型

此 [!DNL Profile] 儲存資料模型包含兩種核心實體類型： [主要實體](#primary-entity) 和 [維實體](#dimension-entity).

#### 主要實體

主要實體或設定檔實體會合併資料，為個人形成「單一真相來源」。 此統一資料會使用所謂的「聯合檢視」來表示。 聯合檢視會將實施相同類別之所有結構的欄位匯總至單一聯合結構。 的聯合架構 [!DNL Real-Time Customer Profile] 是非正常的混合資料模型，可作為所有設定檔屬性和行為事件的容器。

與時間無關的屬性（也稱為「記錄資料」）是使用 [!DNL XDM Individual Profile]，而時間序列資料（也稱為「事件資料」）則使用 [!DNL XDM ExperienceEvent]. 在Adobe Experience Platform中擷取記錄和時間序列資料時，就會觸發 [!DNL Real-Time Customer Profile] 開始擷取已啟用供其使用的資料。 擷取的互動和詳細資訊越多，個別設定檔就越健全。

![說明記錄資料和時間序列資料之間差異的資訊圖。](../profile/images/guardrails/profile-entity.png)

#### Dimension實體

雖然設定檔資料存放區維護設定檔資料不是關係存放區，但設定檔允許與小型維度實體整合，以便以簡化且直覺的方式建立區段。 此整合稱為 [多實體分割](../segmentation/multi-entity-segmentation.md).

貴組織也可以定義XDM類別，以說明個人以外的項目，例如商店、產品或屬性。 這些非[!DNL XDM Individual Profile] 結構稱為「維度實體」（也稱為「查詢實體」），且不包含時間序列資料。 表示維實體的結構通過使用連結到配置檔案實體 [模式關係](../xdm/tutorials/relationship-ui.md).

Dimension實體提供查閱資料，這有助於並簡化多實體區段定義，且必須足夠小，以便區段引擎能將整個資料集載入記憶體，以獲得最佳處理（快速點查閱）。

![顯示配置檔案實體由維實體組成的資訊圖。](../profile/images/guardrails/profile-and-dimension-entities.png)