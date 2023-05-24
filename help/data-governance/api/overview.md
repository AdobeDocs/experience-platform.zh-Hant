---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 策略服務API指南
description: 策略服務API允許開發人員管理Experience Platform中的資料使用標籤和策略。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 3%

---

# [!DNL Policy Service] API指南

Adobe Experience Platform資料治理允許您管理客戶資料並確保遵守適用於資料使用的法規、限制和策略。 它在 [!DNL Experience Platform] 包括編目、資料沿襲、資料使用標籤、資料使用策略以及控制資料在營銷活動中的使用。

的 [!DNL Policy Service] API提供了多個端點，允許您以寫程式方式管理資料使用標籤和策略，並評估違反策略的營銷操作。 下面概述了這些端點。 請訪問各個端點指南以瞭解詳細資訊，並參閱 [入門指南](./getting-started.md) 有關所需標頭、讀取示例API調用等的重要資訊。

要查看所有可用端點和CRUD操作，請訪問 [[!DNL Policy Service] API交換器](https://www.adobe.io/experience-platform-apis/references/policy-service/)。

## 標記

資料使用情況標籤允許您根據應用於該資料的使用情況策略對資料集和欄位進行分類。 標籤可以隨時應用，在選擇管理資料的方式上提供了靈活性。 最佳做法鼓勵在將資料攝取到 [!DNL Experience Platform]，或當資料可用時 [!DNL Platform]。 您可以使用 `/labels` 端點。 要瞭解如何使用此終結點，請訪問 [標籤端點指南](./labels.md)。

## 市場營銷操作

在「資料治理」框架的上下文中，市場營銷操作（也稱為市場營銷使用案例）是 [!DNL Experience Platform] 資料使用者可以採用，您的組織希望限制其資料使用。 有關使用市場營銷活動的詳細資訊，請參閱 [市場營銷操作終結點指南](./marketing-actions.md)。

## 原則

資料治理策略是描述允許或限制您對內部資料執行的營銷操作類型的規則 [!DNL Experience Platform]。

>[!NOTE]
>
>不要將資料治理策略與訪問控制策略混為一談，這些策略決定了組織中某些平台用戶可以訪問的特定資料屬性。 請參閱上的指南 [基於屬性的訪問控制](../../access-control/abac/overview.md) 的子菜單。

資料管理策略由以下定義：

1. 特定市場營銷操作
1. 限制對其執行操作的資料使用標籤

要瞭解如何管理API中的策略，請參見 [策略終結點指南](./policies.md)

## 評估

資料使用標籤應用到 [!DNL Platform] 資料集和資料使用策略已為針對這些標籤的市場營銷操作定義，資料治理功能允許您強制實施這些策略並防止構成策略違規的資料操作。

的 [!DNL Policy Service] API提供了端點，允許您針對資料集或資料使用標籤的任意組合test營銷操作，以檢查是否發生任何策略違規。 然後，您可以根據API響應在體驗應用程式內設定協定，以適當強制實施資料使用策略合規性。 查看 [評估端點指南](./evaluation.md) 的子菜單。

## 後續步驟

使用 [!DNL Policy Service] API，讀取 [入門指南](./getting-started.md) 然後選擇其中一個端點參考線，以瞭解如何使用特定端點。 使用 [!DNL Experience Platform] UI，請參閱 [標籤使用手冊](../labels/user-guide.md) 和 [策略使用手冊](../policies/user-guide.md)的下界。
