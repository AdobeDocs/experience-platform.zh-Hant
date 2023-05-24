---
keywords: 資料管理rtcdp;rtcdp資料治理；即時客戶資料配置檔案資料治理
title: 資料治理概述
description: 資料治理允許您管理客戶資料並確保遵守適用於資料使用的法規、限制和策略。
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 3%

---

# Real-Time CDP的資料治理

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP)將來自多個企業系統的資料匯集在一起，使營銷商能夠更好地識別、理解和吸引客戶。 此資料可能受貴組織或法律法規所定義的使用限制所約束。 因此，在處理資料時，必須確保Real-Time CDP遵守使用策略。

Adobe Experience Platform資料治理允許您管理客戶資料並確保遵守適用於資料使用的法規、限制和策略。 它在Real-Time CDP發揮著關鍵作用，允許您定義使用策略、根據這些策略對資料進行分類，以及在執行某些市場營銷操作時檢查策略違規。

Real-Time CDP建在Adobe Experience Platform之上，因此大多數資料治理功能都包含在 [!DNL Experience Platform] 文檔。 本文檔旨在補充 [資料治理概述](../../data-governance/home.md) 為 [!DNL Experience Platform]，並概述在Real-Time CDP提供的治理功能。 以下主題將涵蓋介紹：

* [將使用標籤應用於資料](#labels)
* [管理資料使用策略](#policies)
* [強制資料使用符合性](#enforce)

## 將使用標籤應用於資料 {#labels}

資料管理允許您在資料集或資料集欄位級別將使用標籤應用於資料。 資料使用標籤允許您根據應用於該資料的使用策略對資料進行分類。

有關使用資料使用標籤的詳細資訊，請參閱 [資料使用標籤使用手冊](../../data-governance/labels/overview.md) Adobe Experience Platform。

## 配置目標的市場營銷活動 {#destinations}

您可以通過定義目標的市場營銷活動（也稱為市場營銷使用案例）來設定目標的資料使用限制。 目標的市場營銷操作指示要導出到該目標的資料的意圖。

>[!NOTE]
>
>有關市場營銷操作及其在資料使用策略中的使用的詳細資訊，請參閱 [資料使用策略概述](../../data-governance/policies/overview.md) 的 [!DNL Experience Platform] 文檔。

定義目標上的市場營銷活動允許您確保發送到這些目標的任何配置檔案或段符合資料使用策略。 因此，您應根據組織在激活策略限制方面的需要，將適當的市場營銷活動添加到目標。

只有在首次設定目標時才能選擇市場營銷操作。 根據您正在使用的目標類型，配置市場營銷活動的機會將出現在設定工作流中的不同點。 查看 [目標文檔](../destinations/overview.md) 有關如何配置特定目標的步驟。

## 管理資料使用策略 {#policies}

為了使資料使用標籤有效支援資料合規性，必須定義並啟用資料使用策略。 資料使用策略是描述允許或限制您對Real-Time CDP內的資料執行的市場營銷操作類型的規則。 請參閱中的「資料使用策略」部分 [!DNL Experience Platform] [資料治理概述](../../data-governance/home.md) 的子菜單。

Adobe Experience Platform為常見客戶體驗使用案例提供了幾項核心政策。 通過導航到 **[!UICONTROL 策略]** 工作區並選擇 **[!UICONTROL 瀏覽]** 頁籤。 查看 [策略使用手冊](../../data-governance/policies/user-guide.md) 的 [!DNL Experience Platform] 文檔，瞭解有關在UI中使用策略的更詳細步驟，包括如何制定您自己的自定義策略。

## 強制資料使用符合性 {#enforce}

一旦標籤了資料並定義了使用策略，您就可以強制資料使用與策略的一致性。 在將受眾段激活到Real-Time CDP的目的地時，資料治理會在發生任何違規時自動實施使用策略。

查看上的文檔 [自動策略執行](../../data-governance/enforcement/auto-enforcement.md) 的子菜單。

## 後續步驟

現在，您已經介紹了有關Real-Time CDP的關鍵資料治理功能以及如何 [!DNL Experience Platform] 啟用它們，請繼續 [關於Adobe Experience Platform的資料治理文檔](../../data-governance/home.md)。 本文檔提供了基本資料治理概念的概述，以及用於管理資料使用標籤和策略的逐步工作流。

以下視頻概述了Real-Time CDP的資料治理，包括針對不同方案使用目標和示例工作流的營銷使用案例：

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
