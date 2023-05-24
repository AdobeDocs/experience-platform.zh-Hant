---
keywords: Experience Platform；首頁；熱門主題；資料控管；資料使用標籤api；原則服務api；資料使用標籤總覽
solution: Experience Platform
title: 資料使用標籤概觀
description: 瞭解如何使用資料使用標籤來協助強制執行Adobe Experience Platform中的資料控管合規性。
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 5d34781e06c0fa8bfd2e52f73e336d92d16192f6
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 14%

---

# 資料使用標籤總覽 {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="控制敏感和受保護資料的存取權"
>abstract="<h2>說明</h2><p>控制特定資料屬性和/或區段的存取權，使您能夠為操作 Experience Platform 使用案例的各種角色和團隊設計靈活的工作流程。</p>"

Adobe Experience Platform可讓您將資料使用標籤套用至資料集和欄位，並根據相關專案對每個欄位進行分類 [資料治理原則](../policies/overview.md) 和 [存取控制原則](../../access-control/abac/ui/policies.md).

本檔案提供資料使用標籤總覽，位於 [!DNL Experience Platform].

## 瞭解資料使用標籤

資料使用標籤可讓您根據套用至該資料的治理原則來分類資料集和欄位。 標籤可隨時套用，讓您靈活選擇控管資料的方式。 最佳實務建議在資料內嵌至後立即加上標籤 [!DNL Experience Platform]，或在資料可用於以下專案時立即啟用： [!DNL Platform].

套用至資料集層級的資料使用標籤會傳播至資料集內的所有欄位。 標籤也可以直接套用至資料集中的個別欄位（欄標題），而不需傳播。

[!DNL Platform] 提供數種現成的「核心」資料使用標籤，涵蓋適用於資料控管的各種常見限制。 如需這些標籤及其代表的治理原則的詳細資訊，請參閱以下指南： [核心資料使用標籤](reference.md).

除了Adobe提供的標籤之外，您也可以為組織定義自己的自訂標籤。 請參閱以下小節： [管理標籤](#manage-labels) 以取得詳細資訊。

## 對象區段的標籤繼承

建立的所有對象區段 [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) 繼承對應資料集的使用情況標籤。 這可讓Experience Platform在將區段啟用至目的地時，提供自動原則執行。

除了繼承資料集層級標籤之外，根據預設，區段還會從關聯的資料集中繼承所有欄位層級標籤。 因此，您可以更輕鬆地識別應從區段排除的屬性，並防止其從排除的欄位繼承標籤。

如需如何在Platform中自動強制執行的詳細資訊，請參閱以下主題的概觀： [自動原則執行](../enforcement/auto-enforcement.md).

### Adobe Audience Manager資料匯出控制項的繼承

[!DNL Experience Platform] 能夠與Adobe Audience Manager共用區段。 套用至Audience Manager區段的任何資料匯出控制都會轉譯為相等的標籤和行銷動作，可由 [!DNL Experience Platform] 資料控管。

如需瞭解特定資料匯出控制項如何對應至中的資料使用標籤，請參閱 [!DNL Platform]，請參閱 [Audience Manager檔案](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## 管理中的資料使用標籤 [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="說明"
>abstract="<ul><li>標記 XDM 欄位和區段以對要限制存取的欄位和/或區段進行分類。</li><li>標記角色，為角色新增標籤可以讓您定義該角色的成員應該有限制的標籤。</li><li>建立原則，原則會建立被標記物件 (例如 XDM 欄位和區段) 的標籤和角色的標籤之間的關係。如果標籤相符，則可以定義允許存取或限制存取。</li></ul>"

您可以使用以下專案管理資料使用標籤 [!DNL Experience Platform] API或使用者介面。 如需各個專案的詳細資訊，請參閱以下各小節。

### 使用UI

此 **[!UICONTROL 原則]** 工作區在 [!DNL Experience Platform] UI可讓您檢視和管理組織的核心和自訂標籤。 您可以使用 **[!UICONTROL 結構描述]** 工作區至 [將標籤套用至您的Experience Data Model (XDM)結構描述](../../xdm/tutorials/labels.md)，或瞭解如何 [在**中建立和管理自訂標籤[!UICONTROL 原則] UI](./user-guide.md) 請改為閱讀資料使用標籤使用手冊。

>[!IMPORTANT]
>
>標籤無法再套用至資料集層級的欄位。 此工作流程已過時，改為在結構描述層級套用標籤。 在2024年5月31日之前，先前在資料集物件層級套用的任何標籤仍可透過Platform UI取得支援。 為確保您的標籤在所有結構描述中保持一致，您必須在來年將之前附加至資料集層級欄位的任何標籤移轉至結構描述層級。 請參閱以下小節： [移轉先前套用的標籤](../e2e.md#migrate-labels) 以取得相關指示。

### 使用API

此 `/labels` 中的端點 [原則服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 可讓您以程式設計方式管理資料使用標籤，包括建立自訂標籤。 請參閱 [標籤端點指南](../api/labels.md) 以取得詳細資訊。

此 [資料集服務API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 用於管理資料集和欄位的標籤。 請參閱指南： [管理資料集標籤](./dataset-api.md) 以取得詳細資訊。

## 後續步驟

本檔案介紹了資料使用標籤及其在資料控管框架中的角色。 請參閱本指南中的檔案連結，以進一步瞭解如何在中管理標籤 [!DNL Experience Platform].
