---
keywords: Experience Platform；首頁；熱門主題；資料控管；資料使用標籤api；原則服務api；資料使用標籤概觀
solution: Experience Platform
title: 資料使用量標籤概述
topic-legacy: labels
description: Adobe Experience Platform資料控管可讓您將資料使用量標籤套用至資料集和欄位，並根據相關資料使用量原則將每個欄位分類。 本檔案概述Experience Platform中的資料使用量標籤。
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 937225ff08e2e02c5840f86d6ed50644e05bdfe5
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# 資料使用量標籤概觀

Adobe Experience Platform [!DNL Data Governance]可讓您將資料使用量標籤套用至資料集和欄位，並根據相關資料使用策略來分類每個資料。

本文檔概述[!DNL Experience Platform]中的資料使用標籤。 閱讀本指南之前，請參閱[資料控管概觀](../home.md) ，以取得更健全的資料控管架構簡介。

## 了解資料使用量標籤

資料使用量標籤可讓您根據套用至該資料的使用量原則，對資料集和欄位進行分類。 標籤可隨時套用，提供您選擇控管資料的彈性。 最佳實務鼓勵在將資料擷取至[!DNL Experience Platform]時，或當資料可供[!DNL Platform]使用時，立即將資料加以標籤。

在資料集層級套用的資料使用量標籤會傳播至資料集內的所有欄位。 標籤也可直接套用至資料集中的個別欄位（欄標題），不需傳播。

[!DNL Platform] 提供數個「核心」資料使用標籤且立即可用，涵蓋適用於資料控管的各種常見限制。如需這些標籤及其代表的使用原則的詳細資訊，請參閱[核心資料使用標籤](reference.md)的指南。

除了Adobe提供的標籤外，您也可以為組織定義自己的自訂標籤。 如需詳細資訊，請參閱[管理標籤](#manage-labels)的區段。

## 對象區段的標籤繼承

由[Adobe Experience Platform區段服務](../../segmentation/home.md)建立的所有對象區段會繼承其對應資料集的使用標籤。 這可讓Experience Platform在將區段啟用至目的地時，提供自動資料使用策略強制執行功能。

除了繼承資料集層級標籤外，區段預設會繼承其關聯資料集中的所有欄位層級標籤。 因此，您可以更輕鬆識別應從區段中排除的屬性，並防止它們繼承排除欄位中的標籤。

如需自動執行如何在Platform中運作的詳細資訊，請參閱[自動原則執行](../enforcement/auto-enforcement.md)的概觀。

### 繼承Adobe Audience Manager資料匯出控制項

[!DNL Experience Platform] 可與Adobe Audience Manager共用區段。已套用至Audience Manager區段的任何資料匯出控制項都會轉換為由[!DNL Experience Platform] [!DNL Data Governance]所識別的等同標籤和行銷動作。

有關特定資料導出控制項如何映射到[!DNL Platform]中的資料使用標籤的參考，請參閱[Audience Manager文檔](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)。

## 管理[!DNL Experience Platform]中的資料使用量標籤 {#manage-labels}

您可以使用[!DNL Experience Platform] API或使用者介面來管理資料使用量標籤。 如需各個項目的詳細資訊，請參閱以下子區段。

### 使用UI

[!DNL Experience Platform] UI中的&#x200B;**[!UICONTROL Policys]**&#x200B;工作區可讓您檢視及管理組織的核心和自訂標籤。 **[!DNL Datasets]**&#x200B;工作區可讓您將標籤套用至資料集和欄位。 有關詳細資訊，請參閱[標籤使用手冊](user-guide.md)。

### 使用API

[策略服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/)中的`/labels`端點允許您以寫程式方式管理資料使用標籤，包括建立自定義標籤。 如需詳細資訊，請參閱[標籤端點指南](../api/labels.md) 。

[資料集服務API](https://www.adobe.io/experience-platform-apis/references/dataset-service/)用於管理資料集和欄位的標籤。 如需詳細資訊，請參閱[管理資料集標籤的指南](./dataset-api.md) 。

## 後續步驟

本檔案簡介資料使用標籤及其在資料控管架構中的角色。 請參閱本指南中連結的檔案，深入了解如何在[!DNL Experience Platform]中管理標籤。
