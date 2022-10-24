---
keywords: 資料控管rtcdp;rtcdp資料控管；即時客戶資料設定檔資料控管
title: 資料控管概觀
description: 資料控管可讓您管理客戶資料，並確保符合適用於資料使用的法規、限制和政策。
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Real-Time CDP中的資料控管

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP)將來自多個企業系統的資料匯整在一起，讓行銷人員更能識別、了解客戶，並與其互動。 此資料可能受貴組織或法律法規所定義的使用限制所限制。 因此，在處理資料時，務必確保Real-Time CDP符合使用原則。

Adobe Experience Platform資料控管可讓您管理客戶資料，並確保符合適用於資料使用的法規、限制和政策。 它在Real-Time CDP中扮演關鍵角色，可讓您定義使用原則、根據這些原則對您的資料進行分類，以及在執行特定行銷動作時檢查是否有違反原則的情況。

Real-Time CDP是以Adobe Experience Platform為基礎而建，因此大部分的資料控管功能都會在 [!DNL Experience Platform] 檔案。 本檔案旨在補充 [資料控管概觀](../../data-governance/home.md) for [!DNL Experience Platform]，並概述Real-Time CDP中提供的控管功能。 以下主題將涵蓋介紹：

* [將使用量標籤套用至您的資料](#labels)
* [管理資料使用策略](#policies)
* [強制資料使用合規性](#enforce)

## 將使用量標籤套用至您的資料 {#labels}

資料控管可讓您在資料集或資料集欄位層級，將使用量標籤套用至資料。 資料使用量標籤可讓您根據套用至該資料的使用量原則來分類資料。

如需使用資料使用量標籤的詳細資訊，請參閱 [資料使用標籤使用指南](../../data-governance/labels/overview.md) Adobe Experience Platform。

## 設定目的地的行銷動作 {#destinations}

您可以定義目的地的行銷動作（也稱為行銷使用案例），借此設定目的地的資料使用限制。 目的地的行銷動作會指出要匯出至該目的地之資料的目的。

>[!NOTE]
>
>如需行銷動作及其在資料使用原則中的使用的詳細資訊，請參閱 [資料使用原則概觀](../../data-governance/policies/overview.md) 在 [!DNL Experience Platform] 檔案。

在目的地定義行銷動作可讓您確保傳送至這些目的地的任何設定檔或區段都符合資料使用原則。 因此，您應根據貴組織對啟用強制實施原則限制的需求，將適當的行銷動作新增至您的目的地。

只有在首次設定目的地時，才能選取行銷動作。 根據您使用的目的地類型，設定行銷動作的機會會顯示在設定工作流程中的不同時間點。 請參閱 [目的地檔案](../destinations/overview.md) 以取得設定特定目的地的步驟。

## 管理資料使用策略 {#policies}

為了讓資料使用標籤有效支援資料合規性，必須定義並啟用資料使用策略。 資料使用原則是描述您可在Real-Time CDP內對資料執行或限制執行的行銷動作類型的規則。 請參閱 [!DNL Experience Platform] [資料控管概觀](../../data-governance/home.md) 以取得更多資訊。

Adobe Experience Platform針對常見客戶體驗使用案例提供數個核心原則。 導覽至 **[!UICONTROL 原則]** 工作區和選取 **[!UICONTROL 瀏覽]** 標籤。 請參閱 [原則使用手冊](../../data-governance/policies/user-guide.md) 在 [!DNL Experience Platform] 說明檔案，以取得在UI中使用原則的詳細步驟，包括如何建立您自己的自訂原則。

## 強制資料使用合規性 {#enforce}

在對資料進行標籤並定義使用策略後，您就可以使用策略強制資料使用符合性。 在Real-Time CDP中將對象區段啟用至目的地時，資料控管會在發生任何違反情形時自動強制使用原則。

請參閱 [自動策略執行](../../data-governance/enforcement/auto-enforcement.md) 以取得更多資訊。

## 後續步驟

現在您已熟悉Real-Time CDP的重要資料控管功能，以及如何 [!DNL Experience Platform] 啟用，請繼續 [Adobe Experience Platform上的資料控管檔案](../../data-governance/home.md). 本檔案提供基本資料控管概念的概述，以及管理資料使用標籤和原則的逐步工作流程。

以下影片概略介紹Real-Time CDP中的資料控管，包括針對不同案例使用行銷使用案例和工作流程範例：

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
