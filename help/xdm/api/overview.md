---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: 架構註冊API開發人員指南
description: '架構註冊表API可讓您以程式設計方式管理Experience Platform中所有可用的架構及相關XDM資源。 '
topic: developer guide
translation-type: tm+mt
source-git-commit: 33f9ee45e8dd649d23f9b3b4f03ecf00d8e18fd2
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---


# [!DNL Schema Registry] API開發人員指南

此 [!DNL Schema Registry] 程式庫用於存取Adobe Experience Platform中的「架構庫」，提供使用者介面和RESTful API，讓所有可用的程式庫資源都可從中存取。

架構註冊表API提供數個端點，可讓您以程式設計方式管理平台內所有架構及您可用的相關Experience Data Model(XDM)資源。 這包括由您使用之應用程式的Adobe [!DNL Experience Platform] 、合作夥伴和廠商所定義的應用程式。

這些端點如下所示。 如需詳細資訊，請造訪個別端點指南，並參 [閱快速入門手冊](./getting-started.md) ，以取得必要標題、讀取範例API呼叫等重要資訊。

>[!IMPORTANT]
>
>XDM使用JSON結構描述格式來說明並驗證所擷取客戶體驗資料的結構。 在使用結構註冊表API之前，強烈建議您先檢閱正式的 [JSON結構描述檔案](https://json-schema.org/) ，以進一步瞭解此基礎技術。

若要檢視所有可用的端點和CRUD作業，請造訪 [Schema Registry API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。

## 結構描述

XDM模式表示並驗證了被引入平台的資料的結構和格式。 方案由類和零個或多個混合組成。 您可以使用端點來建立、查看、編輯和刪除 `/schemas` 方案。 要瞭解如何使用此端點，請參見 [方案端點指南](./schemas.md)。

有關如何在架構註冊表API中建立完整架構（包括建立和添加混合和資料類型）的逐步指南，請參見 [API架構建立教程](../tutorials/create-schema-api.md)。

## 行為

行為定義了模式描述的資料的性質。 每個XDM類都必須引用特定的行為，使用該類的所有方案都將繼承該行為。 請參閱 [行為端點指南](./behaviors.md) ，瞭解如何在API中檢視可用行為。

## 類別

類定義基於該類的所有方案必須包含的公共屬性的基本結構，並確定哪些混合適用於這些方案。 每個類都必須與現有行為相關聯。 有關在API [中使用類的詳細資訊](./classes.md) ，請參閱類端點指南。

## Mixins

Mixin是可重複使用的元件，它定義了表示特定概念的一個或多個欄位，例如個人、郵寄地址或Web瀏覽器環境。 Mixin將作為實現相容類的方案的一部分被包括，具體取決於它們所代表的資料（記錄或時間序列）的行為。 請參閱 [mixins端點指南](./mixins.md) ，以瞭解如何在API中使用mixin。

## 資料類型

資料類型與基本常值欄位的使用方式相同，可當成類別或混合的參考類型欄位，其主要差異在於資料類型可定義多個子欄位。 雖然與允許一致使用多欄位結構的混音類似，但資料類型更具彈性，因為它們可以包含在架構結構中的任何位置，而混音只能在根層級新增。 如需在 [API中使用資料類型的詳細資訊](./data-types.md) ，請參閱資料類型端點指南。

## 描述符

描述符是指派給架構中特定欄位的一組元資料，提供了各種上下文詳細資訊，包括這些欄位（和架構本身）如何與其他架構相關聯。 每個模式可以應用一個或多個描述符實體，並有幾種不同的描述符類型用於不同的用途。 有關在API [中使用描述符的詳細資訊](./descriptors.md) ，請參閱描述符端點指南，以及不同描述符類型及其使用案例的概述。

## 工會

雖然Platform允許您為特定使用案例合成方案，但它也允許您合成屬於特定類的方案的「聯合」。 聯合模式將共用同一類的所有模式的欄位聚合到單個表示中。 通過啟用與即時客戶配 [置檔案一起使用的架構](../../profile/home.md)，該架構將包括在其特定類的聯合中。 因此，聯合結構描述不能直接編輯，並且只能受到包括或排除結構描述在配置檔案中使用的影響。

要瞭解如何在方案註冊表API中查看聯合，請參閱聯合 [端點指南](./unions.md)。

## 匯出／匯入

架構註冊表API可讓您在沙盒和IMS組織之間傳輸和共用XDM資源。 對於任何方案、混合或資料類型，可以生成包含資源結構和任何從屬資源的導出裝載。 然後，此裝載可用來將資源匯入目標沙盒和IMS組織。

有關使 [用此端點的詳細資訊](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) ，請參閱方案註冊表API參考。

## 範例資料

可以為架構庫內的任何指定架構生成示例資料。 然後，返回的響應對象可用作資料接收的源。

有關使 [用此端點的詳細資訊](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) ，請參閱方案註冊表API參考。

## 審計日誌

方案註冊表維護不同更新之間對資源（類、混合、資料類型或方案）發生的所有更改的日誌。 通過在到此端點的GET請求路徑中提供特定資 `$id` 源的 `meta:altId` 日誌或日誌，可以檢索該資源的日誌。

有關使 [用此端點的詳細資訊](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) ，請參閱方案註冊表API參考。

## 後續步驟

若要開始使用「架構註冊表API」進行呼叫，請閱讀 [快速入門手冊](./getting-started.md) ，然後選取其中一個端點指南，以瞭解如何使用特定端點。