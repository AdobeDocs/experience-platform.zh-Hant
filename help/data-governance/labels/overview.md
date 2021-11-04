---
keywords: Experience Platform；首頁；熱門主題；資料控管；資料使用標籤api；原則服務api；資料使用標籤概觀
solution: Experience Platform
title: 資料使用量標籤概述
topic-legacy: labels
description: Adobe Experience Platform資料控管可讓您將資料使用量標籤套用至資料集和欄位，並根據相關資料使用量原則將每個欄位分類。 本檔案概述Experience Platform中的資料使用量標籤。
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 資料使用量標籤概觀

Adobe Experience Platform資料控管可讓您將資料使用量標籤套用至資料集和欄位，並根據相關資料使用量原則對每個資料進行分類。

本檔案概述 [!DNL Experience Platform]. 閱讀本指南之前，請參閱 [資料控管概觀](../home.md) 以更健全地介紹資料控管架構。

## 了解資料使用量標籤

資料使用量標籤可讓您根據套用至該資料的使用量原則，對資料集和欄位進行分類。 標籤可隨時套用，提供您選擇控管資料的彈性。 最佳實務鼓勵將資料擷取至時立即加上標籤 [!DNL Experience Platform]，或資料可供使用時 [!DNL Platform].

在資料集層級套用的資料使用量標籤會傳播至資料集內的所有欄位。 標籤也可直接套用至資料集中的個別欄位（欄標題），不需傳播。

[!DNL Platform] 提供數個「核心」資料使用標籤且立即可用，涵蓋適用於資料控管的各種常見限制。 如需這些標籤及其代表的使用原則的詳細資訊，請參閱 [核心資料使用量標籤](reference.md).

除了Adobe提供的標籤外，您也可以為組織定義自己的自訂標籤。 請參閱 [管理標籤](#manage-labels) 以取得更多資訊。

## 對象區段的標籤繼承

所有建立者的受眾區段 [Adobe Experience Platform區段服務](../../segmentation/home.md) 繼承其對應資料集的使用量標籤。 這可讓Experience Platform在將區段啟用至目的地時，提供自動資料使用策略強制執行功能。

除了繼承資料集層級標籤外，區段預設會繼承其關聯資料集中的所有欄位層級標籤。 因此，您可以更輕鬆識別應從區段中排除的屬性，並防止它們繼承排除欄位中的標籤。

如需自動執行如何在Platform中運作的詳細資訊，請參閱 [自動策略執行](../enforcement/auto-enforcement.md).

### 繼承Adobe Audience Manager資料匯出控制項

[!DNL Experience Platform] 可與Adobe Audience Manager共用區段。 任何已套用至Audience Manager區段的資料匯出控制項，都會轉譯為相等標籤，以及 [!DNL Experience Platform] 資料控管。

如需特定資料匯出控制項如何對應至 [!DNL Platform]，請參閱 [Audience Manager檔案](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## 在中管理資料使用量標籤 [!DNL Experience Platform] {#manage-labels}

您可以使用 [!DNL Experience Platform] API或使用者介面。 如需各個項目的詳細資訊，請參閱以下子區段。

### 使用UI

此 **[!UICONTROL 原則]** 工作區中 [!DNL Experience Platform] UI可讓您檢視及管理組織的核心標籤及自訂標籤。 此 **[!DNL Datasets]** 工作區可讓您將標籤套用至資料集和欄位。 如需詳細資訊，請參閱 [標籤使用手冊](user-guide.md).

### 使用API

此 `/labels` 端點 [策略服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 可讓您以程式設計方式管理資料使用量標籤，包括建立自訂標籤。 請參閱 [標籤端點指南](../api/labels.md) 以取得更多資訊。

此 [資料集服務API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 可用來管理資料集和欄位的標籤。 請參閱 [管理資料集標籤](./dataset-api.md) 以取得更多資訊。

## 後續步驟

本檔案簡介資料使用標籤及其在資料控管架構中的角色。 請參閱本指南中連結的檔案，深入了解如何在 [!DNL Experience Platform].
