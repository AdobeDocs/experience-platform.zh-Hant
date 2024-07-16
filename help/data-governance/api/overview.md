---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 原則服務API指南
description: 原則服務API可讓開發人員管理Experience Platform中的資料使用標籤和原則。 請遵循本指南以了解如何使用 API 執行關鍵作業。
role: Developer
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 3%

---

# [!DNL Policy Service] API指南

Adobe Experience Platform資料控管可讓您管理客戶資料，並確保遵守適用於資料使用的法規、限制和政策。 在[!DNL Experience Platform]中，它在各種層級上扮演關鍵角色，包括編目、資料譜系、資料使用標籤、資料使用原則，以及控制行銷動作的資料使用。

[!DNL Policy Service] API提供數個端點，可讓您以程式設計方式管理資料使用標籤和原則，以及評估原則違規的行銷動作。 這些端點概述如下。 如需詳細資訊，請瀏覽個別端點指南，並參閱[快速入門手冊](./getting-started.md)，以取得必要標頭、讀取範例API呼叫等重要資訊。

若要檢視所有可用的端點和CRUD作業，請造訪[[!DNL Policy Service] API swagger](https://www.adobe.io/experience-platform-apis/references/policy-service/)。

## 標記

將資料使用標籤套用至結構描述，以根據套用至該資料的使用原則來分類資料集和欄位。 標籤可隨時套用，提供您選擇控管資料方式的靈活性。 最佳實務建議在資料內嵌至[!DNL Experience Platform]時，或資料可在[!DNL Platform]中使用時，立即加上標籤。 您可以使用`/labels`端點建立、檢視、編輯和刪除標籤。 若要瞭解如何使用此端點，請造訪[標籤端點指南](./labels.md)。

## 行銷動作

在資料控管架構中的行銷動作（也稱為行銷使用案例）是[!DNL Experience Platform]資料消費者可以採取的動作，貴組織想要限制這些動作的資料使用。 如需有關使用行銷動作的詳細資訊，請參閱[行銷動作端點指南](./marketing-actions.md)。

## 原則

資料治理原則是描述允許或限制您在[!DNL Experience Platform]內對資料執行的行銷動作型別的規則。

>[!NOTE]
>
>資料控管原則與存取控制原則不應混淆，存取控制原則會決定貴組織中特定Platform使用者可存取的特定資料屬性。 如需詳細資訊，請參閱[以屬性為基礎的存取控制](../../access-control/abac/overview.md)指南。

資料治理原則由以下內容定義：

1. 特定行銷動作
1. 動作被限制執行的資料使用標籤

若要瞭解如何在API中管理原則，請參閱[原則端點指南](./policies.md)

## 評估

一旦資料使用標籤套用至Platform結構描述，且針對這些標籤為行銷動作定義資料使用原則後，您就可以透過資料控管功能強制執行這些原則，並防止構成原則違規的資料作業。

[!DNL Policy Service] API提供的端點可讓您針對資料集或資料使用標籤的任意組合來測試行銷動作，以檢查是否發生任何原則違規。 接著，您可以根據API回應，在體驗應用程式中設定通訊協定，以適當地強制資料使用原則相容。 如需詳細資訊，請參閱[評估端點指南](./evaluation.md)。

## 後續步驟

若要開始使用[!DNL Policy Service] API進行呼叫，請閱讀[快速入門手冊](./getting-started.md)，然後選取其中一個端點指南，以瞭解如何使用特定端點。 若要使用[!DNL Experience Platform] UI使用標籤和原則，請分別參閱[標籤使用手冊](../labels/user-guide.md)和[原則使用手冊](../policies/user-guide.md)。
