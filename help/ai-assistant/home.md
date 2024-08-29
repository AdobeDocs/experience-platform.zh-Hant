---
title: Adobe Experience Platform中的AI助理概述
description: 了解 AI 助理、其細微差別和使用案例，以及如何使用它來加快 Adobe Experience Platform 和 Real-Time Customer Data Platform 的工作流程。
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: fc87c28d7019e123d974e4d2ad307928a3d3fe89
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 8%

---

# Adobe Experience Platform中的AI助理

請閱讀本檔案，瞭解Adobe Experience Platform中的AI助理。

Adobe Experience Platform中的AI助理是一種對話式體驗，可用來加速Adobe應用程式中的工作流程。 您可以使用AI Assistant來進一步瞭解產品知識、疑難排解問題，或搜尋資訊並尋找營運見解。 AI助理支援Experience Platform、Real-time Customer Data Platform、Adobe Journey Optimizer和Customer Journey Analytics。

![首次觸發使用者體驗的AI助理介面。](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>您必須先同意[使用者合約](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)，才能使用AI小幫手。 使用者合約也包含公開測試版合約。 這樣一來，您就可以在以Beta版容量推出其他AI Assistant功能時使用它們。

+++選取以檢視使用者合約介面

![使用者合約的第一頁。](./images/user-agreement-1.png)

![使用者合約的最後一頁。](./images/user-agreement-2.png)

+++

## 瞭解AI助理 {#understanding-ai-assistant}

AI Assistant會查詢資料庫，然後將資料庫中的資料轉譯成人類看得懂的答案，以回應您提交的問題。

此基礎資料的內部表示也稱為&#x200B;**[!DNL Knowledge Graph]** — 特定答案的概念、資料和中繼資料的完整網路。

[!DNL Knowledge Graph]包含每次提交查詢時所參考的子圖形：

* 客戶營運分析。
* 各種中繼商店的客戶營運分析。
* Experience League檔案。

在查詢AI Assistant之前，需要考慮兩種型別的問題：

### 產品知識 {#product-knowledge}

產品知識是以Experience League檔案為根據的概念和主題。 產品知識問題可進一步指定到下列子群組中：

| 產品知識 | 範例 |
| --- | --- |
| 點式學習 | <ul><li>身分識別與主要或外部索引鍵之間有何差異？</li><li>如何計算設定檔豐富度？</li></ul> |
| 開啟探索 | <ul><li>如何匯出此資料集？</li><li>是否有適用於醫療保健客戶的結構描述？</li></ul> |
| 疑難排解 | <ul><li>為什麼我無法為設定檔開啟Adobe擁有的結構描述？</li><li>我為何刪除不了區段？</li></ul> |

{style="table-layout:auto"}

### 運作深入分析 {#operational-insights}

>[!IMPORTANT]
>
>營運見解答案為測試版。 有權存取&#x200B;**檢視營運分析**&#x200B;許可權的任何人將有權存取營運分析答案。

營運深入分析是指回答AI助理產生的中繼資料物件（屬性、受眾、資料流、資料集、目的地、歷程、結構描述和來源），包括計數、查閱和歷程影響。 它不會檢視沙箱中的任何資料。

* 我有多少資料集？
* 有多少結構描述屬性從未使用過？
* 已啟用哪些對象？

您可以在下列網域中向AI Assistant詢問有關您的營運見解的問題：

| 網域 | 支援的中繼資料 | 不支援的中繼資料 |
| --- | --- | --- |
| 屬性 | <ul><li>屬性名稱搜尋</li><li>屬性 — 結構描述關係</li><li>屬性 — 資料集關係</li><li>屬性 — 對象關係</li><li>屬性 — 目的地關係</li></ul> | <ul><li>屬性類別</li><li>稽核</li><li>淘汰狀態</li><li>標記</li><li>儲存在屬性中的值</li></ul> |
| 客群 | <ul><li>客群計數</li><li>對象型別（串流或批次）</li><li>建立/修改日期</li><li>啟用狀態</li><li>設定檔計數</li><li>複製對象</li><li>對象定義搜尋</li><li>對象 — 對象關係</li><li>對象 — 屬性關係</li><li>對象 — 資料集關係</li><li>對象 — 目的地關係</li><li>名稱搜尋</li><li>名稱和ID搜尋 | <ul><li>對象重疊</li><li>客群啟用</li><li>對象 — 行銷活動關係</li><li>稽核</li><li>建立/修改</li><li>標記</li><li>設定檔資格趨勢</li></ul> |
| 資料流 | <ul><li>資料流計數</li><li>資料流程狀態</li><li>資料流 — 資料集關係</li><li>資料流 — 來源關係</li></ul> | <ul><li>建立/修改</li><li>資料流 — 批次關係</li><li>擷取設定檔計數</li></ul> |
| 資料集 | <ul><li>資料集計數</li><li>設定檔啟用狀態</li><li>建立/修改日期</li><li>資料集 — 結構描述關係</li><li>資料集 — 對象關係</li><li>資料集 — 屬性關係</li><li>資料集 — 資料流關係</li><li>名稱搜尋 </li><li>名稱和ID搜尋</li></ul> | <ul><li>稽核</li><li>建立者：</li><li>資料集 — 批次關係</li><li>資料集建立/修改</li><li>資料集大小</li><li>設定檔數</li><li>列數</li><li>值搜尋</li></ul> |
| 目的地 | <ul><li>設定的目的地計數</li><li>目的地 — 對象關係</li><li>目的地屬性關係</li></ul> | <ul><li>帳戶設定</li><li>帳戶認證資訊</li><li>啟用的不重複設定檔</li></ul> |
| 歷程 | <ul><li>計數</li><li>名稱搜尋</li><li>名稱和ID搜尋</li><li>歷程狀態</li><li>觸發狀態（對象與事件）</li><li>建立/修改日期</li><li>循環頻率</li></ul> | <ul><li>屬性 — 歷程關係</li><li>稽核</li><li>建立/修改</li><li>建立者：</li><li>活動</li><li>歷程 — 資料集</li><li>歷程 — 結構描述</li><li>優惠</li><li>設定檔資格趨勢</li><li>步驟事件</li></ul> |
| 結構描述 | <ul><li>結構描述計數</li><li>建立/修改日期</li><li>結構描述 — 屬性關係</li><li>結構描述 — 資料集關係</li><li>結構描述 — 對象關係</li><li>設定檔啟用狀態</li><li>名稱搜尋</li><li>名稱和ID搜尋</li></ul> | <ul><li>稽核</li><li>建立/修改</li><li>建立者：</li><li>欄位群組</li><li>身分</li><li>身分識別命名空間</li><li>標記</li><li>設定檔數</li></ul> |
| 來源 | <ul><li>帳戶計數</li><li>帳戶狀態</li><li>每個帳戶的作用中/非作用中資料流</li><li>Source聯結器 — 資料流關係</li><li>Source帳戶 — 資料流關係</li></ul> | <ul><li>帳戶認證資訊</li><li>帳戶設定</li><li>資料擷取量度</li><li>設定檔數</li><li>Source — 批次關係</li></ul> |

{style="table-layout:auto"}

若是操作見解問題，答案可能不會反映UI的目前狀態。 支援這些問題的資料每24小時更新一次。 例如，使用者白天在Real-Time CDP中所做的變更會在夜間與資料存放區同步，然後早上就可供使用者提問。 您需要登入沙箱以查詢與物件相關的特定資料。

### 功能範圍 {#feature-scope}

目前，AI助理的範圍如下：

* [產品知識](./home.md#product-knowledge)： AI助理可以回答Experience Platform、Real-time Customer Data Platform和Adobe Journey Optimizer的產品知識問題。 您也可以深入探討Customer Journey Analytics的產品知識主題，但必須透過Customer Journey AnalyticsUI。
* [營運分析](./home.md#operational-insights)：您可以向AI助理詢問有關下列資料物件的營運分析問題：屬性、對象、資料流、資料集、目的地、歷程、結構描述和來源。

## 後續步驟

現在您已大致瞭解AI助理，您可以繼續並在工作流程中使用AI助理。 如需詳細資訊，請參閱下列檔案：

* [AI助理使用者介面指南](./ui-guide.md)
* [功能存取](./access.md)
* [問題指南](./questions.md)
* [AI助理的隱私權、安全性和控管](./privacy.md)
* [常見問題集](./faq.md)
