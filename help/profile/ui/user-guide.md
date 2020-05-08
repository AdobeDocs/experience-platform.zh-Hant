---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 即時客戶基本資料使用指南
topic: guide
translation-type: tm+mt
source-git-commit: 667aadde831a1d010f8cbbbb20bd92f914558bd1
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---


# 即時客戶基本資料使用指南

即時客戶個人檔案可讓您對個別客戶建立全方位的檢視，並結合來自多個通道的資料，包括線上、離線、CRM和協力廠商資料。

本檔案可做為在Adobe Experience Platform使用者介面中與即時客戶個人檔案互動的指南。

## 快速入門

本使用指南需要瞭解與管理即時客戶個人檔案有關的各種Experience Platform服務。 閱讀本使用指南之前，請先閱讀下列服務的說明檔案：

* [即時客戶個人檔案](../home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [身分服務](../../identity-service/home.md): 借由橋接來自不同資料來源的身分，並將之收錄至平台，以建立即時客戶個人檔案。
* [體驗資料模型(XDM)](../../xdm/home.md): 平台組織客戶體驗資料的標準化架構。

## 描述檔概述

在Experience Platform UI中 [，按一下左側導覽中的「設定檔](http://platform.adobe.com)」，以開啟「設定檔」工作區 **的「概述** 」 ____ 標籤。 此標籤會顯示數個介面工具集，提供描述檔商店的高階資訊，包括可定址對象總數、上週內收錄的描述檔記錄數，以及同一時段成功和失敗記錄的統計資料。

![](../images/user-guide/profile-overview.png)

## 檢視描述檔範例

按一 **下「瀏覽** 」以檢視可用描述檔的範例清單。 此範例包含來自您總個人檔案計數的最多50個 [個人檔案](#profile-count)。 樣本由自動作業重新整理，該作業會在擷取新的描述檔資料時加以擷取。 每個列出的描述檔都會顯示其ID、名字、姓氏和個人電子郵件。 按一下列出的描述檔ID，會在描述檔檢視器中顯示其 [詳細資訊](#profile-viewer)。

![](../images/user-guide/profile-samples.png)

您可以按一下欄選擇器圖示來自訂清單中顯示的屬性。 這會顯示一個下拉式清單，其中包含您可新增或移除的常用描述檔屬性。

![](../images/user-guide/column-selector.png)

### 描述檔計數 {#profile-count}

在組織的預設合併政策將描述檔片段合併為每個個別客戶組成單一描述檔後，描述檔計數會顯示您組織在Experience Platform中擁有的描述檔總數。 換言之，您的組織可能有多個與跨不同通道與品牌互動的單一客戶相關的描述檔片段，但這些片段會合併在一起（根據預設合併政策），並會傳回「1」個描述檔計數，因為這些片段都與同一個人相關。

描述檔計數也包含具有屬性（記錄資料）的描述檔，以及僅包含時間系列（事件）資料的描述檔，例如Adobe Analytics描述檔。 設定檔計數會定期重新整理，以提供平台內設定檔的最新總數。

當將配置式提取到Profile Store時，計數會增加或減少5%以上，則會觸發作業以更新計數。 對於串流資料工作流程，會每小時檢查一次，以判斷是否符合5%增加或減少臨界值。 如果已觸發，則會自動觸發作業以更新描述檔計數。 對於批處理，在成功將批處理到配置檔案儲存的15分鐘內，如果達到5%增加或減少閾值，則運行作業以更新配置檔案計數。

![](../images/user-guide/profile-count.png)

### 描述檔搜尋

如果您知道特定描述檔的連結身分（例如其電子郵件位址），可以按一下「尋找描述檔」來尋 **找該描述檔**。 這是存取特定描述檔最可靠的方式，不論其是否出現在範例清單中。

![](../images/user-guide/find-a-profile.png)

在出現的對話方塊中，從下拉式清單（此範例中為「電子郵件」）中選取適當的ID名稱空間，然後在按一下「確定」之前，輸入下方的ID **值**。 如果找到，則定位描述檔的詳細資料會顯示在描述檔檢視器中，如下一節所述。

![](../images/user-guide/find-a-profile-details.png)

### 設定檔檢視器 {#profile-viewer}

在選取或搜尋特定描述檔時，描述檔檢視器的 _「詳細資訊_ 」畫面隨即開啟。 此頁顯示有關所選配置檔案的資訊，如配置檔案的基本屬性、連結的身份和可用聯繫渠道。 顯示的描述檔資訊已從多個描述檔片段合併在一起，以形成個別客戶的單一檢視。

![](../images/user-guide/profile-viewer-detail.png)

描述檔檢視器也提供標籤，可讓您檢視與此描述檔相關的事件和區段成員資格（如果有的話）。

![](../images/user-guide/profile-viewer-events-seg.png)

## 合併原則

按一下 **合併策略** ，查看屬於您組織的合併策略清單。 每個列出的策略都顯示其名稱，無論它是否是預設合併策略，以及它所應用的方案。

![](../images/user-guide/profile-merge-policies.png)

有關在UI中使用合併策略的詳細資訊，請參閱合 [並策略使用手冊](merge-policies.md)。

## 聯合模式

按一下 **Union Schema** （聯合模式）可查看配置檔案資料儲存的聯合模式。 聯合模式是同一類下所有Experience Data Model(XDM)欄位的合併，該類中的模式可用於即時客戶配置檔案。 按一下左側清單中的類別，在畫布中檢視其聯合架構的結構。

![](../images/user-guide/profile-union-schema.png)

有關聯合方案及其在即時客戶配置檔案中 [的角色的詳細資訊](../../xdm/schema/composition.md) ，請參閱方案組合指南中關於聯合方案的部分。

## 後續步驟

閱讀本指南，您現在知道如何使用Experience Platform UI檢視和管理您的個人檔案資料。 如需如何運用即時客戶個人檔案資料產生受眾細分的詳細資訊，請參閱細分 [檔案](../../segmentation/home.md)。