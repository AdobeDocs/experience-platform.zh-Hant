---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 政策服務API開發人員指南
topic: developer guide
translation-type: tm+mt
source-git-commit: 71678b10c9e137016ea404305b272508b9c8cabe
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---


# [!DNL Policy Service] API開發人員指南

Adobe Experience Platform可 [!DNL Data Governance] 讓您管理客戶資料，並確保符合資料使用適用的法規、限制和政策。 它在各個層級中都發揮著關鍵作用， [!DNL Experience Platform] 包括編目、資料傳承、資料使用標籤、資料使用政策，以及控制資料在行銷動作中的使用。

API提 [!DNL Policy Service] 供數個端點，可讓您以程式設計方式管理資料使用標籤和原則，以及評估違反原則的行銷動作。 這些端點如下所示。 如需詳細資訊，請造訪個別端點指南，並參 [閱快速入門手冊](./getting-started.md) ，以取得必要標題、讀取範例API呼叫等重要資訊。

若要檢視所有可用的端點和CRUD作業，請造訪 [[!DNL Policy Service] API Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)。

## 標籤

資料使用標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 標籤可隨時套用，提供您選擇控制資料的彈性。 最佳做法鼓勵在資料被吸收或資料可供使 [!DNL Experience Platform]用時，立即加上標籤 [!DNL Platform]。 您可以使用端點來建立、檢視、編輯和刪除標 `/labels` 簽。 若要瞭解如何使用此端點，請造訪標 [簽端點指南](./labels.md)。

## 行銷動作

在架構中，行銷動作（也稱為行銷使用案例）是資料使用者可以採取的 [!DNL Data Governance] 動作，而您的組織 [!DNL Experience Platform] 想要限制其資料使用。 如需使用行銷動作的詳細資訊，請參閱行 [銷動作端點指南](./marketing-actions.md)。

## 策略

資料使用原則是描述您允許或限制對內資料執行之行銷動作類型的規則 [!DNL Experience Platform]。 策略由以下定義：

1. 特定行銷動作
1. 限制動作的資料使用標籤

要瞭解如何在API中管理策略，請參閱策略端 [點指南](./policies.md)

## 評估

一旦資料使用標籤套用至資料集，並為針對這些標籤的行銷動作定義資料使用原則後，「資料管理」功能可讓您強制執行這些原則，並防止構成違反原則的資料作業。 [!DNL Platform]

API [!DNL Policy Service] 提供端點，可讓您針對資料集或資料使用標籤的任意組合來測試行銷動作，以檢查是否發生任何違反原則的情況。 然後，您可以根據API回應，在體驗應用程式中設定通訊協定，以適當強制符合資料使用原則。 See the [evaluation endpoints guide](./evaluation.md) for more information.

## 後續步驟

若要開始使用 [!DNL Policy Service] API進行呼叫，請閱讀 [快速入門手冊](./getting-started.md) ，然後選取其中一個端點指南，以瞭解如何使用特定端點。 若要使用UI使用標籤和原則，請 [!DNL Experience Platform] 分別參閱標籤 [使用指南](../labels/user-guide.md)[和原則使用指南](../policies/user-guide.md)。