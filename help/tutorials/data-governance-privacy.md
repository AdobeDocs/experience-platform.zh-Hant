---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料管理與隱私權教學課程
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# 資料治理與隱私權教學課程

資料使用標籤與實施(DULE)是Adobe Experience Platform資料治理的核心機制。 DULE功能可讓您將資料使用量標籤套用至資料集和欄位，並依據相關資料使用策略將每個標籤分類。 在開始使用標籤之前，請參閱 [資料治理概觀](../data-governance/home.md) ，以取得平台內DULE架構的更強穩簡介。

Adobe Experience Platform Privacy Service提供REST風格的API和使用者介面，讓您協調各種解決方案的隱私權和合規性要求。 若要進一步瞭解，請先閱讀隱私權 [服務概觀](../privacy-service/home.md)。

## 新增資料使用標籤

資料使用標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 標籤可隨時套用，提供您選擇控制資料的彈性。 最佳實務鼓勵在資料吸收到Experience Platform後，或當資料可供Platform使用時，立即加上標籤。 在資料集層級套用的資料使用標籤會傳播至資料集內的所有欄位。 標籤也可以直接套用至資料集中的個別欄位（欄標題），而不需傳播。 若要瞭解如何將資料使用標籤套用至您的資料，請造訪資料使 [用標籤總覽](../data-governance/labels/overview.md)。

## 建立資料使用原則

DULE Policy Service API可讓您建立和管理DULE原則，以決定可針對包含特定DULE標籤的資料採取哪些行銷動作。 若要開始，請閱讀資料使 [用政策概觀](../data-governance/policies/overview.md)。

## 強制實施資料使用原則

在您為資料建立「資料使用標籤與實施」(DULE)標籤，並針對這些標籤建立行銷動作的DULE原則後，您可以使用DULE原則服務API來評估在資料集或任意DULE標籤群組上執行的行銷動作是否構成原則違規。 然後，您可以設定自己的內部通訊協定，以根據API回應來處理原則違規。 若要開始，請造訪原 [則實施概觀](../data-governance/enforcement/overview.md)。

## 對受眾細分強制實施資料使用合規性

在即時客戶描述檔中啟用的區段在其區段定義中包含合併原則ID。 此合併策略包含有關哪些資料集要包含在段中的資訊，這些資料集又包含任何適用的資料使用標籤。 如需針對對象區段強制實施資料使用合規性的特定步驟，請遵循區 [段的資料使用合規性教學課程](../segmentation/tutorials/governance.md)。

## 開始使用隱私權服務

隱私權服務提供REST風格的API和使用者介面，可讓您跨Adobe Experience Cloud應用程式管理資料主體（客戶）的個人資料。 隱私權服務也提供集中稽核和記錄機制，讓您存取與Experience Cloud應用程式有關的工作狀態和結果。 如需指示如何建立和監控Privacy Service工作的指示，請依照 [Privacy Service開發人員指南](../privacy-service/api/getting-started.md) 或 [Privacy Service使用指南中的步驟進行](../privacy-service/ui/overview.md)。