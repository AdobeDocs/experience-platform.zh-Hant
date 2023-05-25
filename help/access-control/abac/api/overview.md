---
keywords: Experience Platform；首頁；熱門主題；API；屬性型存取控制；屬性型存取控制
solution: Experience Platform
title: Attribute-based Access Control API指南
description: 屬性型存取控制API可讓您以程式設計方式管理Adobe Experience Platform中的角色和存取原則。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 14%

---

# 屬性型存取控制API指南

以屬性為基礎的存取控制是Adobe Experience Platform的一項功能，可讓管理員根據屬性控制對特定物件和/或權能的存取。 屬性可以是新增至物件的中繼資料，例如新增至結構描述欄位或區段的標籤。 管理員定義包含管理使用者存取許可權的屬性的存取原則。

以屬性為基礎的存取控制API可用來存取Adobe Experience Platform中的角色、產品、許可權類別和許可權集，提供可存取所有可用程式庫資源的使用者介面和RESTful API。

>[!IMPORTANT]
>
>以屬性為基礎的存取控制不應與Experience Platform的資料控管功能混淆，後者可讓您使用標籤和原則來控制資料在Platform中的使用方式，而不是貴組織中的哪些使用者有權存取資料。 請參閱 [原則服務API指南](../../../data-governance/api/overview.md) 以程式設計方式利用這些功能的步驟。

這些端點概述如下。 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](./getting-started.md) 如需必要標題的重要資訊，請參閱範例API呼叫等。

## 角色

角色定義管理員、專家或一般使用者對貴組織資源的存取權。 在基於角色的存取控制環境中，使用者存取布建是透過共同責任和需求進行分組。 一個角色具有一組給定的權限，您的組織成員可以指派到一個或多個角色，依據他們需要的視圖範圍或寫入權限而定。請參閱 [角色端點指南](./roles.md) 以取得有關在API中使用角色的詳細資訊。

## 原則

策略是將屬性組合在一起的陳述式，用於建立允許和不允許的動作。原則可以是本機或全域，並且可以覆寫其他原則。 此 `/policies` 端點可讓您以程式設計方式管理組織中的原則。 請參閱 [原則端點指南](./policies.md) 以取得在API中使用原則的詳細資訊。

## 產品

此 `/products` 屬性型存取控制API中的端點可讓您以程式設計方式管理產品，以及與組織中產品相關聯的許可權類別和許可權集。 請參閱 [產品端點指南](./products.md) 有關在API中使用產品及其對應許可權類別和許可權集的詳細資訊。

## 後續步驟

若要開始使用屬性型存取控制API進行呼叫，請閱讀 [快速入門手冊](./getting-started.md) 然後選取其中一個端點指南，以瞭解如何使用特定端點。
