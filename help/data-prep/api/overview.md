---
keywords: Experience Platform；資料準備；資料準備api；故障排除；API
title: 資料準備API概觀
topic-legacy: guide
description: 資料準備API可讓您以程式設計方式建立對應集和函式，讓您在來源和目標結構描述之間轉換資料。
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# 對應服務API指南

資料準備可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。 「資料準備」會以「地圖」步驟顯示在「資料擷取」程式中，包括「CSV擷取」工作流程。

映射服務API（也稱為資料準備API）包含下面概述的多個端點。 如需詳細資訊，請造訪個別端點指南，並參閱[快速入門手冊](./getting-started.md)，以取得必要標題、讀取範例API呼叫等重要資訊。

## 函數

映射集函式允許您在源方案和目標方案之間轉換資料。 您可以使用`/languages/el`端點來驗證您的表達式，並獲取所有可用映射集函式和操作的清單。

有關如何使用映射集函式的詳細資訊，請閱讀[函式端點指南](./functions.md)。

## 映射集

映射集可用於定義源模式中的資料映射到目標模式的資料的方式。 您可以使用資料準備API中的`/mappingSets`端點，以程式設計方式擷取、建立、更新和驗證對應集。

有關如何使用映射集的詳細資訊，請閱讀[映射集端點指南](./mapping-set.md)。

## 後續步驟

若要開始使用映射服務API進行呼叫，請閱讀[快速入門手冊](./getting-started.md)，然後選取其中一個端點指南，以瞭解如何使用特定端點。
