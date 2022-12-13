---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 策略服務API指南
topic-legacy: developer guide
description: 策略服務API允許開發人員管理Experience Platform中的資料使用標籤和策略。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 3%

---

# [!DNL Policy Service] API指南

Adobe Experience Platform資料控管可讓您管理客戶資料，並確保符合適用於資料使用的法規、限制和政策。 在 [!DNL Experience Platform] 在各個層級，包括編目、資料處理、資料使用標籤、資料使用策略，以及控制資料在行銷動作中的使用。

此 [!DNL Policy Service] API提供數個端點，可讓您以程式設計方式管理資料使用量標籤和原則，以及評估違反原則的行銷動作。 這些端點概述如下。 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](./getting-started.md) 如需必要標題、讀取範例API呼叫等的重要資訊。

若要檢視所有可用端點和CRUD作業，請造訪 [[!DNL Policy Service] API Swagger](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## 標記

資料使用量標籤可讓您根據套用至該資料的使用量原則，對資料集和欄位進行分類。 標籤可隨時套用，提供您選擇控管資料的彈性。 最佳實務鼓勵將資料擷取至時立即加上標籤 [!DNL Experience Platform]，或資料可供使用時 [!DNL Platform]. 您可以使用 `/labels` 端點。 若要了解如何使用此端點，請造訪 [標籤端點指南](./labels.md).

## 行銷動作

在資料控管架構中，行銷動作（又稱為行銷使用案例）是 [!DNL Experience Platform] 資料使用者可採用，而您的組織想要限制資料使用量。 如需使用行銷動作的詳細資訊，請參閱 [marketing actions端點指南](./marketing-actions.md).

## 原則

資料控管原則是一種規則，可說明您可對內的資料執行或限制的行銷動作類型 [!DNL Experience Platform].

>[!NOTE]
>
>資料控管原則與存取控制原則不容混淆，存取控制原則會決定貴組織中特定Platform使用者可存取的特定資料屬性。 請參閱 [基於屬性的訪問控制](../../access-control/abac/overview.md) 以取得更多資訊。

資料控管原則的定義如下：

1. 特定行銷動作
1. 限制針對執行動作的資料使用量標籤

若要了解如何在API中管理原則，請參閱 [原則端點指南](./policies.md)

## 評估

將資料使用量標籤套用至 [!DNL Platform] 針對這些標籤的行銷動作定義了資料集和資料使用原則，資料控管功能可讓您強制執行這些原則，並防止構成違反原則的資料操作。

此 [!DNL Policy Service] API提供的端點可讓您針對資料集或資料使用標籤的任意組合測試行銷動作，以檢查是否發生任何違反原則的情況。 然後，您可以根據API回應，在體驗應用程式中設定通訊協定，以適當強制執行資料使用原則符合性。 請參閱 [評估端點指南](./evaluation.md) 以取得更多資訊。

## 後續步驟

若要開始使用進行呼叫 [!DNL Policy Service] API，請閱讀 [快速入門手冊](./getting-started.md) 然後，選取其中一個端點指南，以了解如何使用特定端點。 若要使用標籤和原則，請使用 [!DNL Experience Platform] UI，請參閱 [標籤使用手冊](../labels/user-guide.md) 和 [原則使用手冊](../policies/user-guide.md)，分別為。
