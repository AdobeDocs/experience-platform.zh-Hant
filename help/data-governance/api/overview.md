---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 策略服務API指南
topic-legacy: developer guide
description: 策略服務API允許開發人員管理Experience Platform中的資料使用標籤和策略。 請依照本指南，了解如何使用API執行重要作業。
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# [!DNL Policy Service] API指南

Adobe Experience Platform [!DNL Data Governance]可讓您管理客戶資料，並確保符合適用於資料使用的法規、限制和政策。 它在[!DNL Experience Platform]中在各個級別中扮演著關鍵角色，包括編目、資料處理、資料使用標籤、資料使用策略以及控制資料在市場營銷操作中的使用。

[!DNL Policy Service] API提供數個端點，可讓您以程式設計方式管理資料使用標籤和原則，以及評估違反原則的行銷動作。 這些端點概述如下。 如需詳細資訊，請造訪個別端點指南，並參閱[快速入門手冊](./getting-started.md)，以取得必要標題、讀取範例API呼叫等的重要資訊。

若要檢視所有可用端點和CRUD操作，請造訪[[!DNL Policy Service] API swagger](https://www.adobe.io/experience-platform-apis/references/policy-service/)。

## 標記

資料使用量標籤可讓您根據套用至該資料的使用量原則，對資料集和欄位進行分類。 標籤可隨時套用，提供您選擇控管資料的彈性。 最佳實務鼓勵在將資料擷取至[!DNL Experience Platform]時，或當資料可供[!DNL Platform]使用時，立即將資料加以標籤。 您可以使用`/labels`端點建立、檢視、編輯和刪除標籤。 若要了解如何使用此端點，請造訪[標籤端點指南](./labels.md)。

## 行銷動作

在[!DNL Data Governance]架構的內容中，行銷動作（又稱為行銷使用案例）是[!DNL Experience Platform]資料使用者可採取的動作，而您的組織想要針對這些動作限制資料使用。 如需使用行銷動作的詳細資訊，請參閱[行銷動作端點指南](./marketing-actions.md)。

## 原則

資料使用原則是描述您可對[!DNL Experience Platform]內的資料執行或限制執行之行銷動作類型的規則。 策略由以下項定義：

1. 特定行銷動作
1. 限制針對執行動作的資料使用量標籤

若要了解如何在API中管理原則，請參閱[原則端點指南](./policies.md)

## 評估

將資料使用量標籤套用至[!DNL Platform]資料集，並針對這些標籤定義了行銷動作的資料使用量原則後，資料控管功能可讓您強制執行這些原則，並防止構成違反原則的資料操作。

[!DNL Policy Service] API提供的端點可讓您針對資料集或資料使用標籤的任意組合測試行銷動作，以檢查是否發生任何違反原則的情況。 然後，您可以根據API回應，在體驗應用程式中設定通訊協定，以適當強制執行資料使用原則符合性。 如需詳細資訊，請參閱[評估端點指南](./evaluation.md) 。

## 後續步驟

若要開始使用[!DNL Policy Service] API進行呼叫，請閱讀[快速入門手冊](./getting-started.md)，然後選取其中一個端點手冊，以了解如何使用特定端點。 要使用[!DNL Experience Platform] UI使用標籤和策略，請分別參閱[標籤使用手冊](../labels/user-guide.md)和[策略使用手冊](../policies/user-guide.md)。
