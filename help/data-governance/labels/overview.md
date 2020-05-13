---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料使用標籤概觀
topic: labels
translation-type: tm+mt
source-git-commit: 4b6b9ca5ae7861f8e8b974550be14fbce6efdcf1
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# 資料使用標籤概觀

資料使用標籤與實施(DULE)是Adobe Experience Platform資料治理的核心機制。 DULE功能可讓您將資料使用量標籤套用至資料集和欄位，並依據相關資料使用策略將每個標籤分類。

本檔案提供Experience Platform中資料使用標籤（也稱為DULE標籤）的概述。 在閱讀本指南之前，請參閱 [資料治理概觀](../home.md) ，以取得DULE架構的更強穩簡介。

## 瞭解資料使用標籤

資料使用標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 標籤可隨時套用，提供您選擇控制資料的彈性。 最佳實務鼓勵在資料吸收到Experience Platform後，或當資料可供Platform使用時，立即加上標籤。

在資料集層級套用的資料使用標籤會傳播至資料集內的所有欄位。 標籤也可以直接套用至資料集中的個別欄位（欄標題），而不需傳播。

如需Experience Platform中可用資料使用標籤及其所代表之使用原則的詳細資訊，請參閱支援資料使 [用標籤的指南](reference.md)。

## 對象區段的標籤繼承

由 [Adobe Experience Platform Segmentation Service建立的所有受眾細分](../../segmentation/home.md) ，都會繼承其對應資料集的使用標籤。 這可讓以Experience Platform（例如即時客戶資料平台）為基礎的應用程式，在將區段啟動至目標時，提供自動資料使用原則的實施。

除了繼承資料集層級標籤外，依預設，區段會繼承其關聯資料集的所有欄位層級標籤。 根據您的平台應用程式使用區段的方式，您可能會指定使用哪些欄位，從而防止區段繼承排除欄位的標籤。

有關自動強制執行在即時CDP中如何運作的詳細資訊，請參 [見即時CDP資料治理概述](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)。

## 後續步驟

現在您已經引進資料使用標籤，您可以繼續閱讀使 [用指南](user-guide.md) ，以瞭解如何在Experience Platform UI中管理標籤。 如需如何使用API管理標籤的步驟，請參閱目錄服務開發人員指 [南中的適當章節](../../catalog/api/labels.md)。