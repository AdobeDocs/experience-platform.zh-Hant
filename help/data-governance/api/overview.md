---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 原則服務API指南
topic-legacy: developer guide
description: Policy Service API可讓開發人員管理Experience Platform中的資料使用標籤和原則。 請依照本指南，瞭解如何使用API執行關鍵作業。
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# [!DNL Policy Service] API指南

Adobe Experience Platform[!DNL Data Governance]可讓您管理客戶資料，並確保符合適用於資料使用的法規、限制和政策。 它在[!DNL Experience Platform]的不同層次中發揮關鍵作用，包括編目、資料承傳、資料使用標籤、資料使用政策，以及控制資料在行銷動作中的使用。

[!DNL Policy Service] API提供數個端點，可讓您以程式設計方式管理資料使用標籤和原則，並評估違反原則的行銷動作。 這些端點如下所示。 如需詳細資訊，請造訪個別端點指南，並參閱[快速入門手冊](./getting-started.md)，以取得必要標題、讀取範例API呼叫等重要資訊。

若要檢視所有可用的端點和CRUD作業，請造訪[[!DNL Policy Service] API Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)。

## 標籤

資料使用標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 標籤可隨時套用，提供您選擇控制資料的彈性。 最佳做法鼓勵在資料被收錄到[!DNL Experience Platform]或資料可供[!DNL Platform]使用時，立即加上標籤。 您可以使用`/labels`端點來建立、檢視、編輯和刪除標籤。 要瞭解如何使用此端點，請訪問[標籤端點指南](./labels.md)。

## 行銷動作

在[!DNL Data Governance]架構中，行銷動作（也稱為行銷使用案例）是[!DNL Experience Platform]資料使用者可採取的動作，您的組織想要限制資料使用。 如需使用行銷動作的詳細資訊，請參閱[行銷動作端點指南](./marketing-actions.md)。

## 策略

資料使用原則是描述您可對[!DNL Experience Platform]內的資料執行或受限制之行銷動作的類型的規則。 策略由以下定義：

1. 特定行銷動作
1. 限制動作的資料使用標籤

要瞭解如何在API中管理策略，請參閱[策略端點指南](./policies.md)

## 評估

一旦資料使用標籤套用至[!DNL Platform]資料集，並且已針對這些標籤定義資料使用策略以執行行銷動作，「資料治理」功能可讓您強制執行這些原則並防止構成違反原則的資料作業。

[!DNL Policy Service] API提供端點，可讓您針對資料集或資料使用標籤的任意組合來測試行銷動作，以檢查是否發生任何違反原則的情況。 然後，您可以根據API回應，在體驗應用程式中設定通訊協定，以適當強制符合資料使用原則。 如需詳細資訊，請參閱[評估端點指南](./evaluation.md)。

## 後續步驟

若要開始使用[!DNL Policy Service] API進行呼叫，請閱讀[快速入門手冊](./getting-started.md)，然後選取其中一個端點手冊，以瞭解如何使用特定端點。 要使用[!DNL Experience Platform] UI使用標籤和策略，請分別參閱[標籤使用手冊](../labels/user-guide.md)和[策略使用手冊](../policies/user-guide.md)。
