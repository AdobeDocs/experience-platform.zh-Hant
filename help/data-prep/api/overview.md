---
keywords: Experience Platform；資料準備；資料準備api；疑難排解；API
title: 資料準備API概述
description: 資料準備API可讓您以程式設計方式建立對應集和函式，以便在來源和目的地結構之間轉換資料。
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# 對應服務API指南

資料準備可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。 資料準備會在資料擷取程式（包括CSV擷取工作流程）中顯示為「對應」步驟。

對應服務API（也稱為資料準備API）包含以下概述的多個端點。 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](./getting-started.md) 如需必要標題、讀取範例API呼叫等的重要資訊。

## 函式

對應集函式允許您在源架構和目標架構之間轉換資料。 您可以使用 `/languages/el` 端點來驗證您的運算式，並取得所有可用映射集函式和操作的清單。

有關如何使用映射集函式的詳細資訊，請閱讀 [函式端點指南](./functions.md).

## 映射集

映射集可用於定義源架構中的資料如何映射到目標架構的資料。 您可以使用 `/mappingSets` 資料準備API中的端點，以程式設計方式擷取、建立、更新及驗證對應集。

有關如何使用映射集的詳細資訊，請閱讀 [映射集終結點指南](./mapping-set.md).

## 後續步驟

若要開始使用對應服務API進行呼叫，請閱讀 [快速入門手冊](./getting-started.md) 然後，選取端點指南之一，了解如何使用特定端點。
