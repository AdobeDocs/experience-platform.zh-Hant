---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料使用標籤概觀
topic: labels
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---


# 資料使用標籤概觀

資料使用標籤與實施(DULE)是Adobe Experience Platform的核心機制 [!DNL Data Governance]。 DULE功能可讓您將資料使用量標籤套用至資料集和欄位，並依據相關資料使用策略將每個標籤分類。

本文檔概述中的資料使用標籤（也稱為DULE標籤） [!DNL Experience Platform]。 在閱讀本指南之前，請參閱 [資料治理概觀](../home.md) ，以取得DULE架構的更強穩簡介。

## 瞭解資料使用標籤

資料使用標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 標籤可隨時套用，提供您選擇控制資料的彈性。 最佳做法鼓勵在資料被吸收或資料可供使 [!DNL Experience Platform]用時，立即加上標籤 [!DNL Platform]。

在資料集層級套用的資料使用標籤會傳播至資料集內的所有欄位。 標籤也可以直接套用至資料集中的個別欄位（欄標題），而不需傳播。

[!DNL Platform] 提供數種「核心」資料使用標籤，其中涵蓋適用於資料治理的各種常見限制。 如需這些標籤及其所代表之使用原則的詳細資訊，請參閱核心資料使 [用標籤的指南](reference.md)。

除了Adobe提供的標籤外，您也可以定義您自己的自訂標籤。 如需如何在UI中執行此動作的步驟，請參閱資 [料使用標籤使用指南](./user-guide.md)。 如需如何使用API呼叫執行此動作的步驟，請參閱資 [料使用標籤API指南](./api.md)。

## 對象區段的標籤繼承

由 [Adobe Experience Platform Segmentation Service建立的所有受眾細分](../../segmentation/home.md) ，都會繼承其對應資料集的使用標籤。 這可讓建立在（例如）之上的應 [!DNL Experience Platform] 用程式，在啟用區段至目的地時 [!DNL Real-time Customer Data Platform]，提供自動資料使用原則的強制執行。

除了繼承資料集層級標籤外，依預設，區段會繼承其關聯資料集的所有欄位層級標籤。 根據您的應用程 [!DNL Platform]式使用區段的方式，您可能會指定使用哪些欄位，從而防止區段繼承排除欄位的標籤。

如需有關自動強制執行在即時CDP中如何運作的詳細資訊，請參閱 [Adobe即時CDP資料治理總覽](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)。

### 繼承Adobe Audience Manager資料匯出控制項

[!DNL Experience Platform] 能夠與Adobe Audience Manager共用區段。 套用至Audience Manager區段的任何「資料匯出控制」都會轉換為由所識別的相同標籤和行銷動 [!DNL Experience Platform] 作 [!DNL Data Governance]。

如需特定「資料匯出控制」如何對應至中的資料使用標籤的參考 [!DNL Platform]資訊，請參閱 [Audience Manager檔案](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)。


## 後續步驟

現在，您已引進資料使用標籤，您可以繼續閱讀使用 [指南](user-guide.md) ，以瞭解如何在 [!DNL Experience Platform] UI中管理標籤。 如需如何使用API管理標籤的步驟，請參 [閱使用標籤API指南](./api.md)。