---
keywords: 資料控管rtcdp；rtcdp資料控管；即時客戶資料設定檔資料控管
title: 資料治理概觀
description: 資料控管可讓您管理客戶資料，並確保遵守適用於資料使用的法規、限制和原則。
feature: Get Started, Data Governance
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 3%

---

# Real-Time CDP中的資料控管

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP)將來自多個企業系統的資料彙集在一起，讓行銷人員更能識別、瞭解客戶，並與客戶互動。 此資料可能受貴組織或法律法規所定義的使用限制所約束。 因此，在處理您的資料時，請務必確保Real-Time CDP符合使用原則。

Adobe Experience Platform資料控管可讓您管理客戶資料，並確保遵守適用於資料使用的法規、限制和政策。 它在Real-Time CDP中起著關鍵作用，可讓您定義使用原則、根據這些原則將資料分類，以及在執行某些行銷動作時檢查原則違規。

Real-Time CDP是以Adobe Experience Platform為建置基礎，因此[!DNL Experience Platform]檔案中涵蓋了大部分資料控管功能。 本檔案旨在補充[!DNL Experience Platform]的[資料控管總覽](../../data-governance/home.md)，並概述Real-Time CDP中可用的控管功能。 以下主題將涵蓋介紹：

* [將使用標籤套用至您的資料](#labels)
* [管理資料使用原則](#policies)
* [強制資料使用規範](#enforce)

## 將使用標籤套用至您的資料 {#labels}

資料控管可讓您在資料集或資料集欄位層級，將使用標籤套用至資料。 資料使用情況標籤可讓您根據套用至該資料的使用原則將資料分類。

如需使用資料使用標籤的詳細資訊，請參閱Adobe Experience Platform的[資料使用標籤使用手冊](../../data-governance/labels/overview.md)。

## 設定目的地的行銷動作 {#destinations}

您可以定義目的地的行銷動作（也稱為行銷使用案例），藉此設定目的地的資料使用限制。 目的地的行銷動作會指出匯出至該目的地的資料意圖。

>[!NOTE]
>
>如需有關行銷動作及其在資料使用原則中之使用的詳細資訊，請參閱[!DNL Experience Platform]檔案中的[資料使用原則概觀](../../data-governance/policies/overview.md)。

對目的地定義行銷動作可讓您確保傳送至這些目的地的任何設定檔或對象都符合資料使用原則。 因此，您應該根據組織對啟用實施原則限制的需求，將適當的行銷動作新增到您的目的地。

行銷動作只能在第一次設定目的地時選取。 根據您使用的目的地型別，設定行銷動作的機會會顯示在設定工作流程的不同位置。 請參閱[目的地檔案](../destinations/overview.md)，以瞭解如何設定特定目的地的步驟。

## 管理資料使用原則 {#policies}

為了使資料使用標籤有效地支援資料合規性，必須定義並啟用資料使用原則。 資料使用原則是描述允許或限制您在Real-Time CDP中對資料執行的行銷動作型別的規則。 如需詳細資訊，請參閱[!DNL Experience Platform] [資料控管概觀](../../data-governance/home.md)中的「資料使用原則」一節。

Adobe Experience Platform為常見客戶體驗使用案例提供數項核心原則。 您可以導覽至&#x200B;**[!UICONTROL 原則]**&#x200B;工作區並選取&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤，在UI中檢視這些原則。 請參閱[!DNL Experience Platform]檔案中的[原則使用手冊](../../data-governance/policies/user-guide.md)，以取得在UI中使用原則的詳細步驟，包括如何建立您自己的自訂原則。

## 強制資料使用規範 {#enforce}

一旦標籤資料並定義使用原則，您就可以強制資料使用符合原則。 在Real-Time CDP中啟用目的地的對象時，資料控管會在任何違規發生時自動強制執行使用原則。

如需詳細資訊，請參閱[自動原則執行](../../data-governance/enforcement/auto-enforcement.md)上的檔案。

## 後續步驟

現在您已瞭解Real-Time CDP上的主要資料控管功能以及[!DNL Experience Platform]如何啟用這些功能，請繼續參閱[Adobe Experience Platform上的資料控管檔案](../../data-governance/home.md)。 本檔案提供基本資料控管概念的概觀，以及管理資料使用標籤和原則的逐步工作流程。

下列影片提供Real-Time CDP中資料控管的概觀，包括在目的地使用行銷使用案例，以及不同情境的範例工作流程：

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
