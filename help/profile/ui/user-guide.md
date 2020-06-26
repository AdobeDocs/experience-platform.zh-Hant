---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 即時客戶基本資料使用指南
topic: guide
translation-type: tm+mt
source-git-commit: 59dff7687f8a0c5b5084eb1ce7dd222cc18d8dbf
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 0%

---


# 即時客戶基本資料使用指南

即時客戶個人檔案可讓您對個別客戶建立全方位的檢視，並結合來自多個通道的資料，包括線上、離線、CRM和協力廠商資料。

本檔案可做為在Adobe Experience Platform使用者介面中與即時客戶個人檔案互動的指南。

## 快速入門

本使用指南需要瞭解與管理即時客戶個人檔案有關的各種Experience Platform服務。 閱讀本使用指南之前，請先閱讀下列服務的說明檔案：

* [即時客戶個人檔案](../home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [身分服務](../../identity-service/home.md): 當不同資料來源的身分被收錄到平台時，可橋接其身分，以建立即時客戶個人檔案。
* [體驗資料模型(XDM)](../../xdm/home.md): 平台組織客戶體驗資料的標準化架構。

## 概述

在 [Experience Platform UI](http://platform.adobe.com)，按一下左側導 **覽中的Profiles** ，以開啟 _Overview_ 標籤。 此標籤提供檔案和影片的連結，以協助您瞭解並開始使用描述檔。

![](../images/user-guide/profiles-overview.png)

## 瀏覽

選擇「瀏 *覽* 」頁籤，以便按身份瀏覽配置檔案。

![](../images/user-guide/profiles-browse.png)

### 描述檔度量 {#profile-metrics}

在「瀏覽」標籤的右側是幾個與您的描述檔資料相關的重要度量，包括您的 *描述檔總數* ，以及依命名空間 [的描述檔清單](#profile-count)[](#profiles-by-namespace)。

這些描述檔度量會使用您組織的預設合併原則來評估。 有關使用合併策略的詳細資訊，包括如何定義預設合併策略，請參閱合 [並策略使用手冊](merge-policies.md)。

除了這些量度外，描述檔量度區段也提供「上次更新 *的日期* 」和時間，顯示上次評估量度的時間。

![](../images/user-guide/profiles-profile-metrics.png)

### 描述檔計數 {#profile-count}

在組織的預設合併政策將描述檔片段合併為每個個別客戶組成單一描述檔後，描述檔計數會顯示您組織在Experience Platform中擁有的描述檔總數。 換言之，您的組織可能有多個與跨不同通道與品牌互動的單一客戶相關的描述檔片段，但這些片段會合併在一起（根據預設合併政策），並會傳回「1」個描述檔計數，因為這些片段都與同一個人相關。

描述檔計數也包含具有屬性（記錄資料）的描述檔，以及僅包含時間系列（事件）資料的描述檔，例如Adobe Analytics描述檔。 設定檔計數會定期重新整理，以提供平台內設定檔的最新總數。

當將記錄提取到Profile Store時，計數會增加或減少5%以上，則會觸發一個作業以更新計數。 對於串流資料工作流程，會每小時檢查一次，以判斷是否符合5%增加或減少臨界值。 如果已觸發，則會自動觸發作業以更新描述檔計數。 對於批處理，在成功將批處理到配置檔案儲存的15分鐘內，如果達到5%增加或減少閾值，則運行作業以更新配置檔案計數。

### 依命名空間劃分的描述檔 {#profiles-by-namespace}

「依命 *名空間劃分的描述檔* 」度量會顯示描述檔商店中所有合併描述檔的名稱空間總數和劃分。 依名稱空間劃分的描述檔總數（換言之，將每個名稱空間顯示的值加在一起）將永遠高於描述檔計數量度，因為一個描述檔可能有多個與其關聯的名稱空間。 例如，如果客戶在多個通道上與您的品牌互動，則多個名稱空間將與該個別客戶關聯。

與描述檔 [計數量度類似](#profile-count) ，當將記錄擷取至描述檔商店時，將計數增加或減少超過5%，則會觸發工作以更新命名空間量度。 對於串流資料工作流程，會每小時檢查一次，以判斷是否符合5%增加或減少臨界值。 如果已觸發，則會自動觸發作業以更新描述檔計數。 對於批次擷取，在成功將批次擷取至描述檔商店的15分鐘內，如果達到5%增加或減少臨界值，則會執行工作以更新量度。

### 合併原則

「合 **並策略** 」選擇器會自動為您的組織選擇預設的合併策略。 如果不想使用該合併策略，可以選擇預設合併策略旁邊的 `X` ，以開啟「選擇合併策略 ** 」對話框，您可以在其中選擇其他合併策略。 要瞭解有關合併策略的更多資訊，請參 [閱合併策略使用手冊](merge-policies.md)。

![](../images/user-guide/profiles-search-merge-policy.png)

### 身分命名空間

「 **Identity namespace** 」選擇器會開啟一個對話方塊，您可以在其中選擇要搜尋的身分名稱空間，也可以自訂從搜尋中顯示的屬性，方法是選取篩選圖示並選擇您要新增或移除的屬性。

![](../images/user-guide/profiles-search-filter.png)

從「選 *取身分名稱空間* 」對話方塊中，選擇您要搜尋的名稱空間，或使用對話方塊中的「搜尋 **** 」列開始輸入名稱空間的名稱。 您可以選擇一個命名空間來查看其他詳細資訊，一旦找到要搜索的命名空間後，可以選擇單選按鈕，然後按 **Select** 繼續。

![](../images/user-guide/profiles-select-identity-namespace.png)

### 身分值

在選取 **Identity命名空間**，您會返回「 *Browse* 」（瀏覽）標籤，您可在其中輸入 **Identity值**。 此值是個別客戶個人檔案專屬的值，必須是提供之命名空間的有效項目。 例如，選取 **Identity namespace** &quot;Email&quot;需要 **Identity值** ，以有效電子郵件地址的形式。

![](../images/user-guide/profiles-show-profile.png)

輸入值後，選擇「顯示配 **置檔案** 」並返回與值匹配的單個配置檔案。 選擇「 **Profile ID** 」（配置檔案ID）以查看配置檔案詳細資訊。

![](../images/user-guide/profiles-display-profile.png)

### 描述檔詳細資料

在選擇「配置 **式ID**」後， _將開啟_ 「詳細資訊」頁籤。 此頁顯示有關所選配置檔案的資訊，包括基本屬性、連結身份和可用聯繫渠道。 顯示的描述檔資訊已從多個描述檔片段合併在一起，以形成個別客戶的單一檢視。

![](../images/user-guide/profiles-profile-detail.png)

您可以檢視與描述檔相關的其他資訊，包括 *描述檔所屬*、事件和 **** 區段。

![](../images/user-guide/profiles-attributes-events-segments.png)

## 合併原則

選擇「合 *並策略* 」頁籤可查看屬於您組織的合併策略清單。 每個列出的策略都顯示其名稱，無論它是否是預設合併策略，以及它所應用的方案。

有關合併策略的詳細資訊，請參閱合 [並策略使用手冊](merge-policies.md)。

![](../images/user-guide/profiles-merge-policies.png)

## 聯合模式

選擇「 *聯合方案* 」頁籤，查看配置檔案儲存的聯合方案。 聯合模式是同一類下所有Experience Data Model(XDM)欄位的合併，該類中的模式可用於即時客戶配置檔案。 在左側清單中選擇一個類，以在畫布中查看其聯合架構的結構。

例如，選擇「XDM配置檔案」會顯示XDM單個配置檔案類的聯合模式。

有關聯合方案及其在即時客戶概要檔案 [中的角色的詳細資訊](../../xdm/schema/composition.md) ，請參閱方案組合指南中有關聯合方案的部分。

![](../images/user-guide/profiles-union-schema.png)

## 後續步驟

閱讀本指南，您現在知道如何使用Experience Platform UI檢視和管理您的個人檔案資料。 如需如何運用即時客戶個人檔案資料產生受眾細分的詳細資訊，請參閱細分 [檔案](../../segmentation/home.md)。