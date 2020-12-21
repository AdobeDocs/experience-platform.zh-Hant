---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance
title: 資料治理概觀
seo-title: 即時客戶資料平台中的資料治理
description: '「資料管理」可讓您管理客戶資料，並確保符合適用於資料使用的法規、限制和政策。 '
seo-description: '「資料管理」可讓您管理客戶資料，並確保符合適用於資料使用的法規、限制和政策。 '
translation-type: tm+mt
source-git-commit: e680191d495e4c33baa8242d40a15b9124eec8cd
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---


# [!DNL Data Governance] 即時CDP

[!DNL Real-time Customer Data Platform] （即時CDP）將來自多個企業系統的資料整合在一起，讓行銷人員能夠更好地識別、瞭解並吸引客戶。此資料可能受您組織或法律法規所定義的使用限制所約束。 因此，在處理資料時，務必確保即時CDP符合使用策略。

Adobe Experience Platform [!DNL Data Governance]可讓您管理客戶資料，並確保符合資料使用適用的法規、限制和政策。 它在即時CDP中扮演了關鍵角色，允許您定義使用策略、根據這些策略對資料進行分類，以及在執行某些行銷操作時檢查是否違反策略。

即時CDP建立在Adobe Experience Platform之上，因此[!DNL Data Governance]檔案中涵蓋了大部分的功能。 [!DNL Experience Platform]本文檔旨在補充[[!DNL Experience Platform]的](../../data-governance/home.md)資料治理概述，並概述即時CDP中提供的治理功能。 涵蓋下列主題：

* [將使用標籤套用至您的資料](#labels)
* [管理資料使用原則](#policies)
* [強制符合資料使用規範](#enforce)

## 將使用標籤套用至您的資料{#labels}

[!DNL Data Governance] 可讓您在資料集或資料集欄位層級，將使用標籤套用至您的資料。資料使用標籤可讓您根據套用至該資料的使用原則來分類資料。

如需使用資料使用標籤的詳細資訊，請參閱[資料使用標籤使用指南](../../data-governance/labels/overview.md) for Adobe Experience Platform。

## 設定目標{#destinations}的行銷使用案例

您可以定義目標的行銷使用案例（也稱為行銷動作），以設定目標的資料使用限制。 目的地的行銷使用案例會指出將匯出至該目的地的資料意圖。

>[!NOTE]
>
>如需有關行銷動作及其在資料使用政策中使用的詳細資訊，請參閱[!DNL Experience Platform]檔案中的[資料使用政策概述](../../data-governance/policies/overview.md)。

定義目的地的行銷使用案例可讓您確保傳送至這些目的地的任何描述檔或區段符合資料使用政策。 因此，您應根據組織對啟動實施政策限制的需求，將適當的行銷使用案例新增至您的目的地。

行銷使用案例只能在第一次設定目標時選取。 根據您使用的目的地類型，設定行銷使用案例的機會會顯示在設定工作流程的不同點。 有關如何配置特定目標的步驟，請參閱[目標文檔](../destinations/overview.md)。

## 管理資料使用策略{#policies}

為了讓資料使用標籤有效支援資料遵循，必須定義並啟用資料使用原則。 資料使用原則是描述您允許或限制在即時CDP中對資料執行的行銷動作類型的規則。 如需詳細資訊，請參閱[!DNL Experience Platform] [資料治理概觀](../../data-governance/home.md)中的「資料使用政策」一節。

Adobe Experience Platform針對常見客戶體驗使用案例提供數個核心政策。 瀏覽至&#x200B;**[!UICONTROL Policys]**&#x200B;工作區並選擇&#x200B;**[!UICONTROL Browse]**&#x200B;標籤，即可在UI中檢視這些原則。 請參閱[!DNL Experience Platform]說明檔案中的[原則使用指南](../../data-governance/policies/user-guide.md)，以取得在UI中使用原則的詳細步驟，包括如何建立您自己的自訂原則。

## 強制符合資料使用規定{#enforce}

在標籤資料並定義使用策略後，您就可以強制資料使用與策略相符。 在即時CDP中激活對象段至目標時，[!DNL Data Governance]會在發生任何違規時自動實施使用策略。

如需詳細資訊，請參閱[自動原則實施](../../data-governance/enforcement/auto-enforcement.md)上的檔案。

## 後續步驟

現在，您已經介紹了Real-time CDP的[!DNL Data Governance]主要功能，以及[!DNL Experience Platform]如何啟用這些功能，請繼續閱讀有關Adobe Experience Platform](../../data-governance/home.md)資料治理的[檔案。 本檔案提供基本[!DNL Data Governance]概念的概觀，以及管理資料使用標籤和原則的逐步工作流程。

以下視頻概述了即時CDP中的[!DNL Data Governance] ，包括對目標的市場營銷使用案例以及不同方案的示例工作流：

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)