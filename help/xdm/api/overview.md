---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構註冊表；結構註冊表；
solution: Experience Platform
title: Schema Registry API指南
description: Schema Registry API可讓開發人員以程式設計方式管理Adobe Experience Platform中的所有結構描述和相關Experience Data Model(XDM)資源。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 2%

---

# [!DNL Schema Registry] API指南

此 [!DNL Schema Registry] 可用來存取Adobe Experience Platform中的結構資料庫，提供使用者介面和RESTful API，供您存取所有可用的程式庫資源。

Schema Registry API提供數個端點，可讓您以程式設計方式管理Platform中可用的所有結構和相關Experience Data Model(XDM)資源。 這包括由Adobe定義， [!DNL Experience Platform] 您使用應用程式的合作夥伴和供應商。

這些端點概述如下。 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](./getting-started.md) 如需必要標題、讀取範例API呼叫等的重要資訊。

>[!IMPORTANT]
>
>XDM使用JSON結構描述格式來說明和驗證擷取的客戶體驗資料結構。 使用結構註冊表API前，強烈建議您檢閱 [官方JSON結構檔案](https://json-schema.org/) 來更好地理解這個基礎技術。

若要檢視所有可用端點和CRUD作業，請造訪 [結構註冊表API參考](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## 結構描述

XDM結構表示並驗證匯入Platform的資料結構和格式。 架構由類和零個或多個架構欄位組組成。 您可以使用 `/schemas` 端點。 若要了解如何使用此端點，請參閱 [schemas endpoint指南](./schemas.md).

如需如何在Schema Registry API中建立完整架構（包括建立和新增欄位群組和資料類型）的逐步指南，請參閱 [API結構建立教學課程](../tutorials/create-schema-api.md).

## 行為

行為定義架構描述的資料性質。 每個XDM類別都必須參考特定行為，採用該類別的所有結構都將繼承該行為。 請參閱 [行為端點指南](./behaviors.md) 了解如何在API中檢視可用行為。

## 類別

類定義了基於該類的所有架構必須包含的公共屬性的基本結構，並確定了哪些欄位組有資格在這些架構中使用。 每個類都必須與現有行為相關聯。 請參閱 [classes endpoint guide](./classes.md) 以取得在API中使用類別的詳細資訊。

## 欄位群組

欄位群組是可重複使用的元件，可定義代表特定概念的一或多個欄位，例如個人、郵寄地址或網頁瀏覽器環境。 欄位組將作為實現相容類的架構的一部分，具體取決於它們所代表的資料（記錄或時間序列）的行為。 請參閱 [欄位群組端點指南](./field-groups.md) 了解如何使用API中的欄位群組。

## 資料類型

在類或欄位組中，資料類型與基本常值欄位的使用方式相同，其主要區別在於資料類型可以定義多個子欄位。 雖然與中的欄位組類似，它們允許一致地使用多欄位結構，但資料類型更靈活，因為它們可以包含在架構結構中的任何位置，而欄位組只能在根級別添加。 請參閱 [data types端點指南](./data-types.md) 以取得在API中使用資料類型的詳細資訊。

## 描述符

描述符是指派給架構內特定欄位的一組中繼資料，提供各種內容詳細資訊，包括這些欄位（和架構本身）如何與其他架構相關聯。 每個架構可以應用一個或多個描述符實體，並且有多種不同的描述符類型用於不同的用途。 請參閱 [descriptors endpoint worke](./descriptors.md) 有關在API中使用描述符的詳細資訊，以及不同描述符類型及其使用案例的概述。

## 工會

雖然Platform可讓您針對特定使用案例撰寫結構，但也可讓您撰寫屬於特定類別之結構的「聯合」。 聯合架構會將共用相同類別之所有架構的欄位匯總為單一表示。 啟用結構以用於 [即時客戶個人檔案](../../profile/home.md)，該架構會包含在其特定類別的聯合中。 因此，聯合結構無法直接編輯，而且只能受包含或排除結構以用於設定檔的影響。

若要了解如何在Schema Registry API中檢視聯合，請參閱 [union endpoint指南](./unions.md).

## 從CSV轉換為結構 {#csv-to-schema}

您可以使用CSV檔案作為範本，自動產生XDM結構，以建立範本來大量匯入結構欄位，並減少手動API或UI的工作。

請參閱 [CSV結構轉換端點指南](./export.md) 以取得更多資訊。

## 轉存 {#export}

「結構註冊表API」可讓您在沙箱與IMS組織之間傳輸和共用XDM資源。 對於任何架構、欄位組或資料類型，您可以生成包含資源結構和任何相依資源的導出裝載。 然後，此裝載可用來將資源匯入目的地沙箱和IMS組織。

請參閱 [匯出端點指南](./export.md) 以取得如何為現有XDM資源建立匯出裝載的詳細資訊。

## 讀入

如果您使用 [匯出](#export) 或 [從CSV轉換為結構](./import.md) 端點來建立匯出裝載，您可以將該裝載傳送至目標組織和沙箱，以匯入指定的資源。

請參閱 [匯入端點指南](./export.md) 以取得如何從匯出裝載產生XDM資源的詳細資訊。

## 範例資料

您可以為架構庫內的任何指定架構產生範例資料。 然後，傳回的回應物件可作為資料擷取的來源。

請參閱 [範例data端點指南](./sample-data.md) 以獲取有關使用此終結點的詳細資訊。

## 稽核記錄

Schema Registry會維護在不同更新之間對資源（類、欄位組、資料類型或架構）發生的所有更改的日誌。 您可以提供特定資源，以擷取其記錄檔 `$id` 或 `meta:altId` 在指向此端點的GET請求的路徑中。

請參閱 [稽核記錄端點指南](./audit-log.md) 以獲取有關使用此終結點的詳細資訊。

## 後續步驟

若要開始使用Schema Registry API進行呼叫，請閱讀 [快速入門手冊](./getting-started.md) 然後，選取其中一個端點指南，以了解如何使用特定端點。
