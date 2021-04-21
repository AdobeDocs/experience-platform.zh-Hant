---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 資料管理與隱私權教學課程
topic-legacy: tutorial
type: Tutorial
description: 本檔案概述與Adobe Experience Platform資料治理和Adobe Experience Platform Privacy Service有關的不同可用教學課程。
exl-id: c3cef447-b343-445b-a3ed-54f873f6dfb9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# [!DNL Data Governance] 和 [!DNL Privacy] Tutorials

Adobe Experience Platform資料治理使您能夠將資料使用標籤應用到資料集和欄位，根據相關資料使用策略對每個資料集和欄位進行分類，並在對這些資料集和／或欄位執行某些操作時評估策略違規情況。 開始使用本檔案所列的教學課程之前，請參閱[[!DNL Data Governance] overview](../data-governance/home.md)以取得更強穩的架構簡介。

Adobe Experience Platform[!DNL Privacy Service]提供REST風格的API和使用者介面，讓您協調各種解決方案的隱私權和合規性要求。 若要瞭解更多資訊，請先閱讀[Privacy Service概觀](../privacy-service/home.md)。

## 新增資料使用標籤

資料使用標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 標籤可隨時套用，提供您選擇控制資料的彈性。 最佳做法鼓勵在資料被收錄到[!DNL Experience Platform]或資料可供[!DNL Platform]使用時，立即加上標籤。 在資料集層級套用的資料使用標籤會傳播至資料集內的所有欄位。 標籤也可以直接套用至資料集中的個別欄位（欄標題），而不需傳播。 若要瞭解如何將資料使用標籤套用至您的資料，請造訪[資料使用標籤概述](../data-governance/labels/overview.md)。

## 建立資料使用原則

[!DNL Policy Service] API可讓您建立和管理資料使用原則，以決定對包含特定使用標籤的資料可採取哪些行銷動作。 若要開始，請閱讀[資料使用政策概述](../data-governance/policies/overview.md)。

## 強制實施資料使用原則

在您新增資料的使用標籤，並針對這些標籤建立行銷動作的原則後，您可以使用[!DNL Policy Service API]來評估在資料集或任意使用標籤群組上執行的行銷動作是否構成原則違規。 然後，您可以設定自己的內部通訊協定，以根據API回應來處理原則違規。 若要開始，請造訪[原則實施概述](../data-governance/enforcement/overview.md)。

## 對受眾細分強制實施資料使用合規性

在[!DNL Real-time Customer Profile]中啟用的區段在其區段定義中包含合併原則ID。 此合併策略包含有關哪些資料集要包含在段中的資訊，這些資料集又包含任何適用的資料使用標籤。 如需針對對象區段強制執行資料使用合規性的特定步驟，請依照[區段資料使用合規性實施教學課程](../segmentation/tutorials/governance.md)進行。

## 開始使用 [!DNL Privacy Service]

[!DNL Privacy Service] 提供REST風格的API和使用者介面，讓您跨Adobe Experience Cloud應用程式管理資料主體（客戶）的個人資料。[!DNL Privacy Service] 還提供了集中審計和記錄機制，允許您訪問涉及應用程式的作業的狀態和 [!DNL Experience Cloud] 結果。有關如何建立和監視[!DNL Privacy Service]作業的說明，請遵循[Privacy Service開發人員指南](../privacy-service/api/getting-started.md)或[Privacy Service使用手冊](../privacy-service/ui/overview.md)中提供的步驟。
