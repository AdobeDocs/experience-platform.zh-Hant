---
keywords: Experience Platform；首頁；熱門主題；api；基於屬性的訪問控制；基於屬性的訪問控制
solution: Experience Platform
title: 《基於屬性的訪問控制API指南》
description: 基於屬性的訪問控制API允許您以寫程式方式管理Adobe Experience Platform內的角色和策略。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: 567bfe089fd96cb08cb8ea7c90d065c804be9413
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 4%

---

# 基於屬性的訪問控制API指南

>[!IMPORTANT]
>
>基於屬性的訪問控制目前在面向美國醫療保健客戶的有限版本中提供。 這一功能一旦完全發佈，將可供所有Real-time Customer Data Platform客戶使用。

基於屬性的訪問控制是Adobe Experience Platform的一種功能，它使管理員能夠基於屬性控制對特定對象和/或權能的訪問。 屬性可以是添加到對象的元資料，如添加到架構欄位或段的標籤。 管理員定義包括屬性的訪問策略以管理用戶訪問權限。

基於屬性的訪問控制API用於訪問Adobe Experience Platform內的角色、產品、權限類別和權限集，提供用戶介面和REST風格的API，所有可用的庫資源都可以從中訪問。

下面概述了這些端點。 請訪問各個端點指南以瞭解詳細資訊，並參閱 [入門指南](./getting-started.md) 有關所需標頭、讀取示例API調用等的重要資訊。

## 角色

角色定義管理員、專家或最終用戶對您組織中的資源的訪問權限。 在基於角色的訪問控制環境中，用戶訪問設定是通過共同的責任和需要進行分組的。 某個角色具有給定的一組權限，您組織的成員可以分配給一個或多個角色，這取決於他們需要的查看範圍或寫權限。 查看 [角色終結點指南](./roles.md) 的子菜單。

## 原則

策略是將屬性集合在一起以建立允許和不允許的操作的語句。 策略可以是本地策略或全局策略，並且可以覆蓋其他策略。 的 `/policies` endpoint允許您以寫程式方式管理組織中的策略。 查看 [策略終結點指南](./policies.md) 的子菜單。

## 產品

的 `/products` 通過基於屬性的訪問控制API中的端點，您可以以寫程式方式管理產品以及與組織中的產品相關聯的權限類別和權限集。 查看 [產品端點指南](./products.md) 有關在API中使用產品及其相應權限類別和權限集的詳細資訊。

## 後續步驟

要使用基於屬性的訪問控制API開始調用，請閱讀 [入門指南](./getting-started.md) 然後選擇其中一個端點參考線，以瞭解如何使用特定端點。
