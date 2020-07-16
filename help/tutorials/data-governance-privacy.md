---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料管理與隱私權教學課程
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# [!DNL Data Governance] 和教 [!DNL Privacy] 學課程

[!DNL Data Usage Labeling and Enforcement] (DULE)是Adobe Experience Platform [!DNL Data Governanc]e的核心機制。 DULE功能可讓您將資料使用量標籤套用至資料集和欄位，並依據相關資料使用策略將每個標籤分類。 在開始使用標籤之前，請參閱 [Data Governance概觀](../data-governance/home.md) ，以取得DULE架構的更強穩簡介 [!DNL Platform]。

Adobe Experience Platform提 [!DNL Privacy Service] 供REST風格的API和使用者介面，讓您協調各種解決方案的隱私權和合規性要求。 若要進一步瞭解，請先閱讀隱私權 [服務概觀](../privacy-service/home.md)。

## 新增資料使用標籤

資料使用標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 標籤可隨時套用，提供您選擇控制資料的彈性。 最佳做法鼓勵在資料被吸收或資料可供使 [!DNL Experience Platform]用時，立即加上標籤 [!DNL Platform]。 在資料集層級套用的資料使用標籤會傳播至資料集內的所有欄位。 標籤也可以直接套用至資料集中的個別欄位（欄標題），而不需傳播。 若要瞭解如何將資料使用標籤套用至您的資料，請造訪資料使 [用標籤總覽](../data-governance/labels/overview.md)。

## 建立資料使用原則

DULE [!DNL Policy Service] API可讓您建立和管理DULE原則，以決定可針對包含特定DULE標籤的資料採取哪些行銷動作。 若要開始，請閱讀資料使 [用政策概觀](../data-governance/policies/overview.md)。

## 強制實施資料使用原則

在您為資料建立「資料使用標籤與實施」(DULE)標籤，並針對這些標籤建立行銷動作的DULE原則後，您就可以使用DULE [!DNL Policy Service] API來評估在資料集上執行的行銷動作或任意DULE標籤群組是否構成策略違規。 然後，您可以設定自己的內部通訊協定，以根據API回應來處理原則違規。 若要開始，請造訪原 [則實施概觀](../data-governance/enforcement/overview.md)。

## 對受眾細分強制實施資料使用合規性

在中啟用的區段在其區 [!DNL Real-time Customer Profile] 段定義中包含合併原則ID。 此合併策略包含有關哪些資料集要包含在段中的資訊，這些資料集又包含任何適用的資料使用標籤。 如需針對對象區段強制實施資料使用合規性的特定步驟，請遵循區 [段的資料使用合規性教學課程](../segmentation/tutorials/governance.md)。

## Get started with [!DNL Privacy Service]

[!DNL Privacy Service] 提供REST風格的API和使用者介面，可讓您跨Adobe Experience Cloud應用程式管理資料主體（客戶）的個人資料。 [!DNL Privacy Service] 還提供了集中審計和記錄機制，允許您訪問涉及應用程式的作業的狀態和 [!DNL Experience Cloud] 結果。 如需指示如何建立和監控工 [!DNL Privacy Service] 作的指示，請遵循「隱私服務開發人員指南」或「隱私服務」使 [用指南](../privacy-service/api/getting-started.md) 」中提供的 [步驟](../privacy-service/ui/overview.md)。