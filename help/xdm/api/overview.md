---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構註冊表；結構註冊表；
solution: Experience Platform
title: Schema Registry API指南
description: Schema Registry API可讓開發人員以程式設計方式管理Adobe Experience Platform中的所有結構描述和相關Experience Data Model(XDM)資源。 請依照本指南，了解如何使用API執行重要作業。
topic-legacy: developer guide
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: 6ba8da07a4fb36c6e8bd2ede8ac415edaabe0ef6
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# [!DNL Schema Registry] API指南

[!DNL Schema Registry]用於存取Adobe Experience Platform中的結構資料庫，提供使用者介面和RESTful API，可存取所有可用的資料庫資源。

Schema Registry API提供數個端點，可讓您以程式設計方式管理Platform中可用的所有結構和相關Experience Data Model(XDM)資源。 這包括由Adobe、[!DNL Experience Platform]合作夥伴以及您使用其應用程式的供應商定義的應用程式。

這些端點概述如下。 如需詳細資訊，請造訪個別端點指南，並參閱[快速入門手冊](./getting-started.md)，以取得必要標題、讀取範例API呼叫等的重要資訊。

>[!IMPORTANT]
>
>XDM使用JSON結構描述格式來說明和驗證擷取的客戶體驗資料結構。 使用結構註冊表API之前，強烈建議您檢閱[官方JSON結構描述檔案](https://json-schema.org/)，以深入了解此基礎技術。

若要檢視所有可用端點和CRUD作業，請造訪[Schema Registry API參考](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。

## 方案

XDM結構表示並驗證匯入Platform的資料結構和格式。 架構由類和零個或多個架構欄位組組成。 您可以使用`/schemas`端點建立、檢視、編輯和刪除結構。 若要了解如何使用此端點，請參閱[綱要端點指南](./schemas.md)。

有關如何在「架構註冊表」API中建立完整架構（包括建立和添加欄位組和資料類型）的逐步指南，請參閱[API架構建立教程](../tutorials/create-schema-api.md)。

## 行為

行為定義架構描述的資料性質。 每個XDM類別都必須參考特定行為，採用該類別的所有結構都將繼承該行為。 請參閱[行為端點指南](./behaviors.md)，了解如何在API中檢視可用行為。

## 類別

類定義了基於該類的所有架構必須包含的公共屬性的基本結構，並確定了哪些欄位組有資格在這些架構中使用。 每個類都必須與現有行為相關聯。 有關在API中使用類的詳細資訊，請參閱[classes端點指南](./classes.md)。

## 欄位群組

欄位群組是可重複使用的元件，可定義代表特定概念的一或多個欄位，例如個人、郵寄地址或網頁瀏覽器環境。 欄位組將作為實現相容類的架構的一部分，具體取決於它們所代表的資料（記錄或時間序列）的行為。 請參閱[欄位群組端點指南](./field-groups.md)，了解如何使用API中的欄位群組。

## 資料類型

在類或欄位組中，資料類型與基本常值欄位的使用方式相同，其主要區別在於資料類型可以定義多個子欄位。 雖然與中的欄位組類似，它們允許一致地使用多欄位結構，但資料類型更靈活，因為它們可以包含在架構結構中的任何位置，而欄位組只能在根級別添加。 如需在API中使用資料類型的詳細資訊，請參閱[資料類型端點指南](./data-types.md)。

## 描述符

描述符是指派給架構內特定欄位的一組中繼資料，提供各種內容詳細資訊，包括這些欄位（和架構本身）如何與其他架構相關聯。 每個架構可以應用一個或多個描述符實體，並且有多種不同的描述符類型用於不同的用途。 有關在API中使用描述符的詳細資訊，請參閱[描述符終結點指南](./descriptors.md)，以及不同描述符類型及其使用案例的概述。

## 工會

雖然Platform可讓您針對特定使用案例撰寫結構，但也可讓您撰寫屬於特定類別之結構的「聯合」。 聯合架構會將共用相同類別之所有架構的欄位匯總為單一表示。 啟用結構以便與[即時客戶配置檔案](../../profile/home.md)一起使用，該結構便會包含在其特定類的聯合中。 因此，聯合結構無法直接編輯，而且只能受包含或排除結構以用於設定檔的影響。

若要了解如何在Schema Registry API中檢視聯合，請參閱[聯合端點指南](./unions.md)。

## 匯出/匯入

「結構註冊表API」可讓您在沙箱與IMS組織之間傳輸和共用XDM資源。 對於任何架構、欄位組或資料類型，您可以生成包含資源結構和任何相依資源的導出裝載。 然後，此裝載可用來將資源匯入目的地沙箱和IMS組織。

有關如何使用這些端點的詳細資訊，請參閱[匯出/匯入端點指南](./export-import.md)。

## 範例資料

您可以為架構庫內的任何指定架構產生範例資料。 然後，傳回的回應物件可作為資料擷取的來源。

有關使用此端點的詳細資訊，請參閱[示例資料端點指南](./sample-data.md)。

## 稽核記錄

Schema Registry會維護在不同更新之間對資源（類、欄位組、資料類型或架構）發生的所有更改的日誌。 您可以在指向此端點的GET請求路徑中提供其`$id`或`meta:altId`，以檢索特定資源的日誌。

有關使用此端點的詳細資訊，請參閱[審核日誌端點指南](./audit-log.md)。

## 後續步驟

若要開始使用架構註冊表API進行呼叫，請閱讀[快速入門手冊](./getting-started.md)，然後選取其中一個端點手冊，以了解如何使用特定端點。
