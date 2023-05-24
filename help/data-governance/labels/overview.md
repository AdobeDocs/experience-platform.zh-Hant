---
keywords: Experience Platform；首頁；熱門主題；資料管理；資料使用標籤api；策略服務api；資料使用標籤概述
solution: Experience Platform
title: 資料使用情況標籤概述
description: 瞭解如何使用資料使用標籤幫助在Adobe Experience Platform強制實施資料治理合規性。
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 15%

---

# 資料使用標籤總覽 {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="控制敏感和受保護資料的存取權"
>abstract="<h2>說明</h2><p>控制特定資料屬性和/或區段的存取權，使您能夠為操作 Experience Platform 使用案例的各種角色和團隊設計靈活的工作流程。</p>"

Adobe Experience Platform允許您將資料使用標籤應用到資料集和欄位，根據相關內容對每個欄位進行分類 [資料治理策略](../policies/overview.md) 和 [訪問控制策略](../../access-control/abac/ui/policies.md)。

本文檔概述了中的資料使用標籤 [!DNL Experience Platform]。

## 瞭解資料使用標籤

資料使用標籤允許您根據應用於該資料的治理策略對資料集和欄位進行分類。 標籤可以隨時應用，在選擇管理資料的方式上提供了靈活性。 最佳做法鼓勵在將資料攝取到 [!DNL Experience Platform]，或當資料可用時 [!DNL Platform]。

在資料集級別應用的資料使用標籤將傳播到資料集中的所有欄位。 標籤也可以直接應用到資料集中的各個欄位（列標題），而不進行傳播。

[!DNL Platform] 提供了幾個「核心」資料使用標籤，這些標籤包含適用於資料治理的各種常見限制。 有關這些標籤及其代表的治理策略的詳細資訊，請參見上的指南 [核心資料使用標籤](reference.md)。

除了Adobe提供的標籤外，您還可以為組織定義自己的自定義標籤。 請參閱 [管理標籤](#manage-labels) 的子菜單。

## 受眾段的標籤繼承

建立的所有受眾段 [Adobe Experience Platform分段服務](../../segmentation/home.md) 繼承其相應資料集的用法標籤。 這允許Experience Platform在將段激活到目標時提供自動策略強制。

除了繼承資料集級別標籤外，預設情況下，段還繼承與其關聯的資料集中的所有欄位級別標籤。 因此，您可以更輕鬆地確定哪些屬性應從段中排除，並防止它們繼承排除欄位中的標籤。

有關自動強制在平台中如何工作的詳細資訊，請參閱 [自動策略執行](../enforcement/auto-enforcement.md)。

### 從Adobe Audience Manager資料導出控制項繼承

[!DNL Experience Platform] 有能力與Adobe Audience Manager分享。 已應用於Audience Manager段的任何資料導出控制都會轉換為由 [!DNL Experience Platform] 資料治理。

有關特定資料導出控制項如何映射到中的資料使用標籤的參考 [!DNL Platform]，請參閱 [Audience Manager文檔](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)。

## 管理中的資料使用標籤 [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="說明"
>abstract="<ul><li>標記 XDM 欄位和區段以對要限制存取的欄位和/或區段進行分類。</li><li>標記角色，為角色新增標籤可以讓您定義該角色的成員應該有限制的標籤。</li><li>建立原則，原則會建立被標記物件 (例如 XDM 欄位和區段) 的標籤和角色的標籤之間的關係。如果標籤相符，則可以定義允許存取或限制存取。</li></ul>"

您可以使用 [!DNL Experience Platform] API或用戶介面。 有關每個子部分的詳細資訊，請參閱以下各部分。

### 使用UI

的 **[!UICONTROL 策略]** 工作區 [!DNL Experience Platform] UI允許您查看和管理組織的核心標籤和自定義標籤。 您可以使用 **[!UICONTROL 架構]** 工作區 [將標籤應用到您的體驗資料模型(XDM)架構](../../xdm/tutorials/labels.md)，或 **[!DNL Datasets]** 工作區 [將標籤應用於資料集](./user-guide.md) 的雙曲餘切值。

>[!NOTE]
>
>僅在資料治理使用案例中支援在資料集級別應用標籤。 如果試圖為資料建立訪問策略，則必須將標籤應用到資料集所基於的架構。 請參閱 [基於屬性的訪問控制](../../access-control/abac/overview.md) 的子菜單。

### 使用API

的 `/labels` 端點 [策略服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 允許您以寫程式方式管理資料使用標籤，包括建立自定義標籤。 請參閱 [標籤端點指南](../api/labels.md) 的子菜單。

的 [資料集服務API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 用於管理資料集和欄位的標籤。 請參閱上的指南 [管理資料集標籤](./dataset-api.md) 的子菜單。

>[!NOTE]
>
>僅在資料治理使用案例中支援在資料集級別應用標籤。 如果嘗試為資料建立訪問策略，則必須 [將標籤應用於架構](../../xdm/tutorials/labels.md) 資料集所基於。 請參閱 [基於屬性的訪問控制](../../access-control/abac/overview.md) 的子菜單。

## 後續步驟

本文檔介紹了資料使用標籤及其在資料治理框架中的角色。 請參閱本指南中連結的文檔，瞭解有關如何管理標籤的詳細資訊 [!DNL Experience Platform]。
