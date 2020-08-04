---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料使用標籤概觀
topic: labels
translation-type: tm+mt
source-git-commit: 5e65c843c3c612b657ebe915c53f14f0b8d7f541
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---


# 資料使用標籤概觀

Adobe Experience Platform可 [!DNL Data Governance] 讓您將資料使用標籤套用至資料集和欄位，並依據相關資料使用政策對每個欄位進行分類。

本檔案概述中的資料使用標籤 [!DNL Experience Platform]。 在閱讀本指南之前，請參閱資 [料治理概觀](../home.md) ，以取得資料治理架構更健全的簡介。

## 瞭解資料使用標籤

資料使用標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 標籤可隨時套用，提供您選擇控制資料的彈性。 最佳做法鼓勵在資料被吸收或資料可供使 [!DNL Experience Platform]用時，立即加上標籤 [!DNL Platform]。

在資料集層級套用的資料使用標籤會傳播至資料集內的所有欄位。 標籤也可以直接套用至資料集中的個別欄位（欄標題），而不需傳播。

[!DNL Platform] 提供數種「核心」資料使用標籤，其中涵蓋適用於資料治理的各種常見限制。 如需這些標籤及其所代表之使用原則的詳細資訊，請參閱核心資料使 [用標籤的指南](reference.md)。

除了Adobe提供的標籤外，您也可以為組織定義您自己的自訂標籤。 如需詳細資訊，請 [參閱管理](#manage-labels) 標籤一節。

## 對象區段的標籤繼承

由 [Adobe Experience Platform Segmentation Service建立的所有受眾細分](../../segmentation/home.md) ，都會繼承其對應資料集的使用標籤。 這可讓建立在（例如）之上的應 [!DNL Experience Platform] 用程式，在啟用區段至目的地時 [!DNL Real-time Customer Data Platform]，提供自動資料使用原則的強制執行。

除了繼承資料集層級標籤外，依預設，區段會繼承其關聯資料集的所有欄位層級標籤。 根據您的應用程 [!DNL Platform]式使用區段的方式，您可能會指定使用哪些欄位，從而防止區段繼承排除欄位的標籤。

有關自動強制執行在即時CDP中如何運作的詳細資訊，請參見有關即時CDP中 [資料治理的概述](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)。

### 繼承Adobe Audience Manager資料匯出控制項

[!DNL Experience Platform] 能夠與Adobe Audience Manager共用區段。 套用至Audience Manager區段的任何「資料匯出控制」都會轉換為由所識別的相同標籤和行銷動 [!DNL Experience Platform] 作 [!DNL Data Governance]。

如需特定「資料匯出控制」如何對應至中的資料使用標籤的參考 [!DNL Platform]資訊，請參閱 [Audience Manager檔案](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)。

## 管理資料使用標籤 [!DNL Experience Platform] {#manage-labels}

您可以使用API或使用者介面 [!DNL Experience Platform] 來管理資料使用標籤。 請參閱下列子章節，以取得各章節的詳細資訊。

### 使用UI

UI中 **[!UICONTROL 的]** 「原則」工作區 [!DNL Experience Platform] 可讓您檢視並管理組織的核心標籤和自訂標籤。 工作 **[!DNL Datasets]** 區可讓您將標籤套用至資料集和欄位。 如需詳細資訊，請參閱「標 [簽使用指南」](user-guide.md)。

### 使用API

Policy `/labels` Service API中的 [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) 端點可讓您以程式設計方式管理資料使用標籤，包括建立自訂標籤。 如需詳細資 [訊，請參閱標籤端](../api/labels.md) 點指南。

資料 [集服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) 可用來管理資料集和欄位的標籤。 如需詳細資訊，請參 [閱管理資料集標籤](./dataset-api.md) 的指南。

## 後續步驟

本檔案介紹了資料使用標籤及其在資料治理框架中的作用。 請參閱本指南中連結的檔案，進一步瞭解如何管理中的標籤 [!DNL Experience Platform]。