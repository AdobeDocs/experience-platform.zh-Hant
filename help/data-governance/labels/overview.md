---
keywords: Experience Platform;home；熱門主題；資料治理；資料使用標籤api；策略服務api；資料使用標籤概述
solution: Experience Platform
title: 資料使用標籤概觀
topic: labels
description: Adobe Experience Platform資料治理可讓您將資料使用標籤套用至資料集和欄位，並依據相關資料使用政策對每個資料使用標籤進行分類。 本檔案概述Experience Platform中的資料使用標籤。
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---


# 資料使用標籤概觀

Adobe Experience Platform [!DNL Data Governance]可讓您將資料使用標籤套用至資料集和欄位，並依據相關資料使用政策對每個欄位進行分類。

本檔案概述[!DNL Experience Platform]中的資料使用標籤。 在閱讀本指南之前，請參閱[資料治理概觀](../home.md)以取得更強穩的資料治理架構簡介。

## 瞭解資料使用標籤

資料使用標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 標籤可隨時套用，提供您選擇控制資料的彈性。 最佳做法鼓勵在資料被收錄到[!DNL Experience Platform]或資料可供[!DNL Platform]使用時，立即加上標籤。

在資料集層級套用的資料使用標籤會傳播至資料集內的所有欄位。 標籤也可以直接套用至資料集中的個別欄位（欄標題），而不需傳播。

[!DNL Platform] 提供數種「核心」資料使用標籤，其中涵蓋適用於資料治理的各種常見限制。有關這些標籤及其所代表的使用策略的詳細資訊，請參閱[核心資料使用標籤](reference.md)上的指南。

除了Adobe提供的標籤外，您也可以為組織定義您自己的自訂標籤。 如需詳細資訊，請參閱[管理標籤的章節。](#manage-labels)

## 對象區段的標籤繼承

由[Adobe Experience Platform Segmentation Service](../../segmentation/home.md)建立的所有受眾細分會繼承其對應資料集的使用標籤。 這可讓Experience Platform在將區段啟用至目標時，提供自動資料使用原則強制執行功能。

除了繼承資料集層級標籤外，依預設，區段會繼承其關聯資料集的所有欄位層級標籤。 因此，您可以更輕鬆地識別哪些屬性應排除在區段之外，並防止它們繼承排除欄位中的標籤。

有關自動強制執行在平台中如何運作的詳細資訊，請參閱[自動強制執行原則的概觀。](../enforcement/auto-enforcement.md)

### 繼承Adobe Audience Manager資料匯出控制項

[!DNL Experience Platform] 能夠與Adobe Audience Manager共用區段。已套用至Audience Manager區段的任何「資料匯出控制」都會轉換為[!DNL Experience Platform] [!DNL Data Governance]所識別的等同標籤和行銷動作。

有關特定「資料匯出控制」如何對應至[!DNL Platform]中的資料使用標籤的參考，請參閱[Audience Manager檔案](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)。

## 在[!DNL Experience Platform] {#manage-labels}中管理資料使用標籤

您可以使用[!DNL Experience Platform] API或使用者介面來管理資料使用標籤。 請參閱下列子章節，以取得各章節的詳細資訊。

### 使用UI

[!DNL Experience Platform] UI中的&#x200B;**[!UICONTROL Policys]**&#x200B;工作區可讓您檢視和管理組織的核心標籤和自訂標籤。 **[!DNL Datasets]**&#x200B;工作區可讓您將標籤套用至資料集和欄位。 有關詳細資訊，請參閱[標籤使用手冊](user-guide.md)。

### 使用API

[Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)中的`/labels`端點可讓您以程式設計方式管理資料使用標籤，包括建立自訂標籤。 有關詳細資訊，請參閱[標籤端點指南](../api/labels.md)。

[資料集服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml)用於管理資料集和欄位的標籤。 如需詳細資訊，請參閱[管理資料集標籤](./dataset-api.md)上的指南。

## 後續步驟

本檔案介紹了資料使用標籤及其在資料治理框架中的作用。 請參閱本指南中連結的檔案，進一步瞭解如何管理[!DNL Experience Platform]中的標籤。