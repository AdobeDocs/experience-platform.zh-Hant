---
title: Reactor API指南
description: Reactor API 可讓開發人員以程式設計方式管理 Adobe Experience Platform 標記的所有資源。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 153eab11-db08-499e-80d1-c56f254372ce
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 4%

---

# [!DNL Reactor] API指南

Reactor API提供數個端點，可讓您以程式設計方式管理Adobe Experience Platform中標籤的所有資源。

這些端點概述如下。 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](./getting-started.md) 以取得如何驗證API的重要資訊。

若要檢視所有可用端點和CRUD作業，請造訪 [Reactor API參考](https://www.adobe.io/experience-platform-apis/references/reactor/).

## 公司

公司代表標籤使用者的組織，通常是企業。 這些公司會比對1:1與IMS組織ID。 API使用者將只能看見其可存取的公司。

請參閱 [《公司端點指南》](./endpoints/companies.md) 了解如何在API中檢視可用公司。

## 屬性

屬性是容器，可容納Reactor API中大部分的其他可用資源。 屬性不擁有的唯一資源是稽核事件、公司、擴充功能套件和設定檔。 屬性只屬於一個公司，而公司可以有許多屬性。

請參閱 [屬性端點指南](./endpoints/properties.md) 了解如何在API中管理屬性。

## 資料元素

資料元素的作用是變數，指向應用程式內的重要資料片段。 資料元素用於規則和擴充功能設定中。 在瀏覽器或應用程式的執行階段觸發規則時，會解析資料元素的值，並在規則內使用。

請參閱 [data elements端點指南](./endpoints/data-elements.md) 了解如何管理API中的資料元素。

## 規則

規則可控制已部署程式庫中所含資源的行為。 規則是一組一或多個規則元件，其存在可邏輯地將規則元件系結在一起。

請參閱 [rules endpoint指南](./endpoints/rules.md) 了解如何在API中管理規則。

## 規則元件

規則元件是組成規則的個別項目。 規則元件有三種基本類型：

* **事件**:觸發規則的原因
* **條件**:規則要檢查哪些項目以決定動作
* **動作**:根據是否符合條件而執行的規則

請參閱 [rules endpoint指南](./endpoints/rules.md) 了解如何在API中管理規則。

## 擴充功能套件

擴充功能套件代表個別功能的分組，這些功能可供標籤使用者使用。 這些功能大多以規則元件和資料元素的形式提供，但也可包含主要模組和共用模組。 擴充功能套件提供的功能包含在程式庫中時，會以擴充功能的形式安裝。

請參閱 [extension packages端點指南](./endpoints/extension-packages.md) 了解如何在API中管理擴充功能套件。

## 擴充功能

擴充功能代表擴充功能套件的已安裝例項。 擴充功能可讓屬性取得擴充功能套件所定義的功能。 建立資料元素和規則元件時，會運用這些功能。

請參閱 [extensions端點指南](./endpoints/extensions.md) 了解如何在API中管理擴充功能。

## 程式庫

程式庫是資源（擴充功能、規則和資料元素）的集合，代表屬性的所需行為。 程式庫會編譯到組建中，當這些組建從測試移至生產環境時，會將其指派給不同的環境。

請參閱 [libraries endpoint guide（庫端點指南）](./endpoints/libraries.md) 了解如何在API中管理程式庫。

## 組建

標籤程式庫會編譯到組建中，以便指派給環境進行測試和部署。 組建的內容會依程式庫中包含的資源、組建所指派的環境組態，以及組建所屬屬性的平台而有所不同。

請參閱 [builds endpoint guide（組建端點指南）](./endpoints/builds.md) 了解如何在API中管理組建。

## 環境

環境會指出可部署組建的特定主機，以及該組建應部署為一組檔案或以封存格式壓縮。 在Reactor API中，環境與主機本身分開，由 `/hosts` 端點。

請參閱 [builds endpoint guide（組建端點指南）](./endpoints/builds.md) 了解如何在API中管理組建。

## 主機

主機代表可傳送及最終部署程式庫組建的托管目的地。 主機可以是Akamai或SFTP伺服器。

請參閱 [hosts endpoint指南](./endpoints/hosts.md) 了解如何在API中管理主機。

## 應用程式設定

應用程式設定可儲存及擷取憑證以供日後使用。 請參閱 [app configurations端點指南](./endpoints/app-configurations.md) 了解如何在API中管理應用程式設定。

## 稽核事件

稽核事件是對另一個標籤資源的特定變更的記錄，會在進行變更時產生。 這些是可透過使用回撥函式訂閱的系統事件。

請參閱 [稽核事件端點指南](./endpoints/audit-events.md) 了解如何在API中管理稽核事件。

## 回呼

回呼是每當產生新稽核事件時，Platform會傳送至URL主機的訊息。 請參閱 [回撥端點指南](./endpoints/callbacks.md) 了解如何在API中管理回呼。

## 附註

附註是可新增至特定標籤資源的文字注釋，例如資料元素、擴充功能、程式庫、屬性、規則和規則元件。 請參閱 [附註端點指南](./endpoints/notes.md) 了解如何在API中管理附註。

## 設定檔

設定檔包含登入使用者的所有資訊，包括其所屬的所有Adobe組織、每個組織內其所屬的產品設定檔，以及其從每個產品設定檔擁有的權限。

請參閱 [profile endpoint指南](./endpoints/profile.md) 了解如何在API中檢視此資訊。

## 搜尋

此 `/search` 端點提供尋找符合所需條件的資源的方式，以查詢的形式表示。 所有查詢都限定在您目前的公司範圍和可存取的屬性。 請參閱 [search endpoint指南](./endpoints/search.md) 了解如何使用此功能。

## 秘密

機密包含允許事件轉發到另一個系統驗證以進行安全資料交換的憑據。 請參閱 [保密指南](./guides/secrets.md) 以取得機密在事件轉送中如何運作的概述，以及 [secrets端點指南](./endpoints/secrets.md) 了解如何在Reactor API中管理這些項目。

## 後續步驟

若要開始使用Schema Registry API進行呼叫，請閱讀 [快速入門手冊](./getting-started.md) 然後，選取其中一個端點指南，以了解如何使用特定端點。
