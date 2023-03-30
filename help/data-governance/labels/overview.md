---
keywords: Experience Platform；首頁；熱門主題；資料控管；資料使用標籤api；原則服務api；資料使用標籤概觀
solution: Experience Platform
title: 資料使用量標籤概述
description: 了解如何使用資料使用量標籤來協助在Adobe Experience Platform中強制執行資料控管法規遵循。
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 1%

---

# 資料使用標籤總覽 {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="控制對敏感和受保護資料的訪問"
>abstract="<h2>說明</h2><p>控制對特定資料屬性和/或區段的存取，讓您針對各種角色和團隊作業Experience Platform使用案例設計彈性的工作流程。</p>"

Adobe Experience Platform可讓您將資料使用量標籤套用至資料集和欄位，並依相關項目對每個欄位進行分類 [資料控管原則](../policies/overview.md) 和 [訪問控制策略](../../access-control/abac/ui/policies.md).

本檔案概述 [!DNL Experience Platform].

## 了解資料使用量標籤

資料使用量標籤可讓您根據套用至該資料的控管原則，對資料集和欄位進行分類。 標籤可隨時套用，提供您選擇控管資料的彈性。 最佳實務鼓勵將資料擷取至時立即加上標籤 [!DNL Experience Platform]，或資料可供使用時 [!DNL Platform].

在資料集層級套用的資料使用量標籤會傳播至資料集內的所有欄位。 標籤也可直接套用至資料集中的個別欄位（欄標題），不需傳播。

[!DNL Platform] 提供數個「核心」資料使用標籤且立即可用，涵蓋適用於資料控管的各種常見限制。 如需這些標籤及其代表的控管原則的詳細資訊，請參閱 [核心資料使用量標籤](reference.md).

除了Adobe提供的標籤外，您也可以為組織定義自己的自訂標籤。 請參閱 [管理標籤](#manage-labels) 以取得更多資訊。

## 對象區段的標籤繼承

所有建立者的受眾區段 [Adobe Experience Platform區段服務](../../segmentation/home.md) 繼承其對應資料集的使用量標籤。 這可讓Experience Platform在將區段啟用至目的地時，自動執行原則。

除了繼承資料集層級標籤外，區段預設會繼承其關聯資料集中的所有欄位層級標籤。 因此，您可以更輕鬆識別應從區段中排除的屬性，並防止它們繼承排除欄位中的標籤。

如需自動執行如何在Platform中運作的詳細資訊，請參閱 [自動策略執行](../enforcement/auto-enforcement.md).

### 繼承Adobe Audience Manager資料匯出控制項

[!DNL Experience Platform] 可與Adobe Audience Manager共用區段。 任何已套用至Audience Manager區段的資料匯出控制項，都會轉譯為相等標籤，以及 [!DNL Experience Platform] 資料控管。

如需特定資料匯出控制項如何對應至 [!DNL Platform]，請參閱 [Audience Manager檔案](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## 在中管理資料使用量標籤 [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="說明"
>abstract="<ul><li>標籤XDM欄位和區段，以分類您要限制存取的欄位和或區段。</li><li>標籤角色，向角色添加標籤可讓您定義此角色的標籤成員應具有的限制。</li><li>建立策略時，策略會在標籤對象（如XDM欄位和區段）上的標籤與角色上的標籤之間建立關係。 如果標籤匹配，則可以定義允許或限制訪問。</li></ul>"

您可以使用 [!DNL Experience Platform] API或使用者介面。 如需各個項目的詳細資訊，請參閱以下子區段。

### 使用UI

此 **[!UICONTROL 原則]** 工作區中 [!DNL Experience Platform] UI可讓您檢視及管理組織的核心標籤及自訂標籤。 您可以使用 **[!UICONTROL 結構]** 工作區 [將標籤套用至您的Experience Data Model(XDM)結構](../../xdm/tutorials/labels.md)，或者您可以使用 **[!DNL Datasets]** 工作區 [將標籤套用至資料集](./user-guide.md) 。

>[!NOTE]
>
>只有資料控管使用案例才支援在資料集層級套用標籤。 如果您嘗試為資料建立存取原則，則必須將標籤套用至資料集所根據的結構。 請參閱 [基於屬性的訪問控制](../../access-control/abac/overview.md) 以取得更多資訊。

### 使用API

此 `/labels` 端點 [策略服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 可讓您以程式設計方式管理資料使用量標籤，包括建立自訂標籤。 請參閱 [標籤端點指南](../api/labels.md) 以取得更多資訊。

此 [資料集服務API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 可用來管理資料集和欄位的標籤。 請參閱 [管理資料集標籤](./dataset-api.md) 以取得更多資訊。

>[!NOTE]
>
>只有資料控管使用案例才支援在資料集層級套用標籤。 如果您嘗試為資料建立訪問策略，則必須 [將標籤應用於方案](../../xdm/tutorials/labels.md) 資料集所依據之資料集。 請參閱 [基於屬性的訪問控制](../../access-control/abac/overview.md) 以取得更多資訊。

## 後續步驟

本檔案簡介資料使用標籤及其在資料控管架構中的角色。 請參閱本指南中連結的檔案，深入了解如何在 [!DNL Experience Platform].
