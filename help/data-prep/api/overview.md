---
keywords: Experience Platform；資料準備；資料準備；疑難解答；API
title: 資料準備API概述
description: 資料準備API允許您按程式建立映射集和函式，從而在源方案和目標方案之間轉換資料。
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# 映射服務API指南

資料準備允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。 資料準備在資料接收流程中顯示為「映射」步驟，包括CSV接收工作流。

映射服務API（也稱為資料準備API）包括以下概述的多個端點。 請訪問各個端點指南以瞭解詳細資訊，並參閱 [入門指南](./getting-started.md) 有關所需標頭、讀取示例API調用等的重要資訊。

## 函式

映射集函式允許您在源架構和目標架構之間轉換資料。 您可以使用 `/languages/el` 終結點，以驗證表達式並獲取所有可用映射集函式和操作的清單。

有關如何使用映射集函式的詳細資訊，請閱讀 [函式終結點指南](./functions.md)。

## 映射集

映射集可用於定義源模式中的資料如何映射到目標模式的資料。 您可以使用 `/mappingSets` 以寫程式方式檢索、建立、更新和驗證映射集。

有關如何使用映射集的詳細資訊，請閱讀 [映射集端點指南](./mapping-set.md)。

## 後續步驟

要開始使用映射服務API進行調用，請閱讀 [入門指南](./getting-started.md) 然後選擇端點指南中的一個以瞭解如何使用特定端點。
