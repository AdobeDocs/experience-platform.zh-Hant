---
keywords: Experience Platform；首頁；熱門主題；api；基於屬性的存取控制；基於屬性的存取控制
solution: Experience Platform
title: 屬性型存取控制API指南
description: 屬性型存取控制API可讓您以程式設計方式管理Adobe Experience Platform中的角色和原則。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 4%

---

# 基於屬性的訪問控制API指南

基於屬性的存取控制是Adobe Experience Platform的一項功能，可讓管理員根據屬性控制對特定物件和/或功能的存取。 屬性可以是新增至物件的中繼資料，例如新增至架構欄位或區段的標籤。 管理員定義了包括屬性的訪問策略以管理用戶訪問權限。

屬性型存取控制API可用來存取Adobe Experience Platform中的角色、產品、權限類別和權限集，提供使用者介面和RESTful API，所有可用的程式庫資源都可從中存取。

這些端點概述如下。 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](./getting-started.md) 如需必要標題、讀取範例API呼叫等的重要資訊。

## 角色

角色定義管理員、專家或一般使用者對您組織中資源的存取權。 在基於角色的訪問控制環境中，用戶訪問配置是通過共同的責任和需求進行分組的。 角色具有一組指定的權限，而您組織的成員可以根據其所需的檢視或寫入存取範圍，指派給一或多個角色。 請參閱 [角色端點指南](./roles.md) 以取得在API中使用角色的詳細資訊。

## 原則

政策是將屬性集合在一起，以制定允許和不允許的行動的聲明。 策略可以是本地策略或全局策略，也可以覆蓋其他策略。 此 `/policies` 端點允許您以寫程式方式管理組織中的策略。 請參閱 [原則端點指南](./policies.md) 以取得在API中使用原則的詳細資訊。

## 產品

此 `/products` 屬性型存取控制API中的端點可讓您以程式設計方式管理產品，以及與貴組織產品相關聯的權限類別和權限集。 請參閱 [products端點指南](./products.md) 以取得在API中使用產品及其對應權限類別和權限集的詳細資訊。

## 後續步驟

若要開始使用屬性型存取控制API進行呼叫，請閱讀 [快速入門手冊](./getting-started.md) 然後，選取其中一個端點指南，以了解如何使用特定端點。
